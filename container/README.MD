# containerized download

## download a single event
```bash
docker compose -f container/docker-compose.yml run --rm gsutil bash

#generate a list of available files
gsutil ls gs://gfd_v1_4 > gsutil_file_list.txt

#download an event
export EVENT_ID=DFO_4230_From_20150310_to_20150323.zip

gsutil cp gs://gfd_v1_4/$EVENT_ID .
```


## download from a list of events
```bash
# 1) Make a pattern list like: DFO_<ID>_From_
awk -F, 'NR>1 && $1 ~ /^[0-9]+$/ {printf "DFO_%s_From_\n", $1}' dfo_polys_20191203_post2015-US.csv \
| sort -u > dfo_id_patterns.txt

# 2) Filter the GFD listing with those patterns to get the exact URIs to download
grep -F -f dfo_id_patterns.txt gsutil_file_list.txt \
| sort -u > gfd_download_list.txt

# 3) Sanity check: how many events will be downloaded?
wc -l gfd_download_list.txt


mkdir -p ./gfd_us_post2015
cat gfd_download_list.txt | gsutil -m cp -n -I ./gfd_us_post2015/

#unzip them all

for z in ./gfd_us_post2015/DFO_*.zip; do
    unzip -n "$z" -d ./gfd_us_post2015/      # extract to main folder, skip existing files
done


```
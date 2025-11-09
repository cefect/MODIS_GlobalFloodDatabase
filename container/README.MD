# containerized download

```bash
docker compose -f container/docker-compose.yml run --rm gsutil bash

#generate a list of available files
gsutil ls gs://gfd_v1_4 > gsutil_file_list.txt

#download an event
export EVENT_ID=DFO_4730_From_20190313_to_20190402.zip

gsutil cp gs://gfd_v1_4/$EVENT_ID .

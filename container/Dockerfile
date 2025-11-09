# Smallest, no-frills: gsutil preinstalled via official Cloud SDK image.
FROM gcr.io/google.com/cloudsdktool/cloud-sdk:slim

# Optional: verify it's there
RUN gsutil version -l

RUN apt-get update \
    && apt-get install -y unzip \
    && rm -rf /var/lib/apt/lists/*

# Default shell
CMD ["/bin/bash"]

# Notes

# Huggingface Space

## Logs

```
===== Build Queued at 2023-10-16 02:46:25 / Commit SHA: e9e3061 =====

--> FROM docker.io/library/python:3.10@sha256:a20ae344b668753817b8bffb8628e068278d8ddbde1657f7b836fd74559beacd
DONE 0.0s

--> RUN useradd -m -u 1000 user
CACHED

--> RUN pip install --no-cache-dir pip==22.3.1 && 	pip install --no-cache-dir 	datasets 	"huggingface-hub>=0.12.1" "protobuf<4" "click<8.1" "pydantic~=1.0"
CACHED

--> RUN pip install --no-cache-dir 	gradio[oauth]==3.47.1 	uvicorn>=0.14.0 	spaces==0.16.1
CACHED

--> RUN --mount=target=/root/packages.txt,source=packages.txt 	apt-get update && 	xargs -r -a /root/packages.txt apt-get install -y 	&& rm -rf /var/lib/apt/lists/*
CACHED

--> RUN --mount=target=requirements.txt,source=requirements.txt 	pip install --no-cache-dir -r requirements.txt
CACHED

--> RUN --mount=target=pre-requirements.txt,source=pre-requirements.txt 	pip install --no-cache-dir -r pre-requirements.txt
CACHED

--> RUN apt-get update && apt-get install -y 	git 	git-lfs 	ffmpeg 	libsm6 	libxext6 	cmake 	libgl1-mesa-glx 	&& rm -rf /var/lib/apt/lists/* 	&& git lfs install
CACHED

--> WORKDIR /home/user/app
CACHED

--> COPY --link --chown=1000 --from=lfs /app /home/user/app
CACHED

--> COPY --link --chown=1000 ./ /home/user/app
DONE 0.0s

--> Pushing image
DONE 1.0s

--> Exporting cache
DONE 1.2s

```

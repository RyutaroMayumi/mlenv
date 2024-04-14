# FROM pytorch/pytorch:latest
FROM nvcr.io/nvidia/pytorch:23.04-py3

WORKDIR /usr/src/app

RUN apt-get update && apt-get install -y \
    graphviz \
    && rm -rf /var/lib/apt/lists/*

# install opencv-python requirements
RUN apt-get update && apt-get install libgl1-mesa-dev -y

# install pip packages
COPY requirements.txt ./
RUN pip install --upgrade pip
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

# avoid "Bad config encountered during initialization" error
# https://github.com/Project-MONAI/MONAI/issues/5777
COPY jupyter_notebook_config.py /root/.jupyter

# avoid import cv2 error
# https://qiita.com/ballemech/items/e32d8db300bdc788755a
COPY cv2_typing.__init__.py /usr/local/lib/python3.8/dist-packages/cv2/typing/__init__.py

#CMD [ "python", "./your-daemon-or-script.py" ]


FROM ghcr.io/pytorch/pytorch-nightly:b3874ab-cu11.8.0

RUN apt-get update  && apt-get install -y git python3-virtualenv wget

RUN pip install peft

WORKDIR /workspace
# Setup server requriements
COPY ./fast_api_requirements.txt fast_api_requirements.txt
RUN pip install --no-cache-dir --upgrade -r fast_api_requirements.txt

ENV HUGGINGFACE_TOKEN="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"
ENV HUGGINGFACE_REPO="llm-efficiency-challenge/QuyAnh2005-4090-mistral-7b-neurips-v2"

# Copy over single file server
COPY ./main.py main.py
COPY ./api.py api.py
# Run the server
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "80"]

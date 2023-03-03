FROM python:3.11.2-bullseye

WORKDIR /pipeline

RUN pip install "poetry==1.4.0" && poetry config virtualenvs.create false

COPY ./project_a/ ./project_a
COPY ./project_b/ ./project_b


WORKDIR /pipeline/project_b
RUN poetry install

CMD ["/bin/bash"]

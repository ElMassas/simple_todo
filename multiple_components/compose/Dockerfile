ARG PYTHON_VERSION=3.12.0-slim
ARG BUILD_DATE
ARG COMMIT_SHA=local

FROM python:${PYTHON_VERSION}

LABEL maintainer="ElMassas"
LABEL org.label-schema.build-date=${BUILD_DATE}
LABEL org.label-schema.vcs-ref=${COMMIT_SHA}

# Set the working directory in the container to /app
WORKDIR /code

# Add dependicies into the container at /app
COPY requirements.txt /code/requirements.txt

# Install any needed packages specified in requirements.txt
RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt

COPY ./app /code/app

RUN useradd --system --user-group pythoner

USER pythoner

# Run app.py when the container launches with non root port
CMD ["uvicorn", "app.app:app", "--host", "0.0.0.0", "--port", "8000"]
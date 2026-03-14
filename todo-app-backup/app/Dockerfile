FROM python:3.9-slim AS builder

RUN pip install --upgrade pip

COPY requirements.txt .

RUN pip install --user -r requirements.txt && \
    python3 -c "import gunicorn; print(f'Gunicorn {gunicorn.__version__} installed')"


FROM python:3.9-slim

RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*
RUN useradd --create-home appuser

COPY --from=builder --chown=appuser:appuser /root/.local /home/appuser/.local

COPY --chown=appuser:appuser . /app

ENV PATH=/home/appuser/.local/bin:$PATH \
    PYTHONPATH=/app:$PYTHONPATH

USER appuser
WORKDIR /app

RUN ls -la /home/appuser/.local/lib/python3.9/site-packages/ | grep gunicorn

HEALTHCHECK CMD curl -f http://localhost:5000/health || exit 1

CMD ["/home/appuser/.local/bin/gunicorn", "--bind", "0.0.0.0:5000", "app:app"]

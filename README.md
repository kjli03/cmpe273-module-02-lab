## Run Service A
```bash
cd service-a
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python app.py
```

## Run Service B (new terminal)
```bash
cd service-b
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
python app.py
```

## Test
```bash
curl "http://127.0.0.1:8081/call-echo?msg=hello"
```

## What makes this distributed?
Services A and B run separately and are each able to run when the other fails, with an error message being logged to demonstrate that one has failed. On failure of Service A, Service B waits 1 second before timing out and showing an error message accordingly.

## Success
katherine@Katherines-MacBook-Air ~ % curl "http://127.0.0.1:8081/call-echo?msg=hello"

{"service_a":{"echo":"hello"},"service_b":"ok"}

## Failure (after stopping Service A, logs show a graceful error message
katherine@Katherines-MacBook-Air ~ % curl "http://127.0.0.1:8081/call-echo?msg=hello"

{"error":"HTTPConnectionPool(host='127.0.0.1', port=8080): Max retries exceeded with url: /echo?msg=hello (Caused by NewConnectionError(\"HTTPConnection(host='127.0.0.1', port=8080): Failed to establish a new connection: [Errno 61] Connection refused\"))","service_a":"unavailable","service_b":"ok"}

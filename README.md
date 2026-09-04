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


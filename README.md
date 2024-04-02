# PyTraceKit

Elevate Your Distributed Tracing in Python with **PyTraceKit**, a forefront tool designed to simplify the integration of distributed tracing into Python services through the power of OpenTelemetry. This package is your gateway to enhanced application observability with a low-code, straightforward approach, enriching your logging with trace IDs and allowing detailed tracing with minimal setup.

## Key Features

- **Simplified Tracing**: Easily integrate distributed tracing into FastAPI, Flask, or Falcon applications with just one line of code.
- **Function-Level Tracing with Customization**: Add detailed tracing to any function, specifying custom operation names and span attributes for in-depth observability.
- **Advanced Logging**: Each log message includes a trace ID for easy correlation, with customizable logging settings such as file paths, sizes, and rotation.
- **Framework Agnostic**: Automatically detects and integrates with your Python web framework, offering out-of-the-box support for FastAPI, Flask, and Falcon.
- **Extensibility**: Adapt and extend **PyTraceKit** to suit your specific tracing and logging needs.

## Installation

To install **PyTraceKit**, run the following command in your terminal:

```bash
pip install pytracekit
```

## Getting Started

Setup the environment variables

```bash
export TRACE_SERVICE_NAME=your service name
export TRACING_ENDPOINT=http://localhost:4317/api/traces # your collector endpoint
export ENABLE_TRACING=true

```

### For FastAPI or Flask:

```python

from pytracekit import instrument

# Assuming `app` is your FastAPI or Flask application instance
instrument(app)

```

### For Falcon

```python

from pytracekit import instrument

# Instrument before defining your Falcon app
instrument()

app = falcon.App()  # Now define your Falcon app

```

### Add Function-Level Tracing

PyTraceKit allows you to add tracing to specific functions using the @instrument_with_tracing decorator. You can specify a custom operation name and additional span attributes for detailed tracing:

```python

from pytracekit import instrument_with_tracing

@instrument_with_tracing(operation_name="custom_operation", span_attrs={"key": "value"})
def process_data():
    # Your function logic here


```

### Setup Enhanced Logging

To take advantage of PyTraceKit's enhanced logging capabilities, use the get_logger function. This allows you to create a logger that includes trace IDs in log messages, making it easier to correlate logs with traces:

``` python
from pytracekit import get_logger

logger = get_logger(name='my_service_logger', log_file_path='logs/my_service.log', max_bytes=10*1024*1024, backup_count=5)

# Now you can use `logger` to log messages that include trace IDs
logger.info("This log entry includes a trace ID.")
```
# Add Response Headers

Ambassador can add a dictionary of HTTP headers that can be added to each response that is returned to client.

## The `add_response_headers` annotation

The `add_response_headers` attribute is a dictionary of `header`: `value` pairs. The `value` can be a `string`, `bool` or `object`. When its an `object`, the object should have a `value` property, which is the actual header value, and the remaining attributes are additional envoy properties. Look at the example to see the usage.

Envoy dynamic values `%DOWNSTREAM_REMOTE_ADDRESS_WITHOUT_PORT%` and `%PROTOCOL%` are supported, in addition to static values.

## A basic example

```yaml
---
apiVersion: ambassador/v1
kind:  Mapping
name:  qotm_mapping
prefix: /qotm/
add_response_headers:
  x-test-proto: "%PROTOCOL%"
  x-test-ip: "%DOWNSTREAM_REMOTE_ADDRESS_WITHOUT_PORT%"
  x-test-static: This is a test header
  x-test-object:
    append: False
    value: this is from object header config
service: qotm
```

will add the protocol, client IP, and a static header to returning response to client.

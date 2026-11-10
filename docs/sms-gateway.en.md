# Notifications through ZTE MC888 SMS Gateway

[Polski](sms-gateway.md) | [English](sms-gateway.en.md) · [README](../README.en.md)

[ZTE MC888 SMS Gateway](https://github.com/o2eric/zte-mc888-sms-gateway) is a
separate HTTP service that sends SMS through a compatible modem. An application
can read account status with Play24 API, decide whether to alert, and send the
alert through the gateway. The current monitor does not include a gateway adapter.

1. Deploy and secure the gateway according to its documentation. Configure a
   separate client, token and allowed recipient aliases. Use TLS and access
   restrictions between hosts.
2. Obtain data through Play24 API, for example
   `uv run play24-json summary --msisdn 48XXXXXXXXX`. Your script must check
   the result and decide whether the alert condition is met.
3. Send `POST /v1/notify` to the gateway with a Bearer token and JSON such as
   `{"key":"balance-alert-2026-11-10","text":"Check balance","to":["contact1"]}`.
   Use your configured alias and a unique event key.
4. Check each recipient result. `sent` is modem confirmation, not a handset
   delivery receipt; do not blindly retry an uncertain send.

Keep tokens, phone numbers and codes out of Git. A Play24 registration code is
delivered to the number registered with Play; the gateway does not automatically
retrieve it from the handset. Both projects are unofficial and independent of
the operator and modem manufacturer.

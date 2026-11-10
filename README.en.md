# play24 — unofficial Play24 API client

[Polski](README.md) | [English](README.en.md)

Python tools for managing your Play account without the official app, based on
reverse engineering of the self-care API. One core (`play24lib.py`) provides
a CLI, JSON CLI, Python library and MCP server. This project is unofficial and
not affiliated with Play; use it only with accounts you are authorized to manage.

## Capabilities

- Register a number with an SMS code and a FIDO2 passkey; subsequent logins use the passkey.
- Read balances, allowances, packages, invoices, SIM and account information.
- Activate and deactivate services with step-up authorization.
- Handle separate accounts or multiple numbers on one account.
- Use the JSON CLI or MCP server, and run a threshold monitor.

## Quick start

```sh
uv sync
uv run play24 register-start --msisdn 48xxxxxxxxx
uv run play24 register-otp --msisdn 48xxxxxxxxx --code 1234
uv run play24 summary
```

The SMS code and phone number above are placeholders. Passkeys and account data
are stored locally in `~/.play24/`; protect them and keep them out of Git.
Without uv, install `requests` and `cryptography` and run `python3 play24.py`.
The detailed [quick start](QUICKSTART.md) and the existing reference documents
below are currently in Polish.

## Documentation

- [CLI](docs/cli.md) · [authentication](docs/auth.md) · [multiple numbers](docs/multi-number.md)
- [Library, JSON CLI and MCP](docs/agents-mcp.md) · [monitor](docs/monitor.md)
- [API](docs/API.md) · [service activation](docs/ACTIVATION.md)
- [Endpoints](docs/endpoints.txt) · [reverse-engineering methods](docs/METHODS.md)
- [Changelog](CHANGELOG.md)
- [ZTE SMS gateway integration](docs/sms-gateway.en.md) (English)

## Related project

[ZTE MC888 SMS Gateway](https://github.com/o2eric/zte-mc888-sms-gateway) can
send SMS notifications from an application using Play24 API. It is a separate
service: there is no built-in integration and it does not automatically retrieve
Play24 registration codes delivered to a handset.

The project derives from [areqq/play24](https://github.com/areqq/play24) and
retains its license and attribution.

## Support

If this project helps you, you can [support o2eric on BuyCoffee](https://buycoffee.to/o2eric).

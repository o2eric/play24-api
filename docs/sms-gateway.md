# Powiadomienia przez ZTE MC888 SMS Gateway

[Polski](sms-gateway.md) | [English](sms-gateway.en.md) · [README](../README.md)

[ZTE MC888 SMS Gateway](https://github.com/o2eric/zte-mc888-sms-gateway) to
oddzielna bramka HTTP do wysyłania SMS przez zgodny modem. Może uzupełnić
Play24 API: własna aplikacja może odczytać stan konta przez Play24 API,
zdecydować, czy potrzebny jest alert, a następnie wysłać go przez bramkę.
Obecny monitor nie ma gotowego adaptera tej bramki.

1. Uruchom i zabezpiecz bramkę według jej dokumentacji. Skonfiguruj osobnego
   klienta, jego token i dozwolone aliasy odbiorców. Przy dostępie między
   maszynami użyj TLS i ogranicz dostęp.
2. Pobierz dane przez Play24 API, np. `uv run play24-json summary --msisdn 48XXXXXXXXX`.
   Własny skrypt powinien sprawdzić wynik i warunek alertu.
3. Wyślij `POST /v1/notify` do bramki z nagłówkiem Bearer i JSON-em
   `{"key":"balance-alert-2026-11-10","text":"Sprawdź saldo","to":["contact1"]}`.
   Użyj własnego aliasu i unikalnego klucza zdarzenia.
4. Sprawdź wynik każdego odbiorcy. `sent` to potwierdzenie modemu, a nie
   raport doręczenia telefonu; nie ponawiaj niepewnych wysyłek w ciemno.

Nie umieszczaj tokenów, numerów ani kodów w Git. Kod rejestracji Play24 trafia
do numeru wskazanego w Play: bramka nie pobiera go automatycznie z telefonu.
Oba projekty są nieoficjalne i niezależne od operatora oraz producenta modemu.

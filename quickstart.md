# Quickstart: Get your first exchange rate

**Time needed:** about 5 minutes
**Last checked:** 9 October 2026

This guide shows you how to fetch a live currency exchange rate from the Frankfurter API. You will make one request and read the response.

> This is an independent documentation exercise. It is not affiliated with Frankfurter. For the official documentation, see [frankfurter.dev](https://frankfurter.dev).

## What you need

- A terminal (Terminal on Mac, Command Prompt on Windows) or a web browser
- An internet connection

You do **not** need an account or an API key.

## Step 1: Make your first request

Copy this command into your terminal and press Enter:

```
curl "https://api.frankfurter.dev/v1/latest?base=USD&symbols=EUR,GBP"
```

If you use Windows PowerShell, type `curl.exe` instead of `curl`.

You can also paste the web address (the part in quotes) into your browser's address bar.

## Step 2: Read the response

You should see something like this:

```json
{"amount":1.0,"base":"USD","date":"2026-10-08","rates":{"EUR":0.89397,"GBP":0.75718}}
```

Your numbers will be different, because rates change over time. Here is what each part means:

| Field | Meaning |
|---|---|
| `amount` | The amount being converted. It is 1 unless you ask for something else. |
| `base` | The currency you are converting from. |
| `date` | The date the rates apply to. |
| `rates` | The results. Here, 1 US dollar is worth about 0.89 euros and 0.76 British pounds. |

## Step 3: Change the currencies

The `base` is the currency you start from, and `symbols` lists the currencies you want to convert to.

To convert euros to Indian rupees:

```
curl "https://api.frankfurter.dev/v1/latest?base=EUR&symbols=INR"
```

Response:

```json
{"amount":1.0,"base":"EUR","date":"2026-10-08","rates":{"INR":108.2635}}
```

To see every currency you can use, request the list:

```
curl "https://api.frankfurter.dev/v1/currencies"
```

## Step 4: Get a rate from a past date

Put the date in the web address, in the format `YYYY-MM-DD`:

```
curl "https://api.frankfurter.dev/v1/2025-01-02?base=USD&symbols=EUR"
```

Response:

```json
{"amount":1.0,"base":"USD","date":"2025-01-02","rates":{"EUR":0.9689}}
```

## Good to know

- **"Latest" can be a day behind.** Rates are published once per working day, so the `date` in the response may be earlier than today.
- **Weekend dates return the previous working day.** If you ask for a Saturday, the API still returns a normal response, but the `date` field shows the Friday it used. Always check the `date` in the response rather than assuming it matches the date you asked for.
- **These are reference rates.** They are useful for information and conversions in apps, but they are not live trading quotes.

## Something went wrong?

If you see a message like `{"message":"not found"}`, check your currency codes and the web address. See the [error reference](errors.md) for the full list of errors and how to fix them.

## Next steps

- [Use case: convert an amount between currencies](guide-currency-conversion.md)
- [Error reference](errors.md)
- [Sequence diagram of a request](sequence-diagram.md)

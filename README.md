# Bank Account SMS Notifier

A simple Python demo that simulates basic bank account operations — **withdraw** and **deposit** — and sends **real-time SMS notifications** to the account holder using the [Twilio](https://www.twilio.com/) API.

## Features

- Deposit and withdraw funds from an in-memory account balance
- Custom exception (`InvalidAccountError`) for invalid operations (e.g. insufficient funds, non-positive deposits)
- Automatic SMS alerts on successful transactions **and** on failed ones, via Twilio
- Balance displayed in Indian Rupees (₹)

## Requirements

- Python 3.7+
- A [Twilio](https://www.twilio.com/) account with:
  - Account SID
  - Auth Token
  - A Twilio phone number capable of sending SMS

Install the Twilio Python SDK:

```bash
pip install twilio
```

## Setup

1. Clone this repository.
2. Install dependencies (see above).
3. Set your Twilio credentials. **Do not hardcode them in the script** — use environment variables instead:

   ```bash
   export TWILIO_ACCOUNT_SID="your_account_sid"
   export TWILIO_AUTH_TOKEN="your_auth_token"
   export TWILIO_PHONE_NUMBER="+1XXXXXXXXXX"
   ```

   And update the code to read them, e.g.:

   ```python
   import os

   self.account_sid = os.environ["TWILIO_ACCOUNT_SID"]
   self.auth_token = os.environ["TWILIO_AUTH_TOKEN"]
   self.twilio_number = os.environ["TWILIO_PHONE_NUMBER"]
   ```

4. Set the recipient's phone number (in E.164 format, e.g. `+91XXXXXXXXXX`) when creating a `BankAccount` instance.

## Usage

Run the script:

```bash
python bank_account.py
```

You'll be prompted to enter a withdrawal amount and a deposit amount. The script will:

- Update the account balance
- Print the result to the console
- Send an SMS notification to the configured phone number

### Example

```python
account = BankAccount("U0998XXXXXX97", 10000, "+91XXXXXXXXXX")
account.withdraw(500)   # Deducts ₹500, sends SMS confirmation
account.deposit(1000)   # Adds ₹1000, sends SMS confirmation
```

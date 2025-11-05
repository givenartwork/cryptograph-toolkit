## Cryptograph Toolkit

A simple, interactive toolkit for hashing files, checking file integrity, performing AES/RSA encryption-decryption demos, and basic password hygiene (strength checks and verification).

### Features

- **File hashing (SHA-256)**: Compute a file's hash and compare two files for integrity.
- **AES-GCM demo**: Generate a random key/nonce, encrypt and decrypt a provided message.
- **RSA-OAEP demo**: Generate ephemeral RSA keys, encrypt and decrypt a provided message.
- **Password helper**: Assess password strength with `zxcvbn`, hash with `bcrypt`, and verify.

### Project structure

```text
cryptograph-toolkit/
├─ README.md
├─ requirements.txt
└─ venv/
   ├─ main.py
   ├─ modules/
   │  ├─ encryption.py   # AES-GCM and RSA-OAEP demos
   │  ├─ hash.py         # SHA-256 hashing + file integrity check
   │  └─ password.py     # zxcvbn strength, bcrypt hash/verify
   └─ sample_files/
      ├─ sample.txt
      ├─ btc-nyt-ccp.svg
      └─ ccp-nyt-btc-table-big.png
```

Note: In this project, the runnable sources live under the `venv/` directory alongside the Python virtual environment. This is unconventional, but the commands below account for it.

### Requirements

- Python 3.13 (or compatible Python 3.x)
- macOS (other platforms may also work)

Python packages (installed via `requirements.txt`):

- `cryptography`
- `bcrypt`
- `zxcvbn`

### Setup

1. (Recommended) Activate the provided virtual environment:

```bash
source venv/bin/activate
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

If you prefer creating a fresh environment instead of using the included one:

```bash
/usr/bin/python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

### Run

From the project root (after activating your environment):

```bash
python venv/main.py
```

You will see a menu like:

```
Select operation:
1. Hash file
2. Check file integrity
3. AES Encrypt/Decrypt
4. RSA Encrypt/Decrypt
5. Password Manager
0. Exit
```

### Usage details

- **1. Hash file**: Provide a path to any file. The tool prints its SHA-256 hex digest.
- **2. Check file integrity**: Provide two file paths. The tool computes both hashes and tells you whether they match.
- **3. AES Encrypt/Decrypt**: Enter a message. The tool randomly generates a 256-bit key and 96-bit nonce, returns the key, ciphertext (nonce + ciphertext), and the decrypted plaintext.
- **4. RSA Encrypt/Decrypt**: Enter a message. The tool generates an ephemeral RSA key pair (2048-bit), encrypts with the public key (OAEP-SHA256), and decrypts with the private key.
- **5. Password Manager**:
  - Enter a password to assess strength via `zxcvbn`. If weak, you'll be prompted to choose stronger.
  - A strong password is hashed with `bcrypt` and shown.
  - Re-enter the password to verify; the tool confirms whether it matches the stored hash.

### Sample files

You can experiment with integrity checks using files in `venv/sample_files/`, e.g.:

```bash
python venv/main.py
# Choose 2. Check file integrity
# file path 1: venv/sample_files/btc-nyt-ccp.svg
# file path 2: venv/sample_files/ccp-nyt-btc-table-big.png
```

### Security notes

- AES/RSA demos generate keys on-the-fly and print sensitive values to stdout. This is for demonstration only; do not use this pattern for production.
- The password flow prints a bcrypt hash (safe to store) but never prints the raw password.
- Always handle secrets carefully and avoid logging them in real applications.

### Troubleshooting

- If `bcrypt` raises build or import issues, ensure you’re using the activated virtual environment and that your Python version matches wheels available for your platform.
- If `cryptography` fails to import, reinstall dependencies inside the active environment: `pip install -r requirements.txt`.

### License

MIT (or your preferred license). Update this section as needed.

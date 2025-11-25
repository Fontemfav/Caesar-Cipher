# Caesar-Cipher


The **Caesar cipher** is a basic substitution cipher that shifts every letter in the plaintext by a fixed number of positions down the alphabet.
Example with a shift of 3: `A → D`, `B → E`, `Z → C`. It’s easy to implement and good for learning about cryptography, but **not secure** for real-world encryption.

---

# How it works (rules)

* Only alphabetic characters are shifted; other characters (spaces, punctuation, digits) are left unchanged.
* Case is preserved (`A` vs `a`).
* Shifts wrap around the alphabet (`z` with shift 3 → `c`).

---

# Example

Plaintext: `Hello, World!`
Shift: `3`
Ciphertext: `Khoor, Zruog!`

---

# Python Implementation (encrypt, decrypt, brute-force)

```python
# caesar_cipher.py
import string

ALPHABET_LOWER = string.ascii_lowercase
ALPHABET_UPPER = string.ascii_uppercase

def shift_char(c, shift):
    if c.islower():
        idx = ALPHABET_LOWER.index(c)
        return ALPHABET_LOWER[(idx + shift) % 26]
    if c.isupper():
        idx = ALPHABET_UPPER.index(c)
        return ALPHABET_UPPER[(idx + shift) % 26]
    return c  # non-letter characters unchanged

def encrypt(plaintext, shift):
    """Return ciphertext by shifting letters forward by `shift`."""
    return ''.join(shift_char(c, shift) for c in plaintext)

def decrypt(ciphertext, shift):
    """Return plaintext by shifting letters backward by `shift`."""
    return encrypt(ciphertext, -shift % 26)

def brute_force(ciphertext):
    """Try all 26 shifts and return candidate plaintexts."""
    candidates = []
    for s in range(26):
        candidates.append((s, decrypt(ciphertext, s)))
    return candidates

# Simple demo when run as script
if __name__ == "__main__":
    text = "Hello, World!"
    s = 3
    ct = encrypt(text, s)
    print("Plain:", text)
    print("Shift:", s)
    print("Cipher:", ct)
    print("Decrypt:", decrypt(ct, s))

    # Brute force example
    print("\nBrute force candidates:")
    for shift_no, candidate in brute_force(ct):
        print(f"{shift_no:2}: {candidate}")
```

---

# JavaScript (browser / Node) quick version

```javascript
// caesar.js
function shiftChar(c, shift) {
  const A = 'A'.charCodeAt(0);
  const a = 'a'.charCodeAt(0);
  const code = c.charCodeAt(0);
  if (code >= a && code <= a + 25) {
    return String.fromCharCode(((code - a + shift) % 26 + 26) % 26 + a);
  }
  if (code >= A && code <= A + 25) {
    return String.fromCharCode(((code - A + shift) % 26 + 26) % 26 + A);
  }
  return c;
}

function encrypt(text, shift) {
  return text.split('').map(ch => shiftChar(ch, shift)).join('');
}

function decrypt(text, shift) {
  return encrypt(text, (26 - (shift % 26)) % 26);
}

// Example
console.log(encrypt("Hello, World!", 3)); // Khoor, Zruog!
```

---

# How to run locally (Python)

1. Save the Python code above to `caesar_cipher.py`.
2. Open terminal / command prompt.
3. Run:

```bash
python caesar_cipher.py
```

You’ll see the example encrypt/decrypt and brute-force output.

---

# README snippet (copy-paste)

````
## Caesar Cipher

Simple implementation of the Caesar cipher (encrypt/decrypt and brute-force).

### Usage (Python)
1. `python caesar_cipher.py` — runs the demo.
2. Import `encrypt`, `decrypt`, `brute_force` from `caesar_cipher.py` to use in your code.

### Example
```py
from caesar_cipher import encrypt, decrypt
cipher = encrypt("Hello, World!", 3)   # Khoor, Zruog!
plain  = decrypt(cipher, 3)           # Hello, World!
````

```

---

# Notes & Security
- Caesar cipher is an educational cipher — not secure by modern standards.
- For real encryption use proven algorithms (AES, RSA) and established libraries.

---

Would you like me to:
- generate a ready-to-paste `README.md` with badges and examples?
- add a simple GUI (Tkinter) or web demo (Flask) to show encryption live?
- produce tests or expand to Vigenère cipher (a stronger classical cipher)?

Pick one and I’ll generate it right away.
```

# MauiMapMon

A Python tool for generating chaotic noise images using mathematical chaos maps — including the Logistic, Tent, and Henon maps. Outputs are validated against NIST randomness tests and a cryptographic key is derived from each generated sequence.

---

## Features

- Three chaos map types: **Logistic**, **Tent**, and **Henon**
- NIST statistical randomness tests (Frequency + Runs)
- PBKDF2-HMAC-SHA256 key derivation from generated sequences
- CLI mode for headless/bash use
- Optional Tkinter GUI (when a display is available)

---

## Requirements

Install dependencies via pip:

```bash
pip install numpy scipy cryptography matplotlib pillow
```

> **Note:** Tkinter is part of the Python standard library but may need to be installed separately on some systems:
> ```bash
> sudo apt install python3-tk   # Debian/Ubuntu
> brew install python-tk        # macOS with Homebrew
> ```

---

## Installation

```bash
git clone https://github.com/wifiknight45/MauiMapMon.git
cd MauiMapMon
pip install -r requirements.txt
```

---

## Usage

### CLI Mode (Bash)

Run the script directly. If no display is detected, it automatically launches in CLI mode:

```bash
python mauimapmon.py
```

You will be prompted to enter:

| Prompt | Description | Example |
|--------|-------------|---------|
| `x0` | Initial condition — a float between `0` and `1` | `0.5` |
| `param` | Map parameter (`r`, `mu`, or `a`) | `3.9` |
| `map_type` | One of: `logistic`, `tent`, `henon` | `logistic` |
| `filename` | Output `.png` filename | `output.png` |

**Example session:**

```bash
$ python mauimapmon.py
Chaotic Image Generator (CLI Mode)
Enter initial condition (x0, e.g., 0.5): 0.5
Enter parameter (r, mu, or a, e.g., 3.9): 3.9
Enter map type (logistic, tent, henon): logistic
Enter output filename (e.g., output.png): my_chaos.png

NIST Frequency Test Passed: True
NIST Runs Test Passed: True
Derived Key: a3f9c21b...
Image saved as my_chaos.png
```

### Force CLI Mode

To skip the GUI even when a display is available, pass any argument:

```bash
python mauimapmon.py --cli
```

### GUI Mode

If a display environment is detected and no arguments are passed, the Tkinter GUI launches automatically:

```bash
python mauimapmon.py
```

---

## Map Parameter Ranges

Each map type has valid parameter bounds. Values outside these ranges will raise an error.

| Map Type | Parameter | Valid Range | Chaotic Region |
|----------|-----------|-------------|----------------|
| Logistic | `r` | `0` – `4` | `r ≈ 3.57` to `4` |
| Tent | `mu` | `0` – `2` | `mu > 1` |
| Hénon | `a` | `0` – `1.4` | `a ≈ 1.4` |

---

## Output

- A **256×256 PNG image** filled with values derived from the chaotic sequence
- **NIST test results** printed to stdout
- A **PBKDF2-derived cryptographic key** (hex) printed to stdout

---

## Security Notes

- Each run injects `os.urandom` entropy into the initial condition, so outputs differ even with the same inputs
- The PBKDF2 key derivation uses 500,000 iterations with a random 16-byte salt
- Output filenames are sanitized — only alphanumeric characters, hyphens, underscores, and dots are accepted (must end in `.png`)

---

## License

MIT License — see [LICENSE](LICENSE) for details.

## Chaotic Maps Explained

MauiMapMon uses three chaotic maps to generate sequences. Each map exhibits chaotic behavior, producing unpredictable yet deterministic sequences ideal for randomness applications.

Logistic Map:
Definition: Defined by the equation x_{n+1} = r * x_n * (1 - x_n), where x_n is the current state (between 0 and 1) and r is a control parameter.
Behavior: For r between 3.57 and 4, the map produces chaotic sequences sensitive to initial conditions (x0). Small changes in x0 or r lead to vastly different outputs.
Use Case: Generates pseudo-random sequences for image pixel values due to its simplicity and chaotic properties.

Tent Map:
Definition: Defined as x_{n+1} = mu * x_n if x_n < 0.5, else x_{n+1} = mu * (1 - x_n), where x_n is the state (between 0 and 1) and mu is a parameter (typically 0 to 2).
Behavior: Resembles a tent shape, producing chaotic sequences for mu close to 2. It’s highly sensitive to initial conditions, similar to the Logistic map.
Use Case: Provides an alternative chaotic sequence with uniform distribution properties, suitable for cryptographic applications.

Henon Map:
Definition: A two-dimensional map defined by x_{n+1} = 1 - a * x_n^2 + y_n and y_{n+1} = b * x_n, where a and b are parameters (typically a=1.4, b=0.3).
Behavior: Produces chaotic sequences in a two-dimensional phase space, creating complex patterns. It’s more computationally intensive but offers richer dynamics.
Use Case: Generates intricate sequences for applications requiring higher-dimensional chaos, enhancing randomness in images.

# MauiMapMon
1st gen) a chaos-based PRNG using the logistic map to generate cryptographic keys, blending Hawaiian vibes, reggae rhythms, and secure randomness for key generation.
update

# MauiMapMon

MauiMapMon is a Python-based chaotic image generator that leverages chaotic maps (Logistic, Tent, and Henon) to produce random images and derive cryptographic keys. It includes NIST randomness tests to validate sequence randomness and supports both a graphical user interface (GUI) and a command-line interface (CLI) for flexibility across environments.

## Features

- **Chaotic Maps**: Generate sequences using Logistic, Tent, or Henon maps.
- **Image Generation**: Create visually unique images from normalized chaotic sequences.
- **NIST Randomness Tests**: Validate randomness with Frequency and Runs tests.
- **Cryptographic Key Derivation**: Derive secure keys using PBKDF2-HMAC-SHA256.
- **GUI and CLI Support**: Use a Tkinter-based GUI or CLI for headless environments.
- **Security Enhancements**:
  - Secure random seed initialization with `os.urandom`.
  - Input sanitization to prevent invalid or malicious inputs.
  - Enhanced key stretching with high PBKDF2 iteration counts.
- **Image Saving**: Save generated images as PNG files.
- **Visualization**: Display chaotic patterns using Matplotlib.

## Requirements

- Python 3.8+
- Required packages:
  - `numpy`
  - `scipy`
  - `cryptography`
  - `pillow`
  - `matplotlib`
  - `tkinter` (optional for GUI, included in standard Python library)

Install dependencies using:

```bash
pip install numpy scipy cryptography pillow matplotlib
```

## Usage

### GUI Mode
Run the script in a graphical environment:

```bash
python mauimapmon.py
```

- Enter initial condition (`x0`), parameter (`r`, `mu`, or `a`), and select a map type.
- Click "Generate Image" to create and display the image.
- Click "Save Image" to save as a PNG file.

### CLI Mode
Run in a terminal or non-graphical environment:

```bash
python mauimapmon.py --cli
```

- Follow prompts to input `x0`, parameter, map type, and output filename.
- The image is generated and saved as specified.

## Example

Generate an image using the Logistic map with `x0=0.5` and `r=3.9`:

- **GUI**: Enter `0.5` for `x0`, `3.9` for parameter, select "Logistic," and generate.
- **CLI**:
  ```bash
  Enter initial condition (x0, e.g., 0.5): 0.5
  Enter parameter (r, mu, or a, e.g., 3.9): 3.9
  Enter map type (logistic, tent, henon): logistic
  Enter output filename (e.g., output.png): chaotic.png
  ```

Output includes NIST test results and a derived key in the console.

## Security Notes

- **Input Validation**: Parameters and filenames are sanitized to prevent exploits.
- **Randomness**: Sequences are seeded with cryptographically secure randomness.
- **Key Derivation**: Uses 500,000 PBKDF2 iterations for robust key security.

## Limitations

- GUI requires a display environment (e.g., X11, Wayland). Use CLI for headless systems.
- Large images may require significant computation time due to chaotic iterations.
- Henon map parameters are constrained to ensure stability (`a ≤ 1.4`).

## License

MIT License. See `LICENSE` for details.

## Contributing

Contributions are welcome! Please submit issues or pull requests on GitHub.

##acknowledgements: Grok 3 by xAI, Google Colab, Microsoft Copilot were used to generate and modify this python script
for the purposes of learning and teaching others how to code and understand code. 

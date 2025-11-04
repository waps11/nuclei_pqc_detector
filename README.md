# Nuclei Template - Post-Quantum Cryptographic Cipher Suites Detection

## Description
This Nuclei template detects and extracts post-quantum cryptographic (PQC) cipher suites supported by TLS/SSL servers.

## Detected Algorithms

### Key Encapsulation Mechanisms (KEM)
- **Kyber** (512, 768, 1024) - NIST standardized algorithm
- **NTRU** - Robust alternative
- **Classic McEliece** - Based on error-correcting codes
- **SABER** - Algorithm based on Euclidean lattices

### Digital Signatures
- **Dilithium** (2, 3, 5) - NIST standardized
- **Falcon** (512, 1024) - Compact signatures
- **SPHINCS+** - Hash-based

### Hybrid Schemes
- X25519_Kyber768
- P256_Kyber512
- P384_Kyber768
- ECDHE_KYBER

## Installation

Make sure you have Nuclei installed:
```bash
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
```

## Usage

### Scan a single server
```bash
nuclei -t pqc-cipher-suites.yaml -u https://example.com
```

### Scan a list of servers
```bash
nuclei -t pqc-cipher-suites.yaml -l servers.txt
```

### Scan with a custom port
```bash
nuclei -t pqc-cipher-suites.yaml -u https://example.com:8443 -var Port=8443
```

### Scan with verbosity
```bash
nuclei -t pqc-cipher-suites.yaml -l servers.txt -v
```

### Export results to JSON
```bash
nuclei -t pqc-cipher-suites.yaml -l servers.txt -json -o results.json
```

### Export results to Markdown
```bash
nuclei -t pqc-cipher-suites.yaml -l servers.txt -markdown-export results.md
```

## Server List File Format

Create a `servers.txt` file with one URL per line:
```
https://server1.example.com
https://server2.example.com:8443
https://server3.example.com:443
```

## Example Output

```
[pqc-cipher-suites-detection] [ssl] [info] https://example.com:443
  [pqc_ciphers] TLS_AES_256_GCM_SHA384_KYBER768
  [pqc_ciphers] X25519_KYBER768
  [tls_version] TLSv1.3
```

## Results Interpretation

- **INFO**: The server supports post-quantum cryptographic cipher suites
- Extractors display:
  - `pqc_ciphers`: Detected PQC cipher suites
  - `tls_version`: TLS protocol version
  - `all_cipher_info`: Complete cipher information

## Important Notes

1. **Limited current support**: Most production servers do not yet support PQC
2. **Experimental implementations**: Some servers may have test implementations
3. **Evolving standards**: Cipher suite names may vary by implementation
4. **Performance**: PQC algorithms may be slower than classical algorithms

## References

- [NIST Post-Quantum Cryptography](https://csrc.nist.gov/projects/post-quantum-cryptography)
- [Open Quantum Safe Project](https://openquantumsafe.org/)
- [Cloudflare PQC](https://blog.cloudflare.com/post-quantum-for-all/)

## License

This template is licensed under the GNU General Public License v3.0 (GPL-3.0).

See the [LICENSE](LICENSE) file for details or visit https://www.gnu.org/licenses/gpl-3.0.en.html

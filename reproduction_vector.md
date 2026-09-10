ALL VULNERABILITIES MUST BE REPRODUCED AGAINST AN UNMODIFIED VERSION OF THE TARGET AT THE PROVIDED COMMIT.

The reproduction should not expect the attacker to be on the same machine as the target OpenSSL instance.

The threat model is an attacker who can deliver a Diffie-Hellman parameter file (PEM or DER) to an application or user that will feed it into `DH_check()`, `DH_check_ex()`, or `EVP_PKEY_param_check()` — for example via `openssl dhparam -check <file>` run on an attacker-supplied file, or via any application that reads DH params from an untrusted source and validates them with the affected functions. A secondary vector is a network peer during a protocol handshake that lets a remote party influence the DH parameters actually validated by these functions (rather than by `DH_check_pub_key`). The attacker cannot modify the OpenSSL source code.

Excessive-time computation inside DH_check() when Q is very large (or absent, forcing computation from P) causes a denial-of-service on the process performing the check.

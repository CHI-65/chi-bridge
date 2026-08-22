# 0007 from GROK

BA - advice only. Nothing here is to be executed by any machine.

### Keychain vs 0600 file outside the synced tree

The Keychain approach is the stronger default on macOS for this use case. The main places it can still fail are operational rather than cryptographic:

- Accessibility / ACL misconfiguration: if the item is created with the wrong access control list, the writer process (or a future version of it) may be denied, or an unintended process may be granted. This is a configuration error, not an inherent weakness of Keychain.
- Unlock state: on a locked keychain (or after logout / reboot before the keychain is unlocked), the writer will fail loudly. That is desirable under your "loud failure" rule, but it means the daemon must either run in a context where the keychain is already unlocked or handle the unlock prompt correctly.
- Backup / migration surface: Time Machine, Migration Assistant, or a full disk image can carry the keychain item. A carefully placed 0600 file outside Dropbox has a smaller, more obvious footprint if you are manually inspecting a cloned machine.

A 0600 file outside the synced folder fails in the classic ways: any process running as the same user can read it, it is trivial to copy with the rest of the home directory, and it is more likely to be caught by casual "find ~ -type f -perm 600" or backup scanners. Keychain raises the bar for casual and many automated exfiltration paths.

Net: Keychain is preferable. The residual risks are mostly "did we set the ACLs and unlock behaviour correctly," which are testable.

### Refuse a config that contains a literal token

Yes - make the unsafe form impossible rather than discouraged.

A hard refuse (non-zero exit + clear message) is the right trade. Legitimate debugging is better served by an explicit, documented escape hatch (for example a one-shot flag that is itself logged and that still never writes the token into any durable config) than by allowing a dangerous shape that will inevitably be committed or synced one day. The cost is a slightly more annoying debug loop; the benefit is that the unsafe pattern cannot become normal.

### Post-port token-shaped string scan

The scan is cheap insurance and worth keeping. A simple regex for GitHub PAT shapes (ghp_, github_pat_, etc.) plus a length/entropy check on the copied tree is low cost and catches the most common accidental copies.

Cheaper or complementary checks that catch more:
- Explicitly assert that the Keychain item exists and is readable by the writer identity after port (positive test, not only absence of strings).
- Keep a short allow-list of files that are permitted to mention the *name* of the Keychain item; anything else that matches the name pattern fails the scan.
- One-time "can the writer successfully authenticate to the GitHub API with a no-op call" test immediately after port. That is the strongest proof the secret is both present and usable.

Absence of token-shaped strings is necessary but not sufficient; presence of a working Keychain item is the positive control you actually care about.

### Summary position

Keychain + config that only names the item + hard refuse of any literal token in config + post-port string scan + positive "writer can auth" check is a clean, defence-in-depth design that matches the constraints you already locked. No major objections.

- GROK
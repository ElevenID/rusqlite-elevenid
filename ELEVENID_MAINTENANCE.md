# ElevenID rusqlite maintenance

Upstream: https://github.com/rusqlite/rusqlite
Release base: v0.41.1, commit 18ee76dbb976d5ef7e37ad5a8fffae678ca21a78.
Owner: ElevenID. The owned default branch is main; inherited upstream master is preserved.

The only implementation delta is libsqlite3-sys selecting sqlcipher-src =420.0.0,
whose published package is 420.0.0+sqlcipher-4.20.0-sqlite-3.54.1-libtomcrypt-1.18.2.
RUSTSEC-2026-0459 affects the earlier bundled SQLite, including the SQLCipher419
source still pinned by upstream libsqlite3-sys0.39.1. This update retains SQLCipher
and all upstream encryption, feature, OpenSSL, build and runtime API behavior.
No plaintext backend or advisory exception is introduced. The source crate's
Rust1.81 requirement remains below libsqlite3-sys1.88/rusqlite1.89 requirements.
Upstream licensing and copyright files remain unchanged.

Qualification must cover actual encrypted database creation, reopen, wrong-key
refusal and integrity, plus the consuming Core advisory gate. Consumers pin an
immutable commit accepted on this default branch, not a moving branch or tag.

Review upstream monthly and integrate updates only through reviewed internal PRs;
never auto-merge or force-push. Retire this delta after an upstream release ships
the patched SQLCipher source and the same encryption checks pass. No upstream PR
or maintainer contact is implied by this owned fork.

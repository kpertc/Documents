message-digest algorithm

designed for use as a secure cryptographic hash algorithm for authenticating digital signature

no longer safe - collisions practical since 2004, chosen-prefix since 2009

collision resistance broken, preimage not -> ok as plain checksum (dedupe, cache key), never signatures / passwords -> SHA-256, bcrypt / argon2
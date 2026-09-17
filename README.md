## Joshua Chaparro

Computer Engineering + Actuarial Science at ITAM, Mexico City. Vice President of the ITAM
Cybersecurity Center. I write C++ and Python, and most of what I build ends up circling the
same question: how do I know this is actually correct?

**Right now I'm building a local LLM orchestrator in C++17.** It hands coding tasks to models
running locally through Ollama, and every answer goes through a mechanical gate — compile, run
the tests, run the sanitizers — before anything is accepted. The gate exists because of a
measurement: in 3 of 3 benchmark runs the local models returned answers that were conceptually
right and wrong in the details. That is the failure mode worth building against, because it
reads as correct. Private repo until it stabilizes.

### Repositories

**[production-monitoring-system](https://github.com/JoshuaChapS/production-monitoring-system)**
· C++, Splunk, React

An incident pipeline end to end: a C++ log generator writes trading-app logs, Splunk detects the
error-rate spike and fires a webhook at a C++ REST API, the API opens a ticket in SQLite, and a
React dashboard routes it to a team. Then I audited my own code, and that is the part I'd rather
talk about. The best finding was a username-enumeration timing oracle in the login path — a wrong
username answered faster than a wrong password, which leaks which accounts exist. I equalized the
key-derivation cost across both branches and measured the gap from 12.4× down to 1.0×. The same
audit replaced bare SHA-256 password hashing with Argon2id via libsodium, and added refresh-token
rotation with server-side revocation. CI runs three build jobs under `-Wall -Wextra` on every pull
request, and `main` won't merge without all three green.

**[ctf-writeups](https://github.com/JoshuaChapS/ctf-writeups)** · binary exploitation, pwntools

Seven writeups: picoCTF buffer overflow 0 through 3, plus ret2win, split and callme from ROP
Emporium. Exact-offset return overwrites, building a 32-bit call frame by hand, brute-forcing a
per-instance stack canary one byte at a time, multi-gadget ROP chains on x86 and x86-64. Every
writeup has a **What I tripped on** section, because the dead ends are the part I actually learned
from. I solved every binary exploitation challenge at CTF BAL 2025.

**[Leetcodes](https://github.com/JoshuaChapS/Leetcodes)** · C++, some Python and Java

38 problems, solved cold in C++ because that's the language I want to be interviewed in. Each
commit message states the approach and the complexity, so the history reads as a record of
patterns instead of a pile of files. I also write the weekly problem set for the Cybersecurity
Center.

### Currently

Learning C++ properly rather than quickly — build systems, sanitizers, and the semantics I used to
get away with not knowing. Security is the field I want. Correctness is the part of it I find most
interesting.

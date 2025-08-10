# Steg_Aug_Scholarship
A public repository - Steg Scholarship 

# Software Development Life Cycle (SDLC)

**Software Development Life Cycle (SDLC)** is a structured process used to design, develop, test, and deploy software applications. It provides a clear framework to ensure software meets quality standards, budget limits, and deadlines.

## Main Phases of SDLC
1. **Planning** – Defining project scope, objectives, resources, and timelines.  
2. **Requirements Analysis** – Gathering and documenting functional and non-functional requirements.  
3. **Design** – Creating the architecture, system models, and user interfaces.  
4. **Development** – Writing and compiling the actual code.  
5. **Testing** – Verifying the software works as intended and is free of defects.  
6. **Deployment** – Releasing the software to users or production environments.  
7. **Maintenance** – Updating, fixing, and improving the software after release.  

## SDLC Models
Common SDLC models include **Waterfall**, **Agile**, **Iterative**, and **Spiral**, each suited for different project needs.

By following SDLC, organizations reduce risks, manage costs, and deliver high-quality software aligned with user needs.


# LAMP Stack Framework

**LAMP** is a popular open-source web development stack used to build dynamic websites and applications. The acronym stands for:

1. **Linux** – The operating system that provides the foundation for the stack.
2. **Apache** – The web server software responsible for serving web pages to users.
3. **MySQL** – The relational database management system used to store and manage data.
4. **PHP** – The server-side scripting language used to develop dynamic content and interact with the database.

## How It Works
- **Linux** hosts the stack and provides stability, security, and scalability.
- **Apache** processes incoming HTTP requests and serves the correct responses.
- **MySQL** stores application data and enables data retrieval through queries.
- **PHP** runs server-side scripts, processes data, and generates dynamic web pages.

## Advantages
- Open-source and free to use.
- Large community support.
- Cross-platform development flexibility.
- Secure, stable, and scalable for different project sizes.

The LAMP stack remains a foundational technology for web development, offering a proven and reliable framework for building modern applications.


# Understanding `chmod` and `chown` in Linux

## File Access and Ownership in Linux
In Linux, every file and directory has:
- **Owner** – The user who owns the file.
- **Group** – A set of users who share the same group permissions.
- **Others** – All other users on the system.

Each file has three types of permissions:
- **Read (r)** – View file contents or list directory contents.
- **Write (w)** – Modify file contents or create/delete files in a directory.
- **Execute (x)** – Run a file as a program/script or access directory contents.

Permissions are displayed using the `ls -l` command:
```
-rwxr-xr--  1 user group 4096 Jan 1  file.txt
```
Here:
- **rwx** – Owner permissions (read, write, execute).
- **r-x** – Group permissions (read, execute).
- **r--** – Others permissions (read only).

## The `chmod` Command
`chmod` changes file or directory permissions.

### Syntax:
```
chmod [options] mode file
```
**Modes can be specified as:**
- **Symbolic**: `chmod u+x file` (add execute for user/owner)
- **Numeric (octal)**: `chmod 755 file`
    - Read = 4, Write = 2, Execute = 1
    - Example: 7 (rwx) = 4+2+1, 5 (r-x) = 4+0+1

### Examples:
```
chmod u+x script.sh      # Add execute permission for owner
chmod 644 file.txt       # Owner: read/write, Group: read, Others: read
chmod -R 755 /var/www    # Recursively set rwx for owner, rx for group/others
```

## The `chown` Command
`chown` changes file or directory ownership.

### Syntax:
```
chown [options] new_owner:new_group file
```
- `new_owner` – The username of the new owner.
- `new_group` – (Optional) The group name.

### Examples:
```
chown john file.txt         # Change owner to john
chown john:developers file  # Change owner to john and group to developers
chown -R root:root /var/www # Recursively change owner and group to root
```

## Key Notes
- Only the **root user** or file **owner** can change permissions with `chmod`.
- Only **root** can change ownership with `chown`.
- Permissions and ownership are fundamental to Linux security, controlling who can access or modify files.

# TCP vs UDP and Common Web Ports

**Overview**
- **TCP (Transmission Control Protocol)** is connection-oriented and ensures reliable, ordered delivery of data.
- **UDP (User Datagram Protocol)** is connectionless and prioritizes low-latency over reliability.

## Key Features
- **TCP**
  - Three-way handshake (connection setup)
  - Ordered, reliable delivery with error-checking and retransmission
  - Suitable for web pages, email, and file transfers

- **UDP**
  - No handshake; sends independent datagrams
  - Lower overhead and latency; no guaranteed delivery or ordering
  - Suitable for streaming, gaming, VoIP, and DNS queries

## Differences (short)
- Reliability: TCP ✅ / UDP ❌  
- Ordering: TCP ✅ / UDP ❌  
- Speed/Latency: TCP slower / UDP faster  
- Use cases: TCP for reliability; UDP for speed and real-time data

## Common Ports (examples)
| Port | Protocol | Service / Use |
|------|----------|---------------|
| 80   | TCP      | HTTP (web) |
| 443  | TCP      | HTTPS (secure web) |
| 22   | TCP      | SSH (secure shell) |
| 21   | TCP      | FTP (file transfer) |
| 53   | UDP/TCP  | DNS (queries use UDP; zone transfers use TCP) |
| 25   | TCP      | SMTP (send email) |
| 110  | TCP      | POP3 (retrieve email) |
| 143  | TCP      | IMAP (email access) |
| 3306 | TCP      | MySQL database |
| 8080 | TCP      | Alternative HTTP / proxy port |

## Examples
- Loading a website: client opens a **TCP** connection to port **80/443**; data is delivered reliably.
- DNS lookup: typically uses **UDP** on port **53** for fast queries; if response is large, TCP may be used.

## Quick Recommendations
- Use **TCP** when data integrity and order matter (web, file transfer, email).
- Use **UDP** for real-time applications where small delays are worse than occasional packet loss (voice/video/gaming).



# vi Editor — Quick Reference (Basics & Common Commands)

**vi** is a modal text editor found on most Unix-like systems. Below is a concise guide to modes, common commands, and useful tips to get productive quickly.

## Modes
- **Normal (command) mode** — default mode for navigation and commands. Press `Esc` to enter.
- **Insert mode** — for typing text. Enter with `i`, `a`, `o`, etc.
- **Visual mode** — for selecting text (`v` for character, `V` for line).
- **Command-line mode** — for file operations and more (`:` after Esc).

## Starting vi
```bash
vi filename.txt
```

## Basic Navigation (from Normal mode)
- `h` `j` `k` `l` — left, down, up, right (arrow keys also work).  
- `w` / `W` — jump to next word.  
- `b` — back to previous word.  
- `0` — start of line. `$` — end of line.  
- `gg` — go to start of file. `G` — go to end of file.  
- `:n` — go to line number `n` (e.g., `:42`).

## Entering Insert Mode
- `i` — insert before cursor.  
- `I` — insert at start of line.  
- `a` — append after cursor.  
- `A` — append at end of line.  
- `o` — open new line below and enter insert mode. `O` — open above.

Press `Esc` to return to Normal mode.

## Editing & Deleting (Normal mode)
- `x` — delete character under cursor.  
- `dw` — delete from cursor to start of next word.  
- `dd` — delete (cut) entire line.  
- `D` or `d$` — delete to end of line.  
- `~` — toggle case of character.  
- `r<char>` — replace single character with `<char>`.

## Yank (copy) & Paste
- `yy` — yank (copy) current line.  
- `nyy` — yank `n` lines (e.g., `3yy`).  
- `p` — paste after cursor (or below line). `P` — paste before cursor (or above line).

## Undo & Redo
- `u` — undo last change.  
- `U` — undo all changes on the current line.  
- `Ctrl-R` — redo.

## Visual Mode (selecting text)
- `v` — start character-wise visual selection.  
- `V` — start line-wise visual selection.  
- After selecting, use `y` to yank, `d` to delete, or `>`/`<` to indent/outdent.

## Search & Replace
- `/pattern` — search forward for `pattern`. Press `n` for next, `N` for previous.  
- `?pattern` — search backward.  
- `:s/old/new/g` — replace in current line.  
- `:%s/old/new/g` — replace in entire file. Add `c` (e.g., `:%s/old/new/gc`) to confirm each replacement.

## Saving & Exiting (Command-line mode)
(type after pressing `Esc` then `:`)
- `:w` — save (write) file.  
- `:q` — quit (fails if unsaved changes).  
- `:wq` or `:x` — save and quit.  
- `:q!` — quit and discard changes.

## Other Useful Commands
- `:set number` — show line numbers.  
- `:set nonumber` — hide line numbers.  
- `>>` / `<<` — indent / outdent current line.  
- `J` — join the current line with the next line.  
- `.%p` or `:!wc -l %` — run external commands on file (`%` expands to current filename).

## Tips
- Remember to press `Esc` before using navigation or command sequences.  
- Combine counts with commands (e.g., `5j` moves down 5 lines, `3dw` deletes 3 words).  
- `vi` on some systems is a minimal editor; `vim` (Vi IMproved) adds many conveniences (clipboard, plugins).

---



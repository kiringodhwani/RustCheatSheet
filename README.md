# RustCheatSheet

## Cargo
- **<u>cargo</u>** = build system, package manager, important for managing dependencies (this is a pain point with other low-level programming languages so it is really nice that rust has it built in).

When you add dependencies to `cargo.toml`, you have to run `cargo build` to install:

\underline{Example:}
  [package]
  name = "guessing_game"
  version = "0.1.0"
  edition = "2024"

  [dependencies]
  rand = "0.5.5"  // added this dependency

**TO combpile a project, installs dependencies and necessary things for the dependency:** `cargo build`

**TO make new project**: cargo new {project_name}

**TO check code for errors without producing an executable:** cargo check

**TO compile (if necessary) and run project:** cargo run

# Opencode Docker

**Opencode Docker** is a Docker container that provides the **opencode-ai** CLI tool in an isolated environment. Opencode is an ai interactive CLI tool that helps users with software engineering tasks.

---

## Features

- Run opencode-ai in an isolated Docker container
- No need to install Node.js or npm locally
- Mount your project directory as a volume
- Works on any system with Docker installed

---

## Usage

### Build the Docker Image

```bash
docker build -t opencode .
```

### Run Opencode

To run opencode in the current directory:

```bash
docker run -it --rm -u $(id -u):$(id -g) -v "$(pwd):/workspace" opencode
```

---

## License

Released under the MIT/X License.

> RTFM,
> KISS

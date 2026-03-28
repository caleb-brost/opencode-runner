# OpenCode Local Runner

A portable CLI utility to launch **OpenCode** agents in secure Docker sandboxes.

This tool utilizes **Docker Model Runner (DMR)** to provide high-performance local inference via Qwen2.5-Coder. It eliminates the need for cloud API keys, monthly subscriptions, and the risk of exposing source code to external servers.

---

## Key Features

* **Privacy:** Your code and prompts remain on your local machine. Inference occurs on your local GPU/CPU.
* **Cost-Efficient:** No OpenAI or Anthropic API keys required. Operates without per-token charges.
* **Sandboxed Execution:** The AI agent operates within an isolated Docker container, protecting the host file system.
* **Zero Configuration:** Automatically generates runtime configurations, removing the need for local `.env` or `config.json` files in every project.
* **Global Access:** Execute `opencode .` from any directory to initiate an AI-assisted session.

---

## Requirements

* **Docker Desktop:** Version 4.34.0 or higher.
* **AI Features:** "Model Runner" must be enabled in Docker Desktop settings.
* **Hardware:** 16GB RAM recommended for optimal performance with 7B models.

---

## Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/opencode-runner.git
   cd opencode-runner
   ```

2. **Run the installer:**
   This script symlinks the runner to your `~/bin` folder and sets the necessary permissions.
   ```bash
   chmod +x install.sh
   ./install.sh
   ```

3. **Verify PATH:**
   Ensure `~/bin` is in your shell's PATH. If it is not, add the following to your `~/.zshrc` or `~/.bashrc`:
   ```bash
   export PATH="$HOME/bin:$PATH"
   ```

---

## Usage

Navigate to any project directory and execute:

```bash
opencode .
```

### Process Overview
1. **Environment Check:** Verifies Docker and Model Runner status.
2. **Model Verification:** Ensures `ai/qwen2.5-coder` is present locally.
3. **Runtime Config:** Generates a temporary hidden configuration to bridge the agent to local hardware.
4. **Sandbox Launch:** Initializes the OpenCode agent with a volume mount to the current directory.
5. **Cleanup:** Removes temporary configuration files upon session exit.

---

## Customization

To modify the default model for different hardware constraints, edit the `MODEL` variable in `bin/opencode`:

```bash
# Example for low-resource environments
MODEL="ai/smollm2-1.7b-instruct"
```

---

## License
MIT License
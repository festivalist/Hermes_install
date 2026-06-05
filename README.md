# Hermes + SGLang install guide
# 1.WSL2 und Systemabhängigkeiten installieren
- Windows PowerShell als Administrator ausführen.Die native Nutzung von Hermes unter Windows wird nicht unterstützt, weshalb die WSL2-Umgebung (Ubuntu) zwingend erforderlich ist
- Bash `wsl --install`
- Nach einem PC-Neustart öffne das neue Ubuntu-Terminal und aktualisiere die Paketquellen, gefolgt von der Git-Installation
- `sudo apt update && sudo apt upgrade -y`
- `sudo apt install git -y`
# 2 SGLnag installieren in WSL
- sudo apt install -y build-essential curl git python3-pip python3-venv
- `uv` installation per `curl -LsSf https://astral.sh/uv/install.sh | sh`
- dann Pfad-Variablen neu laden: `source $HOME/.local/bin/env`
- SGLang-Umgebung erstellen:
```
uv venv sglang-env --python 3.11
source sglang-env/bin/activate
```
- SGLang & Core-Kernels installieren `uv pip install sglang`
- Installation überprüfen `python -c "import sglang; print(sglang.__version__)"`
- weitere pakete installieren `sudo apt-get update && sudo apt-get install -y libnuma-dev`
- ( model laden `ollama run hf.co/OBLITERATUS/Qwen3.6-27B-OBLITERATED:Q4_K_M` (Link von hugginface)
- ^ kann an der stelle ignoriert werden da wir uns das modell gleich anders laden
- weitere
```
uv pip install gguf

uv pip install huggingface_hub

huggingface-cli download OBLITERATUS/Qwen3.6-27B-OBLITERATED \
  --include "*Q4_K_M.gguf" \
  --local-dir ./qwen-obliterated
```

# 2.Lokalen Inferenz-Server einrichten in WSL
- Hermes Agent bietet Out-of-the-box-Unterstützung für Ollama
- Für ollama muss erst `zstd` installiert werden `sudo apt-get install zstd `
- Installiere dann Ollama direkt im WSL2-Terminal:
- Bash    `curl -fsSL https://ollama.com/install.sh | sh`
- Lade und starte das Qwen 3.6 Modell. Die 35-Milliarden-Parameter-Version (35B) benötigt rund 20 GB Arbeitsspeicher und passt damit ideal in den 24 GB großen VRAM der verbauten RTX 3090 Ti [1]
- Bash `ollama run qwen3.6:35b`
# 3.Hermes Agent herunterladen und installieren in WSL
- Führe das offizielle Installationsskript von Nous Research im WSL2-Terminal aus:
- Bash    `curl -fsSL https://hermes-agent.nousresearch.com/install.sh | bash`
- Lade anschließend die Konfiguration der Shell neu, um den Agenten global verfügbar zu machen:Bash `source ~/.bashrc`
# 4.Hermes und Qwen 3.6 verknüpfen
- Starte das Konfigurationsmenü des Agenten: Bash `hermes setup`
- Wähle den Menüpunkt Model & Provider aus.
- Konfiguriere Ollama als Provider und setze die API Base URL auf `http://localhost:11434/v1` .
- Das System erkennt Qwen 3.6 via GET-Request an die /v1/models-Schnittstelle automatisch; bestätige die Nutzung mit Y.
- Der Agent ist nun einsatzbereit und kann fortan mit dem Befehl `hermes` gestartet werden 

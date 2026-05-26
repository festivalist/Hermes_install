# Hermes install guide
# 1.WSL2 und Systemabhängigkeiten installieren
- Windows PowerShell als Administrator ausführen.Die native Nutzung von Hermes unter Windows wird nicht unterstützt, weshalb die WSL2-Umgebung (Ubuntu) zwingend erforderlich ist
- Bash `wsl --install`
- Nach einem PC-Neustart öffne das neue Ubuntu-Terminal und aktualisiere die Paketquellen, gefolgt von der Git-Installation
- `sudo apt update && sudo apt upgrade -y`
- `sudo apt install git -y`
# 2.Lokalen Inferenz-Server einrichten
- Hermes Agent bietet Out-of-the-box-Unterstützung für Ollama
- Für ollama muss erst `zstd` installiert werden `sudo apt-get install zstd `
- Installiere dann Ollama direkt im WSL2-Terminal:
- Bash    `curl -fsSL https://ollama.com/install.sh | sh`
- Lade und starte das Qwen 3.6 Modell. Die 35-Milliarden-Parameter-Version (35B) benötigt rund 20 GB Arbeitsspeicher und passt damit ideal in den 24 GB großen VRAM der verbauten RTX 3090 Ti [1]
- Bash `ollama run qwen3.6:35b`
- 

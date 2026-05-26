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
# 3.Hermes Agent herunterladen und installieren
- Führe das offizielle Installationsskript von Nous Research im WSL2-Terminal aus:
- Bash    `curl -fsSL https://hermes-agent.nousresearch.com/install.sh | bash`
- Lade anschließend die Konfiguration der Shell neu, um den Agenten global verfügbar zu machen:Bash `source ~/.bashrc`
# 4.Hermes und Qwen 3.6 verknüpfen
- Starte das Konfigurationsmenü des Agenten: Bash `hermes setup`
- Wähle den Menüpunkt Model & Provider aus. Konfiguriere Ollama als Provider und setze die API Base URL auf `http://localhost:11434/v1` . Das System erkennt Qwen 3.6 via GET-Request an die /v1/models-Schnittstelle automatisch; bestätige die Nutzung mit Y [4].Der Agent ist nun einsatzbereit und kann fortan mit dem Befehl hermes gestartet werden [2].

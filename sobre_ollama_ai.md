# Instalação
```
curl -fsSL https://ollama.com/install.sh | sh
```

# Logs
```
journalctl -u ollama
```

# Desinstalação
```
sudo systemctl stop ollama
sudo systemctl disable ollama
sudo rm /etc/systemd/system/ollama.service

sudo rm $(which ollama)

sudo rm -r /usr/share/ollama
sudo userdel ollama
sudo groupdel ollama
```

# Execução
```
ollama run <MODELS>
ollama run codellama
```

# Porta
```
http://localhost:11434/
```

# Exemplo
```
ollama run codellama '
Where is the bug in this code?

def fib(n):
    if n <= 0:
        return n
    else:
        return fib(n-1) + fib(n-2)
'
```


# Com WebUI
Interface similar ao Chat-GPT, rodando localmente
```
docker run -d --network=host -v open-webui:/app/backend/data -e OLLAMA_BASE_URL=http://127.0.0.1:11434 --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

# Porta
```
http://localhost:8080
```

# REFERÊNCIA
[Ollama Docs](https://github.com/ollama/ollama/blob/main/docs/linux.md)
[Ollama](https://ollama.com/)
[Ollama Models](https://ollama.com/library)
[Open WebUI](https://docs.openwebui.com/getting-started/)

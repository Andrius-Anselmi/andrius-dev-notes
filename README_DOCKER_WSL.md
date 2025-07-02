
# Como Usar Docker no WSL (Ubuntu)

Este passo a passo ajuda a rodar o Docker dentro do WSL, sem precisar usar o Docker Desktop.

---

## Passos para rodar Docker no WSL

1. **Abrir o terminal WSL**  
   No Windows, abra o PowerShell, CMD ou Terminal e execute:  
   ```bash
   wsl
   ```  
   Isso abre o shell do Ubuntu dentro do WSL.

2. **Verificar se o Docker daemon está rodando**  
   No terminal do Ubuntu, digite:  
   ```bash
   pgrep dockerd
   ```  
   - Se aparecer um número, o daemon está rodando.  
   - Se não aparecer nada, o daemon não está ativo.

3. **Iniciar o Docker daemon (se necessário)**  
   Se o daemon não estiver rodando, execute:  
   ```bash
   sudo dockerd &
   ```  
   Aguarde alguns segundos para o daemon subir.

4. **Usar comandos Docker normalmente**  
   Exemplos:  
   ```bash
   docker ps
   docker run hello-world
   ```

5. **Rodar comando Docker direto do Windows**  
   Sem abrir o shell do WSL, no PowerShell ou CMD do Windows execute:  
   ```bash
   wsl docker ps
   ```  
   Ou qualquer outro comando Docker substituindo `docker ps`.

6. **(Opcional) Script para facilitar iniciar o daemon e abrir shell**  

   Crie um arquivo `start-docker.sh` no Ubuntu com o conteúdo abaixo:

   ```bash
   #!/bin/bash
   if pgrep dockerd > /dev/null; then
       echo "Docker daemon já está rodando."
   else
       echo "Iniciando Docker daemon em background..."
       sudo nohup dockerd > /dev/null 2>&1 &
       sleep 5
   fi
   echo "Docker pronto! Use os comandos docker normalmente."
   bash
   ```

   Dê permissão para executar:  
   ```bash
   chmod +x start-docker.sh
   ```  
   Rode o script com:  
   ```bash
   ./start-docker.sh
   ```

---

Se precisar de ajuda, é só chamar!

# 🧩 Script: Processador de Logs

Este repositório contém um **script Bash** criado para **automatizar o processamento, filtragem e anonimização de logs**.  
O script organiza, limpa e compacta os arquivos de log, garantindo maior segurança e legibilidade para análise posterior.

---
## ⚙️ Funcionalidade

O script executa uma série de etapas para tratar os arquivos `.log` gerados pela aplicação:

1. **Criação de diretórios**:
   - Cria automaticamente as pastas necessárias para armazenar:
     - Logs processados (`logs-processados`)
     - Arquivos temporários (`logs-temp`)

2. **Filtragem de logs**:
   - Localiza todos os arquivos `.log` no diretório `../myapp/logs`.
   - Extrai apenas as linhas que contêm as palavras-chave:
     - `ERROR`
     - `SENSITIVE_DATA`

3. **Anonimização de dados sensíveis**:
   - Substitui informações confidenciais por `REDACTED`, incluindo:
     - Senhas de usuários  
     - Tokens de redefinição de senha  
     - Chaves de API  
     - Últimos dígitos de cartões de crédito  
     - Tokens de sessão

4. **Organização e estatísticas**:
   - Remove duplicatas e ordena as linhas.
   - Calcula o número de linhas e palavras de cada log.
   - Gera um arquivo `log_stats_<data>.txt` com as estatísticas do dia.

5. **Classificação por origem**:
   - Adiciona prefixos aos logs conforme sua origem:
     - `[FRONTEND]` — para arquivos com “frontend” no nome
     - `[BACKEND]` — para arquivos com “backend” no nome

6. **Combinação e compressão**:
   - Gera um único arquivo combinado com todos os logs processados (`logs_combinados_<data>.log`).
   - Compacta os resultados em um arquivo `.tar.gz`.
   - Limpa os arquivos temporários após a execução.

---

## 🛠️ Tecnologias Utilizadas

- **Bash** — Linguagem de script utilizada para automação e manipulação de arquivos no sistema Linux.
- **Comandos Unix**:
  - `grep` — Filtragem de padrões em arquivos.
  - `sed` — Substituição de textos e anonimização de dados.
  - `sort` e `uniq` — Organização e remoção de duplicatas.
  - `wc` — Contagem de palavras e linhas.
  - `tar` — Compactação de arquivos.
  - `find` — Busca de arquivos `.log` em diretórios.

---

## ▶️ Como Executar

1. Dê permissão de execução ao script:
```bash
chmod +x processar-logs.sh
```

2. Execute o script:
```bash
./processar-logs.sh
```

3. Após a execução, os logs tratados e comprimidos estarão disponíveis em:
```bash
../myapp/logs-processados/
```
---

## 📦 Saída Esperada

Após a execução bem-sucedida, serão gerados os seguintes arquivos:

- log_stats_<data>.txt — resumo estatístico dos logs processados.

- logs_combinados_<data>.log — arquivo consolidado com todos os logs filtrados e limpos.

- logs_<data>.tar.gz — pacote compactado com os arquivos finais.

---

## 🧹 Limpeza Automática

Ao final da execução, o diretório temporário logs-temp é removido automaticamente para manter o ambiente limpo.

---

## ⏰ Sugestão: Agendar Execução Automática com Cron

É possível automatizar a execução diária do script utilizando o crontab.

1. Edite o agendador de tarefas:
```bash
crontab -e
```

2. Será aberto um arquivo com instruções semelhantes a:
```bash
# Edit this file to introduce tasks to be run by cron.
#
# Each task to run has to be defined through a single line
# indicating with different fields when the task will be run
# and what command to run for the task
#
# m h  dom mon dow   command
```

3. Adicione a linha abaixo para executar o script todos os dias às 2h da manhã:
```bash
0 2 * * * /home/jezebel/scripts-linux/monitoramento-logs.sh
```

4. Para verificar os agendamentos ativos, use:
```bash
crontab -l
```

💡 Dessa forma, o processamento dos logs será realizado automaticamente todos os dias, sem necessidade de execução manual.

---
Feito com 💙 por [Jezebel Guedes](https://www.linkedin.com/in/jezebel-guedes/) durante a [Trilha DevOps da Alura](https://cursos.alura.com.br/course/linux-criando-script-processamento-arquivos-logs).
👋 Entre em contato!
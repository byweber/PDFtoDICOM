# Guia de Instalação e Deploy

Este documento descreve o procedimento técnico para implantar o **PDFtoDICOM Gateway**.

---

## 📋 Pré-requisitos de Infraestrutura

Antes de iniciar, verifique se o servidor atende aos requisitos abaixo:

### Sistema
- **Sistema Operacional:**  
  - Windows Server 2019 ou 2022  
  - Windows 10/11 Pro  
- **Permissões:**  
  - Acesso de **Administrador** (necessário para serviços e firewall)

### Rede
- Porta **8000/TCP** liberada no Firewall do Windows (entrada)
- Conectividade com o servidor PACS:
  - Host: `SEU_PACS`
  - Porta: `8042`

### Dependências de Software
Instale previamente:

- [Python 3.10 ou superior](https://www.python.org/downloads/)  
  > ⚠️ Marcar a opção **“Add Python to PATH”** durante a instalação
- [Git](https://git-scm.com/download/win) *(opcional, mas recomendado)*
- [NSSM – Non-Sucking Service Manager](https://nssm.cc/download)

---

## 🚀 Passo a Passo da Instalação

### 1️⃣ Obter o Código Fonte

Abra o **PowerShell** na pasta onde o sistema será instalado (exemplo: `C:\Sistemas`).

#### Opção A — Clonar via Git (recomendado)

```powershell
git clone https://github.com/byweber/PDFtoDICOM.git
cd PDFtoDICOM
Opção B — Download ZIP
Baixe o repositório como .zip

Extraia para:

text
Copiar código
C:\Sistemas\PDFtoDICOM
2️⃣ Criar Ambiente Virtual Python
Isolar o ambiente evita conflitos com outros sistemas do servidor.

powershell
Copiar código
python -m venv venv
Ative o ambiente virtual:

powershell
Copiar código
.\venv\Scripts\activate
✅ O prompt deve exibir (venv) antes do caminho

3️⃣ Instalar Dependências
Com o ambiente virtual ativo:

powershell
Copiar código
pip install -r requirements.txt --upgrade
4️⃣ Configuração de Ambiente (.env)
Crie um arquivo chamado .env na raiz do projeto:

text
Copiar código
C:\Sistemas\PDFtoDICOM\.env
Conteúdo do arquivo:

ini
Copiar código
# ===============================
# Configuração PACS
# ===============================
ORTHANC_URL=http://localhost:8042
ORTHANC_USER=orthanc
ORTHANC_PASSWORD=orthanc

# ===============================
# Configuração da Aplicação
# ===============================
APP_HOST=0.0.0.0
APP_PORT=8000
⚠️ Nunca versionar o arquivo .env no GitHub

🖥️ Configuração como Serviço Windows (NSSM)
Para garantir execução automática e reinício em falhas, o sistema será executado como serviço do Windows.

1. Preparação
Copie o nssm.exe para:

C:\Sistemas\PDFtoDICOM\

ou para um diretório já presente no PATH

2. Criar o Serviço
Abra o PowerShell como Administrador e execute:

powershell
Copiar código
.\nssm.exe install PDF2DICOM
3. Configuração do Serviço
Na janela do NSSM, configure:

Aba Application
Path:

text
Copiar código
C:\Sistemas\PDFtoDICOM\venv\Scripts\python.exe
Startup directory:

text
Copiar código
C:\Sistemas\PDFtoDICOM
Arguments:

text
Copiar código
main.py
Aba Details
Display name:

text
Copiar código
PDF to DICOM Gateway
Description:

text
Copiar código
Middleware de digitalização para PACS Orthanc
Startup type:

text
Copiar código
Automatic
Aba I/O (opcional – recomendado para troubleshooting)
Output (stdout):

text
Copiar código
C:\Sistemas\PDFtoDICOM\service.log
Error (stderr):

text
Copiar código
C:\Sistemas\PDFtoDICOM\service-error.log
Clique em Install service.

4. Iniciar o Serviço
powershell
Copiar código
.\nssm.exe start PDF2DICOM
✅ Validação do Deploy
Teste de Conectividade
No navegador do servidor, acesse:

text
Copiar código
http://localhost:8000/dashboard
Verifique:

🟢 Orthanc PACS: Conectado

🟢 Service Status: Online

Logs da Aplicação
Verifique a criação do arquivo:

text
Copiar código
app.log
Confira também:

service.log

service-error.log

🛠️ Manutenção e Troubleshooting
Comandos Úteis (PowerShell — Admin)
Reiniciar o serviço:

powershell
Copiar código
nssm restart PDF2DICOM
Parar o serviço:

powershell
Copiar código
nssm stop PDF2DICOM
Editar configuração:

powershell
Copiar código
nssm edit PDF2DICOM
Erros Comuns
Sintoma	Causa Provável	Solução
Erro ao conectar no Orthanc	Firewall ou DNS incorreto	Verifique ping "SEU_PACS", porta 8042 e variáveis do .env
Serviço não inicia / Paused	Caminho do Python incorreto	Verifique o Path apontando para venv\Scripts\python.exe
Erro de permissão em logs	Falta de acesso à pasta	Conceda permissão de Modificação ao usuário do serviço

📌 Observações Finais
Recomenda-se reiniciar o servidor após a instalação em produção

Mantenha o Python e as dependências atualizadas conforme política

Qualquer alteração no .env exige reinício do serviço

# PDFtoDICOM Gateway

![Python Version](https://img.shields.io/badge/python-3.10%2B-blue)
![FastAPI](https://img.shields.io/badge/FastAPI-0.104-green)
![Status](https://img.shields.io/badge/status-production-success)

Sistema middleware desenvolvido para o **Hospital Municipal São José** que permite a digitalização, encapsulamento e envio de documentos PDF diretamente para o servidor PACS (Orthanc), com interface web moderna e validações rigorosas.

---

## 🚀 Funcionalidades

### 🏥 Fluxo de Trabalho
- **Portal de Consulta (Home):** Interface principal focada na busca de pacientes.
- **Importação Secundária:** Acesso ao formulário de upload apenas quando necessário.
- **Visualização Integrada:** Links diretos para o **Orthanc Stone WebViewer**.
- **Dashboard:** Monitoramento em tempo real da saude do servidor.

### 🧠 Inteligência de Busca
- **Busca Vazia Inteligente:** Se nenhum filtro for informado, o sistema busca automaticamente os exames do **dia**.
- **Ordenação Robusta:** Resultados sempre ordenados do mais recente para o mais antigo (Data + Hora).

### 🛡️ Segurança e Validação
- **Input Masking:**
  - Nomes aceitam apenas letras e acentos (bloqueia números e símbolos).
  - Prontuários e Pedidos aceitam apenas números.
- **Travas Lógicas:**
  - Impede inserção de datas futuras (Exame ou Nascimento).
  - Verifica duplicidade de *Accession Number* (Pedido) antes do envio.

### ⚙️ Backend & Infraestrutura
- **Conversão DICOM:** Encapsulamento PDF nativo via `pydicom`.
- **Logs JSON:** Logs estruturados para fácil ingestão em ferramentas de monitoramento.
- **Resiliência:** Sistema de *Retry* automático para conexões instáveis com o PACS.

---

## 🛠️ Tecnologias Utilizadas

- **Linguagem:** Python 3.10+
- **Framework Web:** FastAPI + Uvicorn
- **Frontend:** HTML5 + TailwindCSS (CDN)
- **Manipulação DICOM:** Pydicom
- **Processamento PDF:** PyPDF
- **Service Manager:** NSSM (Non-Sucking Service Manager)

---

## 📋 Pré-requisitos

- Servidor Windows (Server 2019/2022 ou Windows 10/11 Pro)
- Python 3.10 ou superior instalado.
- Acesso de rede ao servidor Orthanc (Porta 8042).
- **NSSM** (para rodar como serviço).

---

**Desenvolvido com ❤️ para facilitar a integração de documentos médicos com sistemas PACS**

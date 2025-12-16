# PDF to DICOM Gateway - HMSJ

Sistema de digitalização e integração de documentos PDF para servidor PACS (Orthanc), desenvolvido para o Hospital Municipal São José.

## 🚀 Funcionalidades

- **Conversão Automática:** Transforma arquivos PDF em objetos DICOM encapsulados.
- **Busca Inteligente:**
  - Portal de pesquisa integrado ao Orthanc.
  - Exibição automática dos exames recentes (últimos 60 dias) em caso de busca vazia.
  - Ordenação decrescente (mais recentes primeiro).
- **Validação Rigorosa:**
  - Bloqueio de caracteres numéricos em nomes e letras em IDs.
  - Bloqueio de datas futuras.
  - Verificação de duplicidade de Pedido (Accession Number).
- **Interface Intuitiva:** Frontend responsivo utilizando TailwindCSS.
- **Monitoramento:** Dashboard de saúde do sistema e logs estruturados em JSON.

## 🛠️ Tecnologias

- **Backend:** Python 3.10+, FastAPI, Uvicorn.
- **Processamento:** Pydicom, PyPDF.
- **Frontend:** HTML5, TailwindCSS (CDN).
- **Infraestrutura:** NSSM (para serviço Windows), Logs JSON.

## ⚙️ Instalação (Produção)

1. **Clone o repositório:**
   ```bash
   git clone [https://github.com/byweber/PDFtoDICOM.git](https://github.com/byweber/PDFtoDICOM.git)
   cd PDFtoDICOM

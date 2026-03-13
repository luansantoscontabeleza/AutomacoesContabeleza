# 💇‍♀️ Processos Operacionais Repetitivos — Setor MEI

> Documento técnico que descreve **todos os processos operacionais repetitivos do setor MEI da Contabeleza**, incluindo fluxos operacionais, diagramas e casos de uso.

Este documento foi projetado para ser **visual, técnico e fácil de navegar**, servindo como base para **descoberta de automações**.

---

# 🎯 Objetivo

Mapear de forma clara:

* processos repetitivos
* sistemas envolvidos
* variáveis utilizadas
* pontos de decisão
* possíveis gargalos

Isso permite:

* identificação de automações
* padronização de procedimentos
* entendimento rápido do fluxo operacional

---

# 🧩 Sistemas Envolvidos

Os processos do setor MEI envolvem os seguintes sistemas:

```
Cliente / Salão
      ↓
Digisac (Atendimento)
      ↓
Equipe MEI
      ↓
MEI Contabeleza
      ↓
Key Contabeleza
      ↓
Sistemas Governamentais

    • e-CAC
    • PGMEI
    • Portal Simples Nacional
    • Portal NFS-e
    • Meu Imposto de Renda

Plataformas externas

    • PRO-BELEZA
```

---

# 🔄 FLUXO GERAL DE SOLICITAÇÕES

```mermaid
flowchart TD

A[Cliente / Salão] --> B[Contato via Digisac]
B --> C[Equipe de Atendimento]
C --> D{Tipo de Solicitação}

D -->|MEI| E[Encaminhar para Equipe MEI]

E --> F[Verificar cadastro no MEI Contabeleza]

F --> G{Possui credenciais?}

G -->|Sim| H[Executar processo]
G -->|Não| I[Solicitar dados ao salão]

H --> J[Usar Key Contabeleza]

J --> K[Se necessário acessar portais governamentais]

K --> L[Gerar resultado]

L --> M[Responder atendimento]

M --> N[Encerrar chamado]
```

---

# 📄 PROCESSO 1 — EMISSÃO DE NOTA DO PROFISSIONAL (MEI → SALÃO)

## Descrição

Profissionais parceiros precisam emitir nota contra o salão mensalmente.

A equipe MEI executa esse processo quando:

* o salão não emitiu
* o profissional solicita
* há necessidade de regularização

---

## Fluxo

```mermaid
flowchart TD

A[Receber solicitação]

A --> B[Verificar cadastro no MEI Contabeleza]

B --> C{Possui senha NFS-e?}

C -->|Sim| D[Emitir nota via Key Contabeleza]

C -->|Não| E[Criar senha no Portal NFS-e]

E --> F[Registrar senha]

F --> D

D --> G[Gerar nota]

G --> H[Enviar ao cliente]
```

---

# 📄 PROCESSO 2 — EMISSÃO DE GUIA DAS MEI

## Descrição

Processo recorrente para pagamento mensal do MEI.

---

```mermaid
flowchart TD

A[Receber solicitação]

A --> B[Validar CPF]

B --> C[Verificar senha GOV]

C --> D[Acessar PGMEI]

D --> E[Gerar guia]

E --> F[Salvar PDF]

F --> G[Enviar ao cliente]
```

---

# 📄 PROCESSO 3 — PARCELAMENTO DE DÍVIDA MEI

## Descrição

Executado quando o profissional possui débitos em aberto.

---

```mermaid
flowchart TD

A[Solicitação de parcelamento]

A --> B[Acessar e-CAC]

B --> C[Consultar débitos]

C --> D[Acessar Portal Simples Nacional]

D --> E[Solicitar parcelamento]

E --> F[Gerar primeira parcela]

F --> G[Registrar parcelamento]

G --> H[Enviar guia]
```

---

# 📄 PROCESSO 4 — ENTREGA DA DECLARAÇÃO DASN-SIMEI

## Descrição

Declaração anual obrigatória para MEIs.

---

```mermaid
flowchart TD

A[Receber solicitação]

A --> B[Verificar faturamento]

B --> C[Acessar Portal Simples Nacional]

C --> D[Preencher declaração]

D --> E[Transmitir]

E --> F[Gerar recibo]

F --> G[Enviar ao cliente]
```

---

# 📄 PROCESSO 5 — CRIAÇÃO DE SENHA NFS-e

## Descrição

Necessário para permitir emissão de notas.

---

```mermaid
flowchart TD

A[Receber solicitação]

A --> B[Acessar Portal NFS-e]

B --> C[Selecionar primeiro acesso]

C --> D[Validar CPF]

D --> E[Criar senha]

E --> F[Registrar no Key Contabeleza no padrão Nome@123]
```

---

# 📄 PROCESSO 6 — HOMOLOGAÇÃO DE CONTRATO SALÃO PARCEIRO

## Descrição

Contrato entre salão e profissional precisa ser homologado.

---

```mermaid
flowchart TD

A[Solicitação de contrato]

A --> B[Acessar MEI Contabeleza]

B --> C[Copiar dados do profissional]

C --> D[Acessar PRO-BELEZA]

D --> E[Preencher formulário]

E --> F[Enviar para homologação]

F --> G[Registrar contrato]
```

---

# 👥 DIAGRAMA DE CASO DE USO

```mermaid
flowchart LR

A[Salão]
B[Profissional MEI]
C[Equipe MEI]
D[Sistemas Governamentais]

A --> C
B --> C

C --> D

C -->|Emitir nota| B

C -->|Gerar DAS| B

C -->|Parcelar dívida| B

C -->|Enviar declaração| B

C -->|Homologar contrato| A
```

---

# ⚠️ Principais Gargalos Operacionais

Processos repetitivos identificados:

```
Coleta de credenciais GOV
Criação de senha NFS-e
Acesso manual a portais
Copiar e colar dados entre sistemas
Consulta de dados fiscais
```

---

# 🤖 Potencial de Automação

Alta prioridade para automação:

```
Emissão de notas MEI
Geração de DAS
Consulta de débitos
Parcelamento automático
Coleta e armazenamento de credenciais
```

---

# 📊 Impacto Esperado com Automação

Benefícios:

```
Redução de trabalho manual
Menos erros humanos
Execução mais rápida
Escalabilidade operacional
```

---

# 🧠 Conclusão

O setor MEI possui **diversos processos altamente repetitivos**, com forte dependência de:

* autenticação
* consulta de dados
* navegação em portais

Isso torna o setor **altamente adequado para automações baseadas em APIs, workflows e RPA**.

Este documento serve como base para:

* discovery de automações
* arquitetura de soluções
* planejamento técnico
* implementação futura.

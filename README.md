# 🚗 Automação Inteligente de Controle de Frota

Sistema desktop desenvolvido para automatizar o acompanhamento de deslocamentos de veículos corporativos, transformando dados de rastreamento em registros estruturados e atualizando automaticamente uma planilha de controle operacional.

O projeto surgiu da necessidade de eliminar um processo manual no qual era necessário consultar individualmente o histórico de localização de cada veículo, identificar os principais momentos de uma viagem e posteriormente registrar essas informações em uma planilha Excel.

> 🔒 **Projeto proprietário. O código-fonte e dados utilizados em produção são privados. Este repositório apresenta exclusivamente a arquitetura, funcionalidades e demonstrações do projeto para fins de portfólio.**

---

## 🎯 Problema

O controle dos deslocamentos exigia diversas etapas manuais:

1. acessar a plataforma de rastreamento;
2. localizar o veículo utilizado;
3. analisar seu histórico de posições;
4. identificar quando o veículo saiu da empresa;
5. identificar quando chegou ao contratante;
6. identificar quando saiu do contratante;
7. identificar quando retornou à empresa;
8. localizar o funcionário correspondente na planilha;
9. registrar manualmente cada horário.

Além do tempo gasto, o processo dependia da interpretação humana de uma grande quantidade de registros de localização.

---

## 💡 Solução

A aplicação automatiza esse fluxo.

O operador fornece a programação do dia e o sistema executa o restante do processamento, relacionando funcionários, veículos e contratantes aos dados obtidos do sistema de rastreamento.

A partir das coordenadas GPS e das regras de geolocalização, a aplicação identifica automaticamente os principais eventos da viagem:

```text
🏢 EMPRESA
    │
    │  Saída da base
    ▼
🚗 DESLOCAMENTO
    │
    │  Chegada
    ▼
📍 CONTRATANTE
    │
    │  Saída
    ▼
🚗 RETORNO
    │
    │  Chegada
    ▼
🏢 EMPRESA
```

Os horários identificados são posteriormente registrados na planilha de controle.

---

## ⚙️ Principais funcionalidades

* 📍 Análise automática de posições GPS
* 🗺️ Detecção de entrada e saída por **geofencing**
* 🚗 Associação entre funcionários e veículos
* 🏢 Identificação de diferentes contratantes
* 🕐 Detecção automática dos eventos da viagem
* 📊 Atualização automática de planilhas Excel
* 🧮 Preservação e atualização da estrutura e fórmulas da planilha
* 💾 Backup automático antes de alterações
* 🖥️ Interface gráfica para utilização pelos operadores
* 🔎 Tratamento de situações em que determinados eventos não podem ser identificados
* 📋 Apresentação dos resultados do processamento antes/durante a operação

---

## 🧠 Detecção de viagens

Um dos principais componentes do projeto é a interpretação do histórico de localização.

O sistema não depende apenas de um horário previamente informado. Ele analisa registros de posicionamento e transições entre regiões geográficas para determinar os eventos relevantes de cada deslocamento.

Entre os eventos tratados estão:

```text
Saída da empresa
        ↓
Chegada ao contratante
        ↓
Saída do contratante
        ↓
Retorno à empresa
```

Também existem tratamentos para situações em que nem todos os eventos estão claramente disponíveis no histórico, permitindo identificar movimentos e paradas prováveis sem simplesmente interromper todo o processamento.

---

## 📍 Geofencing

A aplicação utiliza coordenadas geográficas e cálculo de distância para determinar quando um veículo entra ou sai de uma região.

Cada local relevante pode ser representado por:

```text
Latitude
Longitude
Raio de tolerância
```

Isso permite transformar uma sequência de coordenadas GPS em eventos operacionais compreensíveis.

---

## 📊 Integração com Excel

Após identificar os eventos da viagem, a aplicação atualiza automaticamente a planilha utilizada no controle da frota.

O sistema possui lógica para:

* localizar registros existentes;
* inserir novos registros;
* criar estruturas necessárias quando aplicável;
* preencher horários;
* manter fórmulas;
* atualizar cálculos;
* preservar formatação;
* criar backup antes da alteração.

A automação foi construída para trabalhar sobre o processo já utilizado pela operação, evitando a necessidade de substituir toda a estrutura existente.

---

## 🛡️ Segurança dos dados

Antes de modificar a planilha oficial, uma cópia de segurança é criada automaticamente.

```text
Planilha atual
      ↓
Backup com timestamp
      ↓
Processamento
      ↓
Atualização da planilha
```

Dessa forma, versões anteriores permanecem disponíveis caso seja necessário recuperar informações.

---

## 🖥️ Interface

A aplicação possui interface desktop própria para permitir sua utilização por usuários sem conhecimento de programação.

### Demonstração

<!-- Substituir posteriormente pelos arquivos reais -->

```text
[ GIF / VÍDEO DA APLICAÇÃO SENDO EXECUTADA ]
```

### Resultado do processamento

```text
[ IMAGEM DA TELA DE RESULTADOS ]
```

### Planilha atualizada

```text
[ IMAGEM DA PLANILHA COM DADOS SENSÍVEIS OCULTADOS ]
```

---

## 🏗️ Arquitetura conceitual

```text
        PROGRAMAÇÃO DO DIA
                 │
                 ▼
        INTERPRETAÇÃO DOS DADOS
                 │
                 ▼
       FUNCIONÁRIO / VEÍCULO
                 │
                 ▼
      SISTEMA DE RASTREAMENTO
                 │
                 ▼
        HISTÓRICO DE GPS
                 │
                 ▼
      MOTOR DE GEOLOCALIZAÇÃO
                 │
                 ▼
        DETECÇÃO DA VIAGEM
                 │
       ┌─────────┼─────────┐
       ▼         ▼         ▼
     BASE    CONTRATANTE  RETORNO
                 │
                 ▼
         VALIDAÇÃO DOS DADOS
                 │
                 ▼
          BACKUP DO EXCEL
                 │
                 ▼
       ATUALIZAÇÃO AUTOMÁTICA
```

---

## 🛠️ Tecnologias utilizadas

**Python** — linguagem principal da aplicação

**Tkinter** — interface gráfica desktop

**OpenPyXL** — leitura e manipulação de arquivos Excel

**Requests / integração HTTP** — comunicação com serviços utilizados pelo sistema

**Geolocalização / Geofencing** — interpretação das posições dos veículos

**PyInstaller** — distribuição da aplicação como executável Windows

---

## 📈 Impacto

O projeto transforma uma atividade baseada em consulta e preenchimento manual em um fluxo automatizado.

### Antes

```text
Consultar veículo
      ↓
Analisar posições manualmente
      ↓
Encontrar saída
      ↓
Encontrar chegada
      ↓
Encontrar nova saída
      ↓
Encontrar retorno
      ↓
Abrir Excel
      ↓
Localizar funcionário
      ↓
Digitar horários
```

### Depois

```text
Inserir programação
      ↓
Executar automação
      ↓
Dados processados
      ↓
Planilha atualizada
```

O operador passa a atuar principalmente na validação do resultado, enquanto a aplicação realiza o trabalho repetitivo de consulta, interpretação e registro.

---

## 🔐 Código-fonte

O código-fonte deste projeto não está disponível publicamente por conter lógica desenvolvida para um processo operacional real e integrações utilizadas em ambiente corporativo.

Este repositório funciona como documentação técnica e demonstração do projeto.

Nenhuma credencial, dado de rastreamento, informação de funcionário, informação de cliente ou dado operacional real é disponibilizado.

---

## 👨‍💻 Sobre o projeto

Projeto desenvolvido com foco em:

* automação de processos;
* integração entre sistemas;
* redução de trabalho administrativo repetitivo;
* processamento de dados de geolocalização;
* desenvolvimento de aplicações desktop;
* automação de documentos e planilhas.

---

**Desenvolvido por Leonardo de Carvalho da Costa**

-------------------------------------------------------------------------------------------------

# 🚗 Intelligent Fleet Control Automation

A desktop application developed to automate corporate vehicle trip monitoring by transforming GPS tracking data into structured operational records and automatically updating fleet control spreadsheets.

The project was created to eliminate a repetitive manual workflow in which operators had to individually inspect each vehicle's tracking history, identify the key moments of each trip, and manually enter those timestamps into an Excel spreadsheet.

> 🔒 **Proprietary project. Source code and production data are private. This repository showcases the project's architecture, features, and demonstrations for portfolio purposes only.**

---

## 🎯 The Problem

Fleet monitoring required several manual steps:

1. Access the vehicle tracking platform
2. Locate the assigned vehicle
3. Analyze its location history
4. Identify when the vehicle left the company
5. Identify when it arrived at the client location
6. Identify when it left the client location
7. Identify when it returned to the company
8. Locate the corresponding employee in the spreadsheet
9. Manually enter each timestamp

Besides being time-consuming, the process required human interpretation of a large amount of location data.

---

## 💡 The Solution

The application automates this workflow.

The operator provides the daily schedule, and the system processes the remaining information by associating employees, vehicles, and client locations with data retrieved from the tracking system.

Using GPS coordinates and geolocation rules, the application automatically identifies the main events of each trip:

```text
🏢 COMPANY
    │
    │ Departure
    ▼
🚗 TRAVELING
    │
    │ Arrival
    ▼
📍 CLIENT LOCATION
    │
    │ Departure
    ▼
🚗 RETURN TRIP
    │
    │ Arrival
    ▼
🏢 COMPANY
```

The detected timestamps are then automatically recorded in the fleet control spreadsheet.

---

## ⚙️ Key Features

* 📍 Automatic GPS position analysis
* 🗺️ Entry and exit detection using **geofencing**
* 🚗 Employee-to-vehicle association
* 🏢 Support for multiple client locations
* 🕐 Automatic trip event detection
* 📊 Automatic Excel spreadsheet updates
* 🧮 Preservation and updating of spreadsheet structures and formulas
* 💾 Automatic backups before modifications
* 🖥️ Desktop graphical interface
* 🔎 Handling of incomplete or ambiguous trip events
* 📋 Processing results displayed directly to the operator

---

## 🧠 Trip Detection

One of the core components of the project is the interpretation of vehicle location history.

Instead of relying solely on predefined timestamps, the system analyzes GPS records and transitions between geographical areas to determine relevant trip events.

The main events include:

```text
Company Departure
        ↓
Client Arrival
        ↓
Client Departure
        ↓
Company Return
```

The system also handles situations where not every event can be clearly identified in the available tracking history, allowing the application to detect probable movements and stops without automatically interrupting the entire process.

---

## 📍 Geofencing

The application uses geographical coordinates and distance calculations to determine when a vehicle enters or leaves a predefined area.

Each relevant location can be represented by:

```text
Latitude
Longitude
Tolerance Radius
```

This makes it possible to transform a sequence of raw GPS coordinates into meaningful operational events.

---

## 📊 Excel Integration

After identifying the trip events, the application automatically updates the spreadsheet used for fleet control.

The system includes logic to:

* Locate existing records
* Insert new records when necessary
* Fill in detected timestamps
* Preserve formulas
* Update calculations
* Maintain spreadsheet formatting
* Create backups before making changes

The automation was designed to integrate with the existing operational workflow instead of requiring the company to replace its current spreadsheet structure.

---

## 🛡️ Data Protection

Before modifying the official spreadsheet, the system automatically creates a backup.

```text
Current Spreadsheet
        ↓
Timestamped Backup
        ↓
Processing
        ↓
Updated Spreadsheet
```

This ensures that previous versions remain available if data recovery is ever required.

---

## 🖥️ User Interface

The application includes its own desktop interface, allowing employees without programming knowledge to operate the automation.

### Application Demo

```text
[ ADD APPLICATION GIF / VIDEO HERE ]
```

### Processing Results

```text
[ ADD RESULTS SCREENSHOT HERE ]
```

### Updated Spreadsheet

```text
[ ADD SPREADSHEET SCREENSHOT HERE ]
```

> Public demonstrations should always use fictional or anonymized operational data.

---

## 🏗️ Conceptual Architecture

```text
          DAILY SCHEDULE
                │
                ▼
          DATA PROCESSING
                │
                ▼
        EMPLOYEE / VEHICLE
                │
                ▼
          TRACKING SYSTEM
                │
                ▼
          GPS HISTORY DATA
                │
                ▼
        GEOLOCATION ENGINE
                │
                ▼
         TRIP DETECTION
                │
      ┌─────────┼─────────┐
      ▼         ▼         ▼
   COMPANY    CLIENT     RETURN
                │
                ▼
          DATA VALIDATION
                │
                ▼
           EXCEL BACKUP
                │
                ▼
        AUTOMATIC UPDATE
```

---

## 🛠️ Technologies

**Python** — Core application language

**Tkinter** — Desktop graphical interface

**OpenPyXL** — Excel file reading and manipulation

**HTTP Integration** — Communication with services used by the application

**Geolocation / Geofencing** — Vehicle position interpretation

**PyInstaller** — Windows executable distribution

---

## 📈 Impact

The project transforms a manual monitoring and data-entry workflow into an automated process.

### Before

```text
Find Vehicle
     ↓
Analyze GPS History
     ↓
Find Departure
     ↓
Find Arrival
     ↓
Find Client Departure
     ↓
Find Return
     ↓
Open Excel
     ↓
Find Employee
     ↓
Enter Timestamps
```

### After

```text
Provide Daily Schedule
        ↓
Run Automation
        ↓
Process GPS Data
        ↓
Spreadsheet Updated
```

Instead of manually searching through location records and entering timestamps, the operator can focus primarily on validating the results produced by the system.

---

## 🔐 Source Code

The source code is not publicly available because the project contains proprietary logic developed for a real operational workflow and integrations used in a corporate environment.

This public repository serves as technical documentation and a demonstration of the project.

No credentials, tracking data, employee information, client information, or production data are publicly available.

---

## 👨‍💻 About the Project

This project was developed with a focus on:

* Business process automation
* System integration
* Reduction of repetitive administrative work
* Geolocation data processing
* Desktop application development
* Spreadsheet automation

---

**Developed by Leonardo de Carvalho da Costa**

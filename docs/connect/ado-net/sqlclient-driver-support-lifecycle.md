---
title: Ciclo de vida de suporte do driver do SqlClient
description: Página que contém informações sobre o ciclo de vida de suporte do produto.
ms.date: 11/19/2020
dev_langs:
- csharp
- vb
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-jizho2
ms.openlocfilehash: 30155a584de4e22692601a1dcf9551a67d4f580f
ms.sourcegitcommit: 4c3949f620d09529658a2172d00bfe37aeb1a387
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2020
ms.locfileid: "95011790"
---
# <a name="sqlclient-driver-support-lifecycle"></a>Ciclo de vida de suporte do driver do SqlClient

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

A biblioteca Microsoft.Data.SqlClient segue a mais recente política de suporte do .NET Core para todas as versões.

[Exibir a política de suporte do .NET Core](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)

## <a name="microsoftdatasqlclient-release-cadence"></a>Cadência de versão do Microsoft.Data.SqlClient

Novas versões estáveis (GA) serão publicadas a cada seis meses em uma cadência regular, começando com a versão 1.2 e com duas a três versões prévias entre elas. As versões com LTS (suporte de longo prazo) serão escolhidas pelos participantes e pelos mantenedores com base em algumas qualificações e na resposta dos clientes.

### <a name="release-life-cycles"></a>Ciclos de vida da versão

| Versão | Data de lançamento da oficial | Versão de patch mais recente | Data de lançamento do patch | Nível de Suporte  | Fim do suporte |
| -- | -- | -- | -- | -- | -- |
| 2.1 | 19 de novembro de 2020 | 2.1.0 | 19 de novembro de 2020 | Current | |
| 2.0 | 16 de junho de 2020 | 2.0.1 | 25 de agosto de 2020 | Current | |
| 1.1 | 20 de novembro de 2019 | 1.1.3 | 15 de maio de 2020 | LTS | 21 de novembro de 2022 |
| 1,0 | 28 de agosto de 2019 | 1.0.19269.1 | 26 de setembro de 2019 | Current | 20 de fevereiro de 2020 |

### <a name="long-term-support-lts-releases"></a>Versões com LTS (suporte de longo prazo)

Versões LTS recebem suporte por três anos após a versão inicial.

### <a name="current-releases"></a>Versões atuais

As versões atuais recebem suporte por três meses após uma versão com LTS ou versão atual subsequente.

## <a name="sql-version-compatibility-with-microsoftdatasqlclient"></a>Compatibilidade da versão do SQL com Microsoft.Data.SqlClient

|Versão do banco de dados&nbsp;&#8594;<br />&#8595; Versão do driver|Banco de Dados SQL do Azure|Azure Synapse Analytics|Instância Gerenciada do Azure SQL|SQL Server 2019|Microsoft SQL Server 2017|SQL Server 2016|SQL Server 2014|SQL Server 2012|
|---|---|---|---|---|---|---|---|---|
|2.1|Sim|Sim|Sim|Sim|Sim|Sim|Sim|Sim|
|2,0|Sim|Sim|Sim|Sim|Sim|Sim|Sim|Sim|
|1,1|Sim|Sim|Sim|Sim|Sim|Sim|Sim|Sim|
|1.0|Sim|Sim|Sim|Sim|Sim|Sim|Sim|Sim|

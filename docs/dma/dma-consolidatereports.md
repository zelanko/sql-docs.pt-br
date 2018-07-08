---
title: Importar e consolidar relatórios de avaliação de Assistente de migração de dados (SQL Server) | Microsoft Docs
description: Saiba como importar relatórios de avaliação do Assistente de migração de dados para um banco de dados do SQL Server e a consolidação de vários relatórios
ms.custom: ''
ms.date: 04/16/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.suite: sql
ms.technology: dma
ms.tgt_pltfrm: ''
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.openlocfilehash: be9fc224093f0d5ae14372d4674a52589a2d4801
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37781767"
---
# <a name="import-and-consolidate-data-migration-assistant-assessment-reports"></a>Importar e consolidar o Assistente de migração de dados de relatórios de avaliação

Você pode usar a linha de comando para executar avaliações de migração no modo autônomo, começando com o Assistente de migração de dados v2.1. Esse recurso ajuda você a executar avaliações em grande escala. Os resultados da avaliação na forma de um arquivo CSV ou JSON.

Você pode avaliar vários bancos de dados em uma única instância do utilitário de linha de comando do Assistente de migração de dados e exportar todos os resultados de avaliações em um único arquivo JSON. Ou, você pode avaliar um banco de dados em tempo e posteriormente consolidar os resultados desses vários arquivos de JSON em um banco de dados SQL.

Para obter informações sobre como executar o Assistente de migração de dados da linha de comando, consulte [executar dados Assistente de migração de linha de comando](../dma/dma-commandline.md). 

## <a name="import-assessment-results-into-a-sql-server-database"></a>Importar resultados de avaliação para um banco de dados do SQL Server

Use o script do PowerShell disponível neste [repositório Github](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant) para importar os resultados da avaliação de arquivos JSON para um banco de dados do SQL Server.

> [!NOTE]
> PowerShell v5 ou superior é necessário.

Quando você executar o script, você precisará fornecer as seguintes informações: 

- **serverName**: nome da instância do SQL Server que você deseja importar a avaliação de resultados de arquivos JSON.

- **databaseName**: O nome de banco de dados importados para os resultados.

- **jsonDirectory**: A pasta que os resultados da avaliação salvo, em um ou mais arquivos JSON.

- **processTo**: SQLServer

Adicione os valores anteriores na seção "Executar funções", da seguinte maneira.

```
dmaProcessor -serverName localhost \`\
-databaseName DMAReporting \`\
-jsonDirectory "C:\\temp\\DMACmd\\output\\" \`\
-processTo SQLServer
```

O script do PowerShell cria os seguintes objetos na instância do SQL que você especificou, se os objetos não existirem:

- **Banco de dados** – o nome fornecido nos parâmetros do PowerShell

  - Repositório principal

- **Tabela** – dados do relatório

  - Dados para relatórios

- **Tabela** -BreakingChangeWeighting

  - Tabela de referência para todas as alterações de quebra. Aqui você pode definir seus próprios valores de ponderação para influenciar uma classificação de atualização com êxito de porcentagem (%) mais precisa.

- **Modo de exibição** – UpgradeSuccessRanking\_OnPrem

  - Exibindo um fator de sucesso para cada banco de dados a serem migrados no local de modo de exibição.

- **Modo de exibição** – UpgradeSuccessRanking\_Azure

  - Exibindo um fator de sucesso para cada banco de dados a serem migrados no local de modo de exibição.

- **Procedimento armazenado** – JSONResults\_inserir

  - Usado para importar dados de um arquivo JSON no SQL Server.

- **Procedimento armazenado** – AzureFeatureParityResults\_inserir

  - Usado para importar resultados de paridade de recurso do Azure em um arquivo JSON no SQL Server.

- **Tipo de tabela** – JSONResults

  - Usado para armazenar os resultados JSON para avaliações de local e passar para o JSONResults\_inserir o procedimento armazenado

- **Tipo de tabela** – AzureFeatureParityResults

  - Usado para manter o recurso do Azure os resultados de paridade de avaliações do azure e passar para o AzureFeatureParityResults\_inserir o procedimento armazenado

O script do PowerShell cria uma **processadas** diretório dentro do diretório fornecido que contém os arquivos JSON que devem ser processadas.

Depois que o script for concluído, os resultados são importados para a tabela, os dados do relatório.

### <a name="viewing-the-results-in-sql-server"></a>Exibindo os resultados no SQL Server

Depois que os dados foram carregados, conecte-se à instância do SQL Server. Sua tela deverá aparecer como mostrado no gráfico a seguir:

![Relatórios consolidados no banco de dados do SQL Server](../dma/media/DMAReportingDatabase.png)

O dbo. Tabela de dados do relatório contém o conteúdo do arquivo JSON em sua forma bruta.

## <a name="on-premises-upgrade-success-ranking"></a>Classificação de sucesso de atualização no local

Para ver uma lista de bancos de dados e sua classificação de sucesso de porcentagem (%), selecione o dbo. Modo de exibição UpgradeSuccessRanking_OnPrem:

![Dados no modo de exibição UpgradeSuccessRaning_OnPrem](../dma/media/UpgradeSuccessRankingView.png)

Aqui você pode ver um determinado banco de dados para o qual é a chance de atualização com êxito para diferentes níveis de compatibilidade. Portanto, por exemplo, o banco de dados de RH foi avaliado em relação ao níveis de compatibilidade 100, 110, 120 e 130. Essa avaliação ajuda você a ver visualmente quanto esforço está envolvido na migração para uma versão posterior do SQL Server da versão atual do que o banco de dados está no momento.

Normalmente, a métrica que você se preocupa é quantas alterações significativas são para um determinado banco de dados. No exemplo anterior, você pode ver que o banco de dados de RH tem um fator de sucesso de atualização de 50% para níveis de compatibilidade 100, 110, 120 e 130.

Essa métrica pode ser influenciada alterando os valores de peso em dbo. Tabela BreakingChangeWeighting.

No exemplo a seguir, o esforço envolvido na correção do problema de sintaxe no banco de dados de RH é considerado alto para que um valor de 3 é atribuído a **esforço**. Porque ele não seria demorar muito para corrigir o problema de sintaxe, um valor de 1 é atribuído a **FixTime**. Porque deve haver algum custo envolvido em fazer a alteração, um valor de 2 é atribuído a **custo**. Usar esse valor altera o Changerank combinada para 2.

> [!NOTE]
> A pontuação é em uma escala de 1 a 5.  1 sendo baixa e 5 alta. Além disso, o ChangeRank é uma coluna computada.

![Valores de esforço, FixTime e custo para o problema de sintaxe](../dma/media/SyntaxIssueEffort.png)

Agora neste exemplo, quando você consulta o dbo. Modo de exibição UpgradeSuccessRanking_OnPrem, o fator de atualização com êxito para o banco de dados de RH para alterações significativas caiu.

![Fator de sucesso de atualização para o banco de dados de RH](../dma/media/UpgradeSuccessFactor_HR.png)

## <a name="azure-upgrade-success-ranking"></a>Classificação de sucesso de atualização do Azure

Para ver uma lista de bancos de dados para migrar para o BD SQL do Azure e sua classificação de sucesso de porcentagem, selecione o dbo. Modo de exibição UpgradeSuccessRanking_Azure.

![Dados no modo de exibição UpgradeSuccessRanking_Azure](../dma/media/UpgradeSuccessRankingView_Azure.png)

Aqui, você está interessado no valor MigrationBlocker. 100,00 significa que há uma classificação de 100% de êxito para mover um banco de dados para o banco de dados SQL v12.

A diferença com este modo de exibição é que, atualmente, há nenhuma substituição para alterar a importância para regras de bloqueio de migração.

Para obter informações sobre como gerar relatórios sobre esses dados usando o Power BI, consulte [relatar suas avaliações consolidadas com o PowerBI](../dma/dma-powerbiassesreport.md).

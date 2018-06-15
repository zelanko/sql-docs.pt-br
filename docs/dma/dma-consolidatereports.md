---
title: Consolidar relatórios de avaliação (SQL Server Data Migration Assistant) | Microsoft Docs
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
ms.openlocfilehash: 7192c055b4b9bfb6155f0963c598f9dc4a760c0a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32869641"
---
# <a name="consolidate-assessment-reports-data-migration-assistant"></a>Consolidar relatórios de avaliação (Assistente de migração de dados)

Você pode usar a linha de comando para executar avaliações de migração no modo autônomo, começando com v 2.1 do Assistente de migração de dados. Esse recurso ajuda a executar avaliações em escala. Os resultados da avaliação na forma de um arquivo CSV ou JSON.

Você pode avaliar vários bancos de dados em uma única instância do utilitário de linha de comando do Assistente de migração de dados e exportar todos os resultados de avaliação em um único arquivo JSON. Ou, você pode avaliar um banco de dados em tempo e posteriormente consolidar os resultados desses vários arquivos de JSON em um banco de dados do SQL.

Para obter informações sobre como executar o Assistente de migração de dados da linha de comando, consulte [executar dados Assistente de migração de linha de comando](../dma/dma-commandline.md). 


## <a name="import-assessment-results-into-a-sql-server-database"></a>Importar resultados de avaliação para um banco de dados do SQL Server

Use o script do PowerShell disponível neste [repositório Github](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant) para importar os resultados da avaliação dos arquivos JSON para um banco de dados do SQL Server.

> [!NOTE]
> PowerShell v5 ou versão posterior é necessário.

Quando você executar o script, você precisa fornecer as seguintes informações: 

- **serverName**: resultados de nome de instância do SQL Server que você deseja importar a avaliação dos arquivos JSON.

- **databaseName**: O nome do banco de dados que os resultados serão importados para.

- **jsonDirectory**: A pasta que os resultados da avaliação salvo, em um ou mais arquivos JSON.

- **processTo**: SQLServer

Adicione os valores acima na seção "Executar funções", da seguinte maneira.

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

  - Tabela de referência para todas as alterações de quebra. Aqui você pode definir seus próprios valores de peso para influenciar uma classificação de sucesso de atualização de porcentagem (%) mais precisa.

- **Exibição** – UpgradeSuccessRanking\_local

  - Exibindo um fator de sucesso para cada banco de dados a ser migrada no local de exibição.

- **Exibição** – UpgradeSuccessRanking\_Azure

  - Exibindo um fator de sucesso para cada banco de dados a ser migrada no local de exibição.

- **Procedimento armazenado** – JSONResults\_inserir

  - Usado para importar dados de um arquivo JSON no SQL Server.

- **Procedimento armazenado** – AzureFeatureParityResults\_inserir

  - Usado para importar resultados de paridade de recursos do Azure de um arquivo JSON no SQL Server.

- **Tipo de tabela** – JSONResults

  - Usado para armazenar os resultados JSON para avaliações de local e passar para o JSONResults\_inserir o procedimento armazenado

- **Tipo de tabela** – AzureFeatureParityResults

  - Usado para manter o recurso do Azure resultados de paridade para avaliação do azure e passar para o AzureFeatureParityResults\_inserir o procedimento armazenado

O script do PowerShell cria um **processadas** diretório dentro do diretório fornecido que contém os arquivos JSON serão processados.

Depois que o script for concluído, os resultados são importados para a tabela, os dados do relatório.

### <a name="viewing-the-results-in-sql-server"></a>Exibindo os resultados no SQL Server

Depois que os dados forem carregados, conecte-se à instância do SQL Server. Sua tela deve aparecer como mostrado no gráfico a seguir:

![Relatórios consolidados no banco de dados do SQL Server](../dma/media/DMAReportingDatabase.png)

O dbo. Tabela de dados do relatório contém o conteúdo do arquivo JSON em formato bruto.

## <a name="on-premises-upgrade-success-ranking"></a>Classificação de sucesso de atualização no local

Para ver uma lista de bancos de dados e sua posição de sucesso de porcentagem (%), selecione o dbo. Exibição de UpgradeSuccessRanking_OnPrem:

![Exibir dados em UpgradeSuccessRaning_OnPrem](../dma/media/UpgradeSuccessRankingView.png)

Aqui você pode ver um determinado banco de dados que é a chance de sucesso de atualização para níveis de compatibilidade diferentes. Portanto, por exemplo, o banco de dados de RH foi avaliado em relação a níveis de compatibilidade 100, 110, 120 e 130. Essa avaliação ajuda você a ver visualmente quanto esforço está envolvido na migração para uma versão posterior do SQL Server da versão atual do banco de dados está em.

Geralmente a métrica que importam é quantas alterações recentes para um determinado banco de dados. No exemplo anterior, você pode ver que o banco de dados de RH tem um fator de sucesso de atualização de 50% para níveis de compatibilidade 100, 110, 120 e 130.

Essa métrica pode ser influenciada alterando os valores de peso em dbo. Tabela BreakingChangeWeighting.

No exemplo a seguir, o esforço envolvido na correção do problema de sintaxe no banco de dados de RH é considerado alto para um valor de 3 é atribuído a **esforço**. Porque ele não é demorado para corrigir o problema de sintaxe, um valor de 1 é atribuído a **FixTime**. Como haverá alguns custos envolvidos em fazer a alteração, um valor de 2 é atribuído a **custo**. O uso deste valor muda o Changerank combinada para 2.

> [!NOTE]
> A pontuação é em uma escala de 1 a 5.  1 sendo baixa e 5 alta. Além disso, o ChangeRank é uma coluna computada.

![Valores de esforço, FixTime e custo para o problema de sintaxe](../dma/media/SyntaxIssueEffort.png)

Agora neste exemplo, quando você consulta o dbo. Exibição de UpgradeSuccessRanking_OnPrem, o fator de sucesso de atualização para o banco de dados de RH alterações significativas para caiu.

![Atualizar o fator de sucesso do banco de dados de RH](../dma/media/UpgradeSuccessFactor_HR.png)

## <a name="azure-upgrade-success-ranking"></a>Classificação de sucesso de atualização do Azure

Para ver uma lista de bancos de dados para migrar para o banco de dados de SQL do Azure e seu percentil de sucesso, selecione o dbo. Modo de exibição UpgradeSuccessRanking_Azure.

![Exibir dados em UpgradeSuccessRanking_Azure](../dma/media/UpgradeSuccessRankingView_Azure.png)

Aqui, você está interessado no valor MigrationBlocker. 100,00 significa que há uma classificação de sucesso de 100% para mover um banco de dados para o banco de dados SQL v12.

A diferença com esse modo de exibição é que, atualmente, há nenhuma substituição para alterar a importância para regras de Bloqueador de migração.

Para obter informações sobre relatórios de dados usando o Power BI, consulte [de relatório em suas avaliações consolidadas com PowerBI](../dma/dma-powerbiassesreport.md).

---
title: Relatório de avaliações consolidadas por usando o Power BI (SQL Server Data Migration Assistant) | Microsoft Docs
ms.custom: ''
ms.date: 09/07/2017
ms.prod: sql
ms.prod_service: dma
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-dma
ms.tgt_pltfrm: ''
ms.topic: article
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
caps.latest.revision: ''
author: HJToland3
ms.author: jtoland
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5bc47abe135cbe1da304e0e68d2ac8528252ba29
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="report-on-your-consolidated-assessments-by-using-power-bi-data-migration-assistant"></a>Relatório de avaliações consolidadas por usando o Power BI (Assistente de migração de dados)

Este artigo descreve como criar um relatório do Power BI para avaliação de migração consolidados.

Para obter informações sobre a consolidação de avaliações de migração usando o Assistente de migração de dados, consulte [consolidar relatórios de avaliação](../dma/dma-consolidatereports.md).

## <a name="sample-power-bi-reports"></a>Relatórios de exemplo do Power BI

Você pode baixar exemplos de relatórios do Power BI para avaliação de migração consolidados desta [repositório Github](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant).

Os relatórios a seguir estão incluídos: 

- [Painel de controle](#dashboard--details)

  Inclui estatísticas de instantâneo e um relatório de detalhamento.

- [Preparação para atualização no local](#on-premises-upgrade-readiness--details)

  A fonte de dados é o modo de exibição no banco de dados DMAReporting UpgradeSuccessRanking.  Este relatório mostra o sucesso de atualização de porcentagem para seus bancos de dados estimados.

- [Paridade de recursos locais](#on-premise-feature-parity--details)

  Mostra as recomendações do recurso para a versão do SQL Server de destino.

- [Preparação de atualização de banco de dados SQL do Azure](#azure-sql-db-upgrade-readiness--details)

  A fonte de dados é o modo de exibição no banco de dados DMAReporting UpgradeSuccessRanking.  Este relatório mostra o sucesso de atualização de porcentagem para bancos de dados de avaliação do Azure SQL DB migrações.

- [Recursos de banco de dados do SQL sem suporte do Azure](#azure-sql-db-unsupported-features--details)

  Mostra os recursos em seus bancos de dados existentes que não têm suporte no banco de dados do SQL do Azure (V12).

Você pode modificar esses relatórios para trabalhar com seu ambiente, alterando a fonte de dados no Power BI. 

1. Selecione a seta para baixo ao lado de **editar consultas**e selecione **configurações de fonte de dados**.

   ![Editar o menu de consultas, as configurações de fonte de dados](../dma/media/DataSourceSettings.png)

1. Selecione **alterar fonte...** e digite os valores de servidor e banco de dados.

   ![Alterar a fonte, o servidor e o banco de dados](../dma/media/ChangeSource.png)

1. Selecione **Okey**e, em seguida, selecione **fechar**.

1. Atualize seus relatórios.

   ![Atualizar o relatório do Power BI](../dma/media/RefreshReport.png)

### <a name="dashboard-report"></a>Relatórios de painel

![Relatórios de painel](../dma/media/DashboardReport.png)

O painel mostra detalhes sobre todas as avaliações. Você pode usar a segmentação de dados no lado esquerdo para filtrar por instância ou banco de dados. Você pode usar o gráfico de barras para fazer uma busca detalhada em categorias específicas para ver onde estão os problemas.

Para fazer drill down, selecione o círculo com a seta para baixo no canto superior direito do gráfico de barras.

![Busca detalhada de categoria](../dma/media/CategoryDrillDown.png)

A sequência de busca detalhada é definida como mostrado na imagem a seguir (em **eixo**). Para alterar a sequência, arraste colunas para a ordem desejada.

![Visualizações de eixo de gráfico de barras](../dma/media/VisualizationsAxis.png)

Este modo de exibição se torna ainda mais potente quando você primeiro filtrar por um banco de dados específico e, em seguida, detalhar para os problemas de categoria específica. No exemplo a seguir, o banco de dados de RH é selecionado para a instância **SQL01** para exibir todos os objetos que estão impedindo que as migrações (alterações recentes).

![Alterações mais recentes do banco de dados de RH](../dma/media/BreakingChanges.png)

### <a name="on-premises-upgrade-readiness-report"></a>Relatório de preparação de atualização no local

![Relatório de preparação de atualização no local](../dma/media/OnPremisesUpgradeReadinessReport.png)

Este relatório mostra um instantâneo do são de seus bancos de dados como pronto migrar para uma versão posterior do SQL Server. Os dados deste relatório vêm de dbo. UpgradeSuccessFactor\_local de exibição no banco de dados DMAReporting.

Filtragem por instância e o nome do banco de dados e usando os cartões de pontuação na parte superior, você pode ver que o banco de dados pode ser migrado muito de versão. Por exemplo, se você filtrar por banco de dados AdventureWorks 2012, você pode ver que o banco de dados está pronto para mover para todas as versões do SQL Server são listadas no relatório. Isso é determinado, garantindo que nenhuma alteração de quebra para esse nível de compatibilidade e o banco de dados.

![Fator de sucesso de atualização para o banco de dados AdventureWorks](../dma/media/UpgradeSuccessFactor.png)

### <a name="on-premises-feature-parity-report"></a>Relatório de paridade de recursos locais

![Relatório de paridade de recursos locais](../dma/media/OnPremisesFeatureParityReport.png)

Use esse relatório para realçar os novos recursos que podem ser usados para o banco de dados na versão do SQL Server de destino.

Quando você seleciona um recurso no gráfico de funil, os dados na parte inferior realça os objetos que são afetados pelo recurso. No exemplo a seguir, o **Stretch database para economia de armazenamento** está selecionado e uma tabela é listada que podem se beneficiar desse recurso.

![Recomendação de recurso para o Stretch Database](../dma/media/FeatureRecommend_StretchDatabase.png)

### <a name="azure-sql-db-upgrade-readiness-report"></a>Relatório de preparação para atualização de banco de dados SQL do Azure

![Relatório de preparação para atualização de banco de dados SQL do Azure](../dma/media/AzureSQLDBUpgradeReadinessReport.png)

Este relatório mostra a prontidão para migrar para o Azure SQL Database V12 do banco de dados. Os dados desse relatório vêm de dbo. Modo de exibição UpgradeSuccessRanking no banco de dados DMAReporting.

### <a name="azure-features-parity-report"></a>Relatório de paridade de recursos do Azure

![Relatório de paridade de recursos do Azure](../dma/media/AzureFeaturesParityReport.png)

Use esse relatório para realçar o *recursos de nível de instância* que não são suportados pelo V12 de banco de dados do SQL Azure.

Quando você seleciona um recurso no gráfico de funil, os dados na parte inferior listarem as instâncias e recursos de banco de dados que não são suportados. No exemplo a seguir, esse recurso é selecionado: **sempre na configuração do grupo de disponibilidade não tem suporte no banco de dados do SQL Azure**.  

![Sempre no recurso de grupo de disponibilidade](../dma/media/Feature_AlwaysOnAvailability.png)

 
### <a name="azure-sql-db-unsupported-features-report"></a>Relatório de recursos sem suporte do banco de dados do SQL Azure

![Relatório de recursos sem suporte do banco de dados do SQL Azure](../dma/media/AzureSQLDBUnsupportedFeaturesReport.png)

Este relatório realça os recursos que não há suporte para um determinado **banco de dados** quando o destino é o banco de dados do SQL do Azure (V12).

Filtrando pelo valor de nome e o recurso de banco de dados no gráfico de funil, você pode ver detalhes sobre o recurso sem suporte. Os detalhes incluem qual objeto foi afetado e recomendações para abordar o problema.

Por exemplo, a filtragem por banco de dados do DTC e **bancos de dados somente leitura não podem ser atualizados**, você pode ver uma lista de objetos que são afetados.

![Bancos de dados somente leitura não podem ser atualizado de problema](../dma/media/ReadOnlyDatabases.png)

## <a name="see-also"></a>Consulte também

[Visão geral do Assistente de migração de dados](../dma/dma-overview.md)

[Download de Assistente de migração de dados](https://www.microsoft.com/download/details.aspx?id=53595)

[Download do Power BI](https://powerbi.microsoft.com/)

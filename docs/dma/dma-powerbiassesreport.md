---
title: Analisar relatórios de avaliação consolidados com o Power BI
titleSuffix: Data Migration Assistant
description: Saiba como usar Power BI para analisar relatórios de avaliação de migração de dados que você importou e consolidou em SQL Server
ms.custom: seo-lt-2019
ms.date: 03/12/2019
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: HJToland3
ms.author: rajpo
ms.openlocfilehash: f2385914fc97fa8e118d871ddac6e0cdc9d49247
ms.sourcegitcommit: d00ba0b4696ef7dee31cd0b293a3f54a1beaf458
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74056500"
---
# <a name="analyze-consolidated-assessment-reports-created-by-data-migration-assistant-with-power-bi"></a>Analisar relatórios de avaliação consolidados criados por Assistente de Migração de Dados com Power BI

Este artigo descreve como criar um relatório de Power BI para analisar avaliações de migração consolidada.

Para obter informações sobre como consolidar avaliações de migração criadas pelo Assistente de Migração de Dados, consulte [consolidar relatórios de avaliação](../dma/dma-consolidatereports.md).

## <a name="sample-power-bi-reports"></a>Relatórios de Power BI de exemplo

Você pode baixar exemplos de relatórios de Power BI para avaliações de migração consolidadas deste [repositório GitHub](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant).

Os relatórios a seguir estão incluídos: 

- [Painéis](#dashboard-report)

  Inclui estatísticas de instantâneo e um relatório de busca detalhada.

- [Preparação para atualização local](#on-premises-upgrade-readiness-report)

  A fonte de dados é a exibição de UpgradeSuccessRanking no banco de dado DMAReporting.  Este relatório mostra o percentual de êxito de atualização para seus bancos de dados avaliados.

- [Paridade de recurso local](#on-premises-feature-parity-report)

  Mostra as recomendações de recurso para a versão de SQL Server de destino.

- [Preparação para atualização do BD SQL do Azure](#azure-sql-db-upgrade-readiness-report)

  A fonte de dados é a exibição de UpgradeSuccessRanking no banco de dado DMAReporting.  Este relatório mostra o percentual de êxito de atualização para bancos de dados avaliados para migrações de BD SQL do Azure.

- [Recursos sem suporte do banco de BD SQL do Azure](#azure-sql-db-unsupported-features-report)

  Mostra recursos em seus bancos de dados existentes que não têm suporte no BD SQL do Azure (V12).

Você pode modificar esses relatórios para trabalhar com seu ambiente alterando a fonte de dados em Power BI. 

1. Selecione a seta para baixo ao lado de **editar consultas**e selecione **configurações de fonte de dados**.

   ![Menu editar consultas, configurações da fonte de dados](../dma/media/DataSourceSettings.png)

1. Selecione **alterar origem...** e insira os valores do servidor e do banco de dados.

   ![Alterar origem, servidor e banco de dados](../dma/media/ChangeSource.png)

1. Selecione **OK**e, em seguida, selecione **fechar**.

1. Atualize seus relatórios.

   ![Atualizar Power BI relatório](../dma/media/RefreshReport.png)

### <a name="dashboard-report"></a>Relatório do painel

![Relatório do painel](../dma/media/DashboardReport.png)

O painel mostra detalhes sobre todas as suas avaliações. Você pode usar as segmentações do lado esquerdo para filtrar por instância ou banco de dados. Você pode usar o gráfico de barras para fazer uma busca detalhada em categorias específicas para ver onde estão os problemas.

Para fazer uma busca detalhada, selecione o círculo com a seta para baixo no canto superior direito do gráfico de barras.

![Busca detalhada de categoria](../dma/media/CategoryDrillDown.png)

A sequência de busca detalhada é definida conforme mostrado na imagem a seguir (em **eixo**). Para alterar a sequência, arraste as colunas para a ordem desejada.

![Visualizações, eixo do gráfico de barras](../dma/media/VisualizationsAxis.png)

Essa exibição se torna ainda mais potente quando você filtra pela primeira vez por um banco de dados específico e, em seguida, busca detalhadamente os problemas de categoria específicos. No exemplo a seguir, o banco de dados de RH é selecionado para a instância **SQL01** para exibir todos os objetos que estão impedindo migrações (alterações significativas).

![Alterações recentes no banco de dados de RH](../dma/media/BreakingChanges.png)

### <a name="on-premises-upgrade-readiness-report"></a>Relatório de preparação de atualização local

![Relatório de preparação de atualização local](../dma/media/OnPremisesUpgradeReadinessReport.png)

Este relatório mostra um instantâneo de como os bancos de dados são prontos para serem migrados para uma versão mais recente do SQL Server. Os dados neste relatório são provenientes do dbo. UpgradeSuccessFactor\_exibição local no banco de dados DMAReporting.

Filtrando por instância e nome de banco de dados e usando os cartões de pontuação na parte superior, você pode ver qual versão o banco de dados também pode ser migrado. Por exemplo, se você filtrar pelo banco de dados AdventureWorks 2012, poderá ver que o banco de dados está pronto para ser movido para todas as versões de SQL Server listadas no relatório. Isso é determinado garantindo que não haja alterações significativas para esse banco de dados e nível de compatibilidade.

![Fator de sucesso de atualização para o banco de dados AdventureWorks](../dma/media/UpgradeSuccessFactor.png)

### <a name="on-premises-feature-parity-report"></a>Relatório de paridade de recurso local

![Relatório de paridade de recurso local](../dma/media/OnPremisesFeatureParityReport.png)

Use esse relatório para realçar os novos recursos que podem ser usados para o banco de dados na versão de SQL Server de destino.

Quando você seleciona um recurso no gráfico de funil, os dados na parte inferior destacam quais objetos são afetados pelo recurso. No exemplo a seguir, o recurso **banco de dados de ampliação para economia de armazenamento** está selecionado e uma tabela listada pode se beneficiar desse recurso.

![Recomendação de recurso para Stretch Database](../dma/media/FeatureRecommend_StretchDatabase.png)

### <a name="azure-sql-db-upgrade-readiness-report"></a>Relatório de preparação de atualização do BD SQL do Azure

![Relatório de preparação de atualização do BD SQL do Azure](../dma/media/AzureSQLDBUpgradeReadinessReport.png)

Este relatório mostra a prontidão do banco de dados para migrar para o banco de dados SQL do Azure V12. Os dados desse relatório são provenientes do dbo. UpgradeSuccessRanking exibição no banco de dados DMAReporting.

### <a name="azure-features-parity-report"></a>Relatório de paridade de recursos do Azure

![Relatório de paridade de recursos do Azure](../dma/media/AzureFeaturesParityReport.png)

Use este relatório para realçar os *recursos de nível de instância* que não têm suporte do banco de dados SQL do Azure V12.

Quando você seleciona um recurso no gráfico de funil, os dados na parte inferior listam as instâncias e os recursos de banco que não têm suporte. No exemplo a seguir, esse recurso está selecionado: a **configuração do grupo de disponibilidade AlwaysOn não tem suporte no banco de dados SQL do Azure**.  

![Recurso de grupo de disponibilidade Always on](../dma/media/Feature_AlwaysOnAvailability.png)

 
### <a name="azure-sql-db-unsupported-features-report"></a>Relatório de recursos sem suporte do BD SQL do Azure

![Relatório de recursos sem suporte do BD SQL do Azure](../dma/media/AzureSQLDBUnsupportedFeaturesReport.png)

Este relatório realça quais recursos não têm suporte para um determinado **banco de dados** quando o destino é o banco de dados SQL do Azure (V12).

Filtrando pelo nome do banco de dados e pelo valor do recurso no gráfico de funil, você pode ver detalhes sobre o recurso sem suporte. Os detalhes incluem qual objeto é afetado e recomendações para resolver o problema.

Por exemplo, a filtragem pelo banco de dados DTC e bancos de dados **somente leitura não podem ser atualizadas**, você pode ver uma lista de objetos que são afetados.

![O problema de bancos de dados somente leitura não pode ser atualizado](../dma/media/ReadOnlyDatabases.png)

## <a name="see-also"></a>Confira também

[Visão geral do Assistente de Migração de Dados](../dma/dma-overview.md)

[Download de Assistente de Migração de Dados](https://www.microsoft.com/download/details.aspx?id=53595)

[Download de Power BI](https://powerbi.microsoft.com/)

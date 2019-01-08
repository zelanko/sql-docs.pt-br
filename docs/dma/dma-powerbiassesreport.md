---
title: Analisar relatórios consolidados de avaliação de Assistente de migração de dados com o Power BI (SQL Server) | Microsoft Docs
description: Saiba como usar o Power BI para analisar os relatórios de avaliação de migração de dados que você já importou e consolidados no SQL Server
ms.custom: ''
ms.date: 10/20/2018
ms.prod: sql
ms.prod_service: dma
ms.reviewer: ''
ms.technology: dma
ms.topic: conceptual
keywords: ''
helpviewer_keywords:
- Data Migration Assistant, Assess
ms.assetid: ''
author: pochiraju
ms.author: rajpo
manager: craigg
ms.openlocfilehash: 1094d6fd52841a65afa58768dfaee9a05aa20810
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53208285"
---
# <a name="analyze-consolidated-assessment-reports-created-by-data-migration-assistant-with-power-bi"></a>Analisar relatórios de avaliação consolidado criados pelo Assistente de migração de dados com o Power BI

Este artigo descreve como criar um relatório do Power BI para analisar as avaliações de migração consolidado.

Para obter informações sobre como consolidar avaliações de migração criadas pelo Assistente de migração de dados, consulte [consolidar relatórios de avaliação](../dma/dma-consolidatereports.md).

## <a name="sample-power-bi-reports"></a>Exemplos de relatórios do Power BI

Você pode baixar exemplos de relatórios do Power BI para avaliações consolidadas migração desta [repositório Github](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/data-migration-assistant).

Os relatórios a seguir estão incluídos: 

- [Painel de controle](#dashboard--details)

  Inclui estatísticas de instantâneo e um relatório de detalhamento.

- [Preparação de atualização no local](#on-premises-upgrade-readiness--details)

  A fonte de dados é o modo de exibição no banco de dados DMAReporting UpgradeSuccessRanking.  Este relatório mostra o sucesso de atualização de porcentagem para seus bancos de dados avaliados.

- [Paridade de recursos locais](#on-premise-feature-parity--details)

  Mostra as recomendações de recurso para a versão do SQL Server de destino.

- [Preparação de atualização de banco de dados SQL do Azure](#azure-sql-db-upgrade-readiness--details)

  A fonte de dados é o modo de exibição no banco de dados DMAReporting UpgradeSuccessRanking.  Este relatório mostra o sucesso de atualização de porcentagem para bancos de dados avaliados para migrações de BD SQL do Azure.

- [Recursos do banco de dados SQL sem suporte do Azure](#azure-sql-db-unsupported-features--details)

  Mostra os recursos em seus bancos de dados existentes que não têm suporte no banco de dados do SQL do Azure (V12).

Você pode modificar esses relatórios para trabalhar com seu ambiente, alterando a fonte de dados no Power BI. 

1. Selecione a seta para baixo ao lado **editar consultas**e selecione **configurações de fonte de dados**.

   ![Editar menu de consultas, as configurações de fonte de dados](../dma/media/DataSourceSettings.png)

1. Selecione **alterar fonte...** e insira os valores de servidor e banco de dados.

   ![Alterar o código-fonte, servidor e banco de dados](../dma/media/ChangeSource.png)

1. Selecione **Okey**e, em seguida, selecione **fechar**.

1. Atualize seus relatórios.

   ![Atualizar relatório do Power BI](../dma/media/RefreshReport.png)

### <a name="dashboard-report"></a>Relatórios de painel

![Relatórios de painel](../dma/media/DashboardReport.png)

O painel mostra detalhes sobre todas as suas avaliações. Você pode usar as segmentações de dados no lado esquerdo para filtrar por instância ou banco de dados. Você pode usar o gráfico de barras para fazer uma busca detalhada em categorias específicas para ver onde estão os problemas.

Para fazer drill down, selecione o círculo com a seta para baixo no canto superior direito do gráfico de barras.

![Busca detalhada de categoria](../dma/media/CategoryDrillDown.png)

A sequência de busca detalhada é definida conforme mostrado na imagem a seguir (sob **eixo**). Para alterar a sequência, arraste colunas para a ordem desejada.

![Visualizações de eixo de gráfico de barras](../dma/media/VisualizationsAxis.png)

Este modo de exibição se torna ainda mais eficiente quando você filtrar pela primeira vez por um banco de dados específico e, em seguida, fazer drill down até os problemas de categoria específica. No exemplo a seguir, o banco de dados de RH é selecionado por exemplo **SQL01** para exibir todos os objetos que estão impedindo que as migrações (alterações recentes).

![Últimas alterações do banco de dados de RH](../dma/media/BreakingChanges.png)

### <a name="on-premises-upgrade-readiness-report"></a>Relatório de preparação de atualização no local

![Relatório de preparação de atualização no local](../dma/media/OnPremisesUpgradeReadinessReport.png)

Este relatório mostra um instantâneo do são de seus bancos de dados como pronto para migrar para uma versão posterior do SQL Server. Os dados neste relatório vêm de dbo. UpgradeSuccessFactor\_OnPrem exibição no banco de dados DMAReporting.

Filtragem por instância e o nome do banco de dados e usando os cartões de pontuação na parte superior, você pode ver qual versão do banco de dados poderia ser migrado muito. Por exemplo, se você filtrar por banco de dados AdventureWorks 2012, você pode ver que o banco de dados está pronto para mover para todas as versões do SQL Server listadas no relatório. Isso é determinado, garantindo que não há nenhuma alteração significativa para esse nível de compatibilidade de banco de dados.

![Atualizar o fator de sucesso para o banco de dados AdventureWorks](../dma/media/UpgradeSuccessFactor.png)

### <a name="on-premises-feature-parity-report"></a>Relatório de paridade de recursos locais

![Relatório de paridade de recursos locais](../dma/media/OnPremisesFeatureParityReport.png)

Use esse relatório para destacar os novos recursos que podem ser usados para o banco de dados na versão do SQL Server de destino.

Quando você seleciona um recurso no gráfico de funil, os dados na parte inferior realça a quais objetos são afetados pelo recurso. No exemplo a seguir, o **banco de dados de ampliação para economia de armazenamento** está selecionado e uma tabela é listada que poderiam se beneficiar desse recurso.

![Recomendação de recurso para o Stretch Database](../dma/media/FeatureRecommend_StretchDatabase.png)

### <a name="azure-sql-db-upgrade-readiness-report"></a>Relatório de preparação para atualização de banco de dados SQL do Azure

![Relatório de preparação para atualização de banco de dados SQL do Azure](../dma/media/AzureSQLDBUpgradeReadinessReport.png)

Este relatório mostra a preparação do banco de dados para migrar para o V12 de banco de dados SQL do Azure. Os dados desse relatório vêm de dbo. Modo de exibição UpgradeSuccessRanking no banco de dados DMAReporting.

### <a name="azure-features-parity-report"></a>Relatório de paridade de recursos do Azure

![Relatório de paridade de recursos do Azure](../dma/media/AzureFeaturesParityReport.png)

Use esse relatório para destacar as *recursos de nível de instância* que não são suportados pelo V12 de banco de dados SQL do Azure.

Quando você seleciona um recurso no gráfico de funil, os dados na parte inferior listam as instâncias e recursos de banco de dados que não têm suporte. No exemplo a seguir, esse recurso é selecionado: **Sempre na disponibilidade configuração do grupo não tem suporte no Azure SQL Database**.  

![O recurso de grupo de disponibilidade do AlwaysOn](../dma/media/Feature_AlwaysOnAvailability.png)

 
### <a name="azure-sql-db-unsupported-features-report"></a>Relatório de recursos de banco de dados SQL sem suporte do Azure

![Relatório de recursos de banco de dados SQL sem suporte do Azure](../dma/media/AzureSQLDBUnsupportedFeaturesReport.png)

Este relatório realça os recursos que não há suporte para um determinado **banco de dados** quando o destino é o banco de dados SQL (V12).

Filtrando pelo valor de nome e o recurso de banco de dados no gráfico de funil, você pode ver detalhes sobre o recurso sem suporte. Os detalhes incluem qual objeto foi afetado e recomendações para resolver o problema.

Por exemplo, filtrar pelo banco de dados do DTC e **bancos de dados somente leitura não podem ser atualizados**, você pode ver uma lista de objetos que são afetados.

![Bancos de dados somente leitura não podem ser atualizado de problema](../dma/media/ReadOnlyDatabases.png)

## <a name="see-also"></a>Confira também

[Visão geral do Assistente de migração de dados](../dma/dma-overview.md)

[Download do Assistente de migração de dados](https://www.microsoft.com/download/details.aspx?id=53595)

[Download do Power BI](https://powerbi.microsoft.com/)

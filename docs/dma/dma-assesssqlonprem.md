---
title: Realizar uma avaliação de migração do SQL Server (Assistente de migração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 10/04/2017
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
ms.openlocfilehash: 30c44a7aba2a721501996d7a1d53a6a4a83a345e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="perform-a-sql-server-migration-assessment"></a>Realizar uma avaliação de migração do SQL Server
As seguintes instruções passo a passo o ajudarão a realizar a primeira avaliação de migração para o SQL Server no local, em execução em uma VM do Azure, ou um banco de dados SQL Azure, usando o Assistente de migração de dados do SQL Server.

## <a name="create-an-assessment"></a>Criar uma avaliação

1.  Selecione o **novo** (+) ícone e, em seguida, selecione o **avaliação** tipo de projeto.

2.  Defina o tipo de servidor de origem e destino.

    Se você estiver atualizando sua instância do SQL Server local para uma instância do SQL Server local moderna ou SQL Server hospedado em uma VM do Azure, defina o tipo de servidor de origem e destino **do SQL Server**. Se você estiver migrando para o banco de dados do SQL Azure, em vez disso, defina o tipo de servidor de destino **banco de dados do SQL Azure**.

3.  Clique em **Criar**.

    ![Criar uma avaliação](../dma/media/NewAssessment.png)

## <a name="choose-assessment-options"></a>Escolher opções de avaliação

1. Selecione a versão do SQL Server de destino que você planeja migrar para.

2. Selecione o tipo de relatório.

   Quando você está avaliando sua instância do SQL Server de origem para a migração para o SQL Server no local ou para o SQL Server hospedado em destinos de VM do Azure, você pode escolher um ou ambos os seguintes tipos de relatórios de avaliação:

    -   **Problemas de compatibilidade**

    -   **Recomendação de novos recursos**

    ![Selecione um tipo de relatório de avaliação para o destino do SQL Server](../dma/media/AssessmentTypes.png)

   Quando você está avaliando a instância do SQL Server de origem para migração para o banco de dados do SQL Azure, você pode escolher um ou ambos os seguintes tipos de relatórios de avaliação:

    -   **Verificar a compatibilidade de banco de dados**

    -   **Verificação de paridade de recursos**

    ![Selecione o tipo de relatório de avaliação para o destino do banco de dados SQL](../dma/media/AssessmentTypes_Azure.png)

## <a name="add-databases-to-assess"></a>Adicionar bancos de dados para avaliar

1.  Selecione **adicionar fontes** para abrir o menu de atalho de conexão.

2.  Insira o nome de instância do SQL server, escolha o tipo de autenticação, defina as propriedades de conexão correta e, em seguida, selecione **conectar**.

3.  Selecione os bancos de dados para avaliar e, em seguida, selecione **adicionar**.

    > [!NOTE] 
    > Você pode remover vários bancos de dados, selecionando-os ao mesmo tempo mantendo a tecla Shift ou Ctrl e, em seguida, clicando em **remover fontes**. Você também pode adicionar bancos de dados de várias instâncias do SQL Server usando o **adicionar fontes** botão.

4.  Clique em **próximo** para iniciar a avaliação.

    ![Adicionar fontes e Iniciar avaliação](../dma/media/SelectDatabase.png)

## <a name="view-results"></a>Exibir resultados

A duração da avaliação de depende do número de bancos de dados adicionado e o tamanho do esquema de cada banco de dados. Resultados são exibidos para cada banco de dados assim que estiverem disponíveis.

1.  Selecione o banco de dados que foi concluída a avaliação e, em seguida, alternar entre **problemas de compatibilidade** e **recurso recomendações** usando o seletor de exibição.

2.  Examine os problemas de compatibilidade de todos os níveis de compatibilidade com suporte pela versão do SQL Server de destino que você selecionou no **opções** página.

Você pode examinar os problemas de compatibilidade ao analisar o objeto afetado e seus detalhes para cada problema identificado em **alterações significativas**, **alterações de comportamento**, e **recursos preteridos** .

![Exibir resultados da avaliação](../dma/media/ReviewResults.png)

Da mesma forma, você pode examinar a recomendação de recurso em **desempenho**, **armazenamento**, e **segurança** áreas.

Recurso recomendações abrangem uma variedade de recursos, como o OLTP in-memory e Columnstore, Stretch Database, sempre criptografado, máscara de dados dinâmicos e criptografia transparente de dados.

![Recomendações do recurso de exibição](../dma/media/FeatureRecommendations.png)

Para o banco de dados SQL Azure, as avaliações fornecem os problemas de bloqueio de migração e problemas de paridade de recursos. Examine os resultados para ambas as categorias, selecionando as opções específicas.

- O **paridade de recursos do SQL Server** categoria fornece um conjunto abrangente de recomendações, abordagens alternativas disponíveis no Azure e etapas atenuantes. Ele ajuda você a planejar desse esforço em seus projetos de migração.

  ![Exibir as informações de paridade de recursos do SQL Server](../dma/media/SQLFeatureParity.png)

- O **problemas de compatibilidade** categoria fornece recursos parcialmente com suporte ou não há suporte para bloqueiam a migração no SQL Server bancos de dados locais para bancos de dados do SQL Azure. Em seguida, ele fornece recomendações para ajudá-lo a resolver esses problemas.

  ![Problemas de compatibilidade do modo de exibição](../dma/media/CompatibilityIssues.png)

## <a name="export-results"></a>Exportar resultados

Depois que todos os bancos de dados concluir a avaliação, selecione **Exportar relatório** para exportar os resultados para um arquivo CSV ou um arquivo JSON. Em seguida, você pode analisar os dados em sua conveniência.

Você pode executar várias avaliações simultaneamente e exibir o estado de avaliações abrindo o **todas as avaliações** página.

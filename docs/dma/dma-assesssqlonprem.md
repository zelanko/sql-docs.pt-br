---
title: Executar uma avaliação de migração do SQL Server (Assistente de migração de dados) | Microsoft Docs
description: Saiba como usar o Assistente de migração de dados para avaliar um SQL Server no local antes de migrar para outro SQL Server ou banco de dados do Azure SQL
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
ms.openlocfilehash: 12c91f52694c9c7b4cc9abc9e7b96df0ddffb51c
ms.sourcegitcommit: f9b4078dfa3704fc672e631d4830abbb18b26c85
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2018
ms.locfileid: "50965945"
---
# <a name="perform-a-sql-server-migration-assessment-with-data-migration-assistant"></a>Realizar uma avaliação de migração do SQL Server com o Assistente de migração de dados

As instruções passo a passo a seguir o ajudam a executar sua primeira avaliação de migração para o local SQL Server, SQL Server em execução em uma VM do Azure, ou um banco de dados SQL Azure, usando o Assistente de migração de dados.

## <a name="create-an-assessment"></a>Criar uma avaliação

1.  Selecione o **New** (+) ícone e, em seguida, selecione o **avaliação** tipo de projeto.

2.  Defina o tipo de servidor de origem e destino.

    Se você estiver atualizando sua instância do SQL Server local para uma instância do SQL Server moderna no local ou ao SQL Server hospedado em uma VM do Azure, defina o tipo de servidor de origem e destino como **SQL Server**. Se você estiver migrando para o banco de dados SQL, em vez disso, defina o tipo de servidor de destino **banco de dados SQL**.

3.  Clique em **Criar**.

    ![Criar uma avaliação](../dma/media/NewAssessment.png)

## <a name="choose-assessment-options"></a>Escolha as opções de avaliação

1. Selecione a versão do SQL Server de destino que você planeja migrar para o.

2. Selecione o tipo de relatório.

   Quando você está avaliando sua instância do SQL Server de origem para a migração para o SQL Server no local ou ao SQL Server hospedado em destinos de VM do Azure, você pode escolher um ou ambos os seguintes tipos de relatório de avaliação:

    -   **Problemas de compatibilidade**
    -   **Recomendação de novos recursos**

    ![Selecione um tipo de relatório de avaliação para o destino do SQL Server](../dma/media/AssessmentTypes.png)

   Ao avaliar a instância do SQL Server de origem para migração para o banco de dados SQL, você pode escolher um ou ambos os seguintes tipos de relatório de avaliação:

    -   **Verificar a compatibilidade do banco de dados**
    -   **Verificar paridade de recursos**

    ![Selecione o tipo de relatório de avaliação para o destino de banco de dados SQL](../dma/media/AssessmentTypes_Azure.png)

## <a name="add-databases-to-assess"></a>Adicionar bancos de dados para avaliar

1.  Selecione **adicionar fontes** para abrir o menu de atalho da conexão.

2.  Insira o nome de instância do SQL server, escolha o tipo de autenticação, defina as propriedades de conexão correta e, em seguida, selecione **Connect**.

3.  Selecione os bancos de dados para avaliar e, em seguida, selecione **adicionar**.

    > [!NOTE] 
    > Você pode remover vários bancos de dados, selecionando-os ao mesmo tempo mantendo pressionada a tecla Shift ou Ctrl e, em seguida, clicando em **remover fontes**. Você também pode adicionar bancos de dados de várias instâncias do SQL Server usando o **adicionar fontes** botão.

4.  Clique em **próxima** para iniciar a avaliação.

    ![Adicionar fontes e iniciar a avaliação](../dma/media/SelectDatabase.png)

## <a name="view-results"></a>Exibir resultados

A duração da avaliação depende do número de bancos de dados adicionados e o tamanho do esquema de cada banco de dados. Os resultados são exibidos para cada banco de dados assim que elas estão disponíveis.

1.  Selecione o banco de dados que foi concluída a avaliação e, em seguida, alternar entre **problemas de compatibilidade** e **recomendações de recurso** usando o seletor.

2.  Examine os problemas de compatibilidade em todos os níveis de compatibilidade com suporte pela versão do SQL Server de destino que você selecionou na **opções** página.

Você pode examinar os problemas de compatibilidade, analisando o objeto afetado, seus detalhes e potencialmente uma correção para cada problema identificado em **alterações significativas**, **alterações de comportamento**, e  **Recursos preteridos**.

![Exibir resultados da avaliação](../dma/media/ReviewResults.png)

Da mesma forma, você pode examinar a recomendação de recurso entre **desempenho**, **armazenamento**, e **segurança** áreas.

Recomendações de recursos abrangem uma variedade de recursos, como o OLTP in-memory, Columnstore, Stretch Database, Always Encrypted, máscara de dados dinâmicos e Transparent Data Encryption.

![Exibir recomendações de recurso](../dma/media/FeatureRecommendations.png)

Para o banco de dados SQL Azure, as avaliações fornecem os problemas de bloqueio de migração e problemas de paridade de recurso. Examine os resultados para ambas as categorias, selecionando as opções específicas.

- O **paridade de recursos do SQL Server** categoria fornece um conjunto abrangente de recomendações, abordagens alternativas disponíveis no Azure e etapas atenuantes. Ele ajuda você a planejar esse esforço em seus projetos de migração.

  ![Exibir as informações de paridade de recursos do SQL Server](../dma/media/SQLFeatureParity.png)

- O **problemas de compatibilidade** categoria fornece recursos de parcialmente compatíveis ou não bloqueiam a migração do SQL Server bancos de dados local para bancos de dados SQL do Azure. Em seguida, ele fornece recomendações para ajudá-lo a resolver esses problemas.

  ![Problemas de compatibilidade do modo de exibição](../dma/media/CompatibilityIssues.png)

## <a name="export-results"></a>Exportar resultados

Depois de concluir a avaliação a todos os bancos de dados, selecione **Exportar relatório** para exportar os resultados para um arquivo CSV ou um arquivo JSON. Em seguida, você pode analisar os dados em sua própria comodidade.

Você pode executar várias avaliações simultaneamente e exibir o estado das avaliações abrindo a **todas as avaliações** página.

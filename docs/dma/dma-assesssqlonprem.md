---
title: Realize uma avaliação de migração do SQL Server
titleSuffix: Data Migration Assistant
description: Aprenda a usar o Assistente de Migração de Dados para avaliar um SQL Server no local antes de migrar para outro SQL Server ou para o Azure SQL Database
ms.date: 01/15/2020
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
ms.custom: seo-lt-2019
ms.openlocfilehash: 59dc8c96ebda5ac66fb6701d480cb6d633e83158
ms.sourcegitcommit: 48e259549f65f0433031ed6087dbd5d9c0a51398
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/07/2020
ms.locfileid: "80809744"
---
# <a name="perform-a-sql-server-migration-assessment-with-data-migration-assistant"></a>Realizar uma avaliação de migração do SQL Server com o Assistente de Migração de Dados

As seguintes instruções passo a passo ajudam você a realizar sua primeira avaliação para migrar para o SQL Server, SQL Server em execução em um Azure VM ou Banco de Dados Azure SQL usando o Assistente de Migração de Dados.

   > [!NOTE]
   > O Data Migration Assistant v5.0 introduz suporte para analisar a conectividade do banco de dados e as consultas SQL incorporadas no código do aplicativo. Para obter mais informações, consulte o post do blog Usando o [Assistente de Migração de Dados para avaliar a camada de acesso a dados de um aplicativo](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Using-Data-Migration-Assistant-to-assess-an-application-s-data/ba-p/990430).

## <a name="create-an-assessment"></a>Criar uma avaliação

1. Selecione o ícone **Novo** (+) e selecione o tipo de projeto **Avaliação.**

2. Defina o tipo de servidor de origem e de destino.

    Se você estiver atualizando sua instância do SQL Server no local para uma instância moderna do SQL Server no local ou para o SQL Server hospedado em uma VM Azure, defina o tipo de servidor de origem e destino para **SQL Server**. Se você estiver migrando para o Azure SQL Database, em vez disso, defina o tipo de servidor de destino para **o Banco de Dados SQL do Azure**.

3. Clique em **Criar**.

   ![Criar uma avaliação](../dma/media/dma-assesssqlonprem/new-assessment.png)

## <a name="choose-assessment-options"></a>Escolha opções de avaliação

1. Selecione a versão de destino do SQL Server para a qual você planeja migrar.

2. Selecione o tipo de relatório.

   Quando você está avaliando a instância do SQL Server de origem para migrar para o SQL Server no local ou para o SQL Server hospedado em alvos De VM do Azure, você pode escolher um ou ambos os seguintes tipos de relatório de avaliação:

    - **Problemas de compatibilidade**
    - **Recomendação de novos recursos**

   ![Selecione um tipo de relatório de avaliação para o destino sql server](../dma/media/dma-assesssqlonprem/assessment-types.png)

   Ao avaliar a instância do SQL Server de origem para migrar para o Banco de Dados SQL do Azure, você pode escolher um ou ambos os seguintes tipos de relatório de avaliação:

    - **Determinar compatibilidade do banco de dados**
    - **Verificação de paridade de recursos**

    ![Selecione o tipo de relatório de avaliação para o destino do Banco de Dados SQL](../dma/media/dma-assesssqlonprem/assessment-types-azure.png)

## <a name="add-databases-and-extended-events-trace-to-assess"></a>Adicionar bancos de dados e rastreamento de eventos estendidos para avaliar

1. Selecione **Adicionar fontes** para abrir o menu de flyout de conexão.

2. Digite o nome de instância do servidor SQL, escolha o tipo autenticação, defina as propriedades de conexão corretas e selecione **Conectar**.

3. Selecione os bancos de dados para avaliar e, em seguida, **selecione Adicionar**.

    > [!NOTE]
    > Você pode remover vários bancos de dados selecionando-os enquanto segura a tecla Shift ou Ctrl e, em seguida, clicando **em Remover fontes**. Você também pode adicionar bancos de dados de várias instâncias do SQL Server selecionando **Adicionar fontes**.

4. Se você tiver quaisquer consultas SQL ad hoc ou dinâmicas ou quaisquer instruções DML iniciadas através da camada de dados do aplicativo, digite o caminho para a pasta na qual você colocou todos os arquivos de sessão de eventos estendidos que você coletou para capturar a carga de trabalho no SQL Server de origem.

     O exemplo a seguir mostra como criar uma sessão de evento estendida no SQL Server de origem para capturar a carga de trabalho da camada de dados do aplicativo.  Capture a carga de trabalho durante a duração que representa sua carga de trabalho máxima.

    ```
    DROP EVENT SESSION [DatalayerSession] ON SERVER
    go
    CREATE EVENT SESSION [DatalayerSession] ON SERVER  
    ADD EVENT sqlserver.sql_batch_completed( 
        ACTION (sqlserver.sql_text,sqlserver.client_app_name,sqlserver.client_hostname,sqlserver.database_id))
    ADD TARGET package0.asynchronous_file_target(SET filename=N'C:\temp\Demos\DataLayerAppassess\DatalayerSession.xel')  
    WITH (MAX_MEMORY=2048 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=3 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=OFF)
    go
    ---Start the session
    ALTER EVENT SESSION [DatalayerSession]
          ON SERVER
        STATE = START;
    ---Wait for few minutes
    
    ---Query events
        
        SELECT 
        object_name,
        CAST(event_data as xml) as event_data,
        file_name, 
        file_offset
    FROM sys.fn_xe_file_target_read_file('C:\temp\Demos\DataLayerAppassess\DatalayerSession*xel', 
                'C:\\temp\\Demos\\DataLayerAppassess\\DatalayerSession*xem', 
                null,
                null)
    ---Stop the session after capturing the peak load.
    ALTER EVENT SESSION [DatalayerSession]
          ON SERVER
        STATE = STOP;
        
        go
    ```

5. Clique em **Avançar** para iniciar a avaliação.

    ![Adicionar fontes e iniciar a avaliação](../dma/media/dma-assesssqlonprem/select-database1.png)

> [!NOTE]
> Você pode executar várias avaliações simultaneamente e exibir o estado das avaliações abrindo a página **Todas as Avaliações**.

## <a name="view-results"></a>Exibir os resultados

A duração da avaliação depende do número de bancos de dados adicionados e do tamanho do esquema de cada banco de dados. Os resultados são exibidos para cada banco de dados assim que estiverem disponíveis.

1. Selecione o banco de dados que completou a avaliação e, em seguida, alterne entre **problemas de compatibilidade** e **recomendações de recurso** usando o switcher.

2. Revise os problemas de compatibilidade em todos os níveis de compatibilidade suportados pela versão de destino do SQL Server que você selecionou na página **Opções.**

Você pode rever problemas de compatibilidade analisando o objeto afetado, seus detalhes e potencialmente uma correção para cada problema identificado em **Alterações de Quebra,** **Alterações de comportamento**e **recursos depreciados**.

![Ver resultados de avaliação](../dma/media/dma-assesssqlonprem/review-results.png)

Da mesma forma, você pode rever a recomendação de recursos nas áreas **de Desempenho,** **Armazenamento**e **Segurança.**

As recomendações de recursos abrangem diferentes tipos de recursos, como OLTP na memória, Columnstore, Stretch Database, Always Encrypted, Dynamic Data Masking e Transparent Data Encryption.

![Exibir recomendações de recursos](../dma/media/dma-assesssqlonprem/feature-recommendations.png)

Para o Banco de Dados SQL do Azure, as avaliações fornecem problemas de bloqueio de migração e problemas de paridade de recursos.Revise os resultados para ambas as categorias selecionando as opções específicas.

- A categoria **de paridade de recursos do SQL Server** fornece um conjunto abrangente de recomendações, abordagens alternativas disponíveis no Azure e etapas mitigadoras. Isso ajuda você a planejar esse esforço em seus projetos de migração.

  ![Exibir informações para paridade de recursos do SQL Server](../dma/media/dma-assesssqlonprem/sql-feature-parity.png)

- A categoria **Problemas de compatibilidade** fornece recursos parcialmente suportados ou sem suporte que bloqueiam a migração de bancos de dados SQL Server no local para bancos de dados SQL do Azure.Em seguida, fornece recomendações para ajudá-lo a resolver essas questões.

  ![Exibir problemas de compatibilidade](../dma/media/dma-assesssqlonprem/compatibility-issues.png)

## <a name="assess-a-data-estate-for-target-readiness"></a>Avalie uma propriedade de dados para a prontidão do alvo

Se você quiser estender ainda mais essas avaliações para toda a propriedade de dados e encontrar a prontidão relativa das instâncias e bancos de dados do SQL Server para migração para o Banco de Dados SQL do Azure, faça o upload para o **Azure Migrate**.

Isso permite que você visualize os resultados consolidados no projeto de hub Do Zure Migrate.

A orientação detalhada e passo a passo para avaliações de prontidão de destino está disponível [aqui.](https://docs.microsoft.com/sql/dma/dma-assess-sql-data-estate-to-sqldb?view=sql-server-2017)

   ![Enviar resultados para o Azure Migrate](../dma/media/dma-assesssqlonprem/upload-to-azure-migrate.png)

## <a name="export-results"></a>Exportar resultados

Depois que todos os bancos de dados terminarem a avaliação, selecione **Exportar relatório** para exportar os resultados para um arquivo JSON ou um arquivo CSV. Em seguida, você pode analisar os dados à sua própria conveniência.

## <a name="save-and-load-assessments"></a>Salvar e carregar avaliações

Além de exportar os resultados de uma avaliação, você pode salvar detalhes de avaliação em um arquivo e carregar um arquivo de avaliação para revisão posterior.  Para obter mais informações, consulte o artigo [Salvar e carregar avaliações com o Assistente de Migração de Dados](../dma/dma-save-load-assessments.md).

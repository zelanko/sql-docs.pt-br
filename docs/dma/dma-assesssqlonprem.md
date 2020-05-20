---
title: Executar uma avaliação de migração SQL Server
titleSuffix: Data Migration Assistant
description: Saiba como usar Assistente de Migração de Dados para avaliar um SQL Server local antes de migrar para outro SQL Server ou para o banco de dados SQL do Azure
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
author: rajeshsetlem
ms.author: rajpo
ms.custom: seo-lt-2019
ms.openlocfilehash: f45a598c9e96d33f1edcc41c748a6751df712391
ms.sourcegitcommit: fb1430aedbb91b55b92f07934e9b9bdfbbd2b0c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82886103"
---
# <a name="perform-a-sql-server-migration-assessment-with-data-migration-assistant"></a>Realizar uma avaliação de migração do SQL Server com o Assistente de Migração de Dados

As instruções passo a passo a seguir ajudam a executar sua primeira avaliação para migrar para SQL Server locais, SQL Server em execução em uma VM do Azure ou banco de dados SQL do Azure usando Assistente de Migração de Dados.

   > [!NOTE]
   > O Assistente de Migração de Dados v 5.0 apresenta suporte para analisar a conectividade de banco de dados e consultas SQL inseridas no código do aplicativo. Para obter mais informações, consulte a postagem de blog [usando assistente de migração de dados para avaliar a camada de acesso a dados de um aplicativo](https://techcommunity.microsoft.com/t5/Microsoft-Data-Migration/Using-Data-Migration-Assistant-to-assess-an-application-s-data/ba-p/990430).

## <a name="create-an-assessment"></a>Criar uma avaliação

1. Selecione o ícone **novo** (+) e, em seguida, selecione o tipo de projeto de **avaliação** .

2. Defina o tipo de servidor de origem e de destino.

    Se você estiver atualizando sua instância de SQL Server local para uma instância de SQL Server local moderna ou para SQL Server hospedada em uma VM do Azure, defina o tipo de servidor de origem e de destino como **SQL Server**. Se você estiver migrando para o banco de dados SQL do Azure, defina o tipo de servidor de destino como **banco de dados SQL do Azure**.

3. Clique em **Criar**.

   ![Criar uma avaliação](../dma/media/dma-assesssqlonprem/new-assessment.png)

## <a name="choose-assessment-options"></a>Escolher opções de avaliação

1. Selecione a versão de SQL Server de destino para a qual você planeja migrar.

2. Selecione o tipo de relatório.

   Ao avaliar sua instância de SQL Server de origem para migrar para o SQL Server local ou para SQL Server hospedado em destinos de VM do Azure, você pode escolher um ou ambos os seguintes tipos de relatório de avaliação:

    - **Problemas de compatibilidade**
    - **Recomendação de novos recursos**

   ![Selecione um tipo de relatório de avaliação para SQL Server destino](../dma/media/dma-assesssqlonprem/assessment-types.png)

   Ao avaliar sua instância de SQL Server de origem para migrar para o banco de dados SQL do Azure, você pode escolher um ou ambos os tipos de relatório de avaliação a seguir:

    - **Determinar compatibilidade do banco de dados**
    - **Verificação de paridade de recursos**

    ![Selecionar tipo de relatório de avaliação para destino do banco de dados SQL](../dma/media/dma-assesssqlonprem/assessment-types-azure.png)

## <a name="add-databases-and-extended-events-trace-to-assess"></a>Adicionar bancos de dados e rastreamento de eventos estendidos para avaliar

1. Selecione **adicionar fontes** para abrir o menu de atalho de conexão.

2. Insira o nome da instância do SQL Server, escolha o tipo de autenticação, defina as propriedades de conexão corretas e, em seguida, selecione **conectar**.

3. Selecione os bancos de dados a serem avaliados e, em seguida, selecione **Adicionar**.

    > [!NOTE]
    > Você pode remover vários bancos de dados selecionando-os enquanto mantém a tecla Shift ou CTRL pressionada e clicando em **Remover fontes**. Você também pode adicionar bancos de dados de várias instâncias de SQL Server selecionando **adicionar fontes**.

4. Se você tiver qualquer consulta SQL ad hoc ou dinâmica ou quaisquer instruções DML iniciadas por meio da camada de dados de aplicativo, insira o caminho para a pasta na qual você colocou todos os arquivos de sessão de eventos estendidos que você coletou para capturar a carga de trabalho no SQL Server de origem.

     O exemplo a seguir mostra como criar uma sessão de evento estendido em seu SQL Server de origem para capturar a carga de trabalho da camada de dados do aplicativo.  Capture a carga de trabalho pela duração que representa sua carga de trabalho de pico.

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

1. Selecione o banco de dados que concluiu a avaliação e, em seguida, alterne entre os **problemas de compatibilidade** e as **recomendações de recursos** usando o alternador.

2. Examine os problemas de compatibilidade em todos os níveis de compatibilidade com suporte na versão de SQL Server de destino que você selecionou na página **Opções** .

Você pode examinar os problemas de compatibilidade analisando o objeto afetado, seus detalhes e potencialmente uma correção para cada problema identificado em **alterações significativas**, **alterações de comportamento**e **recursos preteridos**.

![Exibir resultados da avaliação](../dma/media/dma-assesssqlonprem/review-results.png)

Da mesma forma, você pode examinar a recomendação de recursos entre áreas de **desempenho**, **armazenamento**e **segurança** .

As recomendações de recursos abrangem diferentes tipos de recursos, como OLTP na memória, Columnstore, Stretch Database, Always Encrypted, Máscara de Dados Dinâmicos e Transparent Data Encryption.

![Exibir recomendações de recursos](../dma/media/dma-assesssqlonprem/feature-recommendations.png)

Para o banco de dados SQL do Azure, as avaliações fornecem problemas de bloqueio de migração e problemas de paridade de recursos.Examine os resultados de ambas as categorias selecionando as opções específicas.

- A categoria de **paridade de recursos SQL Server** fornece um conjunto abrangente de recomendações, abordagens alternativas disponíveis no Azure e etapas de mitigação. Ele ajuda a planejar esse esforço em seus projetos de migração.

  ![Exibir informações para SQL Server paridade de recurso](../dma/media/dma-assesssqlonprem/sql-feature-parity.png)

- A categoria de **problemas de compatibilidade** fornece recursos com suporte parcial ou sem suporte que bloqueiam a migração de bancos de dados de SQL Server locais para bancos de dados SQL do Azure.Em seguida, ele fornece recomendações para ajudá-lo a resolver esses problemas.

  ![Exibir problemas de compatibilidade](../dma/media/dma-assesssqlonprem/compatibility-issues.png)

## <a name="assess-a-data-estate-for-target-readiness"></a>Avaliar um espaço de dados para prontidão de destino

Se você quiser estender ainda mais essas avaliações para todo o espaço de dados e encontrar a preparação relativa de instâncias de SQL Server e bancos de dado para migração para o banco de dados SQL do Azure, carregue os resultados para o Hub migrações para Azure selecionando **carregar para migrações para Azure**.

Isso permite que você exiba os resultados consolidados no projeto do hub de migrações para Azure.

As diretrizes detalhadas passo a passo para avaliações de prontidão de destino estão disponíveis [aqui](https://docs.microsoft.com/sql/dma/dma-assess-sql-data-estate-to-sqldb?view=sql-server-2017).

   ![Carregar resultados para migrações para Azure](../dma/media/dma-assesssqlonprem/upload-to-azure-migrate.png)

## <a name="export-results"></a>Exportar resultados

Depois que todos os bancos de dados concluírem a avaliação, selecione **Exportar relatório** para exportar os resultados para um arquivo JSON ou um arquivo CSV. Em seguida, você pode analisar os dados por sua própria conveniência.

## <a name="save-and-load-assessments"></a>Salvar e carregar avaliações

Além de exportar os resultados de uma avaliação, você pode salvar detalhes de avaliação em um arquivo e carregar um arquivo de avaliação para revisão posterior.  Para obter mais informações, consulte o artigo [salvar e carregar avaliações com assistente de migração de dados](../dma/dma-save-load-assessments.md).

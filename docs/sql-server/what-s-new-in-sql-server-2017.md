---
title: Novidades no SQL Server 2017 | Microsoft Docs
ms.custom: ''
ms.date: 10/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: sql-non-specified
ms.reviewer: ''
ms.suite: sql
ms.technology:
- server-general
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0b57f375-9242-4bb2-9d4b-c560d5a93524
caps.latest.revision: ''
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 47d6f056dce4ad26a10e082d27119523fde303d0
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2018
---
# <a name="whats-new-in-sql-server-2017"></a>Novidades no SQL Server 2017
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]
O SQL Server 2017 é uma etapa importante para transformar o SQL Server em uma plataforma que oferece opções de linguagens de desenvolvimento, tipos de dados, locais ou nuvens e sistemas operacionais, utilizando a capacidade do SQL Server no Linux, em contêineres do Docker baseados em Linux e no Windows. Este tópico resume o que há de novo para áreas de recurso específico e inclui links para obter detalhes adicionais. Para obter mais informações relacionadas ao SQL Server no Linux, consulte [Documentação do SQL Server no Linux](https://docs.microsoft.com/sql/linux/)

[![Baixar do Centro de Avaliação](../includes/media/download2.png)](http://go.microsoft.com/fwlink/?LinkID=829477) **Experimente:** [Baixar a versão do SQL Server 2017, agosto de 2017](http://go.microsoft.com/fwlink/?LinkID=829477).

> [!NOTE]
> Além das alterações abaixo, atualizações cumulativas são liberadas em intervalos regulares após a versão GA. Essas atualizações cumulativas fornecem várias melhorias e correções. Para obter informações sobre a última versão de CU, consulte [Atualizações cumulativas do SQL Server 2017](http://aka.ms/sql2017cu).

## <a name="sql-server-2017-database-engine"></a>Mecanismo de Banco de Dados do SQL Server 2017

O SQL Server 2017 inclui vários novos recursos, aprimoramentos e melhorias de desempenho no Mecanismo de Banco de Dados. 
- **Os assemblies CLR** agora são adicionados a uma lista de permissões como uma solução alternativa para o recurso `clr strict security`, descrito no CTP 2.0. [sp_add_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-add-trusted-assembly-transact-sql.md), [sp_drop_trusted_assembly](../relational-databases/system-stored-procedures/sys-sp-drop-trusted-assembly-transact-sql.md) e [sys.trusted_asssemblies](../relational-databases/system-catalog-views/sys-trusted-assemblies-transact-sql.md) são adicionados para dar suporte à lista de permissões de assemblies confiáveis (RC1).  
- A **Recompilação de índice online retomável** retoma uma operação de recompilação de índice online de onde ela parou após uma falha, como o failover de uma réplica ou espaço em disco insuficiente ou pausa e posteriormente retoma uma operação de recompilação de índice online. Veja [ALTER INDEX](../t-sql/statements/alter-index-transact-sql.md) e [Diretrizes para operações de índice online](../relational-databases/indexes/guidelines-for-online-index-operations.md). (CTP 2.0)
- A opção **IDENTITY_CACHE** da ALTER DATABASE SCOPED CONFIGURATION permite evitar lacunas nos valores de colunas de identidade caso um servidor reinicie inesperadamente ou faça failover para um servidor secundário. Veja [ALTER DATABASE SCOPED CONFIGURATION](../t-sql/statements/alter-database-scoped-configuration-transact-sql.md). (CTP 2.0)
- Uma nova geração de melhorias do processo de consulta que adaptará estratégias de otimização para as condições de tempo de execução da carga de trabalho do aplicativo. Para a primeira versão da família de recursos de **processamento de consulta adaptável**, temos três novas melhorias: **junções adaptáveis de modo de lote**, **comentários de concessão de memória de modo de lote** e **execução intercalada** para funções com valor de tabela de várias instruções.  Veja [Processamento de consultas adaptável em bancos de dados SQL](../relational-databases/performance/adaptive-query-processing.md).
- O **Ajuste automático de banco de dados** fornece informações sobre possíveis problemas de desempenho de consultas e pode corrigir automaticamente os problemas identificados. Consulte [Ajuste automático](../relational-databases/automatic-tuning/automatic-tuning.md). (CTP 2.0)
- Os novos **recursos de banco de dados do gráfico** para modelagem de relações de muitos-para-muitos têm uma nova sintaxe [CREATE TABLE](../t-sql/statements/create-table-sql-graph.md) para a criação de nós e tabelas de borda e a palavra-chave [MATCH](../t-sql/queries/match-sql-graph.md) para consultas. Consulte [Processamento de Gráficos com o SQL Server 2017](../relational-databases/graphs/sql-graph-overview.md). (CTP 2.0)
- Uma opção sp_configure chamada `clr strict security` está habilitada por padrão para aprimorar a segurança de assemblies do CLR. Consulte [Segurança rígida do CLR](../database-engine/configure-windows/clr-strict-security.md). (CTP 2.0)
- Agora, a instalação permite especificar o tamanho do arquivo tempdb inicial em até **256 GB** (262.144 MB) por arquivo, com um aviso se o tamanho do arquivo estiver definido como um valor maior que 1 GB e se a IFI não estiver habilitada. (CTP 2.0)
- A coluna **modified_extent_page_count** no [sys.dm_db_file_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md) controla alterações diferenciais em cada arquivo de banco de dados, habilitando soluções de backup inteligentes que executam backup diferencial ou backup completo com base no percentual de páginas alteradas no banco de dados. (CTP 2.0)
- A sintaxe T-SQL [SELECT INTO](../t-sql/queries/select-into-clause-transact-sql.md) agora dá suporte ao carregamento de uma tabela em um grupo de arquivos diferente do grupo de arquivos padrão do usuário usando a palavra-chave **ON**. (CTP 2.0)
- Agora, há suporte para transações de banco de dados em todos os bancos de dados que fazem parte de um **Grupo de Disponibilidade AlwaysOn**, incluindo bancos de dados que fazem parte da mesma instância. Consulte [Transações – Grupos de Disponibilidade Always On e Espelhamento de Banco de Dados](../database-engine/availability-groups/windows/transactions-always-on-availability-and-database-mirroring.md) (CTP 2.0)
- Uma nova função dos **Grupos de Disponibilidade** oferece suporte sem cluster, configuração de Grupos de Disponibilidade de Confirmação de Réplica Mínima e migrações e testes entre os sistemas operacionais Windows e Linux. (CTP 1.3)
- Novas exibições de gerenciamento dinâmico:
    - O [sys.dm_db_log_stats](../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md) expõe atributos de nível de resumo e informações sobre arquivos de log de transações, que ajudam a monitorar a integridade do log de transações. (CTP 2.1)
    - O [sys.dm_tran_version_store_space_usage](../relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-space-usage.md) controla o uso do repositório de versão por banco de dados, o que ajuda a planejar de forma proativa o dimensionamento do tempdb com base no uso do repositório de versão por banco de dados. (CTP 2.0)
    - O [sys.dm_db_log_info](../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md) expõe informações de VLF a fim de monitorar, alertar e evitar possíveis problemas de log de transações. (CTP 2.0)
    - O [sys.dm_db_stats_histogram](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) é uma nova exibição de gerenciamento dinâmico para a análise de estatísticas. (CTP 1.3)
    - O **sys.dm_os_host_info** fornece informações de sistema operacional para Windows e Linux. (CTP 1.0)
- O **DTA (Orientador de Otimização de Banco de Dados)** tem mais opções e desempenho aprimorado. (CTP 1.2)
- Os **aprimoramentos na memória** oferecem suporte para colunas computadas em tabelas com otimização de memória, suporte completo para funções JSON para o operador CROSS APPLY em módulos compilados nativamente. (CTP 1.1)
- Agora, há suporte para a função STRING_AGG nas novas **funções de cadeia de caracteres** CONCAT_WS, TRANSLATE, TRIM e WITHIN GROUP. (CTP 1.1)
- Há novas **opções de acesso em massa** (BULK INSERT e OPENROWSET(BULK...) ) no CSV e nos arquivos blob do Azure. (CTP 1.1)
- Os **aprimoramentos de objetos com otimização de memória** incluem o sp_spaceused e a eliminação das oito limitações de índice de tabelas com otimização de memória, sp_rename para tabelas com otimização de memória e módulos T-SQL compilados nativamente, bem como CASE e TOP (N) WITH TIES para módulos T-SQL compilados nativamente. Agora, é possível armazenar, fazer backup e restaurar arquivos de grupo de arquivos com otimização de memória no Armazenamento do Microsoft Azure. (CTP 1.0)
- A **DATABASE SCOPED CREDENTIAL** é uma nova classe de permissões protegíveis que oferece suporte a CONTROL, ALTER, REFERENCES, TAKE OWNERSHIP e VIEW DEFINITION. ADMINISTER DATABASE BULK OPERATIONS agora está visível em sys.fn_builtin_permissions. (CTP 1.0)
- O banco de dados **COMPATIBILITY_LEVEL 140** é adicionada. (CTP 1.0).  

Para obter mais informações, consulte [Novidades do Mecanismo de Banco de Dados do SQL Server 2017](~/database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md).

## <a name="sql-server-2017-integration-services-ssis"></a>SQL Server 2017 Integration Services (SSIS)
- O novo recurso **Scale Out** do SSIS tem os seguintes recursos, novos e alterados. Para obter mais informações, consulte [Novidades do Integration Services no SQL Server 2017](~/integration-services/what-s-new-in-integration-services-in-sql-server-2017.md). (RC1)
    -   Agora, há suporte para alta disponibilidade no Mestre de Scale Out.
    -   O tratamento do failover dos logs de execução dos Trabalhos de Scale Out foi aprimorado.
    -   O parâmetro *runincluster* do procedimento armazenado **[catalog].[create_execution]** foi renomeado como *runinscaleout*, a fim de obter consistência e legibilidade.
    -   O catálogo do SSIS tem uma nova propriedade global para especificar o modo padrão de execução de pacotes do SSIS.
- No novo recurso **Scale Out do SSIS**, agora é possível usar o parâmetro **Use32BitRuntime** ao disparar a execução. (CTP 2.1)
- Agora, o SQL Server 2017 Integration Services (SSIS) oferece suporte ao **SQL Server no Linux** e um novo pacote permite executar pacotes do SSIS no Linux na linha de comando. Para obter mais informações, consulte a [postagem de blog que anunciou que o SSIS oferece suporte para Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/). (CTP 2.1)
- O novo recurso **Scale Out do SSIS** facilita a execução do SSIS em vários computadores. Veja [Scale Out do Integration Services](~/integration-services/scale-out/integration-services-ssis-scale-out.md). (CTP 1.0)
- Agora, a Fonte OData e o Gerenciador de Conexões OData oferecem suporte aos feeds OData do Microsoft Dynamics AX Online e do Microsoft Dynamics CRM Online. (CTP 1.0)

Para obter mais informações, consulte [Novidades do Integration Services no SQL Server 2017](~/integration-services/what-s-new-in-integration-services-in-sql-server-2017.md).

## <a name="sql-server-2017-master-data-services-mds"></a>SQL Server 2017 Master Data Services (MDS)
- A experiência e o desempenho são melhorados ao atualizar do SQL Server 2012, do SQL Server 2014 e do SQL Server 2016 para o SQL Server 2017 Master Data Services. 
- Agora você pode exibir as listas classificadas de entidades, coleções e hierarquias na página **Explorer** do aplicativo Web.
- O desempenho foi melhorado para o preparo de milhões de registros usando o procedimento armazenado de preparo.
- O desempenho foi aprimorado ao expandir a pasta **Entidades** na página **Gerenciar Grupos** para atribuir permissões de modelo. A página **Gerenciar Grupos** está localizada na seção **Segurança** do aplicativo Web. Para obter mais informações sobre a melhoria de desempenho, consulte [https://support.microsoft.com/help/4023865?preview](https://support.microsoft.com/help/4023865?preview). Para saber mais sobre como atribuir permissões, confira [Atribuir permissões de objeto do modelo (Master Data Services)](../master-data-services/assign-model-object-permissions-master-data-services.md).

## <a name="sql-server-2017-analysis-services-ssas"></a>SSAS (SQL Server 2017 Analysis Services) 
O SQL Server Analysis Services 2017 apresenta vários aprimoramentos para modelos de tabela. Eles incluem:
- O modo de tabela como opção de instalação padrão para o Analysis Services. (CTP 2.0)
- Segurança do nível de objeto para proteger os metadados dos modelos de tabela. (CTP 2.0)
- Relações de data para criar relações baseadas em campos de data facilmente. (CTP 2.0)
- Há suporte para consultas M nas novas fontes de dados **Get Data** (Power Query) e nas fontes de dados DirectQuery existentes. (CTP 2.0) 
- Editor DAX do SSDT. (CTP 2.0)
- Dicas de codificação, um recurso avançado usado para a atualização de dados de grandes modelos de tabela na memória. (CTP 1.3)
- Há suporte para o **Nível de compatibilidade 1400** para modelos de tabela. Para criar ou atualizar projetos de modelo de tabela novos ou existentes para o nível de compatibilidade 1400, baixe e instale o [SQL Server Data Tools (SSDT) 17.0 RC2](https://go.microsoft.com/fwlink?LinkId=837939). (CTP 1.1)
- Uma experiência moderna do **Get Data** para modelos de tabela no nível de compatibilidade 1400. Consulte o [Blog da equipe do Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2016/12/16/introducing-a-modern-get-data-experience-for-sql-server-2017-on-windows-ctp-1-1-for-analysis-services/). (CTP 1.1)
- Propriedade **Ocultar Membros** para ocultar membros em branco em hierarquias desbalanceadas. (CTP 1.1)
- Nova ação do usuário final **Linhas de Detalhes** para **Mostrar Detalhes** de informações agregadas. Funções [SELECTCOLUMNS](https://msdn.microsoft.com/library/mt761759.aspx) e **DETAILROWS** para criar expressões de Linhas de Detalhes. (CTP 1.1)
- Operador DAX **IN** para especificar vários valores. (CTP 1.1)

Para obter mais informações, consulte [Novidades do SQL Server Analysis Services 2017](~/analysis-services/what-s-new-in-sql-server-analysis-services-2017.md).

## <a name="sql-server-2017-reporting-services-ssrs"></a>SQL Server 2017 Reporting Services (SSRS)
O SQL Server Reporting Services não está mais disponível para ser instalado por meio da instalação do SQL Server. Acesse o Centro de Download da Microsoft para [baixar o Microsoft SQL Server 2017 Reporting Services](https://www.microsoft.com/download/details.aspx?id=55252). 
- Agora, é possível inserir comentários nos relatórios, como uma forma de ampliar a perspectiva e colaborar com outras pessoas. Também é possível incluir anexos com comentários.
- Nas versões mais recentes do Construtor de Relatórios e do SQL Server Data Tools, é possível criar consultas DAX nativas em modelos de dados de tabela do SQL Server Analysis Services com suporte arrastando e soltando os campos desejados nos designers de consultas. Consulte o [blog do Reporting Services](https://blogs.msdn.microsoft.com/sqlrsteamblog/2017/03/09/query-designer-support-for-dax-now-available-in-report-builder-and-sql-server-data-tools/).
- Para possibilitar o desenvolvimento de aplicativos modernos e personalização, o SSRS agora dá suporte a uma API RESTful totalmente em conformidade com OpenAPI. A especificação de API e a documentação completa agora podem ser encontradas no [swaggerhub](https://app.swaggerhub.com/apis/microsoft-rs/SSRS/2.0).

Para obter mais informações, consulte [Novidades do SQL Server Reporting Services (SSRS)](~/reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md).

## <a name="machine-learning-in-sql-server-2017"></a>Machine Learning no SQL Server 2017 

O SQL Server R Services foi renomeado como **Serviços do SQL Server Machine Learning** a fim de mostrar o novo suporte para Python, além das linguagens R. É possível usar os Serviços de Machine Learning (no Banco de Dados) para executar scripts R ou Python no SQL Server ou instalar o **Microsoft Machine Learning Server (Autônomo)** para implantar e consumir modelos R e Python que não exigem o SQL Server. 

Os desenvolvedores do SQL Server agora têm acesso a bibliotecas Python ML e AI extensivas disponíveis no ecossistema do software livre, juntamente com as inovações mais recentes da Microsoft:

- **revoscalepy** – esse equivalente no Python do RevoScaleR inclui os algoritmos paralelos de regressão linear e logística, árvore de decisão, árvores aumentadas e florestas aleatórias, bem como um conjunto sofisticado de APIs para transformação de dados e movimentação de dados, contextos de computação remota e fontes de dados.
- **microsoftml** – este pacote moderno de algoritmos de aprendizado de máquina e transformações com associações de Python inclui redes neurais profundas, árvores de decisão rápidas e florestas de decisão, além de algoritmos otimizados para regressão logística e linear. Também é possível pode obter modelos previamente treinados com base em modelos de ResNet que você pode usar para extração de imagem ou análise de sentimento.
- **Operacionalização do Python com T-SQL** – implante código Python facilmente usando o procedimento armazenado `sp_execute_external_script`. Obtenha ótimo desempenho ao transmitir dados do SQL para processos de Python e usando a paralelização de anel MPI.
- **Python em contextos de computação no SQL Server** – os desenvolvedores e cientistas de dados podem executar código Python remotamente em seus ambientes de desenvolvimento para explorar dados e desenvolver modelos sem movimentação de dados.
- **Pontuação nativa** -a função PREDICT no Transact-SQL pode ser usada para executar a pontuação em qualquer instância do SQL Server 2017, mesmo se o R não estiver instalado. Basta treinar o modelo usando um dos algoritmos RevoScaleR e revoscalepy com suporte e salvar o modelo em um formato binário compacto novo.
- **Gerenciamento de pacote** – o T-SQL agora dá suporte à instrução CREATE EXTERNAL LIBRARY, para proporcionar a DBAs melhor gerenciamento por meio de pacotes R. Use funções para controlar o acesso a pacotes compartilhados ou privados, armazenar pacotes R no banco de dados e compartilhá-los entre os usuários.
- **Melhorias de desempenho** – o procedimento armazenado `sp_execute_external_script` foi otimizado para dar suporte à execução em modo de lote para dados de columnstore.


Para obter mais informações, consulte [Novidades do Serviços do SQL Server Machine Learning](~/advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md).

## <a name="next-steps"></a>Próximas etapas
- Consulte as [Notas de Versão do SQL Server 2017](sql-server-2017-release-notes.md).
- Descubra as [Novidades do SQL Server 2017 no Linux](https://docs.microsoft.com/sql/linux/sql-server-linux-whats-new).
- Descubra as [Novidades do SQL Server 2016](what-s-new-in-sql-server-2016.md).

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
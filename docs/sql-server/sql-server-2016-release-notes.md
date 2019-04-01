---
title: Notas de versão do SQL Server 2016 | Microsoft Docs
ms.date: 04/25/2018
ms.prod: sql
ms.reviewer: ''
ms.custom: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- build notes
- release issues
ms.assetid: c64077a2-bec8-4c87-9def-3dbfb1ea1fb6
author: craigg-msft
ms.author: craigg
manager: jhubbard
monikerRange: = sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 63bbff09e8f9d7ca6fa4658369194c9caee26648
ms.sourcegitcommit: 706f3a89fdb98e84569973f35a3032f324a92771
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58658280"
---
# <a name="sql-server-2016-release-notes"></a>Notas de Versão do SQL Server 2016.
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]
  Este artigo descreve as limitações e os problemas com as versões do SQL Server 2016, incluindo service packs. Para obter informações sobre as novidades, veja [Novidades no SQL Server 2016](https://docs.microsoft.com/sql/sql-server/what-s-new-in-sql-server-2016).

- [![Baixar no Centro de Avaliação](../includes/media/download2.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)  Baixar o SQL Server 2016 no **[Centro de Avaliação](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)**
- [![Máquina Virtual pequena do Azure](../includes/media/azure-vm.png)](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftsqlserver.sql2016sp1-ws2016) Tem uma conta do Azure?  Em seguida, acesse **[aqui](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftsqlserver.sql2016sp1-ws2016)** para criar uma Máquina Virtual com o SQL Server 2016 SP1 já está instalado.
- [![Baixar o SSMS](../includes/media/download2.png)](../ssms/download-sql-server-management-studio-ssms.md) Para obter a versão mais recente do SQL Server Management Studio, veja **[Baixar o SSMS (SQL Server Management Studio)](../ssms/download-sql-server-management-studio-ssms.md)**.

## <a name="bkmk_2016sp2"></a>SQL Server 2016 Service Pack 2 (SP2)

![info_tip](../sql-server/media/info-tip.png) O SQL Server 2016 SP2 inclui todas as atualizações cumulativas liberadas após SP1 2016, até e incluindo CU8.

- [![Centro de Download da Microsoft](../includes/media/download2.png)](https://go.microsoft.com/fwlink/?linkid=869608) [Baixar SQL Server 2016 Service Pack 2 (SP2)](https://go.microsoft.com/fwlink/?linkid=869608)
- Para obter uma lista completa de atualizações, veja [informações de versão do SQL Server 2016 Service Pack 2](https://support.microsoft.com/help/4052908/sql-server-2016-service-pack-2-release-information)

A instalação do SQL Server 2016 SP2 pode exigir a reinicialização após a instalação. Como melhor prática, é recomendável planejar e executar uma reinicialização após a instalação do SQL Server 2016 SP2.

Melhorias de desempenho e escala no SQL Server 2016 SP2.

|Recurso|Descrição|Mais informações|
|---|---|---|
|Procedimento de limpeza de banco de dados de distribuição aprimorado |   Uma distribuição muito grande de tabelas de banco de dados causou bloqueio e deadlock. Um procedimento de limpeza aprimorado tem como objetivo eliminar alguns desses cenários de bloqueio ou de deadlock. |   [KB4040276](https://support.microsoft.com/help/4040276/fix-indirect-checkpoints-on-the-tempdb-database-cause-non-yielding)  |
|Limpeza do controle de alterações    |   Melhoria do desempenho e da eficiência da limpeza de controle de alterações para tabelas laterais do Controle de Alterações.    |   [KB4052129](https://support.microsoft.com//help/4052129/update-for-manual-change-tracking-cleanup-procedure-in-sql-server-2016) |
|Uso do tempo limite da CPU para cancelar a solicitação Resource Governor   |   Melhoria da manipulação de solicitações de consulta por meio do cancelamento da solicitação, se o limite da CPU para uma solicitação for alcançado. Esse comportamento é habilitado no sinalizador de rastreamento 2422. |   [KB4038419](https://support.microsoft.com/help/4038419/add-cpu-timeout-to-resource-governor-request-max-cpu-time-sec)   |
|SELECT INTO para criar a tabela de destino no grupo de arquivos    |   A partir do SQL Server 2016 SP2, a sintaxe SELECT INTO do T-SQL é compatível com o carregamento de uma tabela em um grupo de arquivos diferente do grupo de arquivos padrão do usuário, usando a palavra-chave <Filegroup name> ON na sintaxe do T-SQL. |       |
|Ponto de verificação indireto aprimorado para TempDB    |   Melhoria do ponto de verificação indireto para TempDB para minimizar a contenção de spinlock em DPLists. Essa melhoria permite que a carga de trabalho de TempDB no SQL Server 2016 seja dimensionada imediatamente caso o ponto de verificação indireto seja ON para TempDB.    |   [KB4040276](https://support.microsoft.com/help/4040276) |
|Melhoria do desempenho do backup de banco de dados em computadores de memória grande  |   O SQL Server 2016 SP2 otimiza a maneira como o E/S em andamento é drenado durante o backup, o que gera grandes ganhos de desempenho de backup para bancos de dados pequenos a médios. Houve uma melhoria de mais de 100x ao fazer backup de banco de dados do sistema em um computador de 2 TB. O ganho de desempenho é reduzido à medida que o tamanho do banco de dados aumenta e conforme as páginas a serem copiadas em backup e a E/S de backup levam mais tempo, comparado ao pool de buffers de iteração. Essa mudança ajudará a melhorar o desempenho de backup para os clientes que hospedam vários bancos de dados pequenos em servidores grandes de alto nível e com muita memória.    |       |
|Suporte para compactação de backup de VDI para bancos de dados habilitados para TDE   |   O SQL Server 2016 SP2 adicionou suporte à VDI para permitir que soluções de backup de VDI aproveitem a compactação para bancos de dados habilitados para TDE. Com essa melhoria, um novo formato de backup foi introduzido para oferecer suporte à compactação de backup para bancos de dados habilitados para TDE. O mecanismo do SQL Server manipulará formatos de backup novos e antigos de forma transparente, a fim de restaurar backups.   |       |
|Carregamento dinâmico de parâmetros de perfil de agente de replicação    |   Esse novo aprimoramento permite que parâmetros de agentes de replicação sejam carregados dinamicamente sem a necessidade de reiniciar o agente. Essa alteração se aplica somente aos parâmetros de perfil de agente mais comumente usados. |       |
|Compatibilidade com a opção MAXDOP para estatísticas criar/atualizar |    Essa melhoria permite especificar a opção MAXDOP para uma instrução de estatística CRIAR/ATUALIZAR. Além disso, assegura que a configuração MAXDOP seja usada quando as estatísticas são atualizadas como parte da criação ou recompilação de todos os tipos de índices (caso a opção MAXDOP esteja presente).   |   [KB4041809](https://support.microsoft.com/help/4041809) |
|Melhoria da atualização automática de estatísticas para estatísticas incrementais |    Em determinados cenários, quando uma série de alterações de dados ocorre em várias partições de uma tabela de forma que o número total de alterações em estatísticas incrementais excede o limite de atualização automática, mas nenhuma das partições individuais excede o limite de atualização automática, a atualização de estatísticas pode ser atrasada até que muitas outras modificações ocorram na tabela. Esse comportamento é corrigido no sinalizador de rastreamento 11024.   |       |

Melhorias de compatibilidade e diagnóstico no SQL Server 2016 SP2.

|Recurso|Descrição|Mais informações|
|---|---|---|
|Compatibilidade completa com controle DTC para bancos de dados em grupos de disponibilidade    |   No momento, não há suporte para as transações entre bancos de dados para bancos de dados que fazem parte de um grupo de disponibilidade no SQL Server 2016. Com o SQL Server 2016 SP2, introduzimos compatibilidade completa com transações distribuídas com bancos de dados de grupo de disponibilidade.   |       |
|Atualizar para a coluna is_encrypted do sys.databases para refletir de forma precisa o status de criptografia de TempDB |   O valor da coluna is_encryptedcolumn no sys.databases é de 1 para TempDB, mesmo depois da desativação da criptografia para todos os bancos de dados de usuário e da reinicialização do SQL Server. O comportamento esperado é um valor igual a 0, pois TempDB já não é criptografado nessa situação. A partir do SQL Server 2016 SP2, a coluna is_encrypted do sys.databases reflete com precisão o status de criptografia de TempDB.  |       |
|Novas opções DBCC CLONEDATABASE para gerar clones verificados e backups   |   Com o SQL Server 2016 SP2, o DBCC CLONEDATABASE possibilita duas novas opções: produzir um clone verificado ou um backup de clone. Ao criar um banco de dados clonado com a opção VERIFY_CLONEDB, um banco de dados clonado consistente será criado e verificado, e isso terá suporte da Microsoft para uso em produção. Uma nova propriedade foi introduzida para validar a verificação do clone: SELECT DATABASEPROPERTYEX('clone_database_name', 'IsVerifiedClone'). Quando um clone é criado com a opção BACKUP_CLONEDB, um backup é gerado na mesma pasta do arquivo de dados para facilitar a movimentação do clone para um servidor diferente ou enviá-lo para o CSS (Serviço de Suporte e Atendimento ao Cliente Microsoft) para solução de problemas.  |       |
|Suporte do SSB (Service Broker) para DBCC CLONEDATABASE    |   Aprimoramento do comando DBCC CLONEDATABASE para permitir o script de objetos SSB.  |   [KB4092075](https://support.microsoft.com/help/4092075) |
|Novo DMV para monitorar o uso de espaço de armazenamento de versão de TempDB    |   Um novo DMV sys.dm_tran_version_store_space_usage foi incluído no SQL Server 2016 SP2 para permitir o monitoramento do espaço de armazenamento de versão do TempDB. Agora, os DBAs podem planejar de maneira proativa o dimensionamento do TempDB com base no requisito de uso de armazenamento de versão por banco de dados, sem qualquer sobrecarga de desempenho ao executá-lo em servidores de produção. |       |
|Despejos completos compatíveis com agentes de replicação | Atualmente, se os agentes de replicação encontram uma exceção sem tratamento, o comportamento padrão é criar um minidespejo dos sintomas da exceção. Isso dificulta a solução de problemas de exceção sem tratamento. Por meio desta mudança, introduzimos uma nova chave do Registro, que permitirá a criação de um despejo completo para agentes de replicação.  |       |
|Melhoria dos Eventos Estendidos para falha de roteamento de leitura de um grupo de disponibilidade |   Antigamente, o xEvent read_only_rout_fail seria acionado se houvesse uma lista de roteamento presente, mas nenhum dos servidores nessa lista estivessem disponíveis para conexão. O SQL Server 2016 SP2 inclui informações adicionais para ajudar a solucionar problemas e expandir nos pontos de código em que o xEvent é acionado.  |       |
|Novo DMV para monitorar o log de transações |   Adicionado um novo DMV sys.dm_db_log_stats que retorna atributos de nível de resumo e informações sobre arquivos de log de transações de bancos de dados. |       |
|Novo DMV para monitorar informações de VLF |   Um novo DMV sys.dm_db_log_info foi introduzido no SQL Server 2016 SP2 para expor as informações de VLF semelhantes a DBCC LOGINFO, a fim de monitorar, emitir alertas e evitar possíveis problemas de T-Log enfrentados pelos clientes.    |       |
|Informações do processador em sys.dm_os_sys_info|   Novas colunas foram adicionadas ao DMV sys.dm_os_sys_info para expor as informações relacionadas do processador, como socket_count e cores_per_numa.  |       |
|Informações de extensão modificadas em sys.dm_db_file_space_usage| Uma nova coluna foi adicionada a sys.dm_db_file_space_usage para controlar o número de extensões modificadas desde o último backup completo.  |       |
|Informações de segmento em sys.dm_exec_query_stats |   Novas colunas foram adicionadas a sys.dm_exec_query_stats para controlar o número de segmentos columnstore ignorados e lidos, como total_columnstore_segment_reads e total_columnstore_segment_skips.   |   [KB4051358](https://support.microsoft.com/help/4051358) |
|Definição do nível de compatibilidade correto para o banco de dados de distribuição  |   Após a instalação do Service Pack, o nível de compatibilidade do banco de dados de distribuição é alterado para 90. Isso ocorreu devido a um caminho de código no procedimento armazenado sp_vupgrade_replication. Agora o SP foi alterado para definir o nível de compatibilidade correto para o banco de dados de distribuição.   |       |
|Mostrar as últimas informações conhecidas e bem-sucedidas de DBCC CHECKDB    |   Uma nova opção de banco de dados foi adicionada para retornar programaticamente a data da última execução bem-sucedida de DBCC CHECKDB. Agora, os usuários podem consultar DATABASEPROPERTYEX([database], 'lastgoodcheckdbtime') para obter um valor único que representa a data/hora da última execução bem-sucedida de DBCC CHECKDB no banco de dados especificado.  |       |
|Melhorias na Execução XML| [Informações sobre quais estatísticas foram usadas para compilar o plano de consulta](https://blogs.msdn.microsoft.com/sql_server_team/sql-server-2017-showplan-enhancements/), incluindo o nome da estatística, o número de alterações, a percentagem de amostragem e quando a estatística foi atualizada pela última vez. Adicionado a modelos CE 120 e versões posteriores. Por exemplo, não é compatível com CE 70.| |
| |Um novo atributo [EstimateRowsWithoutRowgoal](https://blogs.msdn.microsoft.com/sql_server_team/more-showplan-enhancements-row-goal/) será adicionado à Execução XML se o Otimizador de Consulta usar a lógica "meta de linhas".| |
| |Novos atributos de tempo de execução [UdfCpuTime e UdfElapsedTime](https://blogs.msdn.microsoft.com/sql_server_team/more-showplan-enhancements-udfs/) na execução real do XML, para controlar o tempo gasto em UDFs (Funções Definidas pelo Usuário) escalares.| |
| |Adicionar o tipo de espera CXPACKET à [lista das 10 principais esperas possíveis](https://blogs.msdn.microsoft.com/sql_server_team/new-showplan-enhancements/) na execução real do XML – a execução paralela da consulta com frequência envolve esperas CXPACKET, mas esse tipo de espera não foi relatado na execução real do XML. |       |
| |O aviso de despejo do tempo de execução foi estendido para relatar o número de páginas escritas para TempDB durante o despejo de um operador de paralelismo.| |
|Compatibilidade da replicação com bancos de dados com ordenações de caracteres Suplementares  |   Agora, a replicação é compatível com bancos de dados que usam ordenações de caracteres Suplementares. |       |
|Manipulação adequada do Service Broker com o failover do grupo de disponibilidade |   Na implementação atual, quando o Service Broker é habilitado em um banco de dados do grupo de disponibilidade, durante um failover do grupo de disponibilidade, todas as conexões do Service Broker originadas na Réplica Primária são deixadas abertas. A melhoria fecha todas essas conexões abertas durante um failover do grupo de disponibilidade. |       |
|Melhoria na solução de problemas das esperas de paralelismo |   com a adição de uma nova espera [CXCONSUMER](https://blogs.msdn.microsoft.com/sql_server_team/making-parallelism-waits-actionable/).   |       |
|Maior consistência entre DMVs para as mesmas informações |   Agora, o DMV sys.dm_exec_session_wait_stats controla as esperas CXPACKET e CXCONSUMER de acordo com a DMV sys.dm_os_wait_stats. |       |
|Melhoria na solução de problemas de deadlocks de paralelismo intraconsulta | Um novo Evento Estendido exchange_spill gerará um relatório com o número de páginas escritas para TempDB durante o despejo de um operador de paralelismo, no nome do campo worktable_physical_writes do xEvent.| |
| |Agora, as colunas de despejo nos DMVs dm_exec_query_stats, sys.dm_exec_procedure_stats e sys.dm_exec_trigger_stats (como total_spills) também incluem os dados despejados pelos operadores de paralelismo.| |
| |O grafo deadlock XML foi aprimorado para cenários de deadlock de paralelismo, com a adição de atributos ao recurso exchangeEvent.| |
| |O grafo deadlock XML foi aprimorado para deadlocks que envolvem operadores em modo de lote, com a adição de atributos ao recurso SyncPoint.| |
|Recarregamento dinâmico de alguns parâmetros de perfil de agente de replicação |   Na implementação atual dos agentes de replicação, qualquer alteração no parâmetro de perfil de agente requer o agente seja interrompido e reiniciado. Esta melhoria permite que os parâmetros sejam recarregados dinamicamente sem a necessidade de reiniciar o agente de replicação.   |       |

![horizontal-bar.png](media/horizontal-bar.png)

## <a name="bkmk_2016sp1"></a>SQL Server 2016 Service Pack 1 (SP1)
![info_tip](../sql-server/media/info-tip.png) O SQL Server 2016 SP1 inclui todas as atualizações cumulativas até o SQL Server 2016 RTM CU3, incluindo a Atualização de Segurança MS16-136. Ele contém um rollup de soluções fornecidas nas atualizações cumulativas do SQL Server 2016 até, e incluindo, a atualização cumulativa mais recente, CU3, e a Atualização de Segurança MS16-136 lançada em 8 de novembro de 2016.

Os seguintes recursos estão disponíveis nas edições Standard, Web, Express e Local DB do SQL Server SP1 (salvo indicação em contrário):
- Always encrypted
- Captura de dados alterados (não disponível no Express)
- columnstore
- Compactação
- Mascaramento de dados dinâmicos
- Auditoria refinada
- OLTP in-memory (não disponível no Local DB)
- Vários contêineres de fluxo de arquivos (não disponíveis no banco de dados Local)
- Particionamento
- PolyBase
- Segurança em nível de linha

A tabela a seguir resume as principais melhorias fornecidas no SQL Server 2016 SP1.

|Recurso|Descrição|Mais informações|
|---|---|---|
|Inserção em massa em heaps com TABLOCK automático em TF 715| O Sinalizador de Rastreamento 715 habilita o bloqueio de tabela para operações de carregamento em massa em um heap sem índices não clusterizados.|[Migrar cargas de trabalho do SAP para o SQL Server ficou 2,5 x mais rápido](https://blogs.msdn.microsoft.com/sql_server_team/migrating-sap-workloads-to-sql-server-just-got-2-5x-faster/)|
|CREATE OR ALTER|Implante objetos, como procedimentos armazenados, disparadores, funções definidas pelo usuário e modos de exibição.|[Blog do Mecanismo de Banco de Dados do SQL Server](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/11/17/create-or-alter-another-great-language-enhancement-in-sql-server-2016-sp1/)|
|Suporte a DROP TABLE para replicação|Suporte a DROP TABLE DDL para replicação a fim de permitir que os artigos de replicação sejam removidos.|[KB 3170123](https://support.microsoft.com/help/3170123/supports-drop-table-ddl-for-articles-that-are-included-in-transactiona)|
|Assinatura do driver Filestream RsFx|O driver Filestream RsFx é assinado e certificado usando o portal do Painel da Central do Desenvolvedor para Hardware do Windows (Portal de desenvolvimento) permitindo que o driver do Filestream RsFx para SQL Server 2016 SP1 seja instalado no Windows Server 2016/Windows 10 sem nenhum problema.|[Migrar cargas de trabalho do SAP para o SQL Server ficou 2,5 x mais rápido](https://blogs.msdn.microsoft.com/sql_server_team/migrating-sap-workloads-to-sql-server-just-got-2-5x-faster/)|
|LPIM para conta de serviço do SQL – identificação programática|Permite que os DBAs identifiquem programaticamente se o privilégio de LPIM (Bloquear páginas na memória) está em vigor no momento da inicialização do serviço.|[Developers Choice: identificar programaticamente privilégios LPIM e IFI no SQL Server](https://blogs.msdn.microsoft.com/sql_server_team/developers-choice-programmatically-identify-lpim-and-ifi-privileges-in-sql-server)|
|Limpeza do controle de alterações manual|O novo procedimento armazenado limpa a tabela interna de controle de alterações sob demanda.| [KB 3173157](https://support.microsoft.com/help/3173157/adds-a-stored-procedure-for-the-manual-cleanup-of-the-change-tracking)|
|Alterações do INSERT..SELECT paralelo para tabelas temporárias locais|Novo INSERT paralelo em operações INSERT..SELECT.|[Equipe de consultoria do cliente do SQL Server](https://blogs.msdn.microsoft.com/sqlcat/2016/07/21/real-world-parallel-insert-what-else-you-need-to-know/)|
|Showplan XML|Diagnóstico estendido, incluindo o aviso de concessão e memória máxima habilitada para uma consulta, sinalizadores de rastreamento habilitados e também resulta em outras informações de diagnóstico. | [KB 3190761](https://support.microsoft.com/help/3190761/update-to-improve-diagnostics-by-expose-data-type-of-the-parameters-fo)|
|Memória de classe de armazenamento|Aumente o processamento de transações usando a memória de classe de armazenamento no Windows Server 2016, resultando na capacidade de acelerar as horas de confirmação de transação por ordem de grandeza.|[Blog do Mecanismo de Banco de Dados do SQL Server](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/12/02/transaction-commit-latency-acceleration-using-storage-class-memory-in-windows-server-2016sql-server-2016-sp1/)|
|USE HINT|Use a opção de consulta `OPTION(USE HINT('<option>'))` para alterar o comportamento do otimizador de consultas usando dicas de nível de consulta compatíveis. Diferentemente do QUERYTRACEON, a opção USE HINT não requer privilégios de administrador do sistema.|[Developers Choice: Dicas de consulta USE HINT](https://blogs.msdn.microsoft.com/sql_server_team/developers-choice-use-hint-query-hints/)|
|Adições de XEvent|Novos recursos de diagnóstico de XEvents e Perfmon melhoram a solução de problemas de latência.|[Eventos estendidos](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events)|

Além disso, observe as seguintes correções:
- Com base nos comentários da comunidade do SQL e de DBAs, a partir do SQL 2016 SP1, as mensagens de registro em log do Hekaton são reduzidas ao mínimo.
- Veja os novos [sinalizadores de rastreamento](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql).
- As versões completas dos bancos de dados de exemplo WideWorldImporters agora funcionam com a Standard Edition e a Express Edition, a partir do SQL Server 2016 SP1, e estão disponíveis no [Github]( https://github.com/Microsoft/sql-server-samples/releases/tag/wide-world-importers-v1.0). Nenhuma alteração é necessária no exemplo. Os backups de banco de dados criados no RTM para o trabalho do Enterprise edition com Standard e Express no SP1.

A instalação do SQL Server 2016 SP1 pode exigir a reinicialização após a instalação. Como prática recomendada, é melhor planejar e executar uma reinicialização após a instalação do SQL Server 2016 SP1.

### <a name="download-pages-and-more-information"></a>Páginas de download e mais informações

- [Baixar o Service Pack 1 para Microsoft SQL Server 2016](https://www.microsoft.com/download/details.aspx?id=54276)
- [SQL Server 2016 Service Pack 1 (SP1) lançado](https://blogs.msdn.microsoft.com/sqlreleaseservices/sql-server-2016-service-pack-1-sp1-released/)
- [Informações de versão do SQL Server 2016 Service Pack 1](https://support.microsoft.com/kb/3182545)
- ![info_tip](../sql-server/media/info-tip.png) Visite o [Centro de Atualização do SQL Server](https://msdn.microsoft.com/library/ff803383.aspx) para obter links e informações para todas as versões compatíveis, incluindo service packs do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)]

![horizontal-bar.png](media/horizontal-bar.png)

##  <a name="bkmk_2016_ga"></a> SQL Server 2016 Release - General Availability (GA)
-   [Mecanismo de Banco de Dados (GA)](#bkmk_ga_instalpatch)
-   [Stretch Database (GA)](#bkmk_ga_stretch)
-   [Repositório de Consultas (GA)](#bkmk_ga_query_store)
-   [Documentação do produto (GA)](#bkmk_ga_docs)

### ![repl_icon_warn](../database-engine/availability-groups/windows/media/repl-icon-warn.gif) <a name="bkmk_ga_instalpatch"></a> Install Patch Requirement (GA)
**Problema e impacto ao cliente:** a Microsoft identificou um problema que afeta os binários do Tempo de Execução Microsoft VC++ 2013 que são instalados como um pré-requisito pelo SQL Server 2016. Uma atualização está disponível para correção deste problema. Se essa atualização para os binários do Tempo de Execução de VC não for instalada, o SQL Server 2016 poderá apresentar problemas de estabilidade em determinados cenários. Antes de instalar o SQL Server 2016, verifique se o computador precisa do patch descrito em [KB 3164398](https://support.microsoft.com/kb/3164398). O patch também é incluído no [CU1 (Pacote de Atualização Cumulativa 1) para o SQL Server 2016 RTM](https://www.microsoft.com/download/details.aspx?id=53338).

**Resolução:** use uma das seguintes soluções:

- Instale a [KB 3138367 – Atualização para o Visual C++ 2013 e o Pacote Redistribuível do Visual C++](https://support.microsoft.com/kb/3138367). A KB é a resolução preferencial. Você pode instalá-la antes ou depois de instalar o SQL Server 2016.

    Se o SQL Server 2016 já estiver instalado, siga as seguintes etapas na ordem:

    1.  Baixe o *vcredist_\*exe* apropriado.
    1.  Interrompa todas as instâncias do mecanismo de banco de dados no serviço do SQL Server.
    1.  Instale a **KB 3138367**.
    1.  Reinicialize o computador.


 - Instalar a  [KB 3164398 – Atualização crítica para os pré-requisitos MSVCRT do SQL Server 2016](https://support.microsoft.com/kb/3164398).

    Se você usar a **KB 3164398**, é possível instalá-la durante a instalação do SQL Server, por meio do Microsoft Update ou no Centro de Download da Microsoft.

    - **Durante a instalação do SQL Server 2016:** se o computador que está executando a instalação do SQL Server tiver acesso à Internet, a instalação do SQL Server verificará a atualização como parte da instalação geral do SQL Server. Se você aceitar a atualização, a instalação baixará e atualizará os binários durante a instalação.

    - **Microsoft Update:** a atualização está disponível no Microsoft Update como uma atualização crítica não relacionada à segurança do SQL Server 2016. A instalação por meio do Microsoft Update, após o SQL Server 2016, exige a reinicialização do servidor após a atualização.

    - **Centro de Download:** finalmente, a atualização está disponível no Centro de Download da Microsoft. Você pode baixar o software da atualização e instalá-lo nos servidores depois que tiverem o SQL Server 2016.


### <a name="bkmk_ga_stretch"></a>Stretch Database

#### <a name="problem-with-a-specific-character-in-a-database-or-table-name"></a>Problema com um caractere específico em um nome de banco de dados ou de tabela

**Problema e impacto ao cliente:** a tentativa de habilitar o Stretch Database em um banco de dados ou uma tabela falha com um erro. O problema ocorre quando o nome do objeto inclui um caractere que é tratado como um caractere diferente quando convertido de letras minúsculas em maiúsculas. Um exemplo de um caractere que causa esse problema é o caractere “ƒ” (criado ao digitar ALT+159).

**Solução alternativa:** se você deseja habilitar o Stretch Database no banco de dados ou na tabela, a única opção é renomear o objeto e remover o caractere problemático.

#### <a name="problem-with-an-index-that-uses-the-include-keyword"></a>Problema com um índice que usa a palavra-chave INCLUDE

**Problema e impacto ao cliente:** a tentativa de habilitar o Stretch Database em uma tabela que contém um índice que usa a palavra-chave INCLUDE para incluir colunas adicionais no índice falha com um erro.

**Solução alternativa:** remova o índice que usa a palavra-chave INCLUDE, habilite o Stretch Database na tabela e recrie o índice. Se você fizer isso, lembre-se de seguir as práticas e políticas de manutenção de sua organização para garantir um impacto mínimo ou nenhum impacto sobre os usuários da tabela afetada.

### <a name="bkmk_ga_query_store"></a>Query Store

#### <a name="problem-with-automatic-data-cleanup-on-editions-other-than-enterprise-and-developer"></a>Problema com a limpeza automática de dados em edições que não sejam Enterprise e Developer

 **Problema e impacto ao cliente:** a limpeza automática de dados falha em edições que não sejam Enterprise e Developer.
Consequentemente, se os dados não forem limpos manualmente o espaço usado pelo Repositório de Consultas aumentará ao longo do tempo até que seja atingido o limite configurado. Se não for atenuado, esse problema também preencherá o espaço em disco alocado para os logs de erros, pois cada tentativa de executar a limpeza produzirá um arquivo de despejo. O período de ativação da limpeza depende da frequência da carga de trabalho, não sendo mais longo do que 15 minutos.

 **Solução alternativa:** se você planeja usar o Repositório de Consultas em edições que não sejam o Enterprise e o Developer, deve desligar explicitamente as políticas de limpeza. Faça isto no SQL Server Management Studio (página Propriedades do banco de dados) ou por meio do script Transact-SQL:

```ALTER DATABASE <database name> SET QUERY_STORE (OPERATION_MODE = READ_WRITE, CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 0), SIZE_BASED_CLEANUP_MODE = OFF)```

Além disso, considere as opções de limpeza manual para impedir que o Repositório de Consultas faça a transição para o modo somente leitura. Por exemplo, execute a seguinte consulta para limpar periodicamente o espaço inteiro de dados:

```ALTER DATABASE <database name> SET QUERY_STORE CLEAR```

Além disso, execute os seguintes procedimentos armazenados do Repositório de Consultas periodicamente para limpar estatísticas de tempo de execução, consultas ou planos específicos:

- `sp_query_store_reset_exec_stats`

- `sp_query_store_remove_plan`

- `sp_query_store_remove_query`


###  <a name="bkmk_ga_docs"></a> Documentação do produto (GA)
 **Problema e impacto ao cliente:** Uma versão para download da documentação do SQL Server 2016 ainda não está disponível. Quando você usa o Gerenciador da Biblioteca da Ajuda para tentar **Instalar o conteúdo online**, a documentação do SQL Server 2012 e do SQL Server 2014 é exibida, mas não existem opções para a documentação do SQL Server 2016.

 **Solução alternativa:** use uma das seguintes soluções alternativas:

 ![Gerenciar configurações da ajuda do SQL Server](../sql-server/media/docs-sql2016-managehelpsettings.png "Gerenciar configurações da ajuda do SQL Server")

-   Use a opção **Escolher ajuda online ou local** e configure a Ajuda para "Eu quero usar a ajuda online".

-   Use a opção **Instalar conteúdo online** e baixe o conteúdo do SQL Server 2014.

 **Ajuda F1:** por design, quando você pressiona F1 no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], a versão online do artigo da Ajuda F1 é exibida no navegador. O problema está na ajuda baseada em navegador, mesmo quando você configurou e instalou a Ajuda local.

**Atualização do conteúdo:** No SQL Server Management Studio e no Visual Studio, o aplicativo Help Viewer poderá congelar (parar de responder) durante o processo de adição da documentação. Para resolver esse problema, conclua as etapas a seguir. Para obter mais informações sobre esse problema, confira [O Visual Studio Help Viewer congela](https://msdn.microsoft.com/library/mt654096.aspx).

* Abra o arquivo %LOCALAPPDATA%\Microsoft\HelpViewer2.2\HlpViewer_SSMS16_en-US.settings | HlpViewer_VisualStudio14_en-US.settings no Bloco de Notas e altere a data no código a seguir para alguma data no futuro.

```
     Cache LastRefreshed="12/31/2017 00:00:00"
```

## <a name="additional-information"></a>Informações adicionais
+ [Instalação do SQL Server 2016](../database-engine/install-windows/installation-for-sql-server-2016.md)
+ [Centro de atualização do SQL Server – links e informações para todas as versões com suporte](https://msdn.microsoft.com/library/ff803383.aspx)

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png "MS_Logo_X-Small")

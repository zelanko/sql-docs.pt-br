---
title: O que&#39;novo no SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/25/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- database-engine
- integration-services
- master-data-services
- replication
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- new features [SQL Server]
- SQL Server, what's new
- SQL Server 2008 what's new
- what's new [SQL Server]
- sql server 2014 sp1
- sql server 2014 sp2
ms.assetid: 6a428023-e3cc-4626-a88a-4c13ccbd7db0
caps.latest.revision: 70
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 9144eeb653649e36cfed3551e4ec465d403ffdcb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010136"
---
# <a name="what39s-new-in-sql-server-2014"></a>O que&#39;novo no SQL Server 2014
  Este tópico resume os links detalhadas aos novos recursos no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] e resume os pacotes de serviços para [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**Experimente:** ![pequeno de máquina Virtual do Azure](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png) tem uma conta do Azure?  Em seguida, acesse **[aqui](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2)** para girar uma máquina Virtual com o SQL Server 2014 Service Pack 1 (SP1) já está instalado. 
  
-   [O que há de novo &#40;mecanismo de banco de dados&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [Novidades no Analysis Services e Business Intelligence](../analysis-services/what-s-new-in-analysis-services.md)  
  
-   [Novidades na instalação do SQL Server](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] não incorporou novos recursos significativos para o seguinte:**  
  
-   [O que há de novo &#40;do Integration Services&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [O que há de novo &#40;replicação&#41;](../relational-databases/replication/what-s-new-replication.md)  
  
-   [O que há de novo &#40;Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="includesssql14includessssql14-mdmd-service-pack-1-sp1"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 1 (SP1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] (SP1) não introduziu novos recursos significativos.
-  [Informações de versão do SQL Server 2014 Service Pack 1 ](https://support.microsoft.com/en-us/kb/3058865).
-  [![Baixe o Service Pack 1 para Microsoft® SQL Server® 2014](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=46694) [baixar o Service Pack 1 para Microsoft® SQL Server® 2014](https://www.microsoft.com/en-us/download/details.aspx?id=46694).


## <a name="includesssql14includessssql14-mdmd-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 2 (SP2)
- [Informações de versão do SQL Server 2014 Service Pack 2](https://support.microsoft.com/en-us/kb/3171021).
-  [![Baixe o Service Pack 2 para Microsoft® SQL Server® 2014](./media/what-s-new-in-sql-server-2016/download.png)](http://go.microsoft.com/fwlink/?LinkID=821558) [baixar o Service Pack 2 para Microsoft® SQL Server® 2014](http://go.microsoft.com/fwlink/?LinkID=821558).
-  [![Baixar o SQL Server 2014 SP2 Feature Pack](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=53164) [baixar o SQL Server 2014 SP2 Feature Pack](https://www.microsoft.com/en-us/download/details.aspx?id=53164).

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] (SP2) Inclui os seguintes aprimoramentos:

### <a name="performance-and-scalability-improvements"></a>Melhorias de desempenho e escalabilidade 
-   **O particionamento automático de NUMA temporário:** com [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2, NUMA temporário automática é habilitada quando 8079 do sinalizador de rastreamento é ativado durante a inicialização de instância. Quando 8079 do sinalizador de rastreamento é habilitado durante a inicialização, [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 será interrogar o layout de hardware e configurar automaticamente o NUMA temporário em sistemas reporting 8 ou mais CPUs por nó NUMA. O comportamento NUMA automático, flexível é Hyperthread (processador HT/lógico) com suporte. O particionamento e a criação de nós adicionais dimensiona o processamento em segundo plano aumentando o número de ouvintes, o dimensionamento e os recursos de rede e de criptografia. É recomendável primeiro teste de carga de trabalho de desempenho com automática Soft NUMA antes de ativá-lo em produção. [Consulte o Blog para obter mais informações](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/). 
-  **Dimensionamento dinâmico do objeto de memória:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 partições dinamicamente com base no número de nós e a escala em hardware moderno de núcleos de objetos de memória. O objetivo da promoção dinâmico é particionar automaticamente um objeto de thread seguro de memória (CMEMTHREAD) se torna um afunilamento. Objetos de memória não particionado podem ser promovidos para ser particionado por nó (número de número de é igual a partições de nós NUMA) dinamicamente e memória podem objetos particionados por nó por mais promovido para ser particionado por CPU (número de partições é igual a inúmeros CPUs). [Consulte o blog para obter mais informações](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/).
-  **Dica MAXDOP para DBCC CHECK\* comandos:** essa melhoria endereços [conectar comentários (468694)](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb). Agora você pode executar o DBCC CHECKDB com a uma configuração de MAXDOP diferente do valor sp_configure. Se MAXDOP exceder o valor configurado com o Resource Governor, o Mecanismo de Banco de Dados usará o valor de MAXDOP do Resource Governor, descrito em ALTER WORKLOAD GROUP (Transact-SQL). Todas as regras semânticas usadas com a opção de configuração grau máximo de paralelismo são aplicáveis ao usar a dica de consulta MAXDOP. Para obter mais informações, consulte [DBCC CHECKDB (Transact-SQL)](https://msdn.microsoft.com/library/ms176064.aspx).
-   **Habilitar > 8TB para Pool de buffers:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 habilita 128 TB de espaço de endereço virtual para uso do pool de buffer. Esse aprimoramento permite que o Pool de buffers do SQL Server dimensionar mais de 8TB em hardware moderno.
-   **SOS_RWLock spinlock aperfeiçoamento:** SOS_RWLock o é um primitivo de sincronização usado em vários locais em toda a base de código do SQL Server.  Como o nome implica, o código pode ter vários compartilhados (leitores) ou a propriedade de único (writer). Essa melhoria elimina a necessidade de spinlock para SOS_RWLock e usa técnicas sem bloqueio semelhantes para OLTP na memória. Com essa alteração, muitos threads podem ler uma estrutura de dados protegida por SOS_RWLock em paralelo sem bloqueio entre si e fornecendo maior escalabilidade. Antes desta alteração, a implementação de spinlock permitido apenas um thread adquirir o SOS_RWLock por vez, até mesmo para uma estrutura de dados de leitura.  [Consulte o blog para obter mais informações](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/).
-    **Implementação nativa espacial:** aprimoramento significativo no desempenho de consulta espacial é introduzido no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 por meio da implementação nativa. Para obter mais informações, consulte o [artigo da base de dados de Conhecimento KB3107399](https://support.microsoft.com/en-us/kb/3107399).

### <a name="supportability-and-diagnostics-improvements"></a>Capacidade de suporte e melhorias de diagnóstico
-   **Clonagem de banco de dados:** banco de dados do Clone é um novo comando DBCC que aprimora os bancos de dados de produção existente de solução de problemas por meio da clonagem o esquema e os metadados sem os dados. O clone é criado com o comando `DBCC clonedatabase(‘source_database_name’, ‘clone_database_name’)`.  **Observação:** duplicação bancos de dados não devem ser usados em ambientes de produção. Use o comando a seguir determinam se um banco de dados foi gerado a partir de um banco de dados clonado: `select DATABASEPROPERTYEX('clonedb', 'isClone')`. O valor de retorno **1** indica que o banco de dados é criado a partir clonedatabase ao **0** indica que não é um clone.
-   **Suporte de tempdb:** uma nova mensagem de log de erros que indica o número de arquivos tempdb e o tamanho/aumento automático de dados tempdb arquivos presente na inicialização do servidor.
-   **Banco de dados instantânea log de inicialização do arquivo:** uma nova mensagem de log de erros indica no servidor statup, o status de inicialização imediata de arquivo do banco de dados (ativado/desativado).
-   **Nomes de módulo na pilha de chamadas:** Xevent a pilha de chamadas agora inclui os nomes de módulos + deslocamento, em vez de endereços absolutos.
-   **Novo DMF para estatísticas incrementais:** essa melhoria endereços [conectar comentários (797156)](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics) para habilitar o controle as estatísticas incrementais no nível da partição. Um novo sys.dm_db_incremental_stats_properties DMF é introduzido para expor informações por partição para as estatísticas incrementais.
-   **Comportamento de DMV do uso de índice atualizado:** essa melhoria endereços [conectar comentários (739566)](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats) de clientes onde recriar um índice será *não* limpar qualquer entrada existente de linha de sys.dm_db _index_usage_stats para que o índice. O comportamento agora será o mesmo do SQL 2008 e SQL Server 2016. [Consulte o blog para obter mais informações](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/).
-   **Melhor a correlação entre DMVs e diagnóstico XE:** essa melhoria endereços [conectar comentários (1934583)](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types). Query_hash e query_plan_hash são usados para identificar uma consulta com exclusividade. O DMV define-os como varbinary(8), enquanto XEvent define-os como UINT64. Como do SQL server não tem "unisigned bigint", conversão nem sempre funcionam. Essa melhoria introduz novas colunas de filtro/ação XEvent equivalentes a query_hash e a query_plan_hash, exceto que elas estão definidas como INT64, o que podem ajudar a correlacionar consultas entre XE e DMVs.
-   **Suporte para UTF-8 em BULK INSERT e BCP:** essa melhoria endereços [conectar comentários (370419)](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001) onde suporte para exportação e importação de dados codificados no conjunto de caracteres UTF-8 agora está habilitado na inserção em MASSA e BCP.
-   **Perfis de execução de consulta do operador de leve:** ao solucionar problemas do desempenho de consulta, embora o plano de execução fornece muitas informações sobre o plano de execução de consulta e o custo do operador no plano mas ele limitou a obter informações sobre real estatísticas de tempo de execução como (CPU, leituras de e/s, tempo decorrido por thread). SQL 2014 SP2 apresenta essas estatísticas de tempo de execução adicional por operador no plano de execução, bem como um XEvent (query_thread_profile) para ajudar a solucionar problemas de desempenho de consulta. [Consulte o blog para obter mais informações](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/).
-   **Limpeza do controle de alteração:** um novo procedimento armazenado `sp_flush_CT_internal_table_on_demand` é introduzida em tabelas internas de alterações de limpeza sob demanda.
-   **Log de tempo limite de concessão de AlwaysON** adicionado novo recurso de log de mensagens de tempo limite de concessão para que a hora atual e os tempos de renovação esperados são registrados. Também uma nova mensagem foi introduzida no SQL Errorlog sobre os tempo limite. [Consulte o blog para obter mais informações](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/).
-   **Entrada de DMF nova para recuperação de buffer no SQL Server:** um novo DMF para recuperar o buffer de entrada para uma sessão/solicitação (sys.DM exec_input_buffer) agora está disponível. Isso é funcionalmente equivalente ao DBCC INPUTBUFFER. [Consulte o blog para obter mais informações](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/).
-   **Mitigação de concessão de memória subestimada e supervalorizado:** adicionadas novas dicas de consulta para o administrador de recursos por meio de MIN_GRANT_PERCENT e MAX_GRANT_PERCENT. Isso permite aproveitar essas dicas durante a execução de consultas limitando suas concessões de memória para evitar contenção de memória. Para obter mais informações, consulte [artigo da base de dados de Conhecimento KB310740](https://support.microsoft.com/en-us/kb/3107401)
-   **Melhor diagnóstico grant/uso de memória:** um novo evento estendido foi adicionado à lista de recursos de rastreamento do SQL Server (query_memory_grant_usage) para rastrear concessões de memória solicitada e concedida. Isso fornece melhores recursos de análise e de rastreamento para solucionar problemas de execução de consulta relacionados para concessões de memória. Para obter mais informações, consulte [artigo da base de dados de Conhecimento KB3107173](https://support.microsoft.com/en-us/kb/3107173).
-   **Diagnóstico de execução para tempdb derramamento de consulta:**-aviso de Hash e avisos de classificação agora tem colunas adicionais para controlar estatísticas de e/s física, memória usada e linhas afetadas. Também apresentamos um novo evento estendido de hash_spill_details. Agora você pode controlar as informações mais detalhadas para avisos de hash e de classificação ([KB3107172](https://support.microsoft.com/en-us/kb/3107172)). Esse aprimoramento também agora é exposto através de planos de consulta XML na forma de um novo atributo para o tipo complexo de SpillToTempDbType ([KB3107400](https://support.microsoft.com/en-us/kb/3107400)). Definir as estatísticas em agora mostra estatísticas de tabela de trabalho de classificação. para obter informações sobre a ferramenta de configuração e recursos adicionais.
-   **Diagnósticos para planos de execução de consulta que envolve a aplicação de predicado residual aprimorados:** reais linhas lidas agora serão relatadas nos planos de execução de consulta para ajudar a melhorar a solução de problemas de desempenho de consulta. Isso deve negar a necessidade de capturar SET STATISTICS IO separadamente. Agora permite que você veja informações relacionadas a uma aplicação de predicado residual em um plano de consulta. Para obter mais informações, consulte [artigo da base de dados de Conhecimento KB3107397](https://support.microsoft.com/en-us/kb/3107397).


## <a name="additional-information"></a>Informações adicionais  
 [Recursos do SQL Server 2014](../2014-toc/books-online-for-sql-server-2014.md)  
  
 [SQL Server 2014 Release Notes](http://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [Central de recursos do SQL Server 2014](http://msdn.microsoft.com/sqlserver/dn135309)  
  
 [Site do SQLCat](http://go.microsoft.com/fwlink/p/?linkID=220963)  
  
  
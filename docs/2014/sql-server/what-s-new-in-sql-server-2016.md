---
title: O que&#39;s do SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/25/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- new features [SQL Server]
- SQL Server, what's new
- SQL Server 2008 what's new
- what's new [SQL Server]
- sql server 2014 sp1
- sql server 2014 sp2
ms.assetid: 6a428023-e3cc-4626-a88a-4c13ccbd7db0
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 26d0c84194f6f2aafb8bc499ff5404a1438ee577
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63295236"
---
# <a name="what39s-new-in-sql-server-2014"></a>O que&#39;s do SQL Server 2014
  Este tópico resume os links detalhadas aos novos recursos do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] e resume os pacotes de serviços para [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**Experimente:** ![Máquina Virtual pequena do Azure](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png) tiver uma conta do Azure?  Em seguida, acesse **[aqui](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2)** para criar uma máquina Virtual com o SQL Server 2014 Service Pack 1 (SP1) já instalado. 
  
-   [O que há de novo &#40;mecanismo de banco de dados&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [O que há de novo no Analysis Services e Business Intelligence](../analysis-services/what-s-new-in-analysis-services.md)  
  
-   [Novidades na instalação do SQL Server](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] não incorporou novos recursos significativos para o seguinte:**  
  
-   [O que há de novo &#40;Integration Services&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [O que há de novo &#40;Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="includesssql14includessssql14-mdmd-service-pack-1-sp1"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 1 (SP1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] (SP1) não introduziu novos recursos significativos.
-  [Informações de versão do SQL Server 2014 Service Pack 1](https://support.microsoft.com/en-us/kb/3058865).
-  [![Baixe o Service Pack 1 para a Microsoft?? SQL Server?? 2014](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=46694) [Baixe o Service Pack 1 para a Microsoft?? SQL Server?? 2014](https://www.microsoft.com/en-us/download/details.aspx?id=46694).


## <a name="includesssql14includessssql14-mdmd-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 2 (SP2)
- [Informações de versão do SQL Server 2014 Service Pack 2](https://support.microsoft.com/en-us/kb/3171021).
-  [![Baixe o Service Pack 2 para a Microsoft?? SQL Server?? 2014](./media/what-s-new-in-sql-server-2016/download.png)](https://go.microsoft.com/fwlink/?LinkID=821558) [Baixe o Service Pack 2 para a Microsoft?? SQL Server?? 2014](https://go.microsoft.com/fwlink/?LinkID=821558).
-  [![Baixar o SQL Server 2014 SP2 Feature Pack](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=53164) [baixar o SQL Server 2014 SP2 Feature Pack](https://www.microsoft.com/en-us/download/details.aspx?id=53164).

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] (SP2) Inclui os seguintes aprimoramentos:

### <a name="performance-and-scalability-improvements"></a>Melhorias no desempenho e escalabilidade 
-   **Particionamento de Soft-NUMA automático:** Com [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2, o Soft-NUMA automático está habilitado quando o sinalizador de rastreamento 8079 é ativado durante a inicialização de instância. Quando o sinalizador de rastreamento 8079 é habilitado durante a inicialização, [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 interrogue o layout de hardware e o configurar automaticamente o Soft-em sistemas que estejam relatando 8 ou mais CPUs por nó NUMA. O comportamento NUMA automático, reversível é Hyperthread (HT/processador lógico) com suporte. O particionamento e a criação de nós adicionais dimensiona o processamento em segundo plano aumentando o número de ouvintes, o dimensionamento e os recursos de rede e de criptografia. É recomendável testar primeiro a carga de trabalho de desempenho com o Soft-NUMA automático antes de ativá-lo em produção. [Consulte o Blog para obter mais informações](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/). 
-  **Dimensionamento do objeto de memória dinâmica:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 particiona dinamicamente a memória para objetos com base no número de nós e núcleos a serem dimensionados no hardware moderno. A meta da promoção dinâmica é particionar automaticamente um objeto de thread-safe de memória (CMEMTHREAD) se ele se tornar um gargalo. Objetos de memória não particionado podem ser promovidos dinamicamente para serem particionados por nó (número de número de equals partições de nós NUMA), e podem objetos particionados por nó por mais de memória é promovido para ser particionado por CPU (número de partições é igual a inúmeros CPUs). [Consulte o blog para obter mais informações](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/).
-  **Dica MAXDOP para DBCC CHECK\* comandos:** Essa melhoria aborda [conectar-se comentários (468694)](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb). Agora você pode executar o DBCC CHECKDB com a uma configuração de MAXDOP diferente do valor sp_configure. Se MAXDOP exceder o valor configurado com o Resource Governor, o Mecanismo de Banco de Dados usará o valor de MAXDOP do Resource Governor, descrito em ALTER WORKLOAD GROUP (Transact-SQL). Todas as regras semânticas usadas com a opção de configuração grau máximo de paralelismo são aplicáveis ao usar a dica de consulta MAXDOP. Para obter mais informações, consulte [DBCC CHECKDB (Transact-SQL)](https://msdn.microsoft.com/library/ms176064.aspx).
-   **Habilitar > 8TB para o Pool de buffers:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 permite 128TB de espaço de endereço virtual para uso do pool de buffer. Essa melhoria permite que o Pool de buffers do SQL Server dimensionar mais de 8TB no hardware moderno.
-   **Spinlock do SOS_RWLock melhoria:** O SOS_RWLock é um primitivo de sincronização usado em vários locais em toda a base de código do SQL Server.  Como o nome implica, o código pode ter vários compartilhados (os leitores) ou a propriedade de única (gravador). Essa melhoria elimina a necessidade de spinlock para SOS_RWLock e usa técnicas sem bloqueio semelhantes ao OLTP na memória. Com essa alteração, muitos threads podem ler uma estrutura de dados protegida por SOS_RWLock em paralelo sem bloqueio uns aos outros e fornecendo assim maior escalabilidade. Antes dessa mudança, a implementação de spinlock permitido apenas um thread adquirir o SOS_RWLock por vez, até mesmo para uma estrutura de dados de leitura.  [Consulte o blog para obter mais informações](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/).
-    **Implementação nativa espacial:** Uma melhoria significativa no desempenho de consulta espacial é introduzida no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 por meio da implementação nativa. Para obter mais informações, consulte o [artigo da base de dados de Conhecimento KB3107399](https://support.microsoft.com/en-us/kb/3107399).

### <a name="supportability-and-diagnostics-improvements"></a>Capacidade de suporte e melhorias de diagnóstico
-   **Clonagem de banco de dados:** Banco de dados do clone é um novo comando DBCC que aprimora a solução de problemas de bancos de dados de produção existentes por meio da clonagem do esquema e os metadados sem os dados. O clone é criado com o comando `DBCC clonedatabase('source_database_name', 'clone_database_name')`.  **Observação:** Os bancos de dados clonados não devem ser usados em ambientes de produção. Use o comando a seguir determinam se um banco de dados foi gerado de um banco de dados clonado: `select DATABASEPROPERTYEX('clonedb', 'isClone')`. O valor de retorno **1** indica que o banco de dados é criado a partir clonedatabase enquanto **0** indica que não é um clone.
-   **Suporte de tempdb:**  Uma nova mensagem de log de erros que indica o número de arquivos tempdb e o tamanho/aumento automático de arquivos de dados do tempdb presentes na inicialização do servidor.
-   **Log de inicialização do banco de dados instantânea de arquivo:** Uma nova mensagem de log de erros que indica em statup do servidor, o status da inicialização instantânea de arquivo do banco de dados (habilitado/desabilitado).
-   **Nomes de módulo na pilha de chamadas:** Agora, a pilha de chamadas Xevent inclui nomes de módulos + deslocamento, em vez de endereços absolutos.
-   **Novo DMF para estatísticas incrementais:** Essa melhoria aborda [conectar-se comentários (797156)](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics) para habilitar as estatísticas incrementais no nível da partição de controle. Um novo DM db_incremental_stats_properties do DMF é introduzida para expor informações por partição para estatísticas incrementais.
-   **Comportamento de DMV do uso de índice atualizado:** Essa melhoria aborda [(739566) de comentários sobre a conexão](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats) de clientes onde a recriação de um índice será *não* limpar qualquer entrada de linha existente do DM db_index_usage_stats para aquele índice. O comportamento agora será o mesmo do SQL 2008 e SQL Server 2016. [Consulte o blog para obter mais informações](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/).
-   **Aprimorada a correlação entre XE e DMVs:** Essa melhoria aborda [conectar-se comentários (1934583)](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types). Query_hash e query_plan_hash são usados para identificar uma consulta com exclusividade. O DMV define-os como varbinary(8), enquanto XEvent define-os como UINT64. Como o SQL server tem "bigint unisigned", conversão nem sempre funciona. Essa melhoria introduz novas colunas de filtro/ação XEvent equivalentes a query_hash e a query_plan_hash, exceto que elas estão definidas como INT64, o que podem ajudar a correlacionar consultas entre XE e DMVs.
-   **Suporte para UTF-8 em BULK INSERT e BCP:** Essa melhoria aborda [conectar-se comentários (370419)](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001) em que o suporte para exportação e importação de dados codificados no conjunto de caracteres UTF-8 agora está habilitado em BULK INSERT e BCP.
-   **Perfis de execução de consulta de por operador leve:** Enquanto a solução de problemas de consulta de desempenho, embora o plano de execução fornece muitas informações sobre o plano de execução de consulta e o custo do operador no plano, mas ele limitou informações sobre real estatísticas de tempo de execução, como (CPU, leituras de e/s, tempo decorrido por thread). SQL 2014 SP2 apresenta essas estatísticas de tempo de execução adicionais por operador no plano de execução, bem como um XEvent (query_thread_profile) para ajudar na solução de problemas de desempenho de consulta. [Consulte o blog para obter mais informações](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/).
-   **Limpeza do controle de alterações:** Um novo procedimento armazenado `sp_flush_CT_internal_table_on_demand` é introduzido para tabelas internas de ChangeTracking de limpeza sob demanda.
-   **Log de tempo limite de concessão de AlwaysON** adicionado a nova funcionalidade de registro em log para mensagens de tempo limite de concessão para que a hora atual e os tempos de renovação esperados são registrados. Também uma nova mensagem foi introduzida no SQL Errorlog sobre os tempos limite. [Consulte o blog para obter mais informações](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/).
-   **Novo DMF para recuperar o buffer de entrada no SQL Server:** Um novo DMF para recuperar o buffer de entrada para uma sessão/solicitação (sys.dm_exec_input_buffer) agora está disponível. Isso é funcionalmente equivalente ao DBCC INPUTBUFFER. [Consulte o blog para obter mais informações](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/).
-   **Mitigação para concessão de memória subestimada e supervalorizado:** Adicionadas novas dicas de consulta para o administrador de recursos por meio de MIN_GRANT_PERCENT e MAX_GRANT_PERCENT. Isso permite que você aproveite essas dicas ao executar consultas limitando suas concessões de memória para evitar a contenção de memória. Para obter mais informações, consulte [KB310740 de artigo da base de dados de Conhecimento](https://support.microsoft.com/en-us/kb/3107401)
-   **Melhor diagnóstico de uso/concessão de memória:** Um novo evento estendido foi adicionado à lista de recursos de rastreamento no SQL Server (query_memory_grant_usage) para controlar as concessões de memória solicitadas e concedidas. Isso fornece maior capacidade de rastreamento e análise para solução de problemas de execução de consulta relacionados a concessões de memória. Para obter mais informações, consulte [artigo da base de dados de Conhecimento KB3107173](https://support.microsoft.com/en-us/kb/3107173).
-   **Consultar diagnóstico de execução para despejo de tempdb:**-aviso de Hash e avisos de classificação agora tem colunas adicionais para rastrear as estatísticas e/s física, memória usada e linhas afetadas. Também introduzimos um novo evento estendido de hash_spill_details. Agora você pode acompanhar informações mais detalhadas para avisos de hash e de classificação ([KB3107172](https://support.microsoft.com/en-us/kb/3107172)). Essa melhoria agora também é exposta por meio de planos de consulta XML na forma de um novo atributo para o tipo complexo de SpillToTempDbType ([KB3107400](https://support.microsoft.com/en-us/kb/3107400)). Defina as estatísticas em agora mostra estatísticas de tabela de trabalho de classificação. .
-   **Diagnóstico aprimorado para planos de execução de consultas que envolvem a aplicação de predicado residual:** As leitura de linhas reais agora serão relatadas nos planos de execução de consulta para ajudar a melhorar a solução de problemas de desempenho de consulta. Isso deve negar a necessidade de capturar SET STATISTICS IO separadamente. Agora permite que você veja informações relacionadas a uma aplicação de predicado residual em um plano de consulta. Para obter mais informações, consulte [artigo da base de dados de Conhecimento KB3107397](https://support.microsoft.com/en-us/kb/3107397).


## <a name="additional-information"></a>Informações adicionais  
 [Recursos do SQL Server 2014](../2014-toc/books-online-for-sql-server-2014.md)  
  
 [SQL Server 2014 Release Notes](https://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [SQL Server 2014 Resource Center](https://msdn.microsoft.com/sqlserver/dn135309)  
  
 [Site do SQLCat](https://go.microsoft.com/fwlink/p/?linkID=220963)  
  
  

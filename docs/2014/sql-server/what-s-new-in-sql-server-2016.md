---
title: O&#39;que há de novo no SQL Server 2014 | Microsoft Docs
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
ms.openlocfilehash: f368da503c90595624f476344724719206cdb77c
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893707"
---
# <a name="what39s-new-in-sql-server-2014"></a>O&#39;que há de novo no SQL Server 2014
  Este tópico resume links detalhados para novos recursos no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] e resume os pacotes de serviços para[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**Experimente:** ![A máquina virtual pequena](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png) do Azure tem uma conta do Azure?  Em seguida, acesse **[aqui](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2)** para criar uma máquina virtual com o SQL Server 2014 Service Pack 1 (SP1) já instalado. 
  
-   [Novidades &#40;mecanismo de banco de dados&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [O que há de novo no Analysis Services e Business Intelligence](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services)  
  
-   [Novidades na instalação do SQL Server](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]o não introduziu novos recursos significativos para o seguinte:**  
  
-   [Novidades &#40;Integration Services&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [Novidades &#40;Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="includesssql14includessssql14-mdmd-service-pack-1-sp1"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 1 (SP1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)](SP1) não introduziu novos recursos significativos.
-  [SQL Server informações de versão do 2014 Service Pack 1](https://support.microsoft.com/en-us/kb/3058865).
-  [![Baixar o Service Pack 1 para Microsoft?? SQL Server?? ](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=46694) 2014[baixar o Service Pack 1 para Microsoft?? SQL Server?? 2014](https://www.microsoft.com/en-us/download/details.aspx?id=46694).


## <a name="includesssql14includessssql14-mdmd-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Service Pack 2 (SP2)
- [SQL Server informações de versão do 2014 Service Pack 2](https://support.microsoft.com/en-us/kb/3171021).
-  [![Baixar o Service Pack 2 para Microsoft?? SQL Server?? ](./media/what-s-new-in-sql-server-2016/download.png)](https://go.microsoft.com/fwlink/?LinkID=821558) 2014[baixar o Service Pack 2 para Microsoft?? SQL Server?? 2014](https://go.microsoft.com/fwlink/?LinkID=821558).
-  [![Baixe SQL Server 2014 SP2 Feature Pack](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/en-us/download/details.aspx?id=53164)[ Baixe o SQL Server Feature Pack 2014 SP2](https://www.microsoft.com/en-us/download/details.aspx?id=53164).

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 Inclui os seguintes aprimoramentos:

### <a name="performance-and-scalability-improvements"></a>Aprimoramentos de desempenho e escalabilidade 
-   **Particionamento automático de soft NUMA:** Com [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] o SP2, o soft numa automático é habilitado quando o sinalizador de rastreamento 8079 é ativado durante a inicialização da instância. Quando o sinalizador de rastreamento 8079 estiver habilitado durante [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] a inicialização, o SP2 interrogará o layout de hardware e configurará automaticamente o soft numa em sistemas que relatam 8 ou mais CPUs por nó numa. O comportamento automático de NUMA suave é reconhecer o hyperthreading (HT/processador lógico). O particionamento e a criação de nós adicionais dimensiona o processamento em segundo plano aumentando o número de ouvintes, o dimensionamento e os recursos de rede e de criptografia. É recomendável primeiro testar a carga de trabalho de desempenho com o NUMA auto-Soft antes de transformá-lo em produção. [Consulte o blog para obter mais informações](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/). 
-  **Dimensionamento do objeto de Memória Dinâmica:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]O SP2 particiona dinamicamente os objetos de memória com base no número de nós e núcleos para dimensionar em hardware moderno. O objetivo da promoção dinâmica é particionar automaticamente um CMEMTHREAD (objeto de memória de thread seguro) se ele se tornar um afunilamento. Os objetos de memória não particionados podem ser promovidos dinamicamente para serem particionados por nó (número de partições igual ao número de nós NUMA) e os objetos de memória particionados por nó podem ser mais promovidos para serem particionados pela CPU (número de partições igual a número de CPUs). [Consulte o blog para obter mais informações](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/).
-  **Dica MAXDOP para comandos DBCC\* check:** Essa melhoria aborda os [comentários de conexão (468694)](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb). Agora você pode executar o DBCC CHECKDB com a configuração MAXDOP diferente do valor sp_configure. Se MAXDOP exceder o valor configurado com o Resource Governor, o Mecanismo de Banco de Dados usará o valor de MAXDOP do Resource Governor, descrito em ALTER WORKLOAD GROUP (Transact-SQL). Todas as regras semânticas usadas com a opção de configuração grau máximo de paralelismo são aplicáveis ao usar a dica de consulta MAXDOP. Para obter mais informações, consulte [DBCC CHECKDB (Transact-SQL)](https://msdn.microsoft.com/library/ms176064.aspx).
-   **Habilitar > 8 TB para o pool de buffers:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]O SP2 permite 128TB de espaço de endereço virtual para uso do pool de buffers. Essa melhoria permite que SQL Server pool de buffers seja dimensionado além do 8 TB no hardware moderno.
-   **Aperfeiçoamento do SpinLock do SOS_RWLock:** O SOS_RWLock é um primitivo de sincronização usado em vários locais em toda a base de código SQL Server.  Como o nome indica, o código pode ter uma propriedade compartilhada (leitores) ou única (gravador). Essa melhoria elimina a necessidade de SpinLock para SOS_RWLock e, em vez disso, usa técnicas sem bloqueio semelhantes ao OLTP na memória. Com essa alteração, muitos threads podem ler uma estrutura de dados protegida por SOS_RWLock em paralelo sem bloquear um ao outro e, assim, fornecer maior escalabilidade. Antes dessa alteração, a implementação de spinlock permitia que apenas um thread adquirisse o SOS_RWLock por vez, mesmo para ler uma estrutura de dados.  [Consulte o blog para obter mais informações](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/).
-    **Implementação nativa espacial:** Uma melhoria significativa no desempenho de consulta espacial é [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] introduzida no SP2 por meio da implementação nativa. Para obter mais informações, consulte o [artigo da base de dados de conhecimento KB3107399](https://support.microsoft.com/en-us/kb/3107399).

### <a name="supportability-and-diagnostics-improvements"></a>Melhorias de diagnóstico e suporte
-   **Clonagem de banco de dados:** Clonar banco de dados é um novo comando DBCC que aprimora a solução de problemas de bancos de dados de produção existentes, clonando o esquema e os metadados sem eles. O clone é criado com o comando `DBCC clonedatabase('source_database_name', 'clone_database_name')`.  **Observação:** Os bancos de dados clonados não devem ser usados em ambientes de produção. Use o seguinte comando para determinar se um banco de dados foi gerado a partir de um `select DATABASEPROPERTYEX('clonedb', 'isClone')`banco de dados clonado:. O valor de retorno **1** indica que o banco de dados é criado a partir de clonedatabase enquanto **0** indica que ele não é um clone.
-   **Suporte a tempdb:**  Uma nova mensagem de log de erros que indica o número de arquivos tempdb e o tamanho/aumento automático de arquivos de dados tempdb presentes na inicialização do servidor.
-   **Log de inicialização de arquivo instantâneo do banco de dados:** Uma nova mensagem de log de erros que indica no servidor statup, o status da inicialização instantânea de arquivo do banco de dados (habilitado/desabilitado).
-   **Nomes de módulo na pilha de chamadas:** A pilha de chamadas de XEvent agora inclui nomes de módulos + offset em vez de endereços absolutos.
-   **Nova DMF para estatísticas incrementais:** Essa melhoria aborda os [comentários de conexão (797156)](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics) para habilitar o acompanhamento das estatísticas incrementais no nível da partição. Uma nova DMF sys. dm _db_incremental_stats_properties é introduzida para expor informações por partição para estatísticas incrementais.
-   **Comportamento de DMV de uso de índice atualizado:** Essa melhoria aborda os [comentários de conexão (739566)](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats) de clientes em que a recriação de um índice *não* limpará nenhuma entrada de linha existente de sys. dm _db_index_usage_stats para esse índice. O comportamento agora será o mesmo que no SQL 2008 e no SQL Server 2016. [Consulte o blog para obter mais informações](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/).
-   **Correlação aprimorada entre o diagnóstico XE e DMVs:** Essa melhoria aborda os [comentários de conexão (1934583)](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types). Query_hash e query_plan_hash são usados para identificar uma consulta exclusivamente. O DMV define-os como varbinary(8), enquanto XEvent define-os como UINT64. Como o SQL Server não tem "unisigned bigint", a conversão nem sempre funciona. Essa melhoria introduz novas colunas de filtro/ação XEvent equivalentes a query_hash e a query_plan_hash, exceto que elas estão definidas como INT64, o que podem ajudar a correlacionar consultas entre XE e DMVs.
-   **Suporte para UTF-8 em BULK INSERT e BCP:** Essa melhoria aborda os [comentários de conexão (370419)](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001) , onde o suporte para exportação e importação de dados codificados no conjunto de caracteres UTF-8 agora está habilitado em BULK INSERT e bcp.
-   **Criação de perfil de execução de consulta por operador leve:** Ao solucionar problemas de desempenho de consulta, embora Showplan forneça muitas informações sobre o plano de execução de consulta e o custo do operador no plano, mas ele tem informações limitadas sobre estatísticas reais de tempo de execução como (CPU, leituras de e/s, tempo decorrido por thread). O SQL 2014 SP2 apresenta essas estatísticas de tempo de execução adicionais por operador no Showplan, bem como um XEvent (query_thread_profile) para auxiliar na solução de problemas de desempenho de consulta. [Consulte o blog para obter mais informações](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/).
-   **Controle de Alterações limpeza:** Um novo procedimento `sp_flush_CT_internal_table_on_demand` armazenado é introduzido para limpar as tabelas internas de controle de alterações sob demanda.
-   **Log de tempo limite de concessão AlwaysON** Adição do novo recurso de log para mensagens de tempo limite de concessão para que a hora atual e os tempos de renovação esperados sejam registrados. Além disso, uma nova mensagem foi introduzida no log de erros do SQL em relação aos tempos limite. [Consulte o blog para obter mais informações](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/).
-   **Novo DMF para recuperar o buffer de entrada no SQL Server:** Um novo DMF para recuperar o buffer de entrada para uma sessão/solicitação (sys.dm_exec_input_buffer) agora está disponível. Isso é funcionalmente equivalente ao DBCC INPUTBUFFER. [Consulte o blog para obter mais informações](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/).
-   **Mitigação para concessão de memória subestimada e Sobreestimada:** Adicionadas novas dicas de consulta para Resource Governor por meio de MIN_GRANT_PERCENT e MAX_GRANT_PERCENT. Isso permite que você aproveite essas dicas durante a execução de consultas, limitando suas concessões de memória para evitar a contenção de memória. Para obter mais informações, consulte o [artigo da base de dados de conhecimento KB310740](https://support.microsoft.com/en-us/kb/3107401)
-   **Melhor diagnóstico de uso/concessão de memória:** Um novo evento estendido foi adicionado à lista de recursos de rastreamento no SQL Server (query_memory_grant_usage) para rastrear as concessões de memória solicitadas e concedidas. Isso fornece melhores recursos de rastreamento e análise para solucionar problemas de execução de consulta relacionados a concessões de memória. Para obter mais informações, consulte o [artigo da base de dados de conhecimento KB3107173](https://support.microsoft.com/en-us/kb/3107173).
-   **Diagnóstico de execução de consulta para despejo de tempdb:** -o aviso de hash e os avisos de classificação agora têm colunas adicionais para rastrear estatísticas de e/s físicas, memória usada e linhas afetadas. Também introduzimos um novo evento estendido hash_spill_details. Agora você pode controlar informações mais granulares para seus avisos de hash e de classificação ([KB3107172](https://support.microsoft.com/en-us/kb/3107172)). Essa melhoria agora também é exposta por meio dos planos de consulta XML na forma de um novo atributo para o tipo complexo SpillToTempDbType ([KB3107400](https://support.microsoft.com/en-us/kb/3107400)). Definir estatísticas em agora mostra classificar estatísticas de tabela de trabalho. .
-   **Diagnóstico aprimorado para planos de execução de consulta que envolvem a aplicação de predicado residuais:** As linhas reais lidas agora serão relatadas nos planos de execução da consulta para ajudar a melhorar a solução de problemas de desempenho de consultas. Isso deve negar a necessidade de capturar as estatísticas SET de e/s separadamente. Isso agora permite que você veja informações relacionadas a uma aplicação de predicado residual em um plano de consulta. Para obter mais informações, consulte o [artigo da base de dados de conhecimento KB3107397](https://support.microsoft.com/en-us/kb/3107397).


## <a name="additional-information"></a>Informações adicionais  
 [SQL Server recursos 2014](../2014-toc/books-online-for-sql-server-2014.md)  
  
 [SQL Server 2014 Release Notes](https://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [Centro de recursos do SQL Server 2014](https://msdn.microsoft.com/sqlserver/dn135309)  
  
 [Site da SQLCat](https://go.microsoft.com/fwlink/p/?linkID=220963)  
  
  

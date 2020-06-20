---
title: O que há de novo no SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 12/10/2019
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
author: rothja
ms.author: jroth
ms.openlocfilehash: cee52973ec114fc52aac17b9c7e4c51e66920269
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85041342"
---
# <a name="whats-new-in-sql-server-2014"></a>Novidades do SQL Server 2014

Este tópico resume links detalhados para novos recursos no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] e resume os pacotes de serviços para[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 
**Experimente:** ![ A máquina virtual pequena do Azure ](./media/what-s-new-in-sql-server-2016/azure-virtual-machine-small.png) tem uma conta do Azure?  Vá para https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2014sp1EnterpriseWindowsServer2012R2 para criar uma máquina virtual com o SQL Server 2014 Service Pack 1 (SP1) já instalado.

> [!TIP]
> [Clique aqui](../2014-toc/index.yml) para obter a página de documentação inicial do SQL Server 2014.

<!--
Do not let this file's filename fool you.
This filename contains "2016", but nevertheless...
This file, at this exact GitHub path, is dedicated to SQL Server version 2014.
-->

## <a name="whats-new-articles"></a>Artigos de novidades

-   [O que há de novo &#40;Mecanismo de Banco de Dados&#41;](../database-engine/whats-new-in-sql-server-2016.md)  
  
-   [Novidades no Analysis Services e no Business Intelligence](https://docs.microsoft.com/analysis-services/what-s-new-in-analysis-services)  
  
-   [Novidades na instalação do SQL Server](install/what-s-new-in-sql-server-installation.md)  
  
 **[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]o não introduziu novos recursos significativos para os seguintes recursos:**  
  
-   [O que há de novo &#40;Integration Services&#41;](../integration-services/what-s-new-in-integration-services-in-sql-server-2016.md)  
  
-   [O que há de novo &#40;Reporting Services&#41;](../reporting-services/what-s-new-reporting-services.md)  
  
## <a name="sssql14-service-pack-1-sp1"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] Service Pack 1 (SP1)
[!INCLUDE[ssSQL14](../includes/sssql14-md.md)](SP1) não introduziu novos recursos significativos.
-  [SQL Server informações de versão do 2014 Service Pack 1](https://support.microsoft.com/kb/3058865).
-  [ ![ Baixe o Service Pack 1 para Microsoft SQL Server 2014](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/download/details.aspx?id=46694) [Baixe o service pack 1 para Microsoft SQL Server 2014](https://www.microsoft.com/download/details.aspx?id=46694).


## <a name="sssql14-service-pack-2-sp2"></a>[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]Service Pack 2 (SP2)
- [SQL Server informações de versão do 2014 Service Pack 2](https://support.microsoft.com/kb/3171021).
-  [ ![ Baixe o Service Pack 2 para Microsoft SQL Server 2014](./media/what-s-new-in-sql-server-2016/download.png)](https://go.microsoft.com/fwlink/?LinkID=821558) [Baixe o service pack 2 para Microsoft SQL Server 2014](https://go.microsoft.com/fwlink/?LinkID=821558).
-  [ ![ Baixe SQL Server 2014 SP2 Feature Pack](./media/what-s-new-in-sql-server-2016/download.png)](https://www.microsoft.com/download/details.aspx?id=53164) [Baixe o SQL Server Feature Pack 2014 SP2](https://www.microsoft.com/download/details.aspx?id=53164).

[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]SP2 Inclui os seguintes aprimoramentos:

### <a name="performance-and-scalability-improvements"></a>Aprimoramentos de desempenho e escalabilidade 
-   **Particionamento automático de soft numa:** Com o [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2, o soft numa automático é habilitado quando o sinalizador de rastreamento 8079 é ativado durante a inicialização da instância. Quando o sinalizador de rastreamento 8079 estiver habilitado durante a inicialização, [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] o SP2 interrogará o layout de hardware e configurará automaticamente o soft numa em sistemas que relatam 8 ou mais CPUs por nó numa. O comportamento automático de NUMA suave é reconhecer o hyperthreading (HT/processador lógico). O particionamento e a criação de nós adicionais dimensiona o processamento em segundo plano aumentando o número de ouvintes, o dimensionamento e os recursos de rede e de criptografia. É recomendável que você primeiro teste a carga de trabalho de desempenho com o NUMA auto-Soft, antes de ajustá-la na produção. [Para obter mais informações, consulte o blog](https://blogs.msdn.microsoft.com/psssql/2016/03/30/sql-2016-it-just-runs-faster-automatic-soft-numa/). 
-  **Dimensionamento do objeto de memória dinâmica:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] O SP2 particiona dinamicamente os objetos de memória com base no número de nós e núcleos para dimensionar em hardware moderno. O objetivo da promoção dinâmica é particionar automaticamente um CMEMTHREAD (objeto de memória de thread seguro) se ele se tornar um afunilamento. Os objetos de memória não particionados podem ser dinamicamente particionados por nó (número de partições é igual ao número de nós NUMA). Os objetos de memória particionados por nó podem ser mais particionados por CPU (número de partições igual a número de CPUs). [Para obter mais informações, consulte o blog](https://blogs.msdn.microsoft.com/psssql/2016/04/06/sql-2016-it-just-runs-faster-dynamic-memory-object-cmemthread-partitioning/).
-  **Dica MAXDOP para comandos DBCC check \* :** essa melhoria aborda [comentários de conexão (468694)](https://connect.microsoft.com/SQLServer/feedback/details/468694/maxdop-option-in-dbcc-checkdb). Agora você pode executar o DBCC CHECKDB com uma configuração MAXDOP diferente do valor sp_configure. Se MAXDOP exceder o valor configurado com o Resource Governor, o Mecanismo de Banco de Dados usará o valor de MAXDOP do Resource Governor, descrito em ALTER WORKLOAD GROUP (Transact-SQL). Todas as regras semânticas usadas com a opção de configuração grau máximo de paralelismo são aplicáveis ao usar a dica de consulta MAXDOP. Para obter mais informações, consulte [DBCC CHECKDB (Transact-SQL)](https://msdn.microsoft.com/library/ms176064.aspx).
-   **Habilitar >8 TB para o pool de buffers:** [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] O SP2 permite 128 TB de espaço de endereço virtual para uso do pool de buffers. Essa melhoria permite que SQL Server pool de buffers dimensione além de 8 TB em hardware moderno.
-   **Aprimoramento do SOS_RWLock SpinLock:** O SOS_RWLock é um primitivo de sincronização usado em vários locais em toda a base de código SQL Server.  Como o nome indica, o código pode ter uma propriedade compartilhada (leitores) ou única (gravador). Essa melhoria elimina a necessidade de SpinLock para SOS_RWLock e, em vez disso, usa técnicas sem bloqueio semelhantes ao OLTP na memória. Com essa alteração, muitos threads podem ler uma estrutura de dados protegida por SOS_RWLock em paralelo, sem bloquear um ao outro. Essa paralelização fornece maior escalabilidade. Antes dessa alteração, a implementação de spinlock permitia que apenas um thread adquirisse o SOS_RWLock de cada vez, mesmo para ler uma estrutura de dados. [Para obter mais informações, consulte o blog](https://blogs.msdn.microsoft.com/psssql/2016/04/07/sql-2016-it-just-runs-faster-sos_rwlock-redesign/).
-    **Implementação nativa espacial:** Uma melhoria significativa no desempenho de consulta espacial é introduzida no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] SP2 por meio da implementação nativa. Para obter mais informações, consulte o [artigo da base de dados de conhecimento KB3107399](https://support.microsoft.com/kb/3107399).

### <a name="supportability-and-diagnostics-improvements"></a>Melhorias de diagnóstico e suporte
-   **Clonagem de banco de dados:** Clonar banco de dados é um novo comando DBCC que aprimora a solução de problemas de bancos de dados de produção existentes, clonando o esquema e os metadados sem eles. O clone é criado com o comando `DBCC clonedatabase('source_database_name', 'clone_database_name')` .  **Observação:** Os bancos de dados clonados não devem ser usados em ambientes de produção. Use o seguinte comando para determinar se um banco de dados foi gerado a partir de um banco de dados clonado: `select DATABASEPROPERTYEX('clonedb', 'isClone')` . O valor de retorno **1** indica que o banco de dados é criado a partir de clonedatabase enquanto **0** indica que ele não é um clone.
-   **Suporte a tempdb:**  Uma nova mensagem de log de erros que indica na inicialização o número de arquivos tempdb e o tamanho e o aumento automático de arquivos de dados tempdb.
-   **Log de inicialização de arquivo instantâneo do banco de dados:** Uma nova mensagem de log de erros que indica na inicialização do servidor, o status da inicialização instantânea de arquivo do banco de dados (habilitado/desabilitado).
-   **Nomes de módulo na pilha de chamadas:** A pilha de chamadas de evento estendido (XEvent) agora inclui nomes de módulos mais deslocamento, em vez de endereços absolutos.
-   **Nova Dmf para estatísticas incrementais:** Essa melhoria aborda os [comentários de conexão (797156)](https://connect.microsoft.com/SQLServer/feedback/details/797156/display-sys-dm-db-stats-properties-per-partition-for-incremental-statistics) para habilitar o acompanhamento das estatísticas incrementais no nível da partição. Uma nova DMF sys. dm_db_incremental_stats_properties é introduzida para expor informações por partição para estatísticas incrementais.
-   **Comportamento de DMV de uso de índice atualizado:** Essa melhoria aborda os [comentários de conexão (739566)](https://connect.microsoft.com/SQLServer/feedback/details/739566/rebuilding-an-index-clears-stats-from-sys-dm-db-index-usage-stats) de clientes em que a recriação de um índice *não* limpará nenhuma entrada de linha existente de sys. dm_db_index_usage_stats para esse índice. O comportamento agora será o mesmo que no SQL 2008 e no SQL Server 2016. [Para obter mais informações, consulte o blog](https://blogs.msdn.microsoft.com/sql_server_team/index-usage-dmv-behavior-updated/).
-   **Correlação aprimorada entre o diagnóstico xe e DMVs:** Essa melhoria aborda os [comentários de conexão (1934583)](https://connect.microsoft.com/SQLServer/feedback/details/1934583/extended-events-query-hash-and-query-plan-hash-data-types). `Query_hash`e `query_plan_hash` são usados para identificar uma consulta exclusivamente. O DMV define-os como varbinary(8), enquanto XEvent define-os como UINT64. Como o SQL Server não tem "bigint não assinado", a conversão nem sempre funciona. Essa melhoria introduz novas colunas de ação XEvent e filtro. As colunas são equivalentes a `query_hash` e `query_plan_hash` , exceto que são definidas como Int64. A definição INT64 ajuda a correlacionar consultas entre XE e DMVs.
-   **Suporte para UTF-8 em BULK INSERT e bcp:** Essa melhoria aborda os [comentários de conexão (370419)](https://connect.microsoft.com/SQLServer/feedback/details/370419/bulk-insert-and-bcp-does-not-recognize-codepage-65001). BULK INSERT e BCP agora podem exportar ou importar dados que são codificados no conjunto de caracteres UTF-8.
-   **Criação de perfil leve de execução de consulta por operador:** Showplan fornece informações sobre o custo de cada operador no plano. Mas as estatísticas reais de tempo de execução são limitadas para coisas como CPU, leituras de e/s e tempo decorrido por thread. SQL Server 2014 SP2 apresenta essas estatísticas de tempo de execução adicionais por operador no Showplan. O R2 também apresenta um XEvent chamado `query_thread_profile` para ajudar na solução de problemas de desempenho de consulta. [Para obter mais informações, consulte o blog](https://blogs.msdn.microsoft.com/sql_server_team/added-per-operator-level-performance-stats-for-query-processing/).
-   **Controle de alterações limpeza:** Um novo procedimento armazenado `sp_flush_CT_internal_table_on_demand` é introduzido para limpar as tabelas internas de controle de alterações sob demanda.
-   **Log de tempo limite de concessão AlwaysON** Adição do novo recurso de log para mensagens de tempo limite de concessão para que a hora atual e os tempos de renovação esperados sejam registrados. Além disso, uma nova mensagem foi introduzida no log de erros do SQL em relação aos tempos limite. [Para obter mais informações, consulte o blog](https://blogs.msdn.microsoft.com/alwaysonpro/2016/02/23/improved-alwayson-availability-group-lease-timeout-diagnostics/).
-   **Novo Dmf para recuperar o buffer de entrada no SQL Server:** Um novo DMF para recuperar o buffer de entrada para uma sessão/solicitação (sys. dm_exec_input_buffer) já está disponível. Essa DMF é funcionalmente equivalente a DBCC INPUTBUFFER. [Para obter mais informações, consulte o blog](https://blogs.msdn.microsoft.com/sql_server_team/new-dmf-for-retrieving-input-buffer-in-sql-server/).
-   **Mitigação para concessão de memória subestimada e Sobreestimada:** Adicionadas novas dicas de consulta para Resource Governor por meio de MIN_GRANT_PERCENT e MAX_GRANT_PERCENT. Essa nova consulta permite que você aproveite essas dicas durante a execução de consultas, limitando suas concessões de memória para evitar a contenção de memória. Para obter mais informações, consulte o [artigo da base de dados de conhecimento KB310740](https://support.microsoft.com/kb/3107401).
-   **Melhor diagnóstico de uso e concessão de memória:** Um novo evento estendido chamado `query_memory_grant_usage` foi adicionado à lista de recursos de rastreamento no SQL Server. Esse evento acompanha as concessões de memória solicitadas e concedidas. Esse evento fornece melhores recursos de rastreamento e análise para solucionar problemas de execução de consulta relacionados a concessões de memória. Para obter mais informações, consulte o [artigo da base de dados de conhecimento KB3107173](https://support.microsoft.com/kb/3107173).
-   **Diagnóstico de execução de consulta para o despejo de tempdb:**-o aviso de hash e os avisos de classificação agora têm colunas adicionais para controlar as estatísticas de e/s físicas, a memória usada e as linhas afetadas. Também introduzimos um novo hash_spill_details evento estendido. Agora você pode controlar informações mais granulares para seus avisos de hash e de classificação ([KB3107172](https://support.microsoft.com/kb/3107172)). Essa melhoria agora também é exposta por meio dos planos de consulta XML na forma de um novo atributo para o tipo complexo SpillToTempDbType ([KB3107400](https://support.microsoft.com/kb/3107400)). Definir estatísticas `ON` agora mostra classificar estatísticas de tabela de trabalho.
-   **Diagnóstico aprimorado para planos de execução de consulta que envolvem a aplicação de predicado residuais:** As linhas reais lidas agora são relatadas nos planos de execução da consulta, para ajudar a melhorar a solução de problemas de desempenho de consultas. Essas linhas negam a necessidade de capturar definir estatísticas e/s separadamente. Essas linhas também permitem que você veja informações relacionadas a um push-down de predicado residuais em um plano de consulta. Para obter mais informações, consulte o [artigo da base de dados de conhecimento KB3107397](https://support.microsoft.com/kb/3107397).


## <a name="additional-information"></a>Informações adicionais  
 [Recursos do SQL Server 2014](../2014-toc/index.yml)  
  
 [SQL Server 2014 Release Notes](https://go.microsoft.com/fwlink/p/?linkID=296445)  
  
 [Central de Recursos do SQL Server 2014](https://msdn.microsoft.com/sqlserver/dn135309)  
  
 [Site do SQLCat](https://go.microsoft.com/fwlink/p/?linkID=220963)  

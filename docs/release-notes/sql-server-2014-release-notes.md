---
title: "Notas de versão do SQL Server 2014 | Microsoft Docs"
ms.custom: 
ms.date: 01/31/2017
ms.prod: sql-server-2014
ms.technology: server-general
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: bf4c4922-80b3-4be3-bf71-228247f97004
caps.latest.revision: 100
author: byham
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0ca391c25a462a5f30d6a9bc51b4541f77adfd48
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-2014-release-notes"></a>SQL Server 2014 Release Notes
Este documento Notas de Versão descreve problemas conhecidos sobre os quais você deve ler antes de instalar ou solucionar problemas do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
## <a name="top"></a>Conteúdo  
[1.0 Antes da instalação](#BeforeInstall)  
  
[2.0 Documentação do produto](#ProdDoc)  
  
[3.0 Mecanismo de Banco de Dados](#DBEngine)  
  
[4.0 Reporting Services](#SSRS)  
  
[5.0 SQL Server 2014 em máquinas virtuais do Microsoft Azure](#AzureVM)  
  
[6.0 Analysis Services](#SSAS)  
  
[7.0 Data Quality Services](#DQS)  
  
[8.0 Supervisor de Atualização](#UA)  
  
## <a name="BeforeInstall"></a>1.0 Antes da instalação  
  
### <a name="11-limitations-and-restrictions-in-sql-server-2014-rtm"></a>1.1 Limitações e restrições no SQL Server 2014 RTM  
  
#### <a name="111-general-limitations-and-restrictions"></a>1.1.1 Limitações e restrições gerais  
  
1.  A atualização do SQL Server 2014 CTP 1 para o SQL Server 2014 RTM NÃO é suportada.  
  
2.  A instalação do SQL Server 2014 CTP 1 em conjunto com o SQL Server 2014 RTM NÃO é suportada.  
  
3.  Os recursos de anexação ou restauração de um banco de dados do SQL Server 2014 CTP 1 ao SQL Server 2014 RTM não têm suporte.  
  
**Solução alternativa:** não há.  
  
#### <a name="12-considerations-for-upgrading-sql-server-2014-ctp-2-to-sql-server-2014-rtm-and-downgrading-from-sql-server-2014-rtm-to-sql-server-2014-ctp-2"></a>1.2 Considerações sobre a atualização do SQL Server 2014 CTP 2 para o SQL Server 2014 RTM e a desatualização do SQL Server 2014 RTM para o SQL Server 2014 CTP 2  
  
#### <a name="121-upgrading-from-sql-server-2014-ctp-2-to-sql-server-rtm-is-fully-supported"></a>1.2.1 A atualização do SQL Server 2014 CTP 2 para o SQL Server RTM é totalmente suportada  
Em especial, você pode:  
  
1.  Anexar um banco de dados do SQL Server 2014 CTP 2 a uma instância do SQL Server 2014 RTM.  
  
2.  Restaurar um banco de dados removido do SQL Server 2014 CTP 2 para uma instância do SQL Server 2014 RTM.  
  
3.  Atualização in-loco do SQL Server 2014 RTM.  
  
4.  Atualização sem interrupção do SQL Server 2014 RTM. É necessário alternar para o modo de failover manual antes de iniciar a atualização sem interrupção. Consulte [Fazer upgrade e atualização dos servidores de grupo de disponibilidade com tempo de inatividade e perda de dados mínimos](http://msdn.microsoft.com/library/dn178483.aspx) para obter detalhes.  
  
5.  Os dados coletados pelos conjuntos de coleta de desempenho da transação instalados no SQL Server 2014 CTP 2 não podem ser visualizados com o SQL Server Management Studio no SQL Server 2014 RTM, e vice-versa. Use o SQL Server Management Studio no SQL Server 2014 CTP 2 para exibir os dados coletados pelo conjunto de coleta instalado no SQL Server 2014 CTP 2, e use o SQL Server Management Studio no SQL Server 2014 RTM para exibir os dados coletados pelo conjunto de coleta instalado no SQL Server 2014 RTM.  
  
### <a name="122-downgrading-from-sql-server-2014-rtm-to-sql-server-2014-ctp-2"></a>1.2.2 Desatualizando do SQL Server 2014 RTM para o SQL Server 2014 CTP 2  
Isso não tem suporte.  
  
**Solução:** Não há solução para a desatualização. Recomendamos que você faça backup do banco de dados antes de atualizar para o SQL Server 2014 RTM.  
  
![Ícone de seta usado com o link Voltar ao início](../release-notes/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Início](#top)  
  
## <a name="13-incorrect-version-of-streaminsight-client-on-sql-server-2014-mediaisocab"></a>1.3 Versão incorreta do StreamInsight Client na mídia/ISO/CAB do SQL Server 2014  
A versão incorreta do StreamInsight.msi e do StreamInsightClient.msi está localizada no seguinte caminho na mídia/ISO/CAB do SQL Server (StreamInsight\\\<Arquitetura\>\\\<ID de idioma\>).  
  
**Solução alternativa:** baixe e instale a versão correta da página de download do [SQL Server 2014 Feature Pack](http://go.microsoft.com/fwlink/?LinkID=306709).  
  
## <a name="ProdDoc"></a>2.0 Documentação do produto  
  
### <a name="21-report-builder-content-is-not-available-in-some-languages"></a>2.1 O conteúdo do Construtor de Relatórios não está disponível em alguns idiomas  
**Problema:** o conteúdo do Construtor de Relatórios não está disponível nos idiomas a seguir.  
  
-   Grego (el-GR)  
  
-   Norueguês (Bokmal) (nb-NO)  
  
-   Finlandês (fi-FI)  
  
-   Dinamarquês (da-DK)  
  
No [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], esse conteúdo estava disponível em um arquivo CHM enviado com o produto e que estava disponível nesses idiomas. Os arquivos CHM não vêm mais com o produto e o conteúdo do Construtor de Relatórios só está disponível no MSDN. O MSDN não oferece suporte a esses idiomas. O Construtor de Relatórios também foi removido do TechNet e não está mais disponível nesses idiomas com suporte.  
  
**Solução alternativa:** não há.  
  
### <a name="22-powerpivot-content-is-not-available-in-some-languages"></a>2.2 O conteúdo do PowerPivot não está disponível em alguns idiomas  
**Problema:** o conteúdo do PowerPivot não está disponível nos idiomas a seguir.  
  
-   Grego (el-GR)  
  
-   Norueguês (Bokmal) (nb-NO)  
  
-   Finlandês (fi-FI)  
  
-   Dinamarquês (da-DK)  
  
-   Tcheco (cs-CZ)  
  
-   Húngaro (hu-HU)  
  
-   Holandês (Países Baixos) (nl-NL)  
  
-   Polonês (pl-PL)  
  
-   Sueco (sv-SE)  
  
-   Turco (tr-TR)  
  
-   Português (Portugal) (pt-PT)  
  
No [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], este conteúdo estava disponível no TechNet e estava disponível nestes idiomas. Esse conteúdo foi removido do TechNet e não está mais disponível nesses idiomas com suporte.  
  
**Solução alternativa:** não há.  
  
![Ícone de seta usado com o link Voltar ao início](../release-notes/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Início](#top)  
  
## <a name="DBEngine"></a>3.0 Mecanismo de Banco de Dados  
  
### <a name="31-changes-made-for-standard-edition-in-sql-server-2014-rtm"></a>3.1 Alterações feitas à edição Standard no SQL Server 2014 RTM  
O padrão do SQL Server 2014 tem as seguintes alterações:  
  
-   O recurso de extensão do pool de buffers permite usar o tamanho máximo de até 4 vezes a memória configurada.  
  
-   A memória máxima foi aumentada de 64GB para 128GB.  
  
### <a name="32-in-memory-oltp-issues"></a>3.2 Problemas de OLTP em Memória  
  
#### <a name="321-memory-optimization-advisor-flags-default-constraints-as-incompatible"></a>3.2.1 O orientador de otimização de memória sinaliza restrições padrão como incompatíveis  
**Problema:** O orientador de otimização de memória no SQL Server Management Studio sinaliza todas as restrições padrão como incompatíveis. Nem todas as restrições padrão têm suporte em uma tabela com otimização de memória; o orientador de otimização do não faz distinção entre tipos com e sem suporte de restrições padrão. As restrições padrão com suporte incluem todas as constantes, expressões e funções internas suportadas nos procedimentos armazenados compilados de forma nativa. Para ver a lista de funções com suporte em procedimentos armazenados compilados de forma nativa, veja [Construções suportadas em procedimentos armazenados compilados de forma nativa](http://msdn.microsoft.com/library/dn452279(v=sql.120).aspx).  
  
**Solução:** Se você quiser usar o orientador para identificar bloqueadores, ignore as restrições padrão correspondentes. Para usar o orientador de otimização de memória para migrar as tabelas que têm restrições padrão correspondentes, mas nenhum outro bloqueador, siga estas etapas:  
  
1.  Remova as restrições padrão da definição de tabela.  
  
2.  Use o orientador de otimização do gerar um script de migração na tabela.  
  
3.  Adicione as restrições padrão novamente no script de migração.  
  
4.  Execute o script de migração.  
  
#### <a name="322-informational-message-file-access-denied-incorrectly-reported-as-an-error-in-the-sql-server-2014-error-log"></a>3.2.2 Mensagem informativa “acesso ao arquivo negado” informada incorretamente como um erro no log de erros do SQL Server 2014  
**Problema:** ao reiniciar um servidor que possui bancos de dados que contêm tabelas com otimização de memória, você pode ver o seguinte tipo de mensagens de erro no log de erros do SQL Server 2014:  
  
```  
[ERROR]Unable to delete file C:\Program Files\Microsoft SQL   
Server\....old.dll. This error may be due to a previous failure to unload   
memory-optimized table DLLs.  
```  
  
Esta mensagem é apenas informativa, e nenhuma ação do usuário é necessária.  
  
**Solução alternativa:** não há. Essa é uma mensagem informativa.  
  
#### <a name="323-missing-index-details-incorrectly-report-included-columns-for-memory-optimized-table"></a>3.2.3 Os detalhes de índice ausentes relatam incorretamente as colunas incluídas para a tabela com otimização de memória  
**Problema:** se o SQL Server 2014 detectar um índice ausente para uma consulta em uma tabela com otimização de memória, relatará um índice ausente em SHOWPLAN_XML, bem como nos DMVs do índice ausente, como sys.dm_db_missing_index_details. Em alguns casos, os detalhes de índice ausentes conterão as colunas incluídas. Uma vez que todas as colunas são incluídas implicitamente com todos os índices nas tabelas com otimização de memória, não é permitido especificar explicitamente as colunas incluídas com os índices otimizados por memória.  
  
**Solução:** não especifique a cláusula INCLUDE com os índices das tabelas com otimização de memória.  
  
#### <a name="324-missing-index-details-omit-missing-indexes-if-a-hash-index-exists-but-is-not-suitable-for-the-query"></a>3.2.4 Os detalhes de índice ausentes omitem os índices ausentes se um índice de hash existir mas não for apropriado para a consulta  
**Problema:** se você tiver um índice de HASH nas colunas de uma tabela com otimização de memória referenciada em uma consulta, mas o índice não puder ser usado na consulta, SQL Server 2014 sem sempre relatará um índice ausente em SHOWPLAN_XML e no DMV sys.dm_db_missing_index_details.  
  
Em particular, se uma consulta contiver os predicados de igualdade que envolvem um subconjunto de colunas de chave de índice ou se contiver os predicados de desigualdade que envolvem as colunas de chave de índice, o índice de HASH não pode ser usado como está, e um índice diferente será necessário para executar a consulta de forma eficaz.  
  
**Solução:** Caso você esteja usando índices de hash, inspecione as consultas e os planos de consulta para determinar se as consultas podem se beneficiar das operações de busca de índice em um subconjunto de chave de índice, ou as operações de busca de índice em predicados de desigualdade. Se você precisar buscar em um subconjunto de chave de índice, use um índice não clusterizado, ou use um índice de HASH exatamente nas colunas em que você precisa buscar. Se você precisar buscar em um predicado de desigualdade, use um índice não clusterizado em vez de HASH.  
  
#### <a name="325-failure-when-using-a-memory-optimized-table-and-memory-optimized-table-variable-in-the-same-query-if-the-database-option-readcommittedsnapshot-is-set-to-on"></a>3.2.5 Ocorrerá uma falha ao usar uma tabela com otimização de memória e uma variável de tabela com otimização de memória na mesma consulta, se a opção READ_COMMITTED_SNAPSHOT do banco de dados for definida como ON  
**Problema:** se a opção READ_COMMITTED_SNAPSHOT do banco de dados for definida como ON, e você acessar uma tabela com otimização de memória e uma variável de tabela com otimização de memória na mesma instrução fora do contexto de uma transação de usuário, você poderá encontrar essa mensagem de erro:  
  
```  
Msg 41359  
A query that accesses memory optimized tables using the READ COMMITTED  
isolation level, cannot access disk based tables when the database option  
READ_COMMITTED_SNAPSHOT is set to ON. Provide a supported isolation level  
for the memory optimized table using a table hint, such as WITH (SNAPSHOT).  
```  
  
**Solução:** utilize a dica de tabela WITH (SNAPSHOT) com a variável de tabela, ou defina a opção MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT do banco de dados para ON, usando a seguinte instrução:  
  
```  
ALTER DATABASE CURRENT   
SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT=ON  
```  
  
#### <a name="326-procedure-and-query-execution-statistics-for-natively-compiled-stored-procedures-record-worker-time-in-multiples-of-1000"></a>3.2.6 Procedimento e estatísticas de execução de consulta para que os procedimentos armazenados compilados de forma nativa armazenem o tempo de trabalho em múltiplos de 1000.  
**Problema:** depois de habilitar a coleção de procedimento ou coleção de estatísticas de execução de consulta para procedimentos armazenados compilados de forma nativa usando sp_xtp_control_proc_exec_stats ou sp_xtp_control_query_exec_stats, você verá o *_worker_time relatado em múltiplos de 1000, nos DMVs sys.dm_exec_procedure_stats e sys.dm_exec_query_stats. As execuções de consulta com um período de trabalho inferior a 500 microssegundos serão relatadas como tendo um worker_time de 0.  
  
**Solução alternativa:** não há. Não confie no worker_time relatado nos DMVs das estatísticas de execução para consultas de curta duração em procedimentos armazenados compilados de forma nativa.  
  
#### <a name="327-error-with-showplanxml-for-natively-compiled-stored-procedures-that-contain-long-expressions"></a>3.2.7 Erro com SHOWPLAN_XML para os procedimentos armazenados compilados de forma nativa que contêm expressões longas  
**Problema:** se um procedimento armazenado compilado de forma nativa contiver uma expressão longa, obter o SHOWPLAN_XML para o procedimento usando a opção SET SHOWPLAN_XML ON do T-SQL ou usando a opção "Exibir plano de execução estimado" no Management Studio, poderá resultar no seguinte erro:  
  
```  
Msg 41322. MAT/PIT export/import encountered a failure for memory  
optimized table or natively compiled stored procedure with object ID  
278292051 in database ID 6. The error code was  
0xc00cee81.  
```  
  
**Solução:** Duas soluções sugeridas:  
  
1.  Adicione parênteses à expressão, semelhante ao seguinte exemplo:  
  
    Em vez de:  
  
    ```  
    SELECT @v0 + @v1 + @v2 + ... + @v199  
    ```  
  
    Gravação:  
  
    ```  
    SELECT((@v0 + ... + @v49) + (@v50 + ... + @v99)) + ((@v100 + ... + @v149) + (@v150 + ... + @v199))  
    ```  
  
2.  Crie um segundo procedimento com uma expressão ligeiramente simplificada, para as finalidades de plano de execução - a forma geral do plano deve ser a mesma. Por exemplo, em vez de:  
  
    ```  
    SELECT @v0 +@v1 +@v2 +...+@v199  
    ```  
  
    Gravação:  
  
    ```  
    SELECT @v0 +@v1  
    ```  
  
#### <a name="328-using-a-string-parameter-or-variable-with-datepart-and-related-functions-in-a-natively-compiled-stored-procedure-results-in-an-error"></a>3.2.8 Usar um parâmetro ou uma variável de cadeia de caracteres com DATEPART e funções relacionadas em um procedimento armazenado compilado de forma nativa resultará em um erro.  
**Problema:** ao usar um parâmetro ou variável que possui um tipo de dados de cadeia de caracteres como (var)char ou n(var)char com as funções internas DATEPART, DAY, MONTH, e YEAR em um procedimento armazenado compilado de forma nativa, você verá uma mensagem de erro indicando que o datetimeoffset do tipo de dados não é suportado com procedimentos armazenados compilados de forma nativa.  
  
**Solução:** Atribua o parâmetro ou variável de cadeia de caracteres a uma nova variável do tipo datetime2, e use essa variável na função DATEPART, DAY, MONTH ou YEAR. Por exemplo:  
  
```  
DECLARE @d datetime2 = @string  
DATEPART(weekday, @d)  
```  
  
#### <a name="329-native-compilation-advisor-flags-delete-from-clauses-incorrectly"></a>3.2.9 O Orientador de Compilação Nativa sinaliza as cláusulas DELETE FROM incorretamente  
**Problema:** o Orientador de Compilação Nativa sinaliza as cláusulas DELETE FROM dentro de um procedimento armazenado incorretamente como incompatível.  
  
**Solução alternativa:** não há.  
  
### <a name="33-register-through-ssms-adds-dac-meta-data-with-mismatched-instance-ids"></a>3.3 O registro com o SSMS adiciona metadados do DAC com as IDs de instância incompatíveis  
**Problema:** ao registrar ou excluir um pacote de aplicativos da camada de dados (.dacpac) com o SQL Server Management Studio, as tabelas de sysdac* não são atualizadas corretamente para permitir que um usuário consulte o histórico do dacpac para o banco de dados.  O instance_id para o sysdac_history_internal e o sysdac_instances_internal não correspondem para permitir uma junção.  
  
**Solução alternativa:** esse problema é corrigido com a redistribuição do feature pack da [Estrutura do aplicativo da camada de dados](https://www.microsoft.com/download/details.aspx?id=42295).  Depois que a atualização for aplicada, todas as novas entradas de histórico usarão o valor listado para instance_id na tabela sysdac_instances_internal.  
  
Se você já tiver o problema com valores de instance_id incompatíveis, a única maneira de corrigir os valores incompatíveis é se conectar ao servidor como um usuário com privilégios para gravar no banco de dados MSDB e atualizar os valores de instance_id para correspondência.  Se houve vários registros e eventos não registrados do mesmo banco de dados, talvez seja necessário examinar a data/hora para ver quais registros correspondem aos valores atuais de instance_id.  
  
1.  Conecte-se ao servidor no SQL Server Management Studio usando um logon que tenha permissões de atualização para o MSDB.  
  
2.  Abra uma nova consulta usando o banco de dados MSDB.  
  
3.  Execute esta consulta para ver todas as instâncias de dac ativas.  Localize a instância que você deseja corrigir e anote o instance_id:  
  
    `select * from` sysdac_instances_internal  
  
4.  Execute esta consulta para ver todas as entradas de histórico:  
  
    `select * from` sysdac_history_internal  
  
5.  Identifique as linhas que devem corresponder à instância que você está solucionando  
  
6.  Atualize o valor de sysdac_history_internal.instance_id para o valor que você observou na etapa 3 (na tabela sysdac_instances_internal):  
  
    `update` sysdac_history_internal `set` instance_id = '\<valor da etapa 3\>' `where` \<expressão que corresponde às linhas que deseja atualizar\>  
  
![Ícone de seta usado com o link Voltar ao início](../release-notes/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Início](#top)  
  
## <a name="SSRS"></a>4.0 Reporting Services  
  
### <a name="41-the-sql-server-2012-reporting-services-native-mode-report-server-cannot-run-side-by-side-with-sql-server-2014-reporting-services-sharepoint-components"></a>4.1 O servidor de relatório do SQL Server 2012 Reporting Services no modo nativo não pode ser executado lado a lado com componentes do SQL Server 2014 Reporting Services SharePoint  
**Problema:** o serviço do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]Windows SQL Server Reporting Services (ReportingServicesService.exe) no modo nativo falha ao iniciar se houver componentes do SharePoint [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] instalados no mesmo servidor.  
  
**Solução alternativa:** Desinstalar os componentes do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] SharePoint e reiniciar o serviço do Microsoft SQL Server 2012 Reporting Services do Windows.  
  
**Mais Informações:**  
  
[!INCLUDE[ssSQL11](../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] O modo nativo não pode ser executado lado a lado com os seguintes itens:  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Suplemento para produtos do SharePoint  
  
-   [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Serviço Compartilhado do SharePoint  
  
A instalação lado a lado impede que o Serviço do Windows no modo nativo do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] inicie. Exemplos de mensagens de erro que aparecerão no Log de Eventos do Windows:  
  
```  
Log Name:   Application  
Source:          Report Server (<SQL instance ID>)  
Event ID:        117  
Task Category:   Startup/Shutdown  
Level:           Error  
Keywords:        Classic  
Description:     The report server database is an invalid version.  
  
Log Name:      Application  
Source:        Report Server (<SQL instance ID>)  
Event ID:      107  
Task Category: Management  
Level:         Error  
Keywords:      Classic  
Description:   Report Server (DENALI) cannot connect to the report server database.  
```  
  
Para obter mais informações, consulte [Dicas, truques e soluções de problemas do SQL Server 2014 Reporting Services](http://go.microsoft.com/fwlink/?LinkID=391254).  
  
### <a name="42-required-upgrade-order-for-multi-node-sharepoint-farm-to-sql-server-2014-reporting-services"></a>4.2 A ordem de atualização necessária para a farm do SharePoint com vários nós do SQL Server 2014 Reporting Services  
**Problema:** a renderização de relatório em uma farm de vários nós falha se as instâncias do Serviço Compartilhado do SharePoint [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] forem atualizadas antes de todas as instâncias do suplemento do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para os produtos do SharePoint.  
  
**Solução:** em uma farm do SharePoint com vários nós:  
  
1.  Atualize primeiro todas as instâncias do suplemento do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para os produtos do SharePoint.  
  
2.  Em seguida, atualize todas as instâncias do serviço compartilhado do SharePoint [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .  
  
Para obter mais informações, consulte [Dicas, truques e soluções de problemas do SQL Server 2014 Reporting Services](http://go.microsoft.com/fwlink/?LinkID=391254)  
  
![Ícone de seta usado com o link Voltar ao início](../release-notes/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Início](#top)  
  
## <a name="AzureVM"></a>5.0 SQL Server 2014 RTM em máquinas virtuais do Microsoft Azure  
  
### <a name="51-the-add-azure-replica-wizard-returns-an-error-when-configuring-an-availability-group-listener-in-windows-azure"></a>5.1 O assistente para adicionar réplica do Azure retorna um erro ao configurar um ouvinte do grupo de disponibilidade no Windows Azure  
**Problema:** Se um grupo de disponibilidade tiver um ouvinte, o assistente para adicionar réplica do Azure retornará um erro ao tentar configurar o ouvinte no Windows Azure.  
  
Isso se deve ao fato dos ouvintes do grupo de disponibilidade exigirem a atribuição de um endereço IP em cada sub-rede que hospeda réplicas do grupo de disponibilidade, inclusive a sub-rede do Azure.  
  
**Solução alternativa:**  
  
1.  Na página do ouvinte, atribua um endereço IP estático livre na sub-rede do Azure que hospedará a réplica do grupo de disponibilidade para o ouvinte do grupo de disponibilidade.  
  
    Isso permitirá que o assistente conclua a adição da réplica no Windows Azure.  
  
2.  Ao concluir o assistente, você precisará concluir a configuração de ouvinte no Windows Azure conforme descrito em [Configuração de ouvinte para grupos de disponibilidade AlwaysOn no Windows Azure](http://msdn.microsoft.com/library/dn376546.aspx)  
  
![Ícone de seta usado com o link Voltar ao início](../release-notes/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Início](#top)  
  
## <a name="SSAS"></a>6.0 Analysis Services  
  
### <a name="61-msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2010-new-farm-configured-with-sql-server-2014"></a>6.1 O MSOLAP.5 deve ser baixado, instalado e registrado para um novo farm do SharePoint 2010 configurado com o SQL Server 2014  
**Problema:**  
  
-   Para um farm do SharePoint 2010 configurado com uma implantação do SQL Server 2014 RTM, as pastas de trabalho PowerPivot não podem se conectar aos modelos de dados porque o provedor referenciado na cadeia de conexão não está instalado.  
  
**Solução alternativa:**  
  
1.  Baixe o provedor MSOLAP.5 do [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] Feature Pack. Instale o provedor nos servidores de aplicativos que executam os Serviços do Excel. Para obter mais informações, consulte a seção "Microsoft Analysis Services OLE DB Provider para Microsoft SQL Server 2012 SP1" [Microsoft SQL Server 2012 SP1 Feature Pack](http://www.microsoft.com/download/details.aspx?id=35580).  
  
2.  Registre o MSOLAP.5 como um provedor confiável em Serviços do Excel do SharePoint. Para obter mais informações, consulte [Adicionar MSOLAP.5 como um provedor de dados confiável em Serviços do Excel](http://technet.microsoft.com/library/hh758436.aspx).  
  
**Mais Informações:**  
  
-   O[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] inclui MSOLAP.6. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] e do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssGemini](../includes/ssgemini-md.md)] usam MSOLAP.5. Se o MSOLAP.5 não estiver instalado no computador que executa os Serviços do Excel, os Serviços do Excel não poderão carregar os modelos de dados.  
  
### <a name="62-msolap5-must-be-downloaded-installed-and-registered-for-a-sharepoint-2013-new-farm-configured-with-sql-server-2014"></a>6.2 O MSOLAP.5 deve ser baixado, instalado e registrado para um novo farm do SharePoint 2013 configurado com o SQL Server 2014  
**Problema:**  
  
-   Para um farm do SharePoint 2013 configurada com uma implantação do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] , as pastas de trabalho do Excel que referenciam o provedor MSOLAP.5 não podem se conectar aos modelos de dados da tabela porque o provedor referenciado na cadeia de conexão não está instalado.  
  
**Solução alternativa:**  
  
1.  Baixe o provedor MSOLAP.5 do [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)] Feature Pack. Instale o provedor nos servidores de aplicativos que executam os Serviços do Excel. Para obter mais informações, consulte a seção "Microsoft Analysis Services OLE DB Provider para Microsoft SQL Server 2012 SP1" [Microsoft SQL Server 2012 SP1 Feature Pack](http://www.microsoft.com/download/details.aspx?id=35580).  
  
2.  Registre o MSOLAP.5 como um provedor confiável em Serviços do Excel do SharePoint. Para obter mais informações, consulte [Adicionar MSOLAP.5 como um provedor de dados confiável em Serviços do Excel](http://technet.microsoft.com/library/hh758436.aspx).  
  
**Mais Informações:**  
  
-   O[!INCLUDE[ssSQL14](../includes/sssql14-md.md)] inclui MSOLAP.6. mas as pastas de trabalho PowerPivot do SQL Server 2014 usam MSOLAP.5. Se o MSOLAP.5 não estiver instalado no computador que executa os Serviços do Excel, os Serviços do Excel não poderão carregar os modelos de dados.  
  
### <a name="63-corrupt-data-refresh-schedules"></a>6.3 Agenda de atualização de dados corrompidos  
**Problema:**  
  
-   Você atualiza uma agenda de atualização e a agenda torna-se corrompida e inutilizável.  
  
**Solução alternativa:**  
  
1.  No Microsoft Excel, desmarque as propriedades avançadas personalizadas. Consulte a seção “Solução alternativa” do seguinte artigo da base de dados de conhecimento [KB 2927748](http://support.microsoft.com/kb/2927748).  
  
**Mais Informações:**  
  
-   Quando você atualiza uma agenda de atualização de dados para uma pasta de trabalho, se o comprimento serializado da agenda de atualização for menor que a agenda original, o tamanho do buffer não será atualizado corretamente e as novas informações de agenda serão mescladas com as antigas informações de agenda resultando em uma agenda corrompida.  
  
![Ícone de seta usado com o link Voltar ao início](../release-notes/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Início](#top)  
  
## <a name="DQS"></a>7.0 Data Quality Services  
  
### <a name="71-no-cross-version-support-for-data-quality-services-in-master-data-services"></a>7.1 Não há suporte entre versões para o Data Quality Services no Master Data Services  
**Problema:** Os cenários a seguir não têm suporte:  
  
-   Master Data Services 2014 hospedado em um banco de dados do Mecanismo de Banco de Dados do SQL Server no SQL Server 2012 com o Data Quality Services 2012 instalado.  
  
-   Master Data Services 2012 hospedado em um banco de dados do Mecanismo de Banco de Dados do SQL Server no SQL Server 2014 com o Data Quality Services 2014 instalado.  
  
**Solução:** Use a mesma versão do Master Data Services que o banco de dados do mecanismo de banco de dados e o Data Quality Services.  
  
![Ícone de seta usado com o link Voltar ao início](../release-notes/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Início](#top)  
  
## <a name="UA"></a>8.0 Problemas do supervisor de atualização  
  
### <a name="81--sql-server-2014-upgrade-advisor-reports-irrelevant-upgrade-issues-for-sql-server-reporting-services"></a>8.1 O supervisor de atualização do SQL Server 2014 relata problemas de atualização irrelevantes do SQL Server Reporting Services  
**Problema:** o supervisor de atualização do SQL Server (SSUA) fornecido com o SQL Server 2014 relata vários erros ao analisar o servidor do SQL Server Reporting Services.  
  
**Solução:** Esse problema é corrigido no supervisor de atualização do SQL Server fornecido no [SQL Server 2014 Feature Pack para SSUA](http://go.microsoft.com/fwlink/?LinkID=306709).  
  
### <a name="82--sql-server-2014-upgrade-advisor-reports-an-error-when-analyzing-sql-server-integration-services-server"></a>8.2 O supervisor de atualização do SQL Server 2014 relata um erro ao analisar o servidor do SQL Server Integration Services  
**Problema:** o Supervisor de Atualização do SQL Server (SSUA) fornecido com a mídia SQL Server 2014 relata um erro ao analisar o servidor do SQL Server Integration Services.  O erro que é exibido para o usuário é:  
  
```  
The installed version of Integration Services does not support Upgrade Advisor.   
The assembly information is "Microsoft.SqlServer.ManagedDTS, Version=11.0.0.0,   
Culture=neutral, PublicKeyToken=89845dcd8080cc91  
```  
  
**Solução:** Esse problema é corrigido no supervisor de atualização do SQL Server fornecido no [SQL Server 2014 Feature Pack para SSUA](http://go.microsoft.com/fwlink/?LinkID=306709).  
  
![Ícone de seta usado com o link Voltar ao início](../release-notes/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Início](#top)  
  


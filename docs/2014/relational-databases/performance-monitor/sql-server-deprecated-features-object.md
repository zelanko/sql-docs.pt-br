---
title: SQL Server, objeto Recursos Preteridos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLServer:Deprecated Features
- performance counters [SQL Server], deprecated features
- deprecation [SQL Server], performance counters
- Deprecated Features object
ms.assetid: e95de9d6-c950-41cd-8aaa-be529c6de198
caps.latest.revision: 58
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e093deb7505ecd6bf7b5afd0b66da2791f34cc51
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116932"
---
# <a name="sql-server-deprecated-features-object"></a>SQL Server, objeto Recursos Preteridos
  O objeto SQLServer:Recursos Preteridos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece um contador para monitorar recursos designados como preteridos. Em cada caso, o contador fornece uma contagem de uso que lista o número de vezes em que o recurso preterido foi encontrado desde a última inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A tabela a seguir descreve as instâncias de contadores dos Recursos Preteridos do SQL Server.  
  
|Instâncias do contador de Recursos Preteridos do SQL Server|Description|  
|------------------------------------------------------|-----------------|  
|'#' e '##' como o nome de tabelas temporárias e procedimentos armazenados|Um identificador que não contém nenhum caractere diferente de # foi encontrado. Use pelo menos um caractere adicional. Ocorre uma vez por compilação.|  
|sintaxe '::' de chamada de função|A sintaxe de chamada de função :: foi encontrada para uma função com valor de tabela. Substituir pelo `SELECT column_list FROM`  *\< nome_da_função >*`()`. Por exemplo, substitua `SELECT * FROM ::fn_virtualfilestats(2,1)`por `SELECT * FROM sys.fn_virtualfilestats(2,1)`. Ocorre uma vez por compilação.|  
|'@' e nomes que começam com '@@' como identificadores [!INCLUDE[tsql](../../includes/tsql-md.md)]|Um identificador que começa com @ ou @@ foi encontrado. Não use @, @@ ou nomes que comecem com @@ como identificadores. Ocorre uma vez por compilação.|  
|ADDING TAPE DEVICE|O recurso preterido sp_addumpdevice'`tape`' foi encontrado. Use sp_addumpdevice'`disk`' em vez disso. Ocorre uma vez por uso.|  
|Permissão ALL|Número total de vezes que a sintaxe GRANT ALL, DENY ALL ou REVOKE ALL foi encontrada. Modifique a sintaxe para negar permissões específicas. Ocorre uma vez por consulta.|  
|ALTER DATABASE WITH TORN_PAGE_DETECTION|Número total de horas que a opção TORN_PAGE_DETECTION do recurso preterido de ALTER DATABASE foi usada desde a inicialização da instância de servidor. Em seu lugar, use a sintaxe PAGE_VERIFY. Ocorre uma vez por uso em uma instrução DDL.|  
|ALTER LOGIN WITH SET CREDENTIAL|As sintaxes de recurso preterido ALTER LOGIN WITH SET CREDENCIAL ou ALTER LOGIN WITH NO CREDENTIAL foram encontradas. Em seu lugar, use as sintaxes ADD ou DROP CREDENCIAL. Ocorre uma vez por compilação.|  
|Azeri_Cyrilllic_90|Evento que ocorre uma vez por inicialização de banco de dados e uma vez por uso de agrupamento. Planeje a modificação de aplicativos que usam este agrupamento.|  
|Azeri_Latin_90|Evento que ocorre uma vez por inicialização de banco de dados e uma vez por uso de agrupamento. Planeje a modificação de aplicativos que usam este agrupamento.|  
|BACKUP DATABASE ou LOG TO TAPE|O recurso preterido BACKUP { DATABASE &#124; LOG } TO TAPE ou BACKUP { DATABASE &#124; LOG } TO *device_that_is_a_tape* foi encontrado.<br /><br /> Em seu lugar, use { DATABASE &#124; LOG } TO DISK ou BACKUP { DATABASE &#124; LOG } TO *device_that_is_a_disk*. Ocorre uma vez por uso.|  
|BACKUP DATABASE ou LOG WITH MEDIAPASSWORD|Os recursos preteridos BACKUP DATABASE WITH MEDIAPASSWORD ou BACKUP LOG WITH MEDIAPASSWORD foram encontrados. Não use WITH MEDIAPASSWORD.|  
|BACKUP DATABASE ou LOG WITH PASSWORD|Os recursos preteridos BACKUP DATABASE WITH PASSWORD ou BACKUP LOG WITH PASSWORD foram encontrados. Não use WITH PASSWORD.|  
|COMPUTE [BY]|As sintaxes COMPUTE ou COMPUTE BY foram encontradas. Refaça a consulta para usar GROUP BY com ROLLUP. Ocorre uma vez por compilação.|  
|CREATE FULLTEXT CATLOG IN PATH|Uma instrução CREATE FULLTEXT CATLOG com a cláusula IN PATH foi encontrada. Esta cláusula não tem nenhum efeito nesta versão do SQL Server. Ocorre uma vez por uso.|  
|CREATE TRIGGER WITH APPEND|A instrução CREATE TRIGGER com a cláusula WITH APPEND foi encontrada. Recrie o gatilho inteiro. Ocorre uma vez por uso em uma instrução DDL.|  
|CREATE_DROP_DEFAULT|As sintaxes CREATE DEFAULT ou DROP DEFAULT foram encontradas. Reescreva o comando usando a opção DEFAULT de CREATE TABLE ou ALTER TABLE. Ocorre uma vez por compilação.|  
|CREATE_DROP_RULE|A sintaxe CREATE RULE foi encontrada. Reescreva o comando usando restrições. Ocorre uma vez por compilação.|  
|Tipos de dados: texto ntext ou imagem|Os tipos de dados `text`, `ntext` ou `image` foram encontrados. Reescreva os aplicativos para usar o `varchar(max)` tipo de dados e removido `text`, `ntext`, e `image` sintaxe de tipo de dados. Ocorre uma vez por consulta.|  
|Nível de compatibilidade 80 do banco de dados|O número total de vezes que um banco de dados foi alterado para o nível de compatibilidade 80. Planeje atualizar o banco de dados e o aplicativo antes da próxima versão. Também ocorre quando se inicia um banco de dados em nível de compatibilidade 80.|  
|Nível de compatibilidade 90 do banco de dados|O número total de vezes que um banco de dados foi alterado para o nível de compatibilidade 90. Planeje atualizar o banco de dados e o aplicativo para uma versão futura. Também ocorre quando se inicia um banco de dados em nível de compatibilidade 90.|  
|DATABASE_MIRRORING|Referencia a recurso de espelhamento de banco de dados foi encontrado. Planeje atualizar para os Grupos de Disponibilidade AlwaysOn ou, se você estiver executando uma edição de SQL Server que não suporte Grupos de Disponibilidade AlwaysOn, planeje migrar para envio de logs.|  
|database_principal_aliases|Referências ao recurso preterido  sys.database_principal_aliases foram encontradas. Use funções em vez de aliases. Ocorre uma vez por compilação.|  
|DATABASEPROPERTY|Uma instrução com referência a DATABASEPROPERTY. Atualize a instrução DATABASEPROPERTY para DATABASEPROPERTYEX. Ocorre uma vez por compilação.|  
|DATABASEPROPERTYEX('IsFullTextEnabled')|Uma instrução fez referência à propriedade IsFullTextEnabled de DATABASEPROPERTYEX. O valor dessa propriedade não tem nenhum efeito. Os bancos de dados de usuário são sempre habilitados para pesquisa de texto completo. Não use esta propriedade. Ocorre uma vez por compilação.|  
|DBCC [UN]PINTABLE|As instruções DBCC PINTABLE ou DBCC UNPINTABLE foram encontradas. Esta instrução não tem nenhum efeito e deve ser removida. Ocorre uma vez por consulta.|  
|DBCC DBREINDEX|A instrução DBCC DBREINDEX foi encontrada. Reescreva a instrução para usar a opção de REBUILD de ALTER INDEX. Ocorre uma vez por consulta.|  
|DBCC INDEXDEFRAG|A instrução DBCC INDEXDEFRAG foi encontrada. Reescreva a instrução para usar a opção REORGANIZE de ALTER INDEX. Ocorre uma vez por consulta.|  
|DBCC SHOWCONTIG|A instrução DBCC SHOWCONTIG foi encontrada. Consulte sys.dm_db_index_physical_stats para obter estas informações. Ocorre uma vez por consulta.|  
|A palavra-chave DEFAULT como um valor padrão|A sintaxe que usa a palavra-chave DEFAULT como valor padrão foi encontrada. Não use. Ocorre uma vez por compilação.|  
|Algoritmo de criptografia substituído|O algoritmo de criptografia preterido rc4 será removido na próxima versão do SQL Server. Evite usar esse recurso em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que o utilizam. O algoritmo RC4 é fraco e tem suporte somente para compatibilidade com versões anteriores. O novo material só pode ser criptografado por meio do algoritmo RC4 ou RC4_128 quando o banco de dados está no nível de compatibilidade 90 ou 100. (Não recomendável.) Use um algoritmo mais recente; por exemplo, um dos algoritmos AES. No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versões posteriores, o material criptografado por meio do algoritmo RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.|  
|Algoritmo DESX|A sintaxe que usa o algoritmo de criptografia DESX foi encontrada. Use outro algoritmo para criptografia. Ocorre uma vez por compilação.|  
|dm_fts_active_catalogs|O contador de dm_fts_active_catalogs sempre permanece em 0 porque algumas colunas da exibição de sys.dm_fts_active_catalogs não foram preteridas. Para monitorar uma coluna preterida, use o contador específico de coluna; por exemplo, dm_fts_active_catalogs.is_paused.|  
|dm_fts_active_catalogs.is_paused|A coluna is_paused da exibição de gerenciamento dinâmico [sys.dm_fts_active_catalogs](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-active-catalogs-transact-sql) foi encontrada. Evite usar esta coluna. Ocorre toda vez que a instância de servidor detecta uma referência à coluna.|  
|dm_fts_active_catalogs.previous_status|A coluna previous_status da exibição de gerenciamento dinâmico de sys.dm_fts_active_catalogs foi encontrada. Evite usar esta coluna. Ocorre toda vez que a instância de servidor detecta uma referência à coluna.|  
|dm_fts_active_catalogs.previous_status_description|A coluna previous_status_description da exibição de gerenciamento dinâmico de sys.dm_fts_active_catalogs foi encontrada. Evite usar esta coluna. Ocorre toda vez que a instância de servidor detecta uma referência à coluna.|  
|dm_fts_active_catalogs.row_count_in_thousands|A coluna row_count_in_thousands da exibição de gerenciamento dinâmico sys.dm_fts_active_catalogs foi encontrada. Evite usar esta coluna. Ocorre toda vez que a instância de servidor detecta uma referência à coluna.|  
|dm_fts_active_catalogs.status|A coluna status da exibição de gerenciamento dinâmico de sys.dm_fts_active_catalogs foi encontrada. Evite usar esta coluna. Ocorre toda vez que a instância de servidor detecta uma referência à coluna.|  
|dm_fts_active_catalogs.status_description|A coluna status_description da exibição de gerenciamento dinâmico de sys.dm_fts_active_catalogs foi encontrada. Evite usar esta coluna. Ocorre toda vez que a instância de servidor detecta uma referência à coluna.|  
|dm_fts_active_catalogs.worker_count|A coluna worker_count da exibição de gerenciamento dinâmico de sys.dm_fts_active_catalogs foi encontrada. Evite usar esta coluna. Ocorre toda vez que a instância de servidor detecta uma referência à coluna.|  
|dm_fts_memory_buffers|O contador dm_fts_memory_buffers sempre permanece em 0 porque a maioria das colunas da exibição sys.dm_fts_memory_buffers não foi preterida. Para monitorar a coluna preterida, use o contador específico de coluna: dm_fts_memory_buffers.row_count.|  
|dm_fts_memory_buffers.row_count|A coluna row_count da exibição de gerenciamento dinâmico [sys.dm_fts_memory_buffers](/sql/relational-databases/system-dynamic-management-views/sys-dm-fts-memory-buffers-transact-sql) foi encontrada. Evite usar esta coluna. Ocorre toda vez que a instância de servidor detecta uma referência à coluna.|  
|DROP INDEX com nome de duas partes|A sintaxe DROP INDEX contida na sintaxe de formato *table_name.index_name* em DROP INDEX. Substitua a sintaxe *index_name* ON *table_name* na instrução DROP INDEX. Ocorre uma vez por compilação.|  
|EXT_CREATE_ALTER_SOAP_ENDPOINT|As instruções CREATE ou ALTER ENDPOINT com a opção FOR SOAP foram encontradas. Os XML Web Services nativos foram preteridos. Em vez disso, use o WCF (Windows Communications Foundation) ou o ASP.NET.|  
|EXT_endpoint_webmethods|sys.endpoint_webmethods foi encontrado. Os XML Web Services nativos foram preteridos. Em vez disso, use o WCF (Windows Communications Foundation) ou o ASP.NET.|  
|EXT_soap_endpoints|sys.soap_endpoints foi encontrado. Os XML Web Services nativos foram preteridos. Em vez disso, use o WCF (Windows Communications Foundation) ou o ASP.NET.|  
|EXTPROP_LEVEL0TYPE|TYPE foi encontrado em level0type. Em seu lugar, use SCHEMA como level0type e TYPE como level1type. Ocorre uma vez por consulta.|  
|EXTPROP_LEVEL0USER|Um USER de level0type quando level1type também foi especificado. Use USER somente como level0type para propriedades estendidas diretamente em um usuário. Ocorre uma vez por consulta.|  
|FASTFIRSTROW|A sintaxe FASTFIRSTROW foi encontrada. Reescreva as instruções para usar a sintaxe OPTION (FAST *n*). Ocorre uma vez por compilação.|  
|FILE_ID|A sintaxe FILE_ID foi encontrada. Reescreva as instruções para usar FILE_IDEX. Ocorre uma vez por compilação.|  
|fn_get_sql|A função fn_get_sql foi compilada. Em vez disso, use sys.dm_exec_sql_text. Ocorre uma vez por compilação.|  
|fn_servershareddrives|A função fn_servershareddrives foi compilada. Use sys.dm_io_cluster_shared_drives. Ocorre uma vez por compilação.|  
|fn_virtualservernodes|A função fn_virtualservernodes foi compilada. Use sys.dm_os_cluster_nodes. Ocorre uma vez por compilação.|  
|fulltext_catalogs|O contador de fulltext_catalogs sempre permanece em 0 porque algumas colunas da exibição sys.fulltext_catalogs não são preteridas. Para monitorar uma coluna preterida, use o contador específico da coluna; por exemplo, fulltext_catalogs.data_space_id. Ocorre toda vez que a instância de servidor detecta uma referência à coluna.|  
|fulltext_catalogs.data_space_id|A coluna data_space_id da exibição de catálogo [sys.fulltext_catalogs](/sql/relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql) foi encontrada. Não use esta coluna. Ocorre toda vez que a instância de servidor detecta uma referência à coluna.|  
|fulltext_catalogs.file_id|A coluna file_id da exibição do catálogo sys.fulltext_catalogs foi encontrada. Não use esta coluna. Ocorre toda vez que a instância de servidor detecta uma referência à coluna.|  
|fulltext_catalogs.path|A coluna path da exibição do catálogo sys.fulltext_catalogs foi encontrada. Não use esta coluna. Ocorre toda vez que a instância de servidor detecta uma referência à coluna.|  
|FULLTEXTCATALOGPROPERTY('LogSize')|A propriedade LogSize da função FULLTEXTCATALOGPROPERTY foi encontrada. Evite usar esta propriedade.|  
|FULLTEXTCATALOGPROPERTY('PopulateStatus')|A propriedade PopulateStatus da função FULLTEXTCATALOGPROPERTY foi encontrada. Evite usar esta propriedade.|  
|FULLTEXTSERVICEPROPERTY('ConnectTimeout')|A propriedade ConnectTimeout da função FULLTEXTSERVICEPROPERTY foi encontrada. Evite usar esta propriedade.|  
|FULLTEXTSERVICEPROPERTY('DataTimeout')|A propriedade DataTimeout da função FULLTEXTSERVICEPROPERTY foi encontrada. Evite usar esta propriedade.|  
|FULLTEXTSERVICEPROPERTY('ResourceUsage')|A propriedade ResourceUsage da função FULLTEXTSERVICEPROPERTY foi encontrada. Evite usar esta propriedade.|  
|GROUP BY ALL|O número total de vezes que a sintaxe GROUP BY ALL foi encontrada. Modifique a sintaxe para agrupar de acordo com tabelas específicas.|  
|Híndi|Evento que ocorre uma vez por inicialização de banco de dados e uma vez por uso de agrupamento. Planeje a modificação de aplicativos que usam este agrupamento. Use Indic_General_90.|  
|Dica da tabela HOLDLOCK sem parênteses||  
|IDENTITYCOL|A sintaxe de INDENTITYCOL foi encontrada. Reescreva instruções para usar a sintaxe de identidade $. Ocorre uma vez por compilação.|  
|Lista de seleção de exibição indexada sem COUNT_BIG (\*)|A lista de seleção de uma exibição indexada de agregação deve conter COUNT_BIG (\*).|  
|INDEX_OPTION|As sintaxes CREATE TABLE, ALTER TABLE ou CREATE INDEX sem parênteses delimitando as opções foram encontradas. Reescreva a instrução para usar a sintaxe atual. Ocorre uma vez por consulta.|  
|INDEXKEY_PROPERTY|A sintaxe INDEXKEY_PROPERTY foi encontrada. Reescreva instruções para consultar sys.index_columns. Ocorre uma vez por compilação.|  
|Dicas TVF indiretas|A aplicação indireta de dicas de tabela à invocação de uma TVF (função com valor de tabela) com várias instruções através de uma exibição será removida em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|INSERT NULL em colunas TIMESTAMP|Um valor NULL foi inserido em uma coluna TIMESTAMP. Use um valor padrão. Ocorre uma vez por compilação.|  
|INSERT_HINTS||  
|Korean_Wansung_Unicode|Evento que ocorre uma vez por inicialização de banco de dados e uma vez por uso de agrupamento. Planeje a modificação de aplicativos que usam este agrupamento.|  
|Lithuanian_Classic|Evento que ocorre uma vez por inicialização de banco de dados e uma vez por uso de agrupamento. Planeje a modificação de aplicativos que usam este agrupamento.|  
|Macedônio|Evento que ocorre uma vez por inicialização de banco de dados e uma vez por uso de agrupamento. Planeje a modificação de aplicativos que usam este agrupamento. Use Macedonian_FYROM_90.|  
|MODIFY FILEGROUP READONLY|A sintaxe MODIFY FILEGROUP READONLY foi encontrada. Reescreva as instruções para usar a sintaxe READ_ONLY. Ocorre uma vez por compilação.|  
|MODIFY FILEGROUP READWRITE|A sintaxe MODIFY FILEGROUP READWRITE foi encontrada. Reescreva as instruções para usar a sintaxe READ_WRITE. Ocorre uma vez por compilação.|  
|Nome de coluna com mais de duas partes|Uma consulta usou um nome de 3 partes ou de 4 partes na lista de colunas. Altere a consulta para usar os nomes de 2 partes em conformidade com o padrão. Ocorre uma vez por compilação.|  
|Várias dicas de tabela sem vírgula|Um espaço foi usado como o separador entre dicas de tabela. Use uma vírgula. Ocorre uma vez por compilação.|  
|NOLOCK ou READUNCOMMITTED em UPDATE ou DELETE|NOLOCK ou READUNCOMMITTED foram encontradas na cláusula FROM de uma instrução UPDATE ou DELETE. Remova as dicas de tabela NOLOCK ou READUNCOMMITTED da cláusula FROM.|  
|Operadores de junção externa não ANSI *= ou =\*|Uma instrução que usa a sintaxe de junção *= ou =\* foi encontrada. Reescreva a instrução para usar a sintaxe de junção ANSI. Ocorre uma vez por compilação.|  
|numbered_stored_procedures||  
|numbered_procedure_parameters|Referencias a sys.numbered_procedure_parameters preterido foram encontradas. Não use. Ocorre uma vez por compilação.|  
|numbered_procedures|Referencias a sys.numbered_procedures preterido foram encontradas. Não use. Ocorre uma vez por compilação.|  
|RAISEERROR em estilo antigo|A sintaxe preterida RAISERROR (Formato: cadeia de inteiros RAISERROR) foi encontrada. Reescreva a instrução usando a sintaxe RAISERROR atual. Ocorre uma vez por compilação.|  
|OLEDB para conexões ad hoc|SQLOLEDB não é um provedor com suporte. Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para conexões ad hoc.|  
|PERMISSIONS|Foram encontradas referencias à função intrínseca PERMISSIONS. Consulte sys.fn_my_permissions. Ocorre uma vez por consulta.|  
|ProcNums|A sintaxe ProcNums preterida foi encontrada. Reescreva as instruções para remover as referências. Ocorre uma vez por compilação.|  
|READTEXT|A sintaxe READTEXT foi encontrada. Reescreva os aplicativos para usar o tipo de dados `varchar(max)` e as sintaxes de tipos de dados removidas `text`. Ocorre uma vez por consulta.|  
|RESTORE DATABASE ou LOG WITH DBO_ONLY|A sintaxe RESTORE ... WITH DBO_ONLY foi encontrada. Em vez disso, use RESTORE … RESTRICTED_USER.|  
|RESTORE DATABASE ou LOG WITH MEDIAPASSWORD|A sintaxe RESTORE ... WITH MEDIAPASSWORD foi encontrada. WITH MEDIAPASSWORD fornece pouca segurança e deve ser removida.|  
|RESTORE DATABASE ou LOG WITH PASSWORD|A sintaxe RESTORE ... WITH PASSWORD foi encontrada. WITH PASSWORD fornece pouca segurança e deve ser removida.|  
|Retornando resultados de gatilho|Este evento ocorre uma vez por invocação de gatilho. Reescreva o gatilho de forma a não retornar conjuntos de resultados.|  
|ROWGUIDCOL|A sintaxe ROWGUIDCOL foi encontrada. Reescreva as instruções para usar a sintaxe $rowguid. Ocorre uma vez por compilação.|  
|SET ANSI_NULLS OFF|A sintaxe SET ANSI_NULLS OFF foi encontrada. Remova esta sintaxe preterida. Ocorre uma vez por compilação.|  
|SET ANSI_PADDING OFF|A sintaxe SET ANSI_PADDING OFF foi encontrada. Remova esta sintaxe preterida. Ocorre uma vez por compilação.|  
|SET CONCAT_NULL_YIELDS_NULL OFF|A sintaxe SET CONCAT_NULL_YIELDS_NULL OFF foi encontrada. Remova esta sintaxe preterida. Ocorre uma vez por compilação.|  
|SET DISABLE_DEF_CNST_CHK|A sintaxe SET DISABLE_DEF_CNST_CHK foi encontrada. Ela não tem efeito algum. Remova esta sintaxe preterida. Ocorre uma vez por compilação.|  
|SET FMTONLY ON|A sintaxe SET FMTONLY foi encontrada. Remova esta sintaxe preterida. Ocorre uma vez por compilação.|  
|SET OFFSETS|A sintaxe SET OFFSETS foi encontrada. Remova esta sintaxe preterida. Ocorre uma vez por compilação.|  
|SET REMOTE_PROC_TRANSACTIONS|A sintaxe SET REMOTE_PROC_TRANSACTIONS foi encontrada. Remova esta sintaxe preterida. Use servidores vinculados e sp_serveroption.|  
|SET ROWCOUNT|A sintaxe SET ROWCOUNT em uma instrução DELETE, INSERT ou UPDATE foi encontrada. Reescreva a instrução usando TOP. Ocorre uma vez por compilação.|  
|SETUSER|A instrução SET USER foi encontrada. Em vez disso, use EXECUTE AS. Ocorre uma vez por consulta.|  
|sp_addapprole|O procedimento sp_addapprole foi encontrado. Em vez disso, use CREATE APPLICATION ROLE. Ocorre uma vez por consulta.|  
|sp_addextendedproc|O procedimento sp_addextendedproc foi encontrado. Em vez disso, use CLR. Ocorre uma vez por compilação.|  
|sp_addlogin|O procedimento sp_addlogin foi encontrado. Em vez disso, use CREATE LOGIN. Ocorre uma vez por consulta.|  
|sp_addremotelogin|O procedimento sp_addremotelogin foi encontrado. Em vez disso, use servidores vinculados.|  
|sp_addrole|O procedimento sp_addrole foi encontrado. Em vez disso, use CREATE ROLE. Ocorre uma vez por consulta.|  
|sp_addserver|O procedimento sp_addserver foi encontrado. Em vez disso, use servidores vinculados.|  
|sp_addtype|O procedimento sp_addtype foi encontrado. Em vez disso, use CREATE TYPE. Ocorre uma vez por compilação.|  
|sp_adduser|O procedimento sp_adduser foi encontrado. Em vez disso, use CREATE USER. Ocorre uma vez por consulta.|  
|sp_approlepassword|O procedimento sp_approlepassword foi encontrado. Em vez disso, use ALTER APPLICATION ROLE. Ocorre uma vez por consulta.|  
|sp_attach_db|O procedimento sp_attach_db foi encontrado. Em vez disso, use CREATE DATABASE FOR ATTACH. Ocorre uma vez por consulta.|  
|sp_attach_single_file_db|O procedimento sp_single_file_db foi encontrado. Em vez disso, use CREATE DATABASE FOR ATTACH_REBUILD_LOG. Ocorre uma vez por consulta.|  
|sp_bindefault|O procedimento sp_bindefault foi encontrado. Em vez disso, use a palavra-chave DEFAULT de ALTER TABLE ou CREATE TABLE. Ocorre uma vez por compilação.|  
|sp_bindrule|O procedimento sp_bindrule foi encontrado. Em vez disso, use restrições de verificação. Ocorre uma vez por compilação.|  
|sp_bindsession|O procedimento sp_bindsession foi encontrado. Em vez disso, use MARS (vários conjuntos de resultados ativos) ou transações distribuídas. Ocorre uma vez por compilação.|  
|sp_certify_removable|O procedimento sp_certify_removable foi encontrado. Use sp_detach_db em seu lugar. Ocorre uma vez por consulta.|  
|sp_changeobjectowner|O procedimento sp_changeobjectowner foi encontrado. Em vez disso, use ALTER SCHEMA ou ALTER AUTHORIZATION. Ocorre uma vez por consulta.|  
|sp_change_users_login|O procedimento sp_change_users_login foi encontrado. Em vez disso, use ALTER USER. Ocorre uma vez por consulta.|  
|sp_configure 'allow updates'|A opção allow updates de sp_configure foi encontrada. As tabelas do sistema não são mais atualizáveis. Não use. Ocorre uma vez por consulta.|  
|sp_configure 'disallow results from triggers'|A opção disallow result sets from triggers de sp_configure foi encontrada. Para desabilitar conjuntos de resultados de gatilhos, use sp_configure para definir a opção como 1. Ocorre uma vez por consulta.|  
|sp_configure 'ft crawl bandwidth (max)'|A opção ft crawl bandwidth (max) de sp_configure foi encontrada. Não use. Ocorre uma vez por consulta.|  
|sp_configure 'ft crawl bandwidth (min)'|A opção ft crawl bandwidth (min) de sp_configure foi encontrada. Não use. Ocorre uma vez por consulta.|  
|sp_configure 'ft notify bandwidth (max)'|A opção ft notify bandwidth (max) de sp_configure foi encontrada. Não use. Ocorre uma vez por consulta.|  
|sp_configure 'ft notify bandwidth (min)'|A opção ft notify bandwidth (min) de sp_configure foi encontrada. Não use. Ocorre uma vez por consulta.|  
|sp_configure 'locks'|A opção locks de sp_configure foi encontrada. Não é mais possível configurar locks. Não use. Ocorre uma vez por consulta.|  
|sp_configure 'open objects'|A opção open objects de sp_configure foi encontrada. Não é mais possível configurar o número de open objects. Não use. Ocorre uma vez por consulta.|  
|sp_configure 'priority boost'|A opção priority boost de sp_configure foi encontrada. Não use. Ocorre uma vez por consulta. Usar a opção start/high… program.exe do Windows.|  
|sp_configure 'remote proc trans'|A opção remote proc trans option de sp_configure foi encontrada. Não use. Ocorre uma vez por consulta.|  
|sp_configure 'set working set size'|A opção set working set size de sp_configure foi encontrada. Não é mais possível configurar working set size. Não use. Ocorre uma vez por consulta.|  
|sp_control_dbmasterkey_password|O procedimento armazenado sp_control_dbmasterkey_password não verifica se uma chave mestra existe. Isso é permitido para compatibilidade com versões anteriores, mas exibe um aviso. Este comportamento é preterido. Em uma versão futura, deverá existir uma chave mestra e a senha usada no procedimento armazenado sp_control_dbmasterkey_password deverá ser a mesma senha usada para criptografar a chave mestra do banco de dados.|  
|sp_create_removable|O procedimento sp_create_removable foi encontrado. Em vez disso, use CREATE DATABASE. Ocorre uma vez por consulta.|  
|sp_db_vardecimal_storage_format|O uso de `vardecimal` o formato de armazenamento foi encontrado. Em vez disso, use a compactação de dados.|  
|sp_dbcmptlevel|O procedimento sp_dbcmptlevel foi encontrado. Em vez disso, use ALTER DATABASE … SET COMPATIBILITY_LEVEL. Ocorre uma vez por consulta.|  
|sp_dbfixedrolepermission|O procedimento sp_dbfixedrolepermission foi encontrado. Não use. Ocorre uma vez por consulta.|  
|sp_dboption|O procedimento sp_dboption foi encontrado. Em vez disso, use ALTER DATABASE e DATABASEPROPERTYEX. Ocorre uma vez por compilação.|  
|sp_dbremove|O procedimento sp_dbremove foi encontrado. Em vez disso, use DROP DATABASE. Ocorre uma vez por consulta.|  
|sp_defaultdb|O procedimento sp_defaultdb foi encontrado. Em vez disso, use ALTER LOGIN. Ocorre uma vez por compilação.|  
|sp_defaultlanguage|O procedimento sp_defaultlanguage foi encontrado. Em vez disso, use ALTER LOGIN. Ocorre uma vez por compilação.|  
|sp_denylogin|O procedimento sp_denylogin foi encontrado. Em vez disso, use ALTER LOGIN DISABLE. Ocorre uma vez por consulta.|  
|sp_depends|O procedimento sp_depends foi encontrado. Use sys.dm_sql_referencing_entities e sys.dm_sql_referenced_entities em vez disso. Ocorre uma vez por consulta.|  
|sp_detach_db @keepfulltextindexfile|O argumento @keepfulltextindexfile foi encontrado em uma instrução sp_detach_db. Não use este argumento.|  
|sp_dropalias|O procedimento sp_dropalias foi encontrado. Substitua aliases por uma combinação de contas de usuário e funções de banco de dados. Use sp_dropalias para remover aliases em bancos de dados atualizados. Ocorre uma vez por compilação.|  
|sp_dropapprole|O procedimento sp_dropapprole foi encontrado. Em vez disso, use DROP APPLICATION ROLE. Ocorre uma vez por consulta.|  
|sp_dropextendedproc|O procedimento sp_dropextendedproc foi encontrado. Em vez disso, use CLR. Ocorre uma vez por compilação.|  
|sp_droplogin|O procedimento sp_droplogin foi encontrado. Em vez disso, use DROP LOGIN. Ocorre uma vez por consulta.|  
|sp_dropremotelogin|O procedimento sp_dropremotelogin foi encontrado. Em vez disso, use servidores vinculados.|  
|sp_droprole|O procedimento sp_droprole foi encontrado. Em vez disso, use DROP ROLE. Ocorre uma vez por consulta.|  
|sp_droptype|O procedimento sp_droptype foi encontrado. Em vez disso, use DROP TYPE.|  
|sp_dropuser|O procedimento sp_dropuser foi encontrado. Em vez disso, use DROP USER. Ocorre uma vez por consulta.|  
|sp_estimated_rowsize_reduction_for_vardecimal|O uso de `vardecimal` o formato de armazenamento foi encontrado. Use compactação de dados e sp_estimate_data_compression_savings em vez disso.|  
|sp_fulltext_catalog|O procedimento sp_fulltext_catalog foi encontrado. Em vez disso, use CREATE/ALTER/DROP FULLTEXT CATALOG. Ocorre uma vez por compilação.|  
|sp_fulltext_column|O procedimento sp_fulltext_column foi encontrado. Em vez disso, use ALTER FULLTEXT INDEX. Ocorre uma vez por compilação.|  
|sp_fulltext_database|O procedimento sp_fulltext_database foi encontrado. Em vez disso, use ALTER DATABASE. Ocorre uma vez por compilação.|  
|sp_fulltext_service @action=clean_up|A opção clean_up do procedimento sp_fulltext_service foi encontrada. Ocorre uma vez por consulta.|  
|sp_fulltext_service @action=connect_timeout|A opção connect_timeout do procedimento sp_fulltext_service foi encontrada. Ocorre uma vez por consulta.|  
|sp_fulltext_service @action=data_timeout|A opção data_timeout do procedimento sp_fulltext_service foi encontrada. Ocorre uma vez por consulta.|  
|sp_fulltext_service @action=resource_usage|A opção resource_usage do procedimento sp_fulltext_service foi encontrada. Essa opção não tem nenhuma função. Ocorre uma vez por consulta.|  
|sp_fulltext_table|O procedimento sp_fulltext_table foi encontrado. Em vez disso, use CREATE/ALTER/DROP FULLTEXT INDEX. Ocorre uma vez por compilação.|  
|sp_getbindtoken|O procedimento sp_getbindtoken foi encontrado. Em vez disso, use MARS (vários conjuntos de resultados ativos) ou transações distribuídas. Ocorre uma vez por compilação.|  
|sp_grantdbaccess|O procedimento sp_grantdbaccess foi encontrado. Em vez disso, use CREATE USER. Ocorre uma vez por consulta.|  
|sp_grantlogin|O procedimento sp_grantlogin foi encontrado. Em vez disso, use CREATE LOGIN. Ocorre uma vez por consulta.|  
|sp_help_fulltext_catalog_components|O procedimento sp_help_fulltext_catalog_components foi encontrado. Esse procedimento retorna linhas vazias. Não use este procedimento. Ocorre uma vez por compilação.|  
|sp_help_fulltext_catalogs|O procedimento sp_help_fulltext_catalogs foi encontrado. Consulte sys.fulltext_catalogs em seu lugar. Ocorre uma vez por compilação.|  
|sp_help_fulltext_catalogs_cursor|O procedimento sp_help_fulltext_catalogs_cursor foi encontrado. Consulte sys.fulltext_catalogs em seu lugar. Ocorre uma vez por compilação.|  
|sp_help_fulltext_columns|O procedimento sp_help_fulltext_columns foi encontrado. Consulte sys.fulltext_index_columns em seu lugar. Ocorre uma vez por compilação.|  
|sp_help_fulltext_columns_cursor|O procedimento sp_help_fulltext_columns_cursor foi encontrado. Consulte sys.fulltext_index_columns em seu lugar. Ocorre uma vez por compilação.|  
|sp_help_fulltext_tables|O procedimento sp_help_fulltext_tables foi encontrado. Consulte sys.fulltext_indexes em seu lugar. Ocorre uma vez por compilação.|  
|sp_help_fulltext_tables_cursor|O procedimento sp_help_fulltext_tables_cursor foi encontrado. Consulte sys.fulltext_indexes em seu lugar. Ocorre uma vez por compilação.|  
|sp_helpdevice|O procedimento sp_helpdevice foi encontrado. Consulte sys.backup_devices em seu lugar. Ocorre uma vez por consulta.|  
|sp_helpextendedproc|O procedimento sp_helpextendedproc foi encontrado. Em vez disso, use CLR. Ocorre uma vez por compilação.|  
|sp_helpremotelogin|O procedimento sp_helpremotelogin foi encontrado. Em vez disso, use servidores vinculados.|  
|sp_indexoption|O procedimento sp_indexoption foi encontrado. Em vez disso, use ALTER INDEX. Ocorre uma vez por compilação.|  
|sp_lock|O procedimento sp_lock foi encontrado. Consulte sys.dm_tran_locks em vez disso. Ocorre uma vez por consulta.|  
|sp_password|O procedimento sp_password foi encontrado. Em vez disso, use ALTER LOGIN. Ocorre uma vez por consulta.|  
|sp_remoteoption|O procedimento sp_remoteoption foi encontrado. Em vez disso, use servidores vinculados.|  
|sp_renamedb|O procedimento sp_renamedb foi encontrado. Em vez disso, use ALTER DATABASE. Ocorre uma vez por consulta.|  
|sp_resetstatus|O procedimento sp_resetstatus foi encontrado. Em vez disso, use ALTER DATABASE. Ocorre uma vez por consulta.|  
|sp_revokedbaccess|O procedimento sp_revokedbaccess foi encontrado. Em vez disso, use DROP USER. Ocorre uma vez por consulta.|  
|sp_revokelogin|O procedimento sp_revokelogin foi encontrado. Em vez disso, use DROP LOGIN. Ocorre uma vez por consulta.|  
|sp_srvrolepermission|O procedimento preterido sp_srvrolepermission foi encontrado. Não use. Ocorre uma vez por consulta.|  
|sp_unbindefault|O procedimento sp_unbindefault foi encontrado. Em vez disso, use a palavra-chave DEFAULT em instruções CREATE TABLE ou ALTER TABLE. Ocorre uma vez por compilação.|  
|sp_unbindrule|O procedimento sp_unbindrule foi encontrado. Use restrições de verificação em vez de regras. Ocorre uma vez por compilação.|  
|SQL_AltDiction_CP1253_CS_AS|Evento que ocorre uma vez por inicialização de banco de dados e uma vez por uso de agrupamento. Planeje a modificação de aplicativos que usam este agrupamento.|  
|Literais de cadeia de caracteres como aliases de coluna|Foi encontrada sintaxe que contém uma cadeia de caracteres usada como um alias de coluna em uma instrução SELECT, como `'string' = expression`. Não use. Ocorre uma vez por compilação.|  
|sys.sql_dependencies|Referências a sys.sql_dependencies foram encontradas. Use sys.sql_expression_dependencies em seu lugar. Ocorre uma vez por compilação.|  
|sysaltfiles|Referências a sysaltfiles foram encontradas. Use sys.master_files em seu lugar. Ocorre uma vez por compilação.|  
|syscacheobjects|Referências a syscacheobjects foram encontradas. Use sys.dm_exec_cached_plans, sys.dm_exec_plan_attributes e sys.dm_exec_sql_text em vez disso. Ocorre uma vez por compilação.|  
|syscolumns|Referências a syscolumns foram encontradas. Use sys.columns em seu lugar. Ocorre uma vez por compilação.|  
|syscomments|Referências a syscomments foram encontradas. Use sys.sql_modules em vez disso. Ocorre uma vez por compilação.|  
|sysconfigures|Referências à tabela sysconfigures foram encontradas. Referencie a exibição sys.sysconfigures em seu lugar. Ocorre uma vez por compilação.|  
|sysconstraints|Referências a sysconstraints foram encontradas. Use sys.check_constraints, sys.default_constraints, sys.key_constraints ou sys.foreign_keys em vez disso. Ocorre uma vez por compilação.|  
|syscurconfigs|Referências a syscurconfigs foram encontradas. Use sys.configurations em seu lugar. Ocorre uma vez por compilação.|  
|sysdatabases|Referências a sysdatabases foram encontradas. Use sys.databases em vez disso. Ocorre uma vez por compilação.|  
|sysdepends|Referências a sysdepends foram encontradas. Use sys.sql_dependencies em vez disso. Ocorre uma vez por compilação.|  
|sysdevices|Referências a sysdevices foram encontradas. Use sys.backup_devices em vez disso. Ocorre uma vez por compilação.|  
|sysfilegroups|Referências a sysfilegroups foram encontradas. Use sys.filegroups em seu lugar. Ocorre uma vez por compilação.|  
|sysfiles|Referências a sysfiles foram encontradas. Use sys.database_files em seu lugar. Ocorre uma vez por compilação.|  
|sysforeignkeys|Referências a sysforeignkeys foram encontradas. Use sys.foreign_keys em seu lugar. Ocorre uma vez por compilação.|  
|sysfulltextcatalogs|Referências a sysfulltextcatalogs foram encontradas. Use sys.fulltext_catalogs em seu lugar. Ocorre uma vez por compilação.|  
|sysindexes|Referências a sysindexes foram encontradas. Use sys.indexes, sys.partitions, sys.allocation_units e sys.dm_db_partition_stats em seu lugar. Ocorre uma vez por compilação.|  
|sysindexkeys|Referências a sysindexkeys foram encontradas. Em vez dele, use sys.index_columns. Ocorre uma vez por compilação.|  
|syslockinfo|Referências a syslockinfo foram encontradas. Use sys.dm_tran_locks em vez disso. Ocorre uma vez por compilação.|  
|syslogins|Referências a syslogins foram encontradas. Use sys.server_principals e sys.sql_logins em seu lugar. Ocorre uma vez por compilação.|  
|sysmembers|Referências a sysmembers foram encontradas. Use sys.database_role_members em vez disso. Ocorre uma vez por compilação.|  
|sysmessages|Referências a sysmessages foram encontradas. Use sys.messages em vez disso. Ocorre uma vez por compilação.|  
|sysobjects|Referências a sysobjects foram encontradas. Use sys.objects em seu lugar. Ocorre uma vez por compilação.|  
|sysoledbusers|Referências a sysoledbusers foram encontradas. Use sys.linked_logins em seu lugar. Ocorre uma vez por compilação.|  
|sysopentapes|Referências a sysopentapes foram encontradas. Use sys.dm_io_backup_tapes em vez disso. Ocorre uma vez por compilação.|  
|sysperfinfo|Referências a sysperfinfo foram encontradas. Use sys.dm_os_performance_counters. . Ocorre uma vez por compilação.|  
|syspermissions|Referências a syspermissions foram encontradas. Use sys.database_permissions e sys.server_permissions em vez disso. Ocorre uma vez por compilação.|  
|sysprocesses|Referências a sysprocesses foram encontradas. Use sys.dm_exec_connections, sys.dm_exec_sessions e sys.dm_exec_requests em seu lugar. Ocorre uma vez por compilação.|  
|sysprotects|Referências a sysprotects foram encontradas. Use sys.database_permissions e sys.server_permissions em vez disso. Ocorre uma vez por compilação.|  
|sysreferences|Referências a sysreferences foram encontradas. Use sys.foreign_keys em seu lugar. Ocorre uma vez por compilação.|  
|sysremotelogins|Referências a sysremotelogins foram encontradas. Use sys.remote_logins em vez disso. Ocorre uma vez por compilação.|  
|sysservers|Referências a sysservers foram encontradas. Use sys.servers em seu lugar. Ocorre uma vez por compilação.|  
|systypes|Referências a systypes foram encontradas. Use sys.types em seu lugar. Ocorre uma vez por compilação.|  
|sysusers|Referências a sysusers foram encontradas. Use sys.database_principals em vez disso. Ocorre uma vez por compilação.|  
|Dica de tabela sem WITH|Uma instrução que usou dicas de tabela sem usar a palavra-chave WITH foi encontrada. Modifique as instruções para incluir a palavra WITH. Ocorre uma vez por compilação.|  
|Opção de tabela 'text in row'|Referências à opção de tabela 'text in row' foram encontradas. Use 'large value types out of row' de sp_tableoption em seu lugar. Ocorre uma vez por consulta.|  
|TEXTPTR|Referências à função TEXTPTR foram encontradas. Reescreva os aplicativos para usar o `varchar(max)` tipo de dados e removido `text`, `ntext`, e `image` sintaxe de tipo de dados. Ocorre uma vez por consulta.|  
|TEXTVALID|Referências à função TEXTVALID foram encontradas. Reescreva os aplicativos para usar o `varchar(max)` tipo de dados e removido `text`, `ntext`, e `image` sintaxe de tipo de dados. Ocorre uma vez por consulta.|  
|timestamp|Número total de vezes preterido `timestamp` foi encontrado o tipo de dados em uma instrução DDL. Use o `rowversion` em vez disso, o tipo de dados.|  
|UPDATETEXT ou WRITETEXT|As instruções UPDATETEXT ou WRITETEXT foram encontradas. Reescreva os aplicativos para usar o `varchar(max)` tipo de dados e removido `text`, `ntext`, e `image` sintaxe de tipo de dados. Ocorre uma vez por consulta.|  
|USER_ID|Referências à função USER_ID foram encontradas. Use a função DATABASE_PRINCIPAL_ID em seu lugar. Ocorre uma vez por compilação.|  
|Usando OLEDB para servidores vinculados||  
|Formato de armazenamento vardecimal|O uso de `vardecimal` o formato de armazenamento foi encontrado. Em vez disso, use a compactação de dados.|  
|XMLDATA|A sintaxe FOR XML foi encontrada. Use a geração de XSD para os modos RAW e AUTO. Não há nenhuma substituição para o modo explícito. Ocorre uma vez por compilação.|  
|XP_API|Uma instrução de procedimento armazenado estendido foi encontrada. Não use.|  
|xp_grantlogin|O procedimento xp_grantlogin foi encontrado. Em vez disso, use CREATE LOGIN. Ocorre uma vez por compilação.|  
|xp_loginconfig|O procedimento xp_loginconfig foi encontrado. Em vez disso, use o argumento IsIntegratedSecurityOnly de SERVERPROPERTY. Ocorre uma vez por consulta.|  
|xp_revokelogin|O procedimento xp_revokelogin foi encontrado. Em vez disso, use ALTER LOGIN DISABLE ou DROP LOGIN. Ocorre uma vez por compilação.|  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do mecanismo de banco de dados preteridos no SQL Server 2014](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)   
 [Recursos de pesquisa de texto completo preteridos no SQL Server 2014](../search/deprecated-full-text-search-features-in-sql-server-2016.md)   
 [Classe de evento Deprecation Announcement](../event-classes/deprecation-announcement-event-class.md)   
 [Classe de evento Deprecation Final Support](../event-classes/deprecation-final-support-event-class.md)   
 [Funcionalidade do mecanismo de banco de dados descontinuada no SQL Server 2014](../../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Recursos de pesquisa de texto completo no SQL Server 2014 descontinuados](../../database-engine/discontinued-full-text-search-features-in-sql-server-2014.md)   
 [Usar objetos do SQL Server](use-sql-server-objects.md)  
  
  

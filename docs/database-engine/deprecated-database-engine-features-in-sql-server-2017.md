---
title: Recursos preteridos do Mecanismo de Banco de Dados no SQL Server 2017 | Microsoft Docs
ms.custom: 
ms.date: 06/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: database-engine
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deprecated features [SQL Server]
- Database Engine [SQL Server], backward compatibility
- deprecation [SQL Server], feature list
ms.assetid: 
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e52b9300c764e99fb3f4bd54ed5b50f9f3ba686f
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="deprecated-database-engine-features-in-sql-server-2017"></a>Recursos preteridos do Mecanismo de Banco de Dados no SQL Server 2017
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve os recursos substituídos do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] que ainda estão disponíveis no [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)]. Esses recursos estão programados para serem removidos em uma versão futura do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Recursos preteridos não devem ser usados em aplicativos novos.  
  
 É possível monitorar o uso de recursos preteridos usando o contador de desempenho do Objeto Recursos Preteridos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e os eventos de rastreamento. Para obter mais informações, confira o artigo [Usar objetos do SQL Server](../relational-databases/performance-monitor/use-sql-server-objects.md).  
  
 O valor desses contadores também está disponível com a execução da seguinte instrução:  
  
```  
SELECT * FROM sys.dm_os_performance_counters   
WHERE object_name = 'SQLServer:Deprecated Features';  
```  

>  [!NOTE]  
>  Esta lista é idêntica à lista [!INCLUDE[sssql15-md](../includes/sssql15-md.md)]. Não há nenhum novo recurso preterido ou descontinuado do Mecanismo de Banco de Dados anunciado para o [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)].

## <a name="features-not-supported-in-the-next-version-of-sql-server"></a>Recursos sem suporte na próxima versão do SQL Server  
 Os recursos do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] a seguir não terão suporte na próxima versão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Não use esses recursos em novo trabalho de desenvolvimento e, assim que possível, modifique os aplicativos que os utilizam atualmente. O valor **Nome do recurso** aparece em eventos de rastreamento como o ObjectName, e em contadores de desempenho e sys.dm_os_performance_counters como o nome de instância. O valor **ID do Recurso** aparece em eventos de rastreamento como o ObjectId.  
  
|Categoria|Recurso substituído|Substituição|Nome do recurso|ID do Recurso|  
|--------------|------------------------|-----------------|------------------|----------------|  
|Backup e restauração|RESTORE { DATABASE &#124; LOG } WITH [MEDIA]PASSWORD continua sendo uma opção preterida. As opções BACKUP { DATABASE &#124; LOG } WITH PASSWORD e BACKUP { DATABASE &#124; LOG } WITH MEDIAPASSWORD serão descontinuadas.|Nenhum.|BACKUP DATABASE ou LOG WITH PASSWORD<br /><br /> BACKUP DATABASE ou LOG WITH MEDIAPASSWORD|104<br /><br /> 103|  
|Níveis de compatibilidade|Atualização da versão 110 ([!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] e [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]).|Os níveis de compatibilidade só estão disponíveis para as duas versões mais recentes. Para obter mais informações sobre níveis de compatibilidade, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md).|Nível de compatibilidade do banco de dados 100|108|  
|Objetos de banco de dados|Capacidade de retornar conjuntos de resultados de gatilhos|Nenhuma|Retornando resultados de gatilho|12|  
|Criptografia|A criptografia que usa o RC4 ou RC4_128 foi substituída e está programada para ser removida na próxima versão. A descriptografia do RC4 e RC4_128 não será substituída.|Usar outro algoritmo de criptografia, como AES.|Algoritmo de criptografia substituído|253|  
|Servidores remotos|sp_addremotelogin<br /><br /> sp_addserver<br /><br /> sp_dropremotelogin<br /><br /> sp_helpremotelogin<br /><br /> sp_remoteoption|Substitua servidores remotos usando servidores vinculados. sp_addserver só pode ser usado com a opção local.|sp_addremotelogin<br /><br /> sp_addserver<br /><br /> sp_dropremotelogin<br /><br /> sp_helpremotelogin<br /><br /> sp_remoteoption|70<br /><br /> 69<br /><br /> 71<br /><br /> 72<br /><br /> 73|  
|Servidores remotos|@@remserver|Substitua servidores remotos usando servidores vinculados.|Nenhuma|Nenhuma|  
|Servidores remotos|SET REMOTE_PROC_TRANSACTIONS|Substitua servidores remotos usando servidores vinculados.|SET REMOTE_PROC_TRANSACTIONS|110|  
|Opções Set|**SET ROWCOUNT** para as instruções **INSERT**, **UPDATE**e **DELETE**|Palavra-chave TOP|SET ROWCOUNT|109|  
|Dicas de tabela|Dica de tabela HOLDLOCK sem parênteses.|Use HOLDLOCK com parênteses.|Dica de tabela HOLDLOCK sem parênteses|167|  
|Ferramentas|Utilitário sqlmaint|Usar o recurso de plano de manutenção do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] |Nenhuma|Nenhuma|  
  
## <a name="features-not-supported-in-a-future-version-of-sql-server"></a>Recursos sem suporte em uma versão futura do SQL Server  
 Os recursos do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] a seguir terão suporte na próxima versão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], mas serão removidos em uma versão posterior. A versão específica do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não foi determinada.  
  
|Categoria|Recurso substituído|Substituição|Nome do recurso|ID do Recurso|  
|--------------|------------------------|-----------------|------------------|----------------|  
|Níveis de compatibilidade|sp_dbcmptlevel|ALTER DATABASE … SET COMPATIBILITY_LEVEL. Para obter mais informações, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md).|sp_dbcmptlevel|80|  
|Níveis de compatibilidade|Nível de compatibilidade 110 e 120 do banco de dados.|Planeje atualizar o banco de dados e o aplicativo para uma versão futura.|Nível de compatibilidade 110 do banco de dados<br /><br /> Nível de compatibilidade 120 do banco de dados||  
|XML|Geração de esquema XDR embutido|A diretiva XMLDATA para a opção FOR XML foi preterida. Use geração de XSD no caso dos modos RAW e AUTO. Não há substituição para a diretiva XMLDATA no modo EXPLICIT.|XMLDATA|181|  
|Backup e restauração|BACKUP { DATABASE &#124; LOG } TO TAPE<br /><br /> BACKUP { DATABASE &#124; LOG } TO *device_that_is_a_tape*|BACKUP { DATABASE &#124; LOG } TO DISK<br /><br /> BACKUP { DATABASE &#124; LOG } TO *device_that_is_a_disk*|BACKUP DATABASE ou LOG TO TAPE|235|  
|Backup e restauração|sp_addumpdevice'**tape**'|sp_addumpdevice'**disk**'|ADDING TAPE DEVICE|236|  
|Backup e restauração|sp_helpdevice|sys.backup_devices|sp_helpdevice|100|  
|Agrupamentos|Korean_Wansung_Unicode<br /><br /> Lithuanian_Classic<br /><br /> SQL_AltDiction_CP1253_CS_AS|Nenhum. Estes agrupamentos existem no [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], mas não são visíveis por meio de fn_helpcollations.|Korean_Wansung_Unicode<br /><br /> Lithuanian_Classic<br /><br /> SQL_AltDiction_CP1253_CS_AS|191<br /><br /> 192<br /><br /> 194|  
|Agrupamentos|Híndi<br /><br /> Macedônio|Estes agrupamentos existem no [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] e superior, mas não são visíveis por meio de fn_helpcollations. Em vez disso, use Macedonian_FYROM_90 e Indic_General_90.|Híndi<br /><br /> Macedônio|190<br /><br /> 193|  
|Agrupamentos|Azeri_Latin_90<br /><br /> Azeri_Cyrilllic_90|Azeri_Latin_100<br /><br /> Azeri_Cyrilllic_100|Azeri_Latin_90<br /><br /> Azeri_Cyrilllic_90|232<br /><br /> 233|  
|Configuração|Opção de banco de dados SET ANSI_NULLS OFF e ANSI_NULLS OFF<br /><br /> Opção de banco de dados SET ANSI_PADDING OFF e ANSI_PADDING OFF<br /><br /> Opção de banco de dados SET CONCAT_NULL_YIELDS_NULL OFF e CONCAT_NULL_YIELDS_NULL OFF<br /><br /> SET OFFSETS|Nenhum.<br /><br /> ANSI_NULLS, ANSI_PADDING e CONCAT_NULLS_YIELDS_NULL sempre serão definidos como ON. SET OFFSETS não estarão disponíveis.|SET ANSI_NULLS OFF<br /><br /> SET ANSI_PADDING OFF<br /><br /> SET CONCAT_NULL_YIELDS_NULL OFF<br /><br /> SET OFFSETS<br /><br /> ALTER DATABASE SET ANSI_NULLS OFF<br /><br /> ALTER DATABASE SET ANSI_PADDING OFF<br /><br /> ALTER DATABASE SET CONCAT_NULL_YIELDS_NULL OFF|111<br /><br /> 113<br /><br /> 112<br /><br /> 36<br /><br /> 111<br /><br /> 113<br /><br /> 112|  
|Tipos de dados|sp_addtype<br /><br /> sp_droptype|CREATE TYPE<br /><br /> DROP TYPE|sp_addtype<br /><br /> sp_droptype|62<br /><br /> 63|  
|Tipos de dados|Sintaxe de**timestamp** para o tipo de dados **rowversion** |Sintaxe do tipo de dados**rowversion** |timestamp|158|  
|Tipos de dados|Capacidade para inserir valores nulos em colunas **timestamp** .|Em vez disso, use um DEFAULT.|INSERT NULL em colunas TIMESTAMP|179|  
|Tipos de dados|Opção de tabela 'text in row'|Use os tipos de dados **varchar(max)**, **nvarchar(max)** e **varbinary(max)**. Para obter mais informações, veja [sp_tableoption &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md).|Opção de tabela 'text in row'|9|  
|Tipos de dados|Tipos de dados:<br /><br /> **texto**<br /><br /> **ntext**<br /><br /> **imagem**|Use os tipos de dados **varchar(max)**, **nvarchar(max)**e **varbinary(max)** .|Tipos de dados: **text** **ntext** ou **image**|4|  
|Gerenciamento de banco de dados|sp_attach_db<br /><br /> sp_attach_single_file_db|Instrução CREATE DATABASE com a opção FOR ATTACH. Para recriar vários arquivos de log quando um ou mais tiver um novo local, use a opção FOR ATTACH_REBUILD_LOG.|sp_attach_db<br /><br /> sp_attach_single_file_db|81<br /><br /> 82|  
|Objetos de banco de dados|CREATE DEFAULT<br /><br /> DROP DEFAULT<br /><br /> sp_bindefault<br /><br /> sp_unbindefault|Palavra-chave DEFAULT em CREATE TABLE e ALTER TABLE|CREATE_DROP_DEFAULT<br /><br /> sp_bindefault<br /><br /> sp_unbindefault|162<br /><br /> 64<br /><br /> 65|  
|Objetos de banco de dados|CREATE RULE<br /><br /> DROP RULE<br /><br /> sp_bindrule<br /><br /> sp_unbindrule|Palavra-chave CHECK em CREATE TABLE e ALTER TABLE|CREATE_DROP_RULE<br /><br /> sp_bindrule<br /><br /> sp_unbindrule|161<br /><br /> 66<br /><br /> 67|  
|Objetos de banco de dados|sp_change_users_login|Use ALTER USER.|sp_change_users_login|231|  
|Objetos de banco de dados|sp_depends|sys.dm_sql_referencing_entities e sys.dm_sql_referenced_entities|sp_depends|19|  
|Objetos de banco de dados|sp_renamedb|MODIFY NAME em ALTER DATABASE|sp_renamedb|79|  
|Objetos de banco de dados|sp_getbindtoken|Use MARS ou transações distribuídas.|sp_getbindtoken|98|  
|Opções de banco de dados|sp_bindsession|Use MARS ou transações distribuídas.|sp_bindsession|97|  
|Opções de banco de dados|sp_resetstatus|ALTER DATABASE SET { ONLINE &#124; EMERGENCY }|sp_resetstatus|83|  
|Opções de banco de dados|Opção TORN_PAGE_DETECTION de ALTER DATABASE|Opção PAGE_VERIFY TORN_PAGE_DETECTION de ALTER DATABASE|ALTER DATABASE WITH TORN_PAGE_DETECTION|102|  
|DBCC|DBCC DBREINDEX|Opção REBUILD de ALTER INDEX.|DBCC DBREINDEX|11|  
|DBCC|DBCC INDEXDEFRAG|Opção REORGANIZE de ALTER INDEX|DBCC INDEXDEFRAG|18|  
|DBCC|DBCC SHOWCONTIG|sys.dm_db_index_physical_stats|DBCC SHOWCONTIG|10|  
|DBCC|DBCC PINTABLE<br /><br /> DBCC UNPINTABLE|Não tem nenhum efeito.|DBCC [UN]PINTABLE|189|  
|Propriedades estendidas|Level0type = 'type' e Level0type = 'USER' para adicionar propriedades estendidas a objetos de tipo de nível 1 ou nível 2.|Use Level0type = 'USER' apenas para adicionar uma propriedade estendida diretamente a um usuário ou uma função.<br /><br /> Use Level0type = 'SCHEMA' para adicionar uma propriedade estendida a tipos de nível 1, como TABLE ou VIEW, ou a tipos de nível 2, como COLUMN ou TRIGGER. Para obter mais informações, veja [sp_addextendedproperty &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md).|EXTPROP_LEVEL0TYPE<br /><br /> EXTPROP_LEVEL0USER|13<br /><br /> 14|  
|Programação de procedimento armazenado estendido|srv_alloc<br /><br /> srv_convert<br /><br /> srv_describe<br /><br /> srv_getbindtoken<br /><br /> srv_got_attention<br /><br /> srv_message_handler<br /><br /> srv_paramdata<br /><br /> srv_paraminfo<br /><br /> srv_paramlen<br /><br /> srv_parammaxlen<br /><br /> srv_paramname<br /><br /> srv_paramnumber<br /><br /> srv_paramset<br /><br /> srv_paramsetoutput<br /><br /> srv_paramstatus<br /><br /> srv_paramtype<br /><br /> srv_pfield<br /><br /> srv_pfieldex<br /><br /> srv_rpcdb<br /><br /> srv_rpcname<br /><br /> srv_rpcnumber<br /><br /> srv_rpcoptions<br /><br /> srv_rpcowner<br /><br /> srv_rpcparams<br /><br /> srv_senddone<br /><br /> srv_sendmsg<br /><br /> srv_sendrow<br /><br /> srv_setcoldata<br /><br /> srv_setcollen<br /><br /> srv_setutype<br /><br /> srv_willconvert<br /><br /> srv_wsendmsg|Em vez disso, use a Integração CLR.|XP_API|20|  
|Programação de procedimento armazenado estendido|sp_addextendedproc<br /><br /> sp_dropextendedproc<br /><br /> sp_helpextendedproc|Em vez disso, use a Integração CLR.|sp_addextendedproc<br /><br /> sp_dropextendedproc<br /><br /> sp_helpextendedproc|94<br /><br /> 95<br /><br /> 96|  
|Procedimentos armazenados estendidos|xp_grantlogin<br /><br /> xp_revokelogin<br /><br /> xp_loginConfig|Use CREATE LOGIN<br /><br /> Use o argumento DROP LOGIN IsIntegratedSecurityOnly de SERVERPROPERTY|xp_grantlogin<br /><br /> xp_revokelogin<br /><br /> xp_loginConfig|44<br /><br /> 45<br /><br /> 59|  
|Funções|fn_get_sql|sys.dm_exec_sql_text|fn_get_sql|151|  
|Algoritmos de hash|Os algoritmos MD2, MD4, MD5, SHA e SHA1. Não estão disponíveis no nível de compatibilidade 130.|Use SHA2_256 ou SHA2_512.|Algoritmo de hash preterido||  
|Alta disponibilidade|espelhamento de banco de dados|[!INCLUDE[ssHADR](../includes/sshadr-md.md)]<br /><br /> Se sua edição do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não der suporte a [!INCLUDE[ssHADR](../includes/sshadr-md.md)], use envio de logs.|DATABASE_MIRRORING|267|  
|Opções de índice|sp_indexoption|ALTER INDEX|sp_indexoption|78|  
|Opções de índice|Sintaxe de CREATE TABLE, ALTER TABLE ou CREATE INDEX sem parênteses delimitando as opções.|Reescreva a instrução para usar a sintaxe atual.|INDEX_OPTION|33|  
|Opções de instância|Opção de sp_configure 'allow updates'|As tabelas do sistema não são mais atualizáveis. A configuração não tem nenhum efeito.|sp_configure 'allow updates'|173|  
|Opções de instância|Opções sp_configure:<br /><br /> 'locks'<br /><br /> 'open objects'<br /><br /> 'set working set size'|Agora é configurado automaticamente. A configuração não tem nenhum efeito.|sp_configure 'locks'<br /><br /> sp_configure 'open objects'<br /><br /> sp_configure 'set working set size'|174<br /><br /> 175<br /><br /> 176|  
|Opções de instância|Opção de sp_configure 'priority boost'|As tabelas do sistema não são mais atualizáveis. A configuração não tem nenhum efeito. Usar a opção start/high… program.exe do Windows.|sp_configure 'priority boost'|199|  
|Opções de instância|Opção de sp_configure 'remote proc trans'|As tabelas do sistema não são mais atualizáveis. A configuração não tem nenhum efeito.|sp_configure 'remote proc trans'|37|  
|Servidores vinculados|Especificando o provedor SQLOLEDB para servidores vinculados.|SQL Server Native Client (SQLNCLI)|SQLOLEDDB para servidores vinculados|19|  
|Bloqueio|sp_lock|sys.dm_tran_locks|sp_lock|99|  
|Metadados|FILE_ID<br /><br /> INDEXKEY_PROPERTY|FILE_IDEX<br /><br /> sys.index_columns|FILE_ID<br /><br /> INDEXKEY_PROPERTY|15<br /><br /> 17|  
|Serviços Web XML nativos|A instrução CREATE ENDPOINT ou ALTER ENDPOINT com a opção FOR SOAP.<br /><br /> sys.endpoint_webmethods<br /><br /> sys.soap_endpoints|Em vez disso, use o WCF (Windows Communications Foundation) ou o ASP.NET.|CREATE/ALTER ENDPOINT<br /><br /> sys.endpoint_webmethods<br /><br /> EXT_soap_endpoints<br /><br /> sys.soap_endpoints|21<br /><br /> 22<br /><br /> 23|  
|Bancos de dados removíveis|sp_certify_removable<br /><br /> sp_create_removable|sp_detach_db|sp_certify_removable<br /><br /> sp_create_removable|74<br /><br /> 75|  
|Bancos de dados removíveis|sp_dbremove|DROP DATABASE|sp_dbremove|76|  
|Segurança|A sintaxe ALTER LOGIN WITH SET CREDENTIAL|Substituída pela nova sintaxe ALTER LOGIN ADD e DROP CREDENTIAL|ALTER LOGIN WITH SET CREDENTIAL|230|  
|Segurança|sp_addapprole<br /><br /> sp_dropapprole|CREATE APPLICATION ROLE<br /><br /> DROP APPLICATION ROLE|sp_addapprole<br /><br /> sp_dropapprole|53<br /><br /> 54|  
|Segurança|sp_addlogin<br /><br /> sp_droplogin|CREATE LOGIN<br /><br /> DROP LOGIN|sp_addlogin<br /><br /> sp_droplogin|39<br /><br /> 40|  
|Segurança|sp_adduser<br /><br /> sp_dropuser|CREATE USER<br /><br /> DROP USER|sp_adduser<br /><br /> sp_dropuser|49<br /><br /> 50|  
|Segurança|sp_grantdbaccess<br /><br /> sp_revokedbaccess|CREATE USER<br /><br /> DROP USER|sp_grantdbaccess<br /><br /> sp_revokedbaccess|51<br /><br /> 52|  
|Segurança|sp_addrole<br /><br /> sp_droprole|CREATE ROLE<br /><br /> DROP ROLE|sp_addrole<br /><br /> sp_droprole|56<br /><br /> 57|  
|Segurança|sp_approlepassword<br /><br /> sp_password|ALTER APPLICATION ROLE<br /><br /> ALTER LOGIN|sp_approlepassword<br /><br /> sp_password|55<br /><br /> 46|  
|Segurança|sp_changeobjectowner|ALTER SCHEMA ou ALTER AUTHORIZATION|sp_changeobjectowner|58|  
|Segurança|sp_control_dbmasterkey_password|Uma chave mestra deve existir e a senha deve estar correta.|sp_control_dbmasterkey_password|274|  
|Segurança|sp_defaultdb<br /><br /> sp_defaultlanguage|ALTER LOGIN|sp_defaultdb<br /><br /> sp_defaultlanguage|47<br /><br /> 48|  
|Segurança|sp_denylogin<br /><br /> sp_grantlogin<br /><br /> sp_revokelogin|ALTER LOGIN DISABLE<br /><br /> CREATE LOGIN<br /><br /> DROP LOGIN|sp_denylogin<br /><br /> sp_grantlogin<br /><br /> sp_revokelogin|42<br /><br /> 41<br /><br /> 43|  
|Segurança|USER_ID|DATABASE_PRINCIPAL_ID|USER_ID|16|  
|Segurança|sp_srvrolepermission<br /><br /> sp_dbfixedrolepermission|Estes procedimentos armazenados retornam as informações que estavam corretas no [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]. A saída não reflete as alterações na hierarquia de permissões que foram implementadas no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Para obter mais informações, consulte [Permissões de funções de servidor fixas](http://msdn.microsoft.com/library/ms175892\(SQL.100\).aspx).|sp_srvrolepermission<br /><br /> sp_dbfixedrolepermission|61<br /><br /> 60|  
|Segurança|GRANT ALL<br /><br /> DENY ALL<br /><br /> REVOKE ALL|Permissões específicas GRANT, DENY e REVOKE.|Permissão ALL|35|  
|Segurança|Função intrínseca PERMISSIONS|Consulte sys.fn_my_permissions.|PERMISSIONS|170|  
|Segurança|SETUSER|EXECUTE AS|SETUSER|165|  
|Segurança|Algoritmos de criptografia RC4 e DESX|Usar outro algoritmo, como AES.|Algoritmo DESX|238|  
|Opções Set|SET FMTONLY|[sys.dm_exec_describe_first_result_set &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md), [sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md), [sp_describe_first_result_set &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) e [sp_describe_undeclared_parameters &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md).|SET FMTONLY|250|  
|Opções de configuração de servidor|opção c2 audit<br /><br /> opção default trace enabled|[Opção de configuração de servidor com conformidade de critérios comuns habilitada](../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md)<br /><br /> [Eventos estendidos](../relational-databases/extended-events/extended-events.md)|sp_configure 'c2 audit mode'<br /><br /> sp_configure 'default trace enabled'|252<br /><br /> 253|  
|Classes SMO|Classe **Microsoft.SQLServer. Management.Smo.Information**<br /><br /> Classe **Microsoft.SQLServer. Management.Smo.Settings**<br /><br /> **Microsoft.SQLServer.Management. Smo.DatabaseOptions**<br /><br /> Propriedade **Microsoft.SqlServer.Management.Smo. DatabaseDdlTrigger.NotForReplication**|Classe **Microsoft.SqlServer.  Management.Smo.Server**<br /><br /> Classe **Microsoft.SqlServer.  Management.Smo.Server**<br /><br /> Classe **Microsoft.SqlServer. Management.Smo.Database**<br /><br /> Nenhuma|Nenhuma|Nenhuma|  
|SQL Server Agent|Notificação**net send** <br /><br /> Notificação por pager|Notificação por email<br /><br /> Notificação por email |Nenhuma|Nenhuma|  
|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]|Integração com o Gerenciador de Soluções no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]||Nenhuma|Nenhuma|  
|Procedimentos armazenados do sistema|sp_db_increased_partitions|Nenhum. O suporte ao aumento de partições está disponível, por padrão, no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].|sp_db_increased_partitions|253|  
|Tabelas do sistema|sysaltfiles<br /><br /> syscacheobjects<br /><br /> syscolumns<br /><br /> syscomments<br /><br /> sysconfigures<br /><br /> sysconstraints<br /><br /> syscurconfigs<br /><br /> sysdatabases<br /><br /> sysdepends<br /><br /> sysdevices<br /><br /> sysfilegroups<br /><br /> sysfiles<br /><br /> sysforeignkeys<br /><br /> sysfulltextcatalogs<br /><br /> sysindexes<br /><br /> sysindexkeys<br /><br /> syslockinfo<br /><br /> syslogins<br /><br /> sysmembers<br /><br /> sysmessages<br /><br /> sysobjects<br /><br /> sysoledbusers<br /><br /> sysopentapes<br /><br /> sysperfinfo<br /><br /> syspermissions<br /><br /> sysprocesses<br /><br /> sysprotects<br /><br /> sysreferences<br /><br /> sysremotelogins<br /><br /> sysservers<br /><br /> systypes<br /><br /> sysusers|Exibições de compatibilidade. Para obter mais informações, veja [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md).<br /><br /> **\*\* Importante \*\*** As exibições de compatibilidade não expõem metadados para os recursos introduzidos no [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]. É recomendável atualizar seus aplicativos para usar exibições do catálogo. Para obter mais informações, veja [Exibições de catálogo e&#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/catalog-views-transact-sql.md).|sysaltfiles<br /><br /> syscacheobjects<br /><br /> syscolumns<br /><br /> syscomments<br /><br /> sysconfigures<br /><br /> sysconstraints<br /><br /> syscurconfigs<br /><br /> sysdatabases<br /><br /> sysdepends<br /><br /> sysdevices<br /><br /> sysfilegroups<br /><br /> sysfiles<br /><br /> sysforeignkeys<br /><br /> sysfulltextcatalogs<br /><br /> sysindexes<br /><br /> sysindexkeys<br /><br /> syslockinfo<br /><br /> syslogins<br /><br /> sysmembers<br /><br /> sysmessages<br /><br /> sysobjects<br /><br /> sysoledbusers<br /><br /> sysopentapes<br /><br /> sysperfinfo<br /><br /> syspermissions<br /><br /> sysprocesses<br /><br /> sysprotects<br /><br /> sysreferences<br /><br /> sysremotelogins<br /><br /> sysservers<br /><br /> systypes<br /><br /> sysusers|141<br /><br /> Nenhuma<br /><br /> 133<br /><br /> 126<br /><br /> 146<br /><br /> 131<br /><br /> 147<br /><br /> 142<br /><br /> 123<br /><br /> 144<br /><br /> 128<br /><br /> 127<br /><br /> 130<br /><br /> 122<br /><br /> 132<br /><br /> 134<br /><br /> 143<br /><br /> 140<br /><br /> 119<br /><br /> 137<br /><br /> 125<br /><br /> 139<br /><br /> 145<br /><br /> 157<br /><br /> 121<br /><br /> 153<br /><br /> 120<br /><br /> 129<br /><br /> 138<br /><br /> 136<br /><br /> 135<br /><br /> 124|  
|Tabelas do sistema|sys.numbered_procedures<br /><br /> sys.numbered_procedure_parameters|Nenhuma|numbered_procedures<br /><br /> numbered_procedure_parameters|148<br /><br /> 149|  
|Funções do sistema|fn_virtualservernodes<br /><br /> fn_servershareddrives|sys.dm_os_cluster_nodes<br /><br /> sys.dm_io_cluster_shared_drives|fn_virtualservernodes<br /><br /> fn_servershareddrives|155<br /><br /> 156|  
|Exibições do sistema|sys.sql_dependencies|sys.sql_expression_dependencies|sys.sql_dependencies|198|  
|Compactação de tabela|O uso do formato de armazenamento vardecimal.|O formato de armazenamento vardecimal foi preterido. Dados de compactação do[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] , compacta valores decimais e outros tipos de dados. É recomendável usar a compactação de dados em vez do formato de armazenamento vardecimal.|Formato de armazenamento vardecimal|200|  
|Compactação de tabela|Uso do procedimento sp_db_vardecimal_storage_format.|O formato de armazenamento vardecimal foi preterido. Dados de compactação do[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] , compacta valores decimais e outros tipos de dados. É recomendável usar a compactação de dados em vez do formato de armazenamento vardecimal.|sp_db_vardecimal_storage_format|201|  
|Compactação de tabela|Uso do procedimento sp_estimated_rowsize_reduction_for_vardecimal.|Use a compactação de dados e o procedimento sp_estimate_data_compression_savings em vez disso.|sp_estimated_rowsize_reduction_for_vardecimal|202|  
|Dicas de tabela|Especificando NOLOCK ou READUNCOMMITTED na cláusula FROM de uma instrução UPDATE ou DELETE.|Remova as dicas de tabela NOLOCK ou READUNCOMMITTED da cláusula FROM.|NOLOCK ou READUNCOMMITTED em UPDATE ou DELETE|1|  
|Dicas de tabela|Especificando dicas de tabela sem usar a palavra-chave WITH.|Use WITH.|Dica de tabela sem WITH|8|  
|Dicas de tabela|INSERT_HINTS||INSERT_HINTS|34|  
|Textpointers|WRITETEXT<br /><br /> UPDATETEXT<br /><br /> READTEXT|Nenhuma|UPDATETEXT ou WRITETEXT<br /><br /> READTEXT|115<br /><br /> 114|  
|Textpointers|TEXTPTR()<br /><br /> TEXTVALID()|Nenhuma|TEXTPTR<br /><br /> TEXTVALID|5<br /><br /> 6|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Sequência da chamada de função ::|Substituída por SELECT *column_list* FROM sys.\<*function_name*>().<br /><br /> Por exemplo, substitua `SELECT * FROM ::fn_virtualfilestats(2,1)`por `SELECT * FROM sys.fn_virtualfilestats(2,1)`.|sintaxe '::' de chamada de função|166|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Referências de coluna de três e quatro partes.|Nomes de duas partes é o comportamento compatível com o padrão.|Nome de coluna com mais de duas partes|3|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Uma cadeia de caracteres entre aspas usada como um alias de coluna para uma expressão em uma lista SELECT:<br /><br /> '*string_alias*' = *expression*|*expression* [AS] *column_alias*<br /><br /> *expression* [AS] [*column_alias*]<br /><br /> *expression* [AS] "*column_alias*"<br /><br /> *expression* [AS] '*column_alias*'<br /><br /> *column_alias* = *expression*|Literais de cadeia de caracteres como aliases de coluna|184|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Procedimentos numerados|Nenhum. Não use.|ProcNums|160|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Sintaxe*table_name.index_name* em DROP INDEX|Sintaxe*index_name* ON *table_name* em DROP INDEX.|DROP INDEX com nome de duas partes|163|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Instruções [!INCLUDE[tsql](../includes/tsql-md.md)] que não terminam com um ponto-e-vírgula.|Instruções [!INCLUDE[tsql](../includes/tsql-md.md)] que terminam com um ponto-e-vírgula ( ; ).|Nenhuma|Nenhuma|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|GROUP BY ALL|Use solução caso a caso personalizada com UNION ou tabela derivada.|GROUP BY ALL|169|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|ROWGUIDCOL como um nome de coluna em instruções DML.|Use $rowguid.|ROWGUIDCOL|182|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|IDENTITYCOL como um nome de coluna em instruções DML.|Use $identity.|IDENTITYCOL|183|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Uso de #, ## como tabela temporária e nomes de procedimento armazenado temporários.|Use pelo menos um caractere adicional.|'#' e '##' como o nome de tabelas temporárias e procedimentos armazenados|185|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Uso de @, @@ ou @@ como identificadores [!INCLUDE[tsql](../includes/tsql-md.md)] .|Não use @, @@ ou nomes que comecem com @@ como identificadores.|'@' e nomes que começam com '@@' como identificadores [!INCLUDE[tsql](../includes/tsql-md.md)]|186.|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Uso da palavra-chave DEFAULT como valor padrão.|Não use a palavra DEFAULT como um valor padrão.|A palavra-chave DEFAULT como um valor padrão|187|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Uso de um espaço como um separador entre dicas de tabela.|Use uma vírgula para separar dicas de tabela.|Várias dicas de tabela sem vírgula|168|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|A lista de seleção de uma exibição indexada de agregação deve conter COUNT_BIG (*) no modo de compatibilidade 90|Use COUNT_BIG (*).|Lista de seleção de exibição indexada sem COUNT_BIG (*)|2|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|O aplicativo indireto de dicas de tabela para uma invocação de uma função com valor de tabela (TVF) de várias instruções por meio de uma exibição.|Nenhum.|Dicas TVF indiretas|7|  
|[!INCLUDE[tsql](../includes/tsql-md.md)]|Sintaxe ALTER DATABASE:<br /><br /> MODIFY FILEGROUP READONLY<br /><br /> MODIFY FILEGROUP READWRITE|MODIFY FILEGROUP READ_ONLY<br /><br /> MODIFY FILEGROUP READ_WRITE|MODIFY FILEGROUP READONLY<br /><br /> MODIFY FILEGROUP READWRITE|195<br /><br /> 196|  
|Outro|DB-Library<br /><br /> Embedded SQL para C|Embora ainda ofereça suporte a conexões de aplicativos existentes que usam as APIS de DB-Library e Embedded SQL, o [!INCLUDE[ssDE](../includes/ssde-md.md)] não inclui a documentação ou os arquivos necessários para fazer o trabalho de programação em aplicativos que usam essas APIs. Uma versão futura do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] descartará suporte para conexões do DB-Library ou aplicativos do Embedded SQL. Não use DB-Library ou Embedded SQL para desenvolver novos aplicativos. Remova qualquer dependência do DB-Library ou do Embedded SQL ao modificar aplicativos existentes. Em vez destas APIs, use o namespace SQLClient ou uma API como ODBC. O[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] não inclui a DLL DB-Library necessária para executar estes aplicativos. Para executar aplicativos DB-Library ou Embedded SQL, a DLL DB-Library do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] versão 6.5, do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 7.0 ou do [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]deve estar disponível.|Nenhuma|Nenhuma|  
|Ferramentas|SQL Server Profiler para captura de rastreamento|Use o Extended Events Profiler inserido no SQL Server Management Studio.|SQL Server Profiler|Nenhuma|  
|Ferramentas|SQL Server Profiler para reprodução de rastreamento|[SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md)|SQL Server Profiler|Nenhuma|  
|Trace Management Objects|Namespace Microsoft.SqlServer.Management.Trace (contém as APIs para Rastreamento do SQL Server e objetos de reprodução)|Configuração de Rastreamento: <xref:Microsoft.SqlServer.Management.XEvent><br /><br /> Leitura de Rastreamento: <xref:Microsoft.SqlServer.XEvent.Linq><br /><br /> Reprodução de rastreamento: nenhuma|||  
|Procedimentos armazenados, funções e exibições de catálogo do Rastreamento do SQL|sp_trace_create<br /><br /> sp_trace_setevent<br /><br /> sp_trace_setfilter<br /><br /> sp_trace_setstatus<br /><br /> fn_trace_geteventinfo<br /><br /> fn_trace_getfilterinfo<br /><br /> fn_trace_getinfo<br /><br /> fn_trace_gettable<br /><br /> sys.traces<br /><br /> sys.trace_events<br /><br /> sys.trace_event_bindings<br /><br /> sys.trace_categories<br /><br /> sys.trace_columns<br /><br /> sys.trace_subclass_values|[Eventos estendidos](../relational-databases/extended-events/extended-events.md)|sp_trace_create<br /><br /> sp_trace_setevent<br /><br /> sp_trace_setfilter<br /><br /> sp_trace_setstatus<br /><br /> fn_trace_geteventinfo<br /><br /> fn_trace_getfilterinfo<br /><br /> fn_trace_getinfo<br /><br /> fn_trace_gettable<br /><br /> sys.traces<br /><br /> sys.trace_events<br /><br /> sys.trace_event_bindings<br /><br /> sys.trace_categories<br /><br /> sys.trace_columns<br /><br /> sys.trace_subclass_values|258<br /><br /> 260<br /><br /> 261<br /><br /> 259<br /><br /> 256<br /><br /> 257|  
  
> [!NOTE]  
>  O parâmetro **OUTPUT** de cookie para **sp_setapprole** está documentado atualmente como **varbinary(8000)** , que tem o tamanho máximo correto. No entanto, a implementação atual retorna **varbinary(50)**. Se os desenvolvedores alocaram **varbinary(50)** , o aplicativo poderá exigir alterações se o cookie retornar aumentos de tamanho em uma versão futura. Embora não seja um problema de substituição, isto é mencionado neste tópico porque os ajustes de aplicativo são semelhantes. Para obter mais informações, veja [sp_setapprole &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
 [Funcionalidade do Mecanismo de Banco de Dados descontinuada no SQL Server 2016](../database-engine/discontinued-database-engine-functionality-in-sql-server-2016.md)  
  
  



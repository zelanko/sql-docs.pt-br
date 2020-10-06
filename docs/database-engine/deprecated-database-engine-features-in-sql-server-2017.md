---
title: Recursos preteridos do mecanismo de banco de dados no SQL Server 2017 | Microsoft Docs
titleSuffix: SQL Server 2019
description: Saiba mais sobre os recursos do mecanismo de banco de dados preteridos que ainda estão disponíveis no SQL Server 2017 (14.x), mas que não devem ser usados em novos aplicativos.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- deprecated features [SQL Server]
- Database Engine [SQL Server], backward compatibility
- deprecation [SQL Server], feature list
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 5285873c9fc81849d8da8b48140dfbb71281e1aa
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670512"
---
# <a name="deprecated-database-engine-features-in-sql-server-2017"></a>Recursos preteridos do Mecanismo de Banco de Dados no SQL Server 2017

[!INCLUDE[SQL Server 2017](../includes/applies-to-version/sqlserver2017.md)]

  Este tópico descreve os recursos substituídos do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] que ainda estão disponíveis no [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)]. Recursos preteridos não devem ser usados em aplicativos novos.  
  
Quando um recurso está marcado como preterido, isso significa que:\

- O recurso está somente no modo de manutenção. Nenhuma alteração será feita, incluindo as relacionadas à interoperabilidade com novos recursos.
- Buscamos não remover um recurso preterido de versões futuras para facilitar a atualização. No entanto, em situações raras, podemos optar por remover permanentemente o recurso de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] caso ele limite inovações futuras.
- Para novos desenvolvimentos, não recomendamos usar recursos preteridos.      

É possível monitorar o uso de recursos preteridos usando o contador de desempenho do Objeto Recursos Preteridos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e os eventos de rastreamento. Para obter mais informações, confira o artigo [Usar objetos do SQL Server](../relational-databases/performance-monitor/use-sql-server-objects.md).  

Os valores desses contadores também estão disponíveis com a execução da seguinte instrução:  

```sql
SELECT * FROM sys.dm_os_performance_counters
WHERE object_name = 'SQLServer:Deprecated Features';
```

> [!NOTE]
> Esta lista é idêntica à lista [!INCLUDE[sssql15-md](../includes/sssql15-md.md)]. Não há nenhum novo recurso preterido ou descontinuado do Mecanismo de Banco de Dados anunciado para o [!INCLUDE[sssqlv14-md](../includes/sssqlv14-md.md)].

## <a name="features-deprecated-in-the-next-version-of-sql-server"></a>Recursos preteridos na próxima versão do SQL Server

Os recursos a seguir do Mecanismo de Banco de Dados do SQL Server serão preteridos na próxima versão do SQL Server. Não use esses recursos em novo trabalho de desenvolvimento e, assim que possível, modifique os aplicativos que os utilizam atualmente. O valor **Nome do recurso** aparece em eventos de rastreamento como o ObjectName e em contadores de desempenho e em `sys.dm_os_performance_counters` como o nome da instância. O valor **ID do Recurso** aparece em eventos de rastreamento como o ObjectId.

### <a name="back-up-and-restore"></a>Fazer backup e restaurar

| Recurso substituído | Substituição | Nome do recurso | ID do Recurso |
|--------------------|-------------|--------------|------------|
| RESTORE { DATABASE &#124; LOG } WITH [MEDIA]PASSWORD continua sendo uma opção preterida.<br /><br />As opções BACKUP { DATABASE &#124; LOG } WITH PASSWORD e BACKUP { DATABASE &#124; LOG } WITH MEDIAPASSWORD serão descontinuadas. | Nenhum. | BACKUP DATABASE ou LOG WITH PASSWORD<br /><br />BACKUP DATABASE ou LOG WITH MEDIAPASSWORD | 104<br /><br /> 103 |

### <a name="compatibility-levels"></a>Níveis de compatibilidade

| Recurso substituído | Substituição | Nome do recurso | ID do Recurso |
|--------------------|-------------|--------------|------------|
Atualização da versão 100 (SQL Server 2008 e SQL Server 2008 R2). | Quando uma versão do SQL Server fica sem [suporte](/lifecycle/products/?products=sql-server), o nível de compatibilidade do banco de dados associado é marcado como preterido. No entanto, continuamos dando suporte a aplicativos certificados em qualquer nível de compatibilidade do banco de dados com suporte, contanto que possível, para facilitar as atualizações. Para obter mais informações sobre níveis de compatibilidade, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md). | Nível de compatibilidade do banco de dados 100 | 108 |

### <a name="database-objects"></a>Objetos de banco de dados

| Recurso substituído | Substituição | Nome do recurso | ID do Recurso |
|--------------------|-------------|--------------|------------|
| Capacidade de retornar conjuntos de resultados de gatilhos | Nenhum | Retornando resultados de gatilho | 12 |

### <a name="encryption"></a>Criptografia

| Recurso substituído | Substituição | Nome do recurso | ID do Recurso |
|--------------------|-------------|--------------|------------|
| A criptografia que usa o RC4 ou RC4_128 foi substituída e está programada para ser removida na próxima versão. A descriptografia do RC4 e do RC4_128 não será preterida. | Usar outro algoritmo de criptografia, como AES. | Algoritmo de criptografia substituído | 253 |
| O uso de MD2, MD4, MD5, SHA e SHA1 foi preterido. | Use SHA2_256 ou SHA2_512. Os algoritmos mais antigos continuam funcionando, mas acionam um evento de preterimento. |Algoritmo de hash preterido | Nenhum |

### <a name="remote-servers"></a>Servidores remotos

| Recurso substituído | Substituição | Nome do recurso | ID do Recurso |
|--------------------|-------------|--------------|------------|
| sp_addremotelogin<br /><br />sp_addserver <br /><br /> sp_dropremotelogin <br /><br /> sp_helpremotelogin <br /><br /> sp_remoteoption|Substitua servidores remotos usando servidores vinculados. sp_addserver só pode ser usado com a opção local. | sp_addremotelogin<br /><br />sp_addserver <br /><br /> sp_dropremotelogin <br /><br /> sp_helpremotelogin <br /><br > sp_remoteoption | 70 <br /><br /> 69 <br /><br /> 71 <br /><br /> 72 <br /><br /> 73 |
| \@\@remserver | Substitua servidores remotos usando servidores vinculados. | Nenhum | Nenhum |
| SET REMOTE_PROC_TRANSACTIONS|Substitua servidores remotos usando servidores vinculados. | SET REMOTE_PROC_TRANSACTIONS | 110 |

### <a name="transact-sql"></a>Transact-SQL

| Recurso substituído | Substituição | Nome do recurso | ID do Recurso |
|--------------------|-------------|--------------|------------|
| **SET ROWCOUNT** para as instruções **INSERT**, **UPDATE**e **DELETE** | Palavra-chave TOP | SET ROWCOUNT | 109 |
| Dica de tabela HOLDLOCK sem parênteses. | Use HOLDLOCK com parênteses. | Dica de tabela HOLDLOCK sem parênteses | 167 |

## <a name="features-deprecated-in-a-future-version-of-sql-server"></a>Recursos preteridos em uma versão futura do SQL Server

Os recursos a seguir do Mecanismo de Banco de Dados do SQL Server terão suporte na próxima versão do SQL Server. A versão específica do SQL Server não foi determinada.

### <a name="back-up-and-restore"></a>Fazer backup e restaurar

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| BACKUP { DATABASE &#124; LOG } TO TAPE <br /><br /> BACKUP { DATABASE &#124; LOG } TO *device_that_is_a_tape*|BACKUP { DATABASE &#124; LOG } TO DISK <br /><br /> BACKUP { DATABASE &#124; LOG } TO *device_that_is_a_disk* | BACKUP DATABASE ou LOG TO TAPE |
| sp_addumpdevice '**tape**' | sp_addumpdevice '**disk**' | ADDING TAPE DEVICE |
| sp_helpdevice | sys.backup_devices | sp_helpdevice |

### <a name="compatibility-levels"></a>Níveis de compatibilidade

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| sp_dbcmptlevel|ALTER DATABASE ... SET COMPATIBILITY_LEVEL. Para obter mais informações, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md). | sp_dbcmptlevel |
| Nível de compatibilidade 110 e 120 do banco de dados. | Planeje atualizar o banco de dados e o aplicativo para uma versão futura. No entanto, continuamos dando suporte a aplicativos certificados em qualquer nível de compatibilidade do banco de dados com suporte, contanto que possível, para facilitar as atualizações. Para obter mais informações sobre níveis de compatibilidade, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md). | Nível de compatibilidade 110 do banco de dados <br /><br /> Nível de compatibilidade 120 do banco de dados |

### <a name="collations"></a>Ordenações

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| Korean_Wansung_Unicode <br /><br /> Lithuanian_Classic <br /><br /> SQL_AltDiction_CP1253_CS_AS | Nenhum. Estas ordenações existem no SQL Server 2005 (9.x), mas não são visíveis por meio de fn_helpcollations. | Korean_Wansung_Unicode <br /><br /> Lithuanian_Classic <br /><br /> SQL_AltDiction_CP1253_CS_AS |
| Híndi <br /><br /> Macedônio | Estas ordenações existem no SQL Server 2005 (9.x) e superiores, mas não são visíveis por meio de fn_helpcollations. Em vez disso, use Macedonian_FYROM_90 e Indic_General_90.|Híndi <br /><br /> Macedônio |
| Azeri_Latin_90 <br /><br /> Azeri_Cyrilllic_90 | Azeri_Latin_100 <br /><br /> Azeri_Cyrilllic_100 | Azeri_Latin_90 <br /><br /> Azeri_Cyrilllic_90 |

### <a name="data-types"></a>Tipos de dados

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| sp_addtype <br /><br /> sp_droptype|CREATE TYPE<br /><br /> DROP TYPE | sp_addtype<br /><br /> sp_droptype |
| Sintaxe de**timestamp** para o tipo de dados **rowversion** | Sintaxe do tipo de dados**rowversion** | timestamp |
| Capacidade para inserir valores nulos em colunas **timestamp** . | Em vez disso, use um DEFAULT. | INSERT NULL em colunas TIMESTAMP |
| Opção de tabela 'text in row'|Use os tipos de dados **varchar(max)** , **nvarchar(max)** e **varbinary(max)** . Para obter mais informações, veja [sp_tableoption &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md).|Opção de tabela 'text in row' |
| Tipos de dados:<br /><br /> **text**<br /><br /> **ntext**<br /><br /> **imagem**|Use os tipos de dados **varchar(max)** , **nvarchar(max)** e **varbinary(max)** .|Tipos de dados: **text**, **ntext** ou **image** |

### <a name="database-management"></a>Gerenciamento de banco de dados

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| sp_attach_db <br /><br /> sp_attach_single_file_db|Instrução CREATE DATABASE com a opção FOR ATTACH. Para recriar vários arquivos de log quando um ou mais tiver um novo local, use a opção FOR ATTACH_REBUILD_LOG. | sp_attach_db <br /><br /> sp_attach_single_file_db |
| sp_certify_removable<br /><br /> sp_create_removable|sp_detach_db|sp_certify_removable<br /><br /> sp_create_removable |
| sp_dbremove | DROP DATABASE | sp_dbremove |
| sp_renamedb | MODIFY NAME em ALTER DATABASE | sp_renamedb |

### <a name="database-objects"></a>Objetos de banco de dados

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| CREATE DEFAULT<br /><br /> DROP DEFAULT<br /><br /> sp_bindefault<br /><br /> sp_unbindefault|Palavra-chave DEFAULT em CREATE TABLE e ALTER TABLE|CREATE_DROP_DEFAULT<br /><br /> sp_bindefault<br /><br /> sp_unbindefault |
| CREATE RULE<br /><br /> DROP RULE<br /><br /> sp_bindrule<br /><br /> sp_unbindrule | Palavra-chave CHECK em CREATE TABLE e ALTER TABLE | CREATE_DROP_RULE<br /><br /> sp_bindrule<br /><br /> sp_unbindrule |
| sp_change_users_login | Use ALTER USER. | sp_change_users_login |
| sp_depends | sys.dm_sql_referencing_entities e sys.dm_sql_referenced_entities | sp_depends |
| sp_getbindtoken | Use MARS ou transações distribuídas. | sp_getbindtoken |

### <a name="database-options"></a>Opções de banco de dados

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| sp_bindsession | Use MARS ou transações distribuídas. | sp_bindsession |
| sp_resetstatus | ALTER DATABASE SET { ONLINE &#124; EMERGENCY } | sp_resetstatus
| Opção TORN_PAGE_DETECTION de ALTER DATABASE|Opção PAGE_VERIFY TORN_PAGE_DETECTION de ALTER DATABASE | ALTER DATABASE WITH TORN_PAGE_DETECTION |

### <a name="dbcc"></a>DBCC

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| DBCC DBREINDEX|Opção REBUILD de ALTER INDEX. | DBCC DBREINDEX |
| DBCC INDEXDEFRAG|Opção REORGANIZE de ALTER INDEX | DBCC INDEXDEFRAG |
| DBCC SHOWCONTIG|sys.dm_db_index_physical_stats | DBCC SHOWCONTIG |
| DBCC PINTABLE<br /><br /> DBCC UNPINTABLE | Não tem nenhum efeito. | DBCC [UN]PINTABLE |

### <a name="extended-properties"></a>Propriedades estendidas

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| Level0type = 'type' e Level0type = 'USER' para adicionar propriedades estendidas a objetos de tipo de nível 1 ou nível 2. | Use Level0type = 'USER' apenas para adicionar uma propriedade estendida diretamente a um usuário ou uma função.<br /><br /> Use Level0type = 'SCHEMA' para adicionar uma propriedade estendida a tipos de nível 1, como TABLE ou VIEW, ou a tipos de nível 2, como COLUMN ou TRIGGER. Para obter mais informações, veja [sp_addextendedproperty &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md). | EXTPROP_LEVEL0TYPE<br /><br /> EXTPROP_LEVEL0USER |

### <a name="extended-stored-procedures"></a>Procedimentos armazenados estendidos

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| xp_grantlogin<br /><br /> xp_revokelogin<br /><br /> xp_loginConfig|Use CREATE LOGIN<br /><br /> Use o argumento DROP LOGIN IsIntegratedSecurityOnly de SERVERPROPERTY|xp_grantlogin<br /><br /> xp_revokelogin<br /><br /> xp_loginConfig |

### <a name="extended-stored-procedures-programming"></a>Programação de procedimentos armazenados estendidos

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| srv_alloc<br /><br /> srv_convert<br /><br /> srv_describe<br /><br /> srv_getbindtoken<br /><br /> srv_got_attention<br /><br /> srv_message_handler<br /><br /> srv_paramdata<br /><br /> srv_paraminfo<br /><br /> srv_paramlen<br /><br /> srv_parammaxlen<br /><br /> srv_paramname<br /><br /> srv_paramnumber<br /><br /> srv_paramset<br /><br /> srv_paramsetoutput<br /><br /> srv_paramstatus<br /><br /> srv_paramtype<br /><br /> srv_pfield<br /><br /> srv_pfieldex<br /><br /> srv_rpcdb<br /><br /> srv_rpcname<br /><br /> srv_rpcnumber<br /><br /> srv_rpcoptions<br /><br /> srv_rpcowner<br /><br /> srv_rpcparams<br /><br /> srv_senddone<br /><br /> srv_sendmsg<br /><br /> srv_sendrow<br /><br /> srv_setcoldata<br /><br /> srv_setcollen<br /><br /> srv_setutype<br /><br /> srv_willconvert<br /><br /> srv_wsendmsg | Em vez disso, use a Integração CLR. | XP_API |
| sp_addextendedproc<br /><br /> sp_dropextendedproc<br /><br /> sp_helpextendedproc | Em vez disso, use a Integração CLR. | sp_addextendedproc<br /><br /> sp_dropextendedproc<br /><br /> sp_helpextendedproc |
| xp_grantlogin<br /><br /> xp_revokelogin<br /><br /> xp_loginConfig|Use CREATE LOGIN<br /><br /> Use o argumento DROP LOGIN IsIntegratedSecurityOnly de SERVERPROPERTY | xp_grantlogin<br /><br /> xp_revokelogin<br /><br /> xp_loginConfig |

### <a name="high-availability"></a>Alta disponibilidade

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| espelhamento de banco de dados | Grupos de disponibilidade AlwaysOn<br /><br /> Se a sua edição do SQL Server não der suporte a grupos de disponibilidade Always On, use o envio de logs. | DATABASE_MIRRORING |

### <a name="index-options"></a>Opções de índice

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| sp_indexoption | ALTER INDEX | sp_indexoption |
| Sintaxe de CREATE TABLE, ALTER TABLE ou CREATE INDEX sem parênteses delimitando as opções. | Reescreva a instrução para usar a sintaxe atual. | INDEX_OPTION |

### <a name="instance-options"></a>Opções de instância

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| Opção de sp_configure 'allow updates'|As tabelas do sistema não são mais atualizáveis. A configuração não tem nenhum efeito. | sp_configure 'allow updates' |
| Opções sp_configure: <br /><br /> 'locks' <br /><br /> 'open objects'<br /><br /> 'set working set size' | Agora é configurado automaticamente. A configuração não tem nenhum efeito. | sp_configure 'locks'<br /><br /> sp_configure 'open objects'<br /><br /> sp_configure 'set working set size' |
| Opção de sp_configure 'priority boost' | As tabelas do sistema não são mais atualizáveis. A configuração não tem nenhum efeito. Em vez disso, use a opção start /high ... program.exe do Windows. | sp_configure 'priority boost' |
| Opção de sp_configure 'remote proc trans' | As tabelas do sistema não são mais atualizáveis. A configuração não tem nenhum efeito. | sp_configure 'remote proc trans' |

### <a name="linked-servers"></a>Servidores vinculados

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| Especificando o provedor SQLOLEDB para servidores vinculados. | SQL Server Native Client (SQLNCLI) | SQLOLEDDB para servidores vinculados |

### <a name="metadata"></a>Metadados

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| FILE_ID<br /><br /> INDEXKEY_PROPERTY | FILE_IDEX<br /><br /> sys.index_columns | FILE_ID<br /><br /> INDEXKEY_PROPERTY |

### <a name="native-xml-web-services"></a>Serviços Web XML nativos

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| A instrução CREATE ENDPOINT ou ALTER ENDPOINT com a opção FOR SOAP.<br /><br /> sys.endpoint_webmethods<br /><br /> sys.soap_endpoints|Em vez disso, use o WCF (Windows Communications Foundation) ou o ASP.NET. | CREATE/ALTER ENDPOINT<br /><br /> sys.endpoint_webmethods<br /><br /> EXT_soap_endpoints<br /><br /> sys.soap_endpoints |

### <a name="other"></a>Outros

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| DB-Library<br /><br />Embedded SQL para C|Embora o Mecanismo de Banco de Dados ainda tenha suporte para conexões de aplicativos existentes que usam as APIS de DB-Library e Embedded SQL, ele não inclui a documentação ou os arquivos necessários para fazer o trabalho de programação em aplicativos que usam essas APIs. Uma versão futura do Mecanismo de Banco de Dados do SQL Server descarta o suporte para conexões de DB-Library ou aplicativos do Embedded SQL. Não use DB-Library ou Embedded SQL para desenvolver novos aplicativos. Remova qualquer dependência do DB-Library ou do Embedded SQL ao modificar aplicativos existentes. Em vez destas APIs, use o namespace SQLClient ou uma API como ODBC. O SQL Server 2019 (15.x) não inclui a DLL DB-Library necessária para executar estes aplicativos. Para executar a DB-Library ou os aplicativos Embedded SQL, é necessário ter disponível a DLL DB-Library DLL do SQL Server versão 6.5, SQL Server 7.0 ou SQL Server 2000 (8.x). | Nenhum |

### <a name="security"></a>Segurança

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| A sintaxe ALTER LOGIN WITH SET CREDENTIAL | Substituída pela nova sintaxe ALTER LOGIN ADD e DROP CREDENTIAL | ALTER LOGIN WITH SET CREDENTIAL |
| sp_addapprole<br /><br /> sp_dropapprole | CREATE APPLICATION ROLE<br /><br /> DROP APPLICATION ROLE | sp_addapprole<br /><br /> sp_dropapprole |
| sp_addlogin<br /><br /> sp_droplogin | CREATE LOGIN<br /><br /> DROP LOGIN|sp_addlogin<br /><br /> sp_droplogin |
| sp_adduser<br /><br /> sp_dropuser | CREATE USER<br /><br /> DROP USER|sp_adduser<br /><br /> sp_dropuser |
| sp_grantdbaccess<br /><br /> sp_revokedbaccess|CREATE USER<br /><br /> DROP USER|sp_grantdbaccess<br /><br /> sp_revokedbaccess |
| sp_addrole<br /><br /> sp_droprole | CREATE ROLE<br /><br /> DROP ROLE|sp_addrole<br /><br /> sp_droprole |
| sp_approlepassword<br /><br /> sp_password | ALTER APPLICATION ROLE<br /><br /> ALTER LOGIN|sp_approlepassword<br /><br /> sp_password |
| sp_changedbowner|ALTER AUTHORIZATION | sp_changedbowner |
| sp_changeobjectowner|ALTER SCHEMA ou ALTER AUTHORIZATION | sp_changeobjectowner |
| sp_control_dbmasterkey_password | Uma chave mestra deve existir e a senha deve estar correta.|sp_control_dbmasterkey_password |
| sp_defaultdb<br /><br /> sp_defaultlanguage | ALTER LOGIN|sp_defaultdb<br /><br /> sp_defaultlanguage |
| sp_denylogin<br /><br /> sp_grantlogin<br /><br /> sp_revokelogin|ALTER LOGIN DISABLE<br /><br /> CREATE LOGIN<br /><br /> DROP LOGIN|sp_denylogin<br /><br /> sp_grantlogin<br /><br /> sp_revokelogin |
| USER_ID|DATABASE_PRINCIPAL_ID | USER_ID |
| sp_srvrolepermission<br /><br /> sp_dbfixedrolepermission|Estes procedimentos armazenados retornam as informações que estavam corretas no [!INCLUDE[ssVersion2000](../includes/ssversion2000-md.md)]. A saída não reflete alterações na hierarquia de permissões implementada no SQL Server 2008. Para obter mais informações, consulte [Permissões de funções de servidor fixas](https://msdn.microsoft.com/library/ms175892\(SQL.100\).aspx). | sp_srvrolepermission<br /><br /> sp_dbfixedrolepermission |
| GRANT ALL<br /><br /> DENY ALL<br /><br /> REVOKE ALL|Permissões específicas a GRANT, DENY e REVOKE.|Permissão ALL |
| Função intrínseca PERMISSIONS | Consulte sys.fn_my_permissions. | PERMISSIONS |
| SETUSER | EXECUTE AS | SETUSER |
| Algoritmos de criptografia RC4 e DESX|Usar outro algoritmo, como AES. | Algoritmo DESX |

### <a name="server-configuration-options"></a>Opções de configuração de servidor

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| opção audit c2 opção default trace enabled<br /><br /> opção default trace enabled | [Opção de configuração de servidor com conformidade de critérios comuns habilitada](../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md)<br /><br /> [Eventos estendidos](../relational-databases/extended-events/extended-events.md) | sp_configure 'c2 audit mode'<br /><br />sp_configure 'default trace enabled' |

### <a name="smo-classes"></a>Classes SMO

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| Classe *Microsoft.SQLServer. Management.Smo.Information*<br /><br />Classe *Microsoft.SQLServer. Management.Smo.Settings*<br /><br />*Microsoft.SQLServer.Management. Smo.DatabaseOptions*<br /><br />Propriedade *Microsoft.SqlServer.Management.Smo. DatabaseDdlTrigger.NotForReplication* | Classe *Microsoft.SqlServer.  Management.Smo.Server*<br /><br />**Classe Microsoft.SqlServer.  Management.Smo.Server* Classe<br /><br />* Microsoft.SqlServer. Management.Smo.Database*<br /><br />Nenhum | Nenhum |

### <a name="sql-server-agent"></a>SQL Server Agent

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| Notificação**net send**<br /><br />Notificação por pager | Notificação por email<br /><br />Notificação por email | Nenhum |

### <a name="sql-server-management-studio"></a>SQL Server Management Studio

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| Integração do Gerenciador de Soluções no SQL Server Management Studio | | Nenhum |

### <a name="system-stored-procedures-and-functions"></a>Funções e procedimentos armazenados no sistema

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| sp_db_increased_partitions | Nenhum. O suporte ao aumento de partições está disponível, por padrão, no SQL Server 2019 (15.x). | sp_db_increased_partitions |
| fn_virtualservernodes<br /><br />fn_servershareddrives | sys.dm_os_cluster_nodes<br /><br />sys.dm_io_cluster_shared_drives | fn_virtualservernodes<br /><br /> fn_servershareddrives |
| fn_get_sql | sys.dm_exec_sql_text | fn_get_sql |
| sp_lock | sys.dm_tran_locks | sp_lock |

### <a name="system-tables"></a>Tabelas do sistema

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| sysaltfiles<br /><br />syscacheobjects<br /><br />syscolumns<br /><br />syscomments<br /><br />sysconfigures<br /><br />sysconstraints<br /><br />syscurconfigs<br /><br />sysdatabases<br /><br />sysdepends<br /><br />sysdevices<br /><br />sysfilegroups<br /><br />sysfiles<br /><br />sysforeignkeys<br /><br />sysfulltextcatalogs<br /><br />sysindexes<br /><br />sysindexkeys<br /><br />syslockinfo<br /><br />syslogins<br /><br />sysmembers<br /><br />sysmessages<br /><br />sysobjects<br /><br />sysoledbusers<br /><br />sysopentapes<br /><br />sysperfinfo<br /><br />syspermissions<br /><br />sysprocesses<br /><br />sysprotects<br /><br />sysreferences<br /><br />sysremotelogins<br /><br />sysservers<br /><br />systypes<br /><br />sysusers|Exibições de compatibilidade. Para obter mais informações, veja [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md).<br /><br />**Importante:** as exibições de compatibilidade não expõem metadados para os recursos introduzidos no SQL Server 2005 (9.x). É recomendável atualizar seus aplicativos para usar exibições do catálogo. Para obter mais informações, veja [Exibições de catálogo e&#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/catalog-views-transact-sql.md). | sysaltfiles<br /><br />syscacheobjects<br /><br />syscolumns<br /><br />syscomments<br /><br />sysconfigures<br /><br />sysconstraints<br /><br />syscurconfigs<br /><br />sysdatabases<br /><br />sysdepends<br /><br />sysdevices<br /><br />sysfilegroups<br /><br />sysfiles<br /><br />sysforeignkeys<br /><br />sysfulltextcatalogs<br /><br />sysindexes<br /><br />sysindexkeys<br /><br />syslockinfo<br /><br />syslogins<br /><br />sysmembers<br /><br />sysmessages<br /><br />sysobjects<br /><br />sysoledbusers<br /><br />sysopentapes<br /><br />sysperfinfo<br /><br />syspermissions<br /><br />sysprocesses<br /><br />sysprotects<br /><br />sysreferences<br /><br />sysremotelogins<br /><br />sysservers<br /><br />systypes<br /><br />sysusers |
| sys.numbered_procedures<br /><br />sys.numbered_procedure_parameters | Nenhum | numbered_procedures<br /><br />numbered_procedure_parameters |

### <a name="sql-trace-stored-procedures-functions-and-catalog-views"></a>Procedimentos armazenados, funções e exibições de catálogo do Rastreamento do SQL

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| sp_trace_create<br /><br />sp_trace_setevent<br /><br />sp_trace_setfilter<br /><br />sp_trace_setstatus<br /><br />fn_trace_geteventinfo<br /><br />fn_trace_getfilterinfo<br /><br />fn_trace_getinfo<br /><br />fn_trace_gettable<br /><br />sys.traces<br /><br />sys.trace_events<br /><br />sys.trace_event_bindings<br /><br />sys.trace_categories<br /><br />sys.trace_columns<br /><br />sys.trace_subclass_values|[Eventos estendidos](../relational-databases/extended-events/extended-events.md) | sp_trace_create<br /><br />sp_trace_setevent<br /><br />sp_trace_setfilter<br /><br />sp_trace_setstatus<br /><br />fn_trace_geteventinfo<br /><br />fn_trace_getfilterinfo<br /><br />fn_trace_getinfo<br /><br />fn_trace_gettable<br /><br />sys.traces<br /><br />sys.trace_events<br /><br />sys.trace_event_bindings<br /><br />sys.trace_categories<br /><br />sys.trace_columns<br /><br />sys.trace_subclass_values |

### <a name="system-views"></a>Exibições do sistema

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| sys.sql_dependencies|sys.sql_expression_dependencies|sys.sql_dependencies |

### <a name="table-compression"></a>Compactação de tabela

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| O uso do formato de armazenamento vardecimal. | O formato de armazenamento vardecimal foi preterido. Compactação de dados do SQL Server 2019 (15.x), compacta valores decimais e outros tipos de dados. É recomendável usar a compactação de dados em vez do formato de armazenamento vardecimal. | Formato de armazenamento vardecimal |
| Uso do procedimento sp_db_vardecimal_storage_format.|O formato de armazenamento vardecimal foi preterido. Compactação de dados do SQL Server 2019 (15.x), compacta valores decimais e outros tipos de dados. É recomendável usar a compactação de dados em vez do formato de armazenamento vardecimal. | sp_db_vardecimal_storage_format |
| Uso do procedimento sp_estimated_rowsize_reduction_for_vardecimal.|Use a compactação de dados e o procedimento sp_estimate_data_compression_savings em vez disso. |sp_estimated_rowsize_reduction_for_vardecimal |

### <a name="text-pointers"></a>Ponteiros de texto

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| WRITETEXT<br /><br />UPDATETEXT<br /><br />READTEXT|Nenhum|UPDATETEXT ou WRITETEXT<br /><br />READTEXT |
| TEXTPTR()<br /><br />TEXTVALID() | Nenhum | TEXTPTR<br /><br />TEXTVALID |

### <a name="transact-sql"></a>Transact-SQL

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| Sequência da chamada de função :: | Substituído por SELECT *column_list* FROM sys.\<*function_name*>().<br /><br />Por exemplo, substitua `SELECT * FROM ::fn_virtualfilestats(2,1)`por `SELECT * FROM sys.fn_virtualfilestats(2,1)`. | sintaxe '::' de chamada de função |
| Referências de coluna de três e quatro partes. | Nomes com duas partes são o comportamento em conformidade com o padrão.|Nome de coluna com mais de duas partes |
| Uma cadeia de caracteres entre aspas usada como um alias de coluna para uma expressão em uma lista SELECT:<br /><br />'*string_alias*' = *expression* | *expression* [AS] *column_alias*<br /><br />*expression* [AS] [*column_alias*]<br /><br />*expression* [AS] "*column_alias*"<br /><br />*expression* [AS] '*column_alias*'<br /><br />*column_alias* = *expression* | Literais de cadeia de caracteres como aliases de coluna |
| Procedimentos numerados | Nenhum. Não use. | ProcNums |
| Sintaxe*table_name.index_name* em DROP INDEX|Sintaxe*index_name* ON *table_name* em DROP INDEX.|DROP INDEX com nome de duas partes |
| Não terminar instruções Transact-SQL com um ponto e vírgula.|Terminar instruções Transact-SQL com um ponto e vírgula (;). | Nenhum |
| GROUP BY ALL|Use solução caso a caso personalizada com UNION ou tabela derivada. | GROUP BY ALL |
| ROWGUIDCOL como um nome de coluna em instruções DML.|Use $rowguid.|ROWGUIDCOL |
| IDENTITYCOL como um nome de coluna em instruções DML.|Use $identity.|IDENTITYCOL |
| Uso de #, ## como tabela temporária e nomes de procedimento armazenado temporários. | Use pelo menos um caractere adicional.|'#' e '##' como o nome de tabelas temporárias e procedimentos armazenados
| O uso de \@, \@\@ ou \@\@ como identificadores Transact-SQL. | Não use \@ nem \@\@ ou nomes que comecem com \@\@ como identificadores. | '\@' e nomes que começam com '\@\@' como identificadores de Transact-SQL |
| Uso da palavra-chave DEFAULT como valor padrão.|Não use a palavra DEFAULT como um valor padrão. | A palavra-chave DEFAULT como um valor padrão |
| Uso de um espaço como um separador entre dicas de tabela.|Use uma vírgula para separar dicas de tabela. | Várias dicas de tabela sem vírgula |
| A lista de seleção de uma exibição indexada de agregação deve conter COUNT_BIG (\*) no modo de compatibilidade 90 | Use COUNT_BIG (\*). | A exibição de índice seleciona a lista sem COUNT_BIG(\*) |
| O aplicativo indireto de dicas de tabela para uma invocação de uma função com valor de tabela (TVF) de várias instruções por meio de uma exibição.|Nenhum.|Dicas TVF indiretas |
| Sintaxe ALTER DATABASE:<br /><br />MODIFY FILEGROUP READONLY<br /><br />MODIFY FILEGROUP READWRITE | MODIFY FILEGROUP READ_ONLY<br /><br />MODIFY FILEGROUP READ_WRITE | MODIFY FILEGROUP READONLY<br /><br />MODIFY FILEGROUP READWRITE |
| Opção de banco de dados SET ANSI_NULLS OFF e ANSI_NULLS OFF<br /><br />Opção de banco de dados SET ANSI_PADDING OFF e ANSI_PADDING OFF<br /><br />Opção de banco de dados SET CONCAT_NULL_YIELDS_NULL OFF e CONCAT_NULL_YIELDS_NULL OFF<br /><br />SET OFFSETS | Nenhum. <br /><br /> ANSI_NULLS, ANSI_PADDING e CONCAT_NULLS_YIELDS_NULL sempre são definidos como ON. SET OFFSETS não estão disponíveis. | SET ANSI_NULLS OFF <br /><br /> SET ANSI_PADDING OFF<br /><br />SET CONCAT_NULL_YIELDS_NULL OFF<br /><br />SET OFFSETS<br /><br />ALTER DATABASE SET ANSI_NULLS OFF<br /><br />ALTER DATABASE SET ANSI_PADDING OFF <br /><br /> ALTER DATABASE SET CONCAT_NULL_YIELDS_NULL OFF |
| SET FMTONLY | [sys.dm_exec_describe_first_result_set &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md), [sys.dm_exec_describe_first_result_set_for_object &#40;Transact-SQL&#41;](../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md), [sp_describe_first_result_set &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) e [sp_describe_undeclared_parameters &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md). | SET FMTONLY |
| Especificando NOLOCK ou READUNCOMMITTED na cláusula FROM de uma instrução UPDATE ou DELETE. | Remova as dicas de tabela NOLOCK ou READUNCOMMITTED da cláusula FROM. | NOLOCK ou READUNCOMMITTED em UPDATE ou DELETE |
| Especificando dicas de tabela sem usar a palavra-chave WITH. | Use WITH. | Dica de tabela sem WITH |
| INSERT_HINTS | | INSERT_HINTS |

### <a name="tools"></a>Ferramentas

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| SQL Server Profiler para captura de rastreamento | Use o Extended Events Profiler inserido no SQL Server Management Studio.|SQL Server Profiler |
| SQL Server Profiler para reprodução de rastreamento | [SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md) |

### <a name="trace-management-objects"></a>Trace Management Objects

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| Namespace Microsoft.SqlServer.Management.Trace (contém as APIs para Rastreamento do SQL Server e objetos de reprodução)|Configuração de Rastreamento: <xref:Microsoft.SqlServer.Management.XEvent><br /><br />Leitura de Rastreamento: <xref:Microsoft.SqlServer.XEvent.Linq><br /><br />Reprodução de rastreamento: Nenhum | |

### <a name="xml"></a>XML

| Recurso substituído | Substituição | Nome do recurso |
|--------------------|-------------|--------------|
| Geração de esquema XDR embutido | A diretiva XMLDATA para a opção FOR XML foi preterida. Use geração de XSD no caso dos modos RAW e AUTO. Não há substituição para a diretiva XMLDATA no modo EXPLICIT. | XMLDATA |

> [!NOTE]
> O parâmetro **OUTPUT** de cookie para **sp_setapprole** está documentado atualmente como **varbinary(8000)** , que tem o tamanho máximo correto. No entanto, a implementação atual retorna **varbinary(50)** . Se os desenvolvedores alocaram **varbinary(50)** , o aplicativo poderá exigir alterações se o cookie retornar aumentos de tamanho em uma versão futura. Embora não seja um problema de substituição, isto é mencionado neste tópico porque os ajustes de aplicativo são semelhantes. Para obter mais informações, veja [sp_setapprole &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/sp-setapprole-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Funcionalidade do Mecanismo de Banco de Dados descontinuada no SQL Server 2016](./discontinued-database-engine-functionality-in-sql-server.md)  

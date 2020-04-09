---
title: sys.database_principals (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_principals
- database_principals_TSQL
- sys.database_principals
- sys.database_principals_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_principals catalog view
ms.assetid: 8cb239e9-eb8c-4109-9cec-0d35de95fa0e
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: feed483cf3ee08c0652e55de51b1f73fc087ed39
ms.sourcegitcommit: 7ed12a64f7f76d47f5519bf1015d19481dd4b33a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80873110"
---
# <a name="sysdatabase_principals-transact-sql"></a>sys.database_principals (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha para cada entidade de segurança em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**Sysname**|Nome da entidade de segurança, exclusivo no banco de dados.|  
|**principal_id**|**Int**|ID da entidade de segurança, exclusiva no banco de dados.|  
|**type**|**char(1)**|Tipo do principal:<br /><br /> A = Função de aplicativo<br /><br /> C = Usuário mapeado para um certificado<br /><br /> E = Usuário externo do Azure Active Directory<br /><br /> G = Grupo do Windows<br /><br /> K = Usuário mapeado para uma chave assimétrica<br /><br /> R = Função de banco de dados<br /><br /> S = Usuário do SQL<br /><br /> U = Usuário do Windows<br /><br /> X = Grupo externo do grupo ou aplicativos do Azure Active Directory|  
|**type_desc**|**nvarchar(60)**|Descrição do tipo de principal.<br /><br /> APPLICATION_ROLE<br /><br /> CERTIFICATE_MAPPED_USER<br /><br /> EXTERNAL_USER<br /><br /> WINDOWS_GROUP<br /><br /> ASYMMETRIC_KEY_MAPPED_USER<br /><br /> DATABASE_ROLE<br /><br /> SQL_USER<br /><br /> WINDOWS_USER<br /><br /> EXTERNAL_GROUPS|  
|**default_schema_name**|**Sysname**|Nome a ser usado quando o nome SQL não especificar um esquema. Nulo para principais que não sejam do tipo S, U ou A.|  
|**create_date**|**datetime**|Hora em que o principal foi criado.|  
|**modify_date**|**datetime**|Hora em que a entidade de segurança foi modificada pela última vez.|  
|**owning_principal_id**|**Int**|ID da entidade de segurança que é proprietária desta entidade de segurança. Todas as Funções de Banco de Dados fixas são de propriedade **da dbo** por padrão.|  
|**Sid**|**varbinary(85)**|SID (ID de segurança) da entidade de segurança.  NULL for SYS e INFORMATION SCHEMAS.|  
|**is_fixed_role**|**bit**|Se 1, essa linha representará uma entrada para uma das funções de banco de dados fixa: db_owner, db_accessadmin, db_datareader, db_datawriter, db_ddladmin, db_securityadmin, db_backupoperator, db_denydatareader, db_denydatawriter.|  
|**authentication_type**|**Int**|**Aplica-se** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a : e depois.<br /><br /> Significa um tipo de autenticação. A seguir, os possíveis valores e suas descrições.<br /><br /> 0 : Sem autenticação<br />1 : Autenticação de instâncias<br />2 : Autenticação de banco de dados<br />3 : Autenticação do Windows<br />4 : Autenticação do Diretório Ativo do Azure|  
|**authentication_type_desc**|**nvarchar(60)**|**Aplica-se** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a : e depois.<br /><br /> Descrição do tipo de autenticação. A seguir, os possíveis valores e suas descrições.<br /><br /> NONE : Sem autenticação<br />INSTÂNCIA : Autenticação de instâncias<br />BANCO DE DADOS : Autenticação de banco de dados<br />WINDOWS : Autenticação do Windows<br />EXTERNAL: Autenticação do Diretório Ativo do Azure|  
|**default_language_name**|**Sysname**|**Aplica-se** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a : e depois.<br /><br /> Significa o idioma padrão para esta entidade de segurança.|  
|**default_language_lcid**|**Int**|**Aplica-se** [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a : e depois.<br /><br /> Significa o LCID padrão para esta entidade de segurança.|  
|**allow_encrypted_value_modifications**|**bit**|**Aplica-se** [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] a : [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]e mais tarde, .<br /><br /> Suprime as verificações de metadados criptográficos no servidor em operações de cópia em massa. Isso permite que o usuário copie em massa dados criptografados usando Always Encrypted, entre tabelas ou bancos de dados, sem descriptografar os dados. O padrão é OFF. |      
  
## <a name="remarks"></a>Comentários  
 As propriedades *PasswordLastSetTime* estão disponíveis em todas as configurações suportadas do SQL Server, mas as outras propriedades só estão disponíveis quando o SQL Server está sendo executado no Windows Server 2003 ou posterior e tanto CHECK_POLICY quanto CHECK_EXPIRATION estão habilitados. Consulte [a Política de Senhas](../../relational-databases/security/password-policy.md) para obter mais informações.
Os valores do principal_id podem ser reutilizados no caso de os diretores terem sido descartados e, portanto, não é garantido que os princípios sejam cada vez maiores.
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário pode ver seu próprio nome de usuário, os usuários do sistema e as funções de banco de dados fixas. Ver outros usuários requer ALTER ANY USER ou uma permissão no usuário. Ver funções definidas pelo usuário requer ALTER ANY ROLE ou associação na função.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-listing-all-the-permissions-of-database-principals"></a>A: Listando todas as permissões de entidades de segurança do banco de dados  
 A consulta a seguir lista as permissões concedidas ou negadas explicitamente a entidades de segurança do banco de dados.  
  
> [!IMPORTANT]  
>  As permissões de funções de banco de dados fixas não aparecem em sys.database_permissions. Portanto, entidades de segurança do banco de dados podem ter permissões adicionais não listadas aqui.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc, pe.permission_name  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
### <a name="b-listing-permissions-on-schema-objects-within-a-database"></a>B: Listando permissões a objetos de esquema em um banco de dados  
 A consulta a seguir une sys.database_principals e sys.database_permissions com sys.objects e sys.schemas para listar permissões concedidas ou negadas a objetos de esquema específicos.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc,   
    pe.permission_name, s.name + '.' + o.name AS ObjectName  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id  
JOIN sys.objects AS o  
    ON pe.major_id = o.object_id  
JOIN sys.schemas AS s  
    ON o.schema_id = s.schema_id;  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-listing-all-the-permissions-of-database-principals"></a>C: Listar todas as permissões dos diretores de banco de dados  
 A consulta a seguir lista as permissões concedidas ou negadas explicitamente a entidades de segurança do banco de dados.  
  
> [!IMPORTANT]  
>  As permissões de funções de `sys.database_permissions`banco de dados fixos não aparecem em . Portanto, entidades de segurança do banco de dados podem ter permissões adicionais não listadas aqui.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc, pe.permission_name  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
### <a name="d-listing-permissions-on-schema-objects-within-a-database"></a>D: Listar permissões em objetos de esquema dentro de um banco de dados  
 A consulta a `sys.database_principals` `sys.database_permissions` seguir `sys.objects` `sys.schemas` se junta e lista permissões concedidas ou negadas a objetos específicos de esquema.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc,   
    pe.permission_name, s.name + '.' + o.name AS ObjectName  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id  
JOIN sys.objects AS o  
    ON pe.major_id = o.object_id  
JOIN sys.schemas AS s  
    ON o.schema_id = s.schema_id;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Principais &#40;&#41;do mecanismo de banco de dados](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [Visualizações do catálogo de segurança &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Usuários de banco de dados contidos - tornando seu banco de dados portátil](../../relational-databases/security/contained-database-users-making-your-database-portable.md)   
 [Conectando-se ao banco de dados SQL usando a autenticação do diretório ativo do Azure](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication)  
  
  



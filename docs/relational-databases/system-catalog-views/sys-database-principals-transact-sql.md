---
title: sys. database_principals (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 8773d6a3a8b65520fad6342477300f8818e9ac4d
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86011967"
---
# <a name="sysdatabase_principals-transact-sql"></a>sys.database_principals (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna uma linha para cada entidade de segurança em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome da entidade de segurança, exclusivo no banco de dados.|  
|**principal_id**|**int**|ID da entidade de segurança, exclusiva no banco de dados.|  
|**type**|**Char (1)**|Tipo do principal:<br /><br /> A = Função de aplicativo<br /><br /> C = Usuário mapeado para um certificado<br /><br /> E = usuário externo do Azure Active Directory<br /><br /> G = Grupo do Windows<br /><br /> K = Usuário mapeado para uma chave assimétrica<br /><br /> R = Função de banco de dados<br /><br /> S = Usuário do SQL<br /><br /> U = Usuário do Windows<br /><br /> X = grupo externo de Azure Active Directory grupo ou aplicativos|  
|**type_desc**|**nvarchar(60)**|Descrição do tipo de principal.<br /><br /> APPLICATION_ROLE<br /><br /> CERTIFICATE_MAPPED_USER<br /><br /> EXTERNAL_USER<br /><br /> WINDOWS_GROUP<br /><br /> ASYMMETRIC_KEY_MAPPED_USER<br /><br /> DATABASE_ROLE<br /><br /> SQL_USER<br /><br /> WINDOWS_USER<br /><br /> EXTERNAL_GROUPS|  
|**default_schema_name**|**sysname**|Nome a ser usado quando o nome SQL não especificar um esquema. Nulo para principais que não sejam do tipo S, U ou A.|  
|**create_date**|**datetime**|Hora em que o principal foi criado.|  
|**modify_date**|**datetime**|Hora em que a entidade de segurança foi modificada pela última vez.|  
|**owning_principal_id**|**int**|ID da entidade de segurança que é proprietária desta entidade de segurança. Todas as funções de banco de dados fixas pertencem a **dbo** por padrão.|  
|**sid**|**varbinary (85)**|SID (ID de segurança) da entidade de segurança.  NULL for SYS e INFORMATION SCHEMAS.|  
|**is_fixed_role**|**bit**|Se 1, essa linha representará uma entrada para uma das funções de banco de dados fixa: db_owner, db_accessadmin, db_datareader, db_datawriter, db_ddladmin, db_securityadmin, db_backupoperator, db_denydatareader, db_denydatawriter.|  
|**authentication_type**|**int**|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> Significa um tipo de autenticação. A seguir estão os possíveis valores e suas descrições.<br /><br /> 0: sem autenticação<br />1: autenticação da instância<br />2: autenticação de banco de dados<br />3: autenticação do Windows<br />4: autenticação Azure Active Directory|  
|**authentication_type_desc**|**nvarchar(60)**|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> Descrição do tipo de autenticação. A seguir estão os possíveis valores e suas descrições.<br /><br /> NENHUM: sem autenticação<br />INSTÂNCIA: autenticação de instância<br />BANCO de dados: autenticação de banco de dados<br />WINDOWS: autenticação do Windows<br />EXTERNO: autenticação de Azure Active Directory|  
|**default_language_name**|**sysname**|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> Significa o idioma padrão para esta entidade de segurança.|  
|**default_language_lcid**|**int**|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> Significa o LCID padrão para esta entidade de segurança.|  
|**allow_encrypted_value_modifications**|**bit**|**Aplica-se a**: [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] e posterior, [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Suprime as verificações de metadados criptográficos no servidor em operações de cópia em massa. Isso permite que o usuário Copie dados em massa criptografados usando Always Encrypted, entre tabelas ou bancos de dados, sem descriptografá-los. O padrão é OFF. |      
  
## <a name="remarks"></a>Comentários  
 As propriedades *PasswordLastSetTime* estão disponíveis em todas as configurações com suporte de SQL Server, mas as outras propriedades só estarão disponíveis quando SQL Server estiver em execução no Windows Server 2003 ou posterior e CHECK_POLICY e CHECK_EXPIRATION estiverem habilitados. Consulte [política de senha](../../relational-databases/security/password-policy.md) para obter mais informações.
Os valores da principal_id podem ser reutilizados caso as entidades tenham sido descartadas e, portanto, não há garantia de que estejam sempre aumentando.
  
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
  
### <a name="c-listing-all-the-permissions-of-database-principals"></a>C: listando todas as permissões de entidades de banco de dados  
 A consulta a seguir lista as permissões concedidas ou negadas explicitamente a entidades de segurança do banco de dados.  
  
> [!IMPORTANT]  
>  As permissões de funções de banco de dados fixas não aparecem no `sys.database_permissions` . Portanto, entidades de segurança do banco de dados podem ter permissões adicionais não listadas aqui.  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc, pe.permission_name  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
### <a name="d-listing-permissions-on-schema-objects-within-a-database"></a>D: listando permissões em objetos de esquema em um banco de dados  
 A consulta a seguir une `sys.database_principals` e `sys.database_permissions` para `sys.objects` `sys.schemas` listar permissões concedidas ou negadas a objetos de esquema específicos.  
  
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
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys. server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [Exibições do catálogo de segurança &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Usuários de banco de dados independente-tornando seu banco de dados portátil](../../relational-databases/security/contained-database-users-making-your-database-portable.md)   
 [Conectar-se ao Banco de Dados SQL usando a autenticação do Azure Active Directory](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication)  
  
  



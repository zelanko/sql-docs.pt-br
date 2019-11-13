---
title: sys. database_permissions (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_permissions
- sys.database_permissions_TSQL
- database_permissions_TSQL
- sys.database_permissions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_permissions catalog view
ms.assetid: c1e261f8-6cb0-4759-b5f1-5ec233602655
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a87be6fe0a68172a99ade4704ae4111cabbe95f1
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982734"
---
# <a name="sysdatabase_permissions-transact-sql"></a>sys.database_permissions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha para cada permissão ou permissão de exceção de coluna no banco de dados. Para colunas, há uma linha para cada permissão que é diferente da permissão no nível de objeto correspondente. Se a permissão de coluna for igual à permissão de objeto correspondente, não haverá nenhuma linha para ela e a permissão aplicada será a do objeto.  
  
> [!IMPORTANT]  
>  As permissões em nível de coluna substituem as permissões em nível de objeto na mesma entidade.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**class**|**tinyint**|Identifica a classe na qual existe a permissão.<br /><br /> 0 = Banco de dados<br />1 = objeto ou coluna<br />3 = Esquema<br />4 = Entidade do Banco de Dados<br />5 = assembly- **aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.<br />6 = Tipo<br />10 = coleção de esquemas XML- <br />                      **Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.<br />15 = tipo de mensagem – **aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.<br />16 = contrato de serviço – **aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.<br />17 = serviço- **aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.<br />18 = Associação de serviço remoto – **aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.<br />19 = rota- **aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.<br />23 = catálogo de texto completo – **aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.<br />24 = chave simétrica – **aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.<br />25 = Certificate- **aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.<br />26 = chave assimétrica- **aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.|  
|**class_desc**|**nvarchar(60)**|Descrição de classe na qual a permissão existe.<br /><br /> DATABASE<br /><br /> OBJECT_OR_COLUMN<br /><br /> SCHEMA<br /><br /> DATABASE_PRINCIPAL<br /><br /> ASSEMBLY<br /><br /> TYPE<br /><br /> XML_SCHEMA_COLLECTION<br /><br /> MESSAGE_TYPE<br /><br /> SERVICE_CONTRACT<br /><br /> SERVICE<br /><br /> REMOTE_SERVICE_BINDING<br /><br /> ROUTE<br /><br /> FULLTEXT_CATALOG<br /><br /> SYMMETRIC_KEYS<br /><br /> CERTIFICATE<br /><br /> ASYMMETRIC_KEY|  
|**major_id**|**int**|ID na qual a permissão existe, interpretada de acordo com a classe. Normalmente, o **major_id** é simplesmente o tipo de ID que se aplica ao que a classe representa. <br /><br /> 0 = o próprio banco de dados <br /><br /> > 0 = IDs de objeto para objetos de usuário <br /><br /> \<0 = IDs de objeto para objetos do sistema |  
|**minor_id**|**int**|ID secundária de algo no qual a permissão existe, interpretada de acordo com a classe. Geralmente, o **minor_id** é zero, porque não há nenhuma subcategoria disponível para a classe de objeto. Caso contrário, é a ID de coluna de uma tabela.|  
|**grantee_principal_id**|**int**|ID do principal de banco de dados para a qual as permissões são concedidas.|  
|**grantor_principal_id**|**int**|ID do principal de banco de dados do concessor dessas permissões.|  
|**tipo**|**char(4)**|Tipo de permissão de banco de dados. Para obter uma lista de tipos de permissão, consulte a próxima tabela.|  
|**permission_name**|**nvarchar(128)**|Nome de permissão.|  
|**state**|**char(1)**|Estado de permissão:<br /><br /> D = Negar<br /><br /> R = Revogar<br /><br /> G = Conceder<br /><br /> W = Opção Concessão com Concessão|  
|**state_desc**|**nvarchar(60)**|Descrição do estado da permissão:<br /><br /> DENY<br /><br /> REVOKE<br /><br /> GRANT<br /><br /> GRANT_WITH_GRANT_OPTION|  

## <a name="database-permissions"></a>Permissões de banco de dados   
Os seguintes tipos de permissões são possíveis.
  
|Tipo de permissão|Nome de permissão|Aplica-se a protegíveis|  
|---------------------|---------------------|--------------------------|  
|AADS |ALTER ANY DATABASE EVENT SESSION |DATABASE |  
|AAMK |ALTER ANY MASK |DATABASE |  
|AEDS |ALTER ANY EXTERNAL DATA SOURCE |DATABASE |  
|AEFF |ALTER ANY EXTERNAL FILE FORMAT |DATABASE |  
|AL|ALTER|APPLICATION ROLE, ASSEMBLY, ASYMMETRIC KEY, CERTIFICATE, CONTRACT, DATABASE, FULLTEXT CATALOG, MESSAGE TYPE, OBJECT, REMOTE SERVICE BINDING, ROLE, ROUTE, SCHEMA, SERVICE, SYMMETRIC KEY, USER, XML SCHEMA COLLECTION|  
|ALAK|ALTER ANY ASYMMETRIC KEY|DATABASE|  
|ALAR|ALTER ANY APPLICATION ROLE|DATABASE|  
|ALAS|ALTER ANY ASSEMBLY|DATABASE|  
|ALCF|ALTER ANY CERTIFICATE|DATABASE|  
|ALDS|ALTER ANY DATASPACE|DATABASE|  
|ALED|ALTER ANY DATABASE EVENT NOTIFICATION|DATABASE|  
|ALFT|ALTER ANY FULLTEXT CATALOG|DATABASE|  
|ALMT|ALTER ANY MESSAGE TYPE|DATABASE|  
|ALRL|ALTER ANY ROLE|DATABASE|  
|ALRT|ALTER ANY ROUTE|DATABASE|  
|ALSB|ALTER ANY REMOTE SERVICE BINDING|DATABASE|  
|ALSC|ALTER ANY CONTRACT|DATABASE|  
|ALSK|ALTER ANY SYMMETRIC KEY|DATABASE|  
|ALSM|ALTER ANY SCHEMA|DATABASE|  
|ALSV|ALTER ANY SERVICE|DATABASE|  
|ALTG|ALTER ANY DATABASE DDL TRIGGER|DATABASE|  
|ALUS|ALTER ANY USER|DATABASE|  
|AUTH|AUTHENTICATE|DATABASE|  
|BADB|BACKUP DATABASE|DATABASE|  
|BALO|BACKUP LOG|DATABASE|  
|CL|CONTROL|APPLICATION ROLE, ASSEMBLY, ASYMMETRIC KEY, CERTIFICATE, CONTRACT, DATABASE, FULLTEXT CATALOG, MESSAGE TYPE, OBJECT, REMOTE SERVICE BINDING, ROLE, ROUTE, SCHEMA, SERVICE, SYMMETRIC KEY, TYPE, USER, XML SCHEMA COLLECTION|  
|CO|CONNECT|DATABASE|  
|CORP|CONNECT REPLICATION|DATABASE|  
|CP|CHECKPOINT|DATABASE|  
|CRAG|CREATE AGGREGATE|DATABASE|  
|CRAK|CREATE ASYMMETRIC KEY|DATABASE|  
|CRAS|CREATE ASSEMBLY|DATABASE|  
|CRCF|CREATE CERTIFICATE|DATABASE|  
|CRDB|CREATE DATABASE|DATABASE|  
|CRDF|CREATE DEFAULT|DATABASE|  
|CRED|CREATE DATABASE DDL EVENT NOTIFICATION|DATABASE|  
|CRFN|CREATE FUNCTION|DATABASE|  
|CRFT|CREATE FULLTEXT CATALOG|DATABASE|  
|CRMT|CREATE MESSAGE TYPE|DATABASE|  
|CRPR|CREATE PROCEDURE|DATABASE|  
|CRQU|CREATE QUEUE|DATABASE|  
|CRRL|CREATE ROLE|DATABASE|  
|CRRT|CREATE ROUTE|DATABASE|  
|CRRU|CREATE RULE|DATABASE|  
|CRSB|CREATE REMOTE SERVICE BINDING|DATABASE|  
|CRSC|CREATE CONTRACT|DATABASE|  
|CRSK|CREATE SYMMETRIC KEY|DATABASE|  
|CRSM|CREATE SCHEMA|DATABASE|  
|CRSN|CREATE SYNONYM|DATABASE|  
|CRSO|**Aplica-se a**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior.<br /><br /> CREATE SEQUENCE|DATABASE|  
|CRSV|CREATE SERVICE|DATABASE|  
|CRTB|CREATE TABLE|DATABASE|  
|CRTY|CREATE TYPE|DATABASE|  
|CRVW|CREATE VIEW|DATABASE|  
|CRXS|**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior.<br /><br /> CREATE XML SCHEMA COLLECTION|DATABASE|  
|DABO |ADMINISTRAR OPERAÇÕES EM LOTE DO BANCO DE DADOS | DATABASE |
|DL|DELETE|DATABASE, OBJECT, SCHEMA|  
|EAES |EXECUTE ANY EXTERNAL SCRIPT |DATABASE |
|EX|EXECUTE|ASSEMBLY, DATABASE, OBJECT, SCHEMA, TYPE, XML SCHEMA COLLECTION|  
|IM|IMPERSONATE|Usuário|  
|IN|Insert (inserir)|DATABASE, OBJECT, SCHEMA|  
|RC|RECEIVE|OBJECT|  
|RF|REFERENCES|ASSEMBLY, ASYMMETRIC KEY, CERTIFICATE, CONTRACT, DATABASE, FULLTEXT CATALOG, MESSAGE TYPE, OBJECT, SCHEMA, SYMMETRIC KEY, TYPE, XML SCHEMA COLLECTION|  
|SL|SELECT|DATABASE, OBJECT, SCHEMA|  
|SN|SEND|SERVICE|  
|SPLN|SHOWPLAN|DATABASE|  
|SUQN|SUBSCRIBE QUERY NOTIFICATIONS|DATABASE|  
|TO|TAKE OWNERSHIP|ASSEMBLY, ASYMMETRIC KEY, CERTIFICATE, CONTRACT, DATABASE, FULLTEXT CATALOG, MESSAGE TYPE, OBJECT, REMOTE SERVICE BINDING, ROLE, ROUTE, SCHEMA, SERVICE, SYMMETRIC KEY, TYPE, XML SCHEMA COLLECTION|  
|UP|UPDATE|DATABASE, OBJECT, SCHEMA|  
|VW|VIEW DEFINITION|APPLICATION ROLE, ASSEMBLY, ASYMMETRIC KEY, CERTIFICATE, CONTRACT, DATABASE, FULLTEXT CATALOG, MESSAGE TYPE, OBJECT, REMOTE SERVICE BINDING, ROLE, ROUTE, SCHEMA, SERVICE, SYMMETRIC KEY, TYPE, USER, XML SCHEMA COLLECTION|  
|VWCK |VIEW ANY COLUMN ENCRYPTION KEY DEFINITION|DATABASE |  
|VWCM |VIEW ANY COLUMN MASTER KEY DEFINITION|DATABASE |  
|VWCT|VIEW CHANGE TRACKING|TABLE, SCHEMA|  
|VWDS|VIEW DATABASE STATE|DATABASE|  
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário pode ver suas próprias permissões. Para ver as permissões de outros usuários, requer VIEW DEFINITION, ALTER ANY USER ou qualquer permissão em um usuário. Ver funções definidas pelo usuário requer ALTER ANY ROLE ou associação na função (como público).  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
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
    
  
## <a name="see-also"></a>Consulte também  
 [Securables](../../relational-databases/security/securables.md)   
 [Hierarquia de permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  



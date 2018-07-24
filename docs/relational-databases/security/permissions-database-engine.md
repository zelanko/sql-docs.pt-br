---
title: Permissões (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseuser.permissions.database.f1--May use common.permissions
- sql13.swb.databaseuser.permissions.object.f1--May use common.permissions
helpviewer_keywords:
- REFERENCES permission
- permissions [SQL Server]
- security [SQL Server], permissions
- naming conventions [SQL Server]
ms.assetid: f28e3dea-24e6-4a81-877b-02ec4c7e36b9
caps.latest.revision: 76
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 85a62bd00ffc5a85ffe2ab62714202ff2f41cfd2
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2018
ms.locfileid: "39107102"
---
# <a name="permissions-database-engine"></a>Permissões (Mecanismo de Banco de Dados)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Todo protegível do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem permissões associadas que podem ser concedidas a uma entidade de segurança. As permissões no [!INCLUDE[ssDE](../../includes/ssde-md.md)] são gerenciadas no nível do servidor atribuídas a funções de logon e de servidor, e no nível do banco de dados atribuídas a funções de usuários do banco de dados e funções de banco de dados. O modelo para o [!INCLUDE[ssSDS](../../includes/sssds-md.md)] tem o mesmo sistema para as permissões de banco de dados, mas as permissões no nível do servidor não estão disponíveis. Este tópico contém a lista completa de permissões. Para obter uma implementação típica das permissões, veja [Introdução às permissões do Mecanismo de Banco de Dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).  
  
O número total de permissões para o [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e o [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] é 237. A maioria das permissões se aplica a todas as plataformas, mas algumas delas, não. Por exemplo, permissões de nível de servidor não podem ser concedidas no banco de dados SQL, e algumas permissões só fazem sentido no [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] expôs 230 permissões. [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] expôs 219 permissões. [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] expôs 214 permissões. [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] expôs 195 permissões. O tópico [fn_builtin_permissions](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md) especifica os tópicos que são novos em versões recentes.

Depois de compreender as permissões, aplique permissões em nível de servidor a logons e a usuários de permissões no nível de banco de dados com as instruções [GRANT](../../t-sql/statements/grant-transact-sql.md), [REVOKE](../../t-sql/statements/revoke-transact-sql.md)e [DENY](../../t-sql/statements/deny-transact-sql.md) . Por exemplo:   
```sql
GRANT SELECT ON OBJECT::HumanResources.Employee TO Larry;
REVOKE SELECT ON OBJECT::HumanResources.Employee TO Larry;
```   
Para obter dicas sobre como planejar um sistema de permissões, confira [Introdução a permissões de mecanismo de banco de dados](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md).
  
##  <a name="_conventions"></a> Convenções de Nomenclatura de Permissões  
 A seguir, encontram-se as convenções gerais a serem adotadas ao se nomear permissões:  
  
-   CONTROL  
  
     Confere capacidades de propriedade ao usuário autorizado. O usuário autorizado efetivamente tem todas as permissões definidas no protegível. Uma entidade à qual foi concedido CONTROL também pode conceder permissões no protegível. Como o modelo de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é hierárquico, CONTROL em um escopo específico inclui implicitamente CONTROL sobre todos os protegíveis naquele escopo. Por exemplo, CONTROL em um banco de dados implica todas as permissões do banco de dados, todas as permissões em todos os assemblies no banco de dados, todas as permissões em todos os esquemas no banco de dados e todas as permissões em objetos de todos os esquemas no banco de dados.  
  
-   ALTER  
  
     Confere a capacidade de alterar as propriedades, menos a propriedade de um protegível específico. Quando concedido em um escopo, ALTER também concede a capacidade de alterar, criar ou descartar qualquer protegível contido naquele escopo. Por exemplo, a permissão ALTER em um esquema inclui a capacidade de criar, alterar e descartar objetos do esquema.  
  
-   ALTER ANY \<*Server Securable*>, em que *Server Securable* pode ser qualquer protegível do servidor.  
  
     Confere a capacidade de criar, alterar ou remover instâncias individuais do *Protegível de Servidor*. Por exemplo, ALTER ANY LOGIN confere a capacidade de criar, alterar ou descartar qualquer logon na instância.  
  
-   ALTER ANY \<*Database Securable*>, em que *Database Securable* pode ser qualquer protegível no nível de banco de dados.  
  
     Confere a capacidade de criar, alterar ou remover instâncias individuais do *Protegível do Banco de Dados*. Por exemplo, ALTER ANY SCHEMA confere a capacidade de criar, alterar ou descartar qualquer esquema no banco de dados.  
  
-   TAKE OWNERSHIP  
  
     Habilita o usuário autorizado a assumir propriedade do protegível no qual é concedido.  
  
-   IMPERSONATE \<*Logon*>  
  
     Permite que o usuário autorizado represente o logon.  
  
-   IMPERSONATE \<*Usuário*>  
  
     Permite que o usuário autorizado represente o usuário.  
  
-   CREATE \<*Server Securable*>  
  
     Confere ao usuário autorizado a habilidade para criar o *Protegível de Servidor*.  
  
-   CREATE \<*Database Securable*>  
  
     Confere ao usuário autorizado a habilidade de criar o *Protegível de Banco de Dados*.  
  
-   CREATE \<*Schema-contained Securable*>  
  
     Confere a capacidade para criar o protegível contido em esquema. Porém, a permissão ALTER no esquema é necessária para criar o protegível em um esquema específico.  
  
-   VIEW DEFINITION  
  
     Permite que o usuário autorizado acesse os metadados.  
  
-   REFERENCES  
  
     A permissão REFERENCES em uma tabela é necessária para criar uma restrição FOREIGN KEY que faça referência àquela tabela.  
  
     A permissão REFERENCES é necessária em um objeto para criar uma FUNCTION ou VIEW com a cláusula `WITH SCHEMABINDING` que faz referência àquele objeto.  
  
## <a name="chart-of-sql-server-permissions"></a>Gráfico de permissões do SQL Server  
[!INCLUDE[database-engine-permissions](../../includes/paragraph-content/database-engine-permissions.md)]
  
##  <a name="_securables"></a> Permissões Aplicáveis a Protegíveis Específicos  
 A tabela a seguir lista classes principais de permissões e os tipos de protegíveis aos quais elas podem ser aplicadas.  
  
|Permissão|Aplica-se a|  
|----------------|----------------|  
|ALTER|Todas as classes de objetos, exceto TYPE.|  
|CONTROL|Todas as classes de objetos: <br />AGGREGATE,<br />APPLICATION ROLE,<br />ASSEMBLY,<br />ASYMMETRIC KEY,<br />AVAILABILITY GROUP,<br />CERTIFICATE,<br />CONTRACT,<br />CREDENTIALS, DATABASE,<br />DATABASE SCOPED CREDENTIAL,<br /> DEFAULT,<br />ENDPOINT,<br />FULLTEXT CATALOG,<br />FULLTEXT STOPLIST,<br />FUNCTION,<br />LOGIN,<br />MESSAGE TYPE,<br />PROCEDURE,<br />QUEUE, <br />REMOTE SERVICE BINDING,<br />ROLE,<br />ROUTE,<br />RULE,<br />SCHEMA,<br />SEARCH PROPERTY LIST,<br />SERVER,<br />SERVER ROLE,<br />SERVICE,<br />SYMMETRIC KEY,<br />SYNONYM,<br />TABLE,<br />TYPE, USER,<br />VIEW e<br />XML SCHEMA COLLECTION|  
|Delete (excluir)|Todas as classes de objetos, exceto DATABASE SCOPED CONFIGURATION e SERVER.|  
|Execute|Tipos de CLR, scripts externos, procedimentos ([!INCLUDE[tsql](../../includes/tsql-md.md)] e CLR), funções escalares e de agregação ([!INCLUDE[tsql](../../includes/tsql-md.md)] e CLR) e sinônimos|  
|IMPERSONATE|Logons e usuários|  
|INSERT|Sinônimos, tabelas e colunas, exibições e colunas. A permissão pode ser concedida em nível de banco de dados, de esquema ou de objeto.|  
|RECEIVE|Filas do[!INCLUDE[ssSB](../../includes/sssb-md.md)] |  
|REFERENCES|AGGREGATE,<br />ASSEMBLY,<br />ASYMMETRIC KEY,<br />CERTIFICATE,<br />CONTRACT,<br />DATABASE,<br />DATABASE SCOPED CREDENTIAL,<br />FULLTEXT CATALOG,<br />FULLTEXT STOPLIST,<br />FUNCTION,<br />MESSAGE TYPE,<br />PROCEDURE,<br />QUEUE, <br />RULE,<br />SCHEMA,<br />SEARCH PROPERTY LIST,<br />SEQUENCE OBJECT, <br />SYMMETRIC KEY,<br />SYNONYM,<br />TABLE,<br />TYPE,<br />VIEW e<br />XML SCHEMA COLLECTION|  
|SELECT|Sinônimos, tabelas e colunas, exibições e colunas. A permissão pode ser concedida em nível de banco de dados, de esquema ou de objeto.|  
|TAKE OWNERSHIP|Todas as classes de objetos, exceto DATABASE SCOPED CONFIGURATION, LOGIN, SERVER e USER.|  
|UPDATE|Sinônimos, tabelas e colunas, exibições e colunas. A permissão pode ser concedida em nível de banco de dados, de esquema ou de objeto.|  
|VIEW CHANGE TRACKING|Esquemas e tabelas|  
|VIEW DEFINITION|Todas as classes de objetos, exceto DATABASE SCOPED CONFIGURATION e SERVER.|  
  
> [!CAUTION]  
>  As permissões padrão concedidas aos objetos de sistema no momento da instalação são avaliadas cuidadosamente contra possíveis ameaças e não precisam ser alteradas como parte do sistema de proteção de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Qualquer alteração nas permissões nos objetos de sistema poderia limitar ou interromper a funcionalidade e potencialmente pode deixar a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um estado sem suporte.  
  
##  <a name="_permissions"></a> Permissões do SQL Server  
 A tabela a seguir fornece uma lista completa de permissões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . As permissões[!INCLUDE[ssSDS](../../includes/sssds-md.md)] estão disponíveis apenas para protegíveis base com suporte. Não é possível dar permissões no nível do servidor no [!INCLUDE[ssSDS](../../includes/sssds-md.md)], no entanto, permissões de banco de dados são disponibilizadas em alguns casos.  
  
|Protegível base|Permissões granulares no protegível base|Código de tipo de permissão|Protegível que contém o protegível base|Permissão no protegível de contêiner que implica permissão granular no protegível base|  
|--------------------|--------------------------------------------|--------------------------|--------------------------------------------|------------------------------------------------------------------------------------------|  
|APPLICATION ROLE|ALTER|AL|DATABASE|ALTER ANY APPLICATION ROLE|  
|APPLICATION ROLE|CONTROL|CL|DATABASE|CONTROL|  
|APPLICATION ROLE|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|ASSEMBLY|ALTER|AL|DATABASE|ALTER ANY ASSEMBLY|  
|ASSEMBLY|CONTROL|CL|DATABASE|CONTROL|  
|ASSEMBLY|REFERENCES|RF|DATABASE|REFERENCES|  
|ASSEMBLY|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|ASSEMBLY|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|ASYMMETRIC KEY|ALTER|AL|DATABASE|ALTER ANY ASYMMETRIC KEY|  
|ASYMMETRIC KEY|CONTROL|CL|DATABASE|CONTROL|  
|ASYMMETRIC KEY|REFERENCES|RF|DATABASE|REFERENCES|  
|ASYMMETRIC KEY|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|ASYMMETRIC KEY|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|AVAILABILITY GROUP|ALTER|AL|SERVER|ALTER ANY AVAILABILITY GROUP|  
|AVAILABILITY GROUP|CONTROL|CL|SERVER|CONTROL SERVER|  
|AVAILABILITY GROUP|TAKE OWNERSHIP|TO|SERVER|CONTROL SERVER|  
|AVAILABILITY GROUP|VIEW DEFINITION|VW|SERVER|VIEW ANY DEFINITION|  
|CERTIFICATE|ALTER|AL|DATABASE|ALTER ANY CERTIFICATE|  
|CERTIFICATE|CONTROL|CL|DATABASE|CONTROL|  
|CERTIFICATE|REFERENCES|RF|DATABASE|REFERENCES|  
|CERTIFICATE|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|CERTIFICATE|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|CONTRACT|ALTER|AL|DATABASE|ALTER ANY CONTRACT|  
|CONTRACT|CONTROL|CL|DATABASE|CONTROL|  
|CONTRACT|REFERENCES|RF|DATABASE|REFERENCES|  
|CONTRACT|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|CONTRACT|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|DATABASE|ADMINISTRAR OPERAÇÕES EM LOTE DO BANCO DE DADOS|DABO|SERVER|CONTROL SERVER|
|DATABASE|ALTER|AL|SERVER|ALTER ANY DATABASE|  
|DATABASE|ALTER ANY APPLICATION ROLE|ALAR|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY ASSEMBLY|ALAS|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY ASYMMETRIC KEY|ALAK|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY CERTIFICATE|ALCF|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY COLUMN ENCRYPTION KEY|ALCK<br /><br /> Aplica-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a versão atual), [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY COLUMN MASTER KEY|ALCM<br /><br /> Aplica-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a versão atual), [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY CONTRACT|ALSC|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY DATABASE AUDIT|ALDA|SERVER|ALTER ANY SERVER AUDIT|  
|DATABASE|ALTER ANY DATABASE DDL TRIGGER|ALTG|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY DATABASE EVENT NOTIFICATION|ALED|SERVER|ALTER ANY EVENT NOTIFICATION|  
|DATABASE|ALTER ANY DATABASE EVENT SESSION|AADS<br /><br /> Aplica-se a [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|SERVER|ALTER ANY EVENT SESSION|  
|DATABASE|ALTER ANY DATABASE SCOPED CONFIGURATION|ALDC<br /><br /> Aplica-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a versão atual), [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY DATASPACE|ALDS|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY EXTERNAL DATA SOURCE|AEDS|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY EXTERNAL FILE FORMAT|AEFF|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY FULLTEXT CATALOG|ALFT|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY MASK|AAMK<br /><br /> Aplica-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até o atual), Banco de Dados SQL.|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY MESSAGE TYPE|ALMT|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY REMOTE SERVICE BINDING|ALSB|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY ROLE|ALRL|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY ROUTE|ALRT|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY SCHEMA|ALSM|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY SECURITY POLICY|ALSP<br /><br /> Aplica-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a versão atual), [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|SERVER|CONTROL SERVER|  
|DATABASE|ALTERAR QUALQUER CLASSIFICAÇÃO DE SENSIBILIDADE|ALSP<br />Aplica-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQL Server vNext (15.x) até a versão atual), Banco de Dados SQL.|DATABASE|CONTROL SERVER|
|DATABASE|ALTER ANY SERVICE|ALSV|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY SYMMETRIC KEY|ALSK|SERVER|CONTROL SERVER|  
|DATABASE|ALTER ANY USER|ALUS|SERVER|CONTROL SERVER|  
|DATABASE|AUTHENTICATE|AUTH|SERVER|AUTHENTICATE SERVER|  
|DATABASE|BACKUP DATABASE|BADB|SERVER|CONTROL SERVER|  
|DATABASE|BACKUP LOG|BALO|SERVER|CONTROL SERVER|  
|DATABASE|CHECKPOINT|CP|SERVER|CONTROL SERVER|  
|DATABASE|CONNECT|CO|SERVER|CONTROL SERVER|  
|DATABASE|CONNECT REPLICATION|CORP|SERVER|CONTROL SERVER|  
|DATABASE|CONTROL|CL|SERVER|CONTROL SERVER|  
|DATABASE|CREATE AGGREGATE|CRAG|SERVER|CONTROL SERVER|  
|DATABASE|CREATE ASSEMBLY|CRAS|SERVER|CONTROL SERVER|  
|DATABASE|CREATE ASYMMETRIC KEY|CRAK|SERVER|CONTROL SERVER|  
|DATABASE|CREATE CERTIFICATE|CRCF|SERVER|CONTROL SERVER|  
|DATABASE|CREATE CONTRACT|CRSC|SERVER|CONTROL SERVER|  
|DATABASE|CREATE DATABASE|CRDB|SERVER|CREATE ANY DATABASE|  
|DATABASE|CREATE DATABASE DDL EVENT NOTIFICATION|CRED|SERVER|CREATE DDL EVENT NOTIFICATION|  
|DATABASE|CREATE DEFAULT|CRDF|SERVER|CONTROL SERVER|  
|DATABASE|CREATE FULLTEXT CATALOG|CRFT|SERVER|CONTROL SERVER|  
|DATABASE|CREATE FUNCTION|CRFN|SERVER|CONTROL SERVER|  
|DATABASE|CREATE MESSAGE TYPE|CRMT|SERVER|CONTROL SERVER|  
|DATABASE|CREATE PROCEDURE|CRPR|SERVER|CONTROL SERVER|  
|DATABASE|CREATE QUEUE|CRQU|SERVER|CONTROL SERVER|  
|DATABASE|CREATE REMOTE SERVICE BINDING|CRSB|SERVER|CONTROL SERVER|  
|DATABASE|CREATE ROLE|CRRL|SERVER|CONTROL SERVER|  
|DATABASE|CREATE ROUTE|CRRT|SERVER|CONTROL SERVER|  
|DATABASE|CREATE RULE|CRRU|SERVER|CONTROL SERVER|  
|DATABASE|CREATE SCHEMA|CRSM|SERVER|CONTROL SERVER|  
|DATABASE|CREATE SERVICE|CRSV|SERVER|CONTROL SERVER|  
|DATABASE|CREATE SYMMETRIC KEY|CRSK|SERVER|CONTROL SERVER|  
|DATABASE|CREATE SYNONYM|CRSN|SERVER|CONTROL SERVER|  
|DATABASE|CREATE TABLE|CRTB|SERVER|CONTROL SERVER|  
|DATABASE|CREATE TYPE|CRTY|SERVER|CONTROL SERVER|  
|DATABASE|CREATE VIEW|CRVW|SERVER|CONTROL SERVER|  
|DATABASE|CREATE XML SCHEMA COLLECTION|CRXS|SERVER|CONTROL SERVER|  
|DATABASE|Delete (excluir)|DL|SERVER|CONTROL SERVER|  
|DATABASE|Execute|EX|SERVER|CONTROL SERVER|  
|DATABASE|EXECUTE ANY EXTERNAL SCRIPT|EAES<br /><br /> Aplica-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a versão atual).|SERVER|CONTROL SERVER|  
|DATABASE|INSERT|IN|SERVER|CONTROL SERVER|  
|DATABASE|KILL DATABASE CONNECTION|KIDC<br /><br /> Aplica-se apenas ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Usar ALTER ANY CONNECTION no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|SERVER|ALTER ANY CONNECTION|  
|DATABASE|REFERENCES|RF|SERVER|CONTROL SERVER|  
|DATABASE|SELECT|SL|SERVER|CONTROL SERVER|  
|DATABASE|SHOWPLAN|SPLN|SERVER|ALTER TRACE|  
|DATABASE|SUBSCRIBE QUERY NOTIFICATIONS|SUQN|SERVER|CONTROL SERVER|  
|DATABASE|TAKE OWNERSHIP|TO|SERVER|CONTROL SERVER|  
|DATABASE|UNMASK|UMSK<br /><br /> Aplica-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até o atual), Banco de Dados SQL.|SERVER|CONTROL SERVER|  
|DATABASE|UPDATE|UP|SERVER|CONTROL SERVER|  
|DATABASE|VIEW ANY COLUMN ENCRYPTION KEY DEFINITION|VWCK<br /><br /> Aplica-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a versão atual), [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|SERVER|VIEW SERVER STATE|  
|DATABASE|VIEW ANY COLUMN MASTER KEY DEFINITION|vWCM<br /><br /> Aplica-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a versão atual), [!INCLUDE[ssSDS](../../includes/sssds-md.md)].|SERVER|VIEW SERVER STATE|  
|DATABASE|VIEW DATABASE STATE|VWDS|SERVER|VIEW SERVER STATE|  
|DATABASE|VIEW DEFINITION|VW|SERVER|VIEW ANY DEFINITION|  
|CREDENCIAL NO ESCOPO DO BANCO DE DADOS|ALTER|AL|DATABASE|CONTROL|
|CREDENCIAL NO ESCOPO DO BANCO DE DADOS|CONTROL|CL|DATABASE|CONTROL|
|CREDENCIAL NO ESCOPO DO BANCO DE DADOS|REFERENCES|RF|DATABASE|REFERENCES|
|CREDENCIAL NO ESCOPO DO BANCO DE DADOS|TAKE OWNERSHIP|TO|DATABASE|CONTROL|
|CREDENCIAL NO ESCOPO DO BANCO DE DADOS|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|
|ENDPOINT|ALTER|AL|SERVER|ALTER ANY ENDPOINT|  
|ENDPOINT|CONNECT|CO|SERVER|CONTROL SERVER|  
|ENDPOINT|CONTROL|CL|SERVER|CONTROL SERVER|  
|ENDPOINT|TAKE OWNERSHIP|TO|SERVER|CONTROL SERVER|  
|ENDPOINT|VIEW DEFINITION|VW|SERVER|VIEW ANY DEFINITION|  
|FULLTEXT CATALOG|ALTER|AL|DATABASE|ALTER ANY FULLTEXT CATALOG|  
|FULLTEXT CATALOG|CONTROL|CL|DATABASE|CONTROL|  
|FULLTEXT CATALOG|REFERENCES|RF|DATABASE|REFERENCES|  
|FULLTEXT CATALOG|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|FULLTEXT CATALOG|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|FULLTEXT STOPLIST|ALTER|AL|DATABASE|ALTER ANY FULLTEXT CATALOG|  
|FULLTEXT STOPLIST|CONTROL|CL|DATABASE|CONTROL|  
|FULLTEXT STOPLIST|REFERENCES|RF|DATABASE|REFERENCES|  
|FULLTEXT STOPLIST|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|FULLTEXT STOPLIST|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|Logon|ALTER|AL|SERVER|ALTER ANY LOGIN|  
|Logon|CONTROL|CL|SERVER|CONTROL SERVER|  
|Logon|IMPERSONATE|IM|SERVER|CONTROL SERVER|  
|Logon|VIEW DEFINITION|VW|SERVER|VIEW ANY DEFINITION|  
|MESSAGE TYPE|ALTER|AL|DATABASE|ALTER ANY MESSAGE TYPE|  
|MESSAGE TYPE|CONTROL|CL|DATABASE|CONTROL|  
|MESSAGE TYPE|REFERENCES|RF|DATABASE|REFERENCES|  
|MESSAGE TYPE|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|MESSAGE TYPE|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|OBJECT|ALTER|AL|SCHEMA|ALTER|  
|OBJECT|CONTROL|CL|SCHEMA|CONTROL|  
|OBJECT|DELETE|DL|SCHEMA|Delete (excluir)|  
|OBJECT|Execute|EX|SCHEMA|Execute|  
|OBJECT|INSERT|IN|SCHEMA|INSERT|  
|OBJECT|RECEIVE|RC|SCHEMA|CONTROL|  
|OBJECT|REFERENCES|RF|SCHEMA|REFERENCES|  
|OBJECT|SELECT|SL|SCHEMA|SELECT|  
|OBJECT|TAKE OWNERSHIP|TO|SCHEMA|CONTROL|  
|OBJECT|UPDATE|UP|SCHEMA|UPDATE|  
|OBJECT|VIEW CHANGE TRACKING|VWCT|SCHEMA|VIEW CHANGE TRACKING|  
|OBJECT|VIEW DEFINITION|VW|SCHEMA|VIEW DEFINITION|  
|REMOTE SERVICE BINDING|ALTER|AL|DATABASE|ALTER ANY REMOTE SERVICE BINDING|  
|REMOTE SERVICE BINDING|CONTROL|CL|DATABASE|CONTROL|  
|REMOTE SERVICE BINDING|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|REMOTE SERVICE BINDING|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|ROLE|ALTER|AL|DATABASE|ALTER ANY ROLE|  
|ROLE|CONTROL|CL|DATABASE|CONTROL|  
|ROLE|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|ROLE|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|ROUTE|ALTER|AL|DATABASE|ALTER ANY ROUTE|  
|ROUTE|CONTROL|CL|DATABASE|CONTROL|  
|ROUTE|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|ROUTE|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|SEARCH PROPERTY LIST|ALTER|AL|SERVER|ALTER ANY FULLTEXT CATALOG|  
|SEARCH PROPERTY LIST|CONTROL|CL|SERVER|CONTROL|  
|SEARCH PROPERTY LIST|REFERENCES|RF|SERVER|REFERENCES|  
|SEARCH PROPERTY LIST|TAKE OWNERSHIP|TO|SERVER|CONTROL|  
|SEARCH PROPERTY LIST|VIEW DEFINITION|VW|SERVER|VIEW DEFINITION|  
|SCHEMA|ALTER|AL|DATABASE|ALTER ANY SCHEMA|  
|SCHEMA|CONTROL|CL|DATABASE|CONTROL|  
|SCHEMA|CREATE SEQUENCE|CRSO|DATABASE|CONTROL|  
|SCHEMA|Delete (excluir)|DL|DATABASE|Delete (excluir)|  
|SCHEMA|Execute|EX|DATABASE|Execute|  
|SCHEMA|INSERT|IN|DATABASE|INSERT|  
|SCHEMA|REFERENCES|RF|DATABASE|REFERENCES|  
|SCHEMA|SELECT|SL|DATABASE|SELECT|  
|SCHEMA|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|SCHEMA|UPDATE|UP|DATABASE|UPDATE|  
|SCHEMA|VIEW CHANGE TRACKING|VWCT|DATABASE|VIEW CHANGE TRACKING|  
|SCHEMA|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|SERVER|ADMINISTER BULK OPERATIONS|ADBO|Não aplicável|Não aplicável|  
|SERVER|ALTER ANY AVAILABILITY GROUP|ALAG|Não aplicável|Não aplicável|  
|SERVER|ALTER ANY CONNECTION|ALCO|Não aplicável|Não aplicável|  
|SERVER|ALTER ANY CREDENTIAL|ALCD|Não aplicável|Não aplicável|  
|SERVER|ALTER ANY DATABASE|ALDB|Não aplicável|Não aplicável|  
|SERVER|ALTER ANY ENDPOINT|ALHE|Não aplicável|Não aplicável|  
|SERVER|ALTER ANY EVENT NOTIFICATION|ALES|Não aplicável|Não aplicável|  
|SERVER|ALTER ANY EVENT SESSION|AAES|Não aplicável|Não aplicável|  
|SERVER|ALTER ANY LINKED SERVER|ALLS|Não aplicável|Não aplicável|  
|SERVER|ALTER ANY LOGIN|ALLG|Não aplicável|Não aplicável|  
|SERVER|ALTER ANY SERVER AUDIT|ALAA|Não aplicável|Não aplicável|  
|SERVER|ALTER ANY SERVER ROLE|ALSR|Não aplicável|Não aplicável|  
|SERVER|ALTER RESOURCES|ALRS|Não aplicável|Não aplicável|  
|SERVER|ALTER SERVER STATE|ALSS|Não aplicável|Não aplicável|  
|SERVER|ALTER SETTINGS|ALST|Não aplicável|Não aplicável|  
|SERVER|ALTER TRACE|ALTR|Não aplicável|Não aplicável|  
|SERVER|AUTHENTICATE SERVER|AUTH|Não aplicável|Não aplicável|  
|SERVER|CONNECT ANY DATABASE|CADB|Não aplicável|Não aplicável|  
|SERVER|CONNECT SQL|COSQ|Não aplicável|Não aplicável|  
|SERVER|CONTROL SERVER|CL|Não aplicável|Não aplicável|  
|SERVER|CREATE ANY DATABASE|CRDB|Não aplicável|Não aplicável|  
|SERVER|Criar grupo de disponibilidade|CRAC|Não aplicável|Não aplicável|  
|SERVER|CREATE DDL EVENT NOTIFICATION|CRDE|Não aplicável|Não aplicável|  
|SERVER|CREATE ENDPOINT|CRHE|Não aplicável|Não aplicável|  
|SERVER|CREATE SERVER ROLE|CRSR|Não aplicável|Não aplicável|  
|SERVER|CREATE TRACE EVENT NOTIFICATION|CRTE|Não aplicável|Não aplicável|  
|SERVER|EXTERNAL ACCESS ASSEMBLY|XA|Não aplicável|Não aplicável|  
|SERVER|IMPERSONATE ANY LOGIN|IAL|Não aplicável|Não aplicável|  
|SERVER|SELECT ALL USER SECURABLES|SUS|Não aplicável|Não aplicável|  
|SERVER|SHUTDOWN|SHDN|Não aplicável|Não aplicável|  
|SERVER|UNSAFE ASSEMBLY|XU|Não aplicável|Não aplicável|  
|SERVER|VIEW ANY DATABASE|VWDB|Não aplicável|Não aplicável|  
|SERVER|VIEW ANY DEFINITION|VWAD|Não aplicável|Não aplicável|  
|SERVER|VIEW SERVER STATE|VWSS|Não aplicável|Não aplicável|  
|SERVER ROLE|ALTER|AL|SERVER|ALTER ANY SERVER ROLE|  
|SERVER ROLE|CONTROL|CL|SERVER|CONTROL SERVER|  
|SERVER ROLE|TAKE OWNERSHIP|TO|SERVER|CONTROL SERVER|  
|SERVER ROLE|VIEW DEFINITION|VW|SERVER|VIEW ANY DEFINITION|  
|SERVICE|ALTER|AL|DATABASE|ALTER ANY SERVICE|  
|SERVICE|CONTROL|CL|DATABASE|CONTROL|  
|SERVICE|SEND|SN|DATABASE|CONTROL|  
|SERVICE|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|SERVICE|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|SYMMETRIC KEY|ALTER|AL|DATABASE|ALTER ANY SYMMETRIC KEY|  
|SYMMETRIC KEY|CONTROL|CL|DATABASE|CONTROL|  
|SYMMETRIC KEY|REFERENCES|RF|DATABASE|REFERENCES|  
|SYMMETRIC KEY|TAKE OWNERSHIP|TO|DATABASE|CONTROL|  
|SYMMETRIC KEY|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|TYPE|CONTROL|CL|SCHEMA|CONTROL|  
|TYPE|Execute|EX|SCHEMA|Execute|  
|TYPE|REFERENCES|RF|SCHEMA|REFERENCES|  
|TYPE|TAKE OWNERSHIP|TO|SCHEMA|CONTROL|  
|TYPE|VIEW DEFINITION|VW|SCHEMA|VIEW DEFINITION|  
|Usuário|ALTER|AL|DATABASE|ALTER ANY USER|  
|Usuário|CONTROL|CL|DATABASE|CONTROL|  
|Usuário|IMPERSONATE|IM|DATABASE|CONTROL|  
|Usuário|VIEW DEFINITION|VW|DATABASE|VIEW DEFINITION|  
|XML SCHEMA COLLECTION|ALTER|AL|SCHEMA|ALTER|  
|XML SCHEMA COLLECTION|CONTROL|CL|SCHEMA|CONTROL|  
|XML SCHEMA COLLECTION|Execute|EX|SCHEMA|Execute|  
|XML SCHEMA COLLECTION|REFERENCES|RF|SCHEMA|REFERENCES|  
|XML SCHEMA COLLECTION|TAKE OWNERSHIP|TO|SCHEMA|CONTROL|  
|XML SCHEMA COLLECTION|VIEW DEFINITION|VW|SCHEMA|VIEW DEFINITION|  
  
##  <a name="_algorithm"></a> Resumo do algoritmo de verificação de permissão  
 A verificação de permissões pode ser uma tarefa complexa. O algoritmo de verificação de permissão inclui a sobreposição de associações de grupo e o encadeamento de propriedades, as permissões explícita e implícita, e pode ser afetado pelas permissões em classes de protegíveis que contêm a entidade protegível. O processo geral do algoritmo é coletar todas as permissões pertinentes. Se nenhum bloqueio DENY for localizado, o algoritmo irá procurar uma permissão GRANT que fornece acesso suficiente. O algoritmo contém três elementos essenciais, o **contexto de segurança**, o **espaço de permissão**e a **permissão necessária**.  
  
> [!NOTE]  
>  Não é possível conceder, negar ou revogar permissões para sa, dbo, o proprietário da entidade, information_schema, sys ou para você mesmo.  
  
-   **Contexto de segurança**  
  
     Este é o grupo de entidades que fornece permissões à verificação de acesso. Essas são as permissões relacionadas com o logon ou usuário atual, a menos que o contexto de segurança tenha sido alterado para outro logon ou usuário por meio da instrução EXECUTE AS. O contexto de segurança inclui as seguintes entidades:  
  
    -   O logon  
  
    -   O usuário  
  
    -   Associações de função  
  
    -   Associações de grupo do Windows  
  
    -   Se a assinatura de módulo estiver sendo usada, qualquer logon ou conta de usuário do certificado usado para assinar o módulo que está em execução no momento e as associações de função associadas a essa entidade.  
  
-   **Espaço de permissão**  
  
     É a entidade protegível e qualquer classe protegível que contém o protegível. Por exemplo, uma tabela (uma entidade protegível) é contida pela classe protegível de esquema e pela classe protegível de banco de dados. O acesso pode ser afetado por permissões em nível de tabela, esquema, banco de dados e servidor. Para obter mais informações, veja [Hierarquia de permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md).  
  
-   **Permissão necessária**  
  
     O tipo de permissão exigido. Por exemplo, INSERT, UPDATE, DELETE, SELECT, EXECUTE, ALTER, CONTROL, e assim por diante.  
  
     O acesso pode exigir várias permissões, como as dos exemplos a seguir.  
  
    -   Um procedimento armazenado pode exigir a permissão EXECUTE no procedimento armazenado e a permissão INSERT em várias tabelas que são referenciadas pelo procedimento armazenado.  
  
    -   Uma exibição de gerenciamento dinâmico pode exibir as permissões VIEW SERVER STATE e SELECT na exibição.  
  
### <a name="general-steps-of-the-algorithm"></a>Etapas gerais do algoritmo  
 Quando o algoritmo estiver determinando a permissão do acesso a um protegível, as etapas que ele utiliza podem variar, dependendo das entidades e dos protegíveis que estão envolvidos. No entanto, o algoritmo executa as seguintes etapas gerais:  
  
1.  Ignorar a verificação de permissão se o logon for um membro da função de servidor fixa sysadmin ou se o usuário for o usuário dbo no banco de dados atual.  
  
2.  Permite o acesso se o encadeamento de propriedades for aplicável e se a verificação de acesso no objeto anterior da cadeia tiver passado pela verificação de segurança.  
  
3.  Agrega as identidades em nível de servidor e de banco de dados e as identidades do módulo assinado associadas ao chamador para criar o **contexto de segurança**.  
  
4.  Para esse **contexto de segurança**, reúna todas as permissões concedidas ou negadas ao **espaço de permissão**. A permissão pode ser declarada explicitamente como GRANT, GRANT WITH GRANT ou DENY; ou as permissões podem ser implícitas ou de cobertura GRANT ou DENY. Por exemplo, a permissão CONTROL em um esquema implica CONTROL em uma tabela. E CONTROL em uma tabela implica SELECT. Portanto, se CONTROL foi concedida no esquema, SELECT será concedida na tabela. Se CONTROL foi negada na tabela, SELECT será negada na tabela.  
  
    > [!NOTE]  
    >  Uma permissão GRANT no nível de coluna substitui DENY no nível de objeto.  
  
5.  Identifica a **permissão necessária**.  
  
6.  Falha ao executar a verificação de permissão se a **permissão necessária** for direta ou implicitamente negada a quaisquer das identidades contidas no **contexto de segurança** para os objetos do **espaço de permissão**.  
  
7.  Executa a verificação de permissão se a **permissão necessária** não tiver sido negada e a **permissão necessária** contiver uma permissão GRANT ou GRANT WITH GRANT direta ou implicitamente para quaisquer das identidades contidas no **contexto de segurança** para qualquer objeto do **espaço de permissão**.  

## <a name="special-considerations-for-column-level-permissions"></a>Considerações especiais para permissões no nível da coluna

Permissões em nível de coluna são concedidas com a sintaxe *<table_name>(\<column _name>)*. Por exemplo:
```sql
GRANT SELECT ON OBJECT::Customer(CustomerName) TO UserJoe;
```
DENY na tabela é substituído por GRANT em uma coluna. No entanto, um DENY posterior na tabela removerá a coluna GRANT. 
  
##  <a name="_examples"></a> Exemplos  
 Os exemplos nesta seção mostram como recuperar informações sobre permissões.  
  
### <a name="a-returning-the-complete-list-of-grantable-permissions"></a>A. Retornando a lista completa de permissões que podem ser concedidas  
 A instrução a seguir retorna todas as permissões de [!INCLUDE[ssDE](../../includes/ssde-md.md)] usando a função `fn_builtin_permissions` . Para obter mais informações, veja [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md).  
  
```sql  
SELECT * FROM fn_builtin_permissions(default);  
GO  
```  
  
### <a name="b-returning-the-permissions-on-a-particular-class-of-objects"></a>B. Retornando permissões em uma classe específica de objetos  
 O exemplo a seguir usa `fn_builtin_permissions` para exibir todas as permissões que estão disponíveis para uma categoria de protegível. O exemplo retorna permissões em assemblies.  
  
```sql  
SELECT * FROM fn_builtin_permissions('assembly');  
GO    
```  
  
### <a name="c-returning-the-permissions-granted-to-the-executing-principal-on-an-object"></a>C. Retornando as permissões concedidas à entidade em execução em um objeto  
 O exemplo a seguir usa `fn_my_permissions` para retornar uma lista das permissões efetivas mantidas pela entidade de chamada em um protegível especificado. O exemplo retorna permissões em um objeto denominado `Orders55`. Para obter mais informações, veja [sys.fn_my_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md).  
  
```sql  
SELECT * FROM fn_my_permissions('Orders55', 'object');  
GO  
```  
  
### <a name="d-returning-the-permissions-applicable-to-a-specified-object"></a>D. Retornando permissões aplicáveis a um objeto especificado  
 O exemplo a seguir retorna permissões aplicáveis a um objeto denominado `Yttrium`. Observe que a função interna `OBJECT_ID` é usada para recuperar a ID do objeto `Yttrium`.  
  
```sql  
SELECT * FROM sys.database_permissions   
    WHERE major_id = OBJECT_ID('Yttrium');  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Hierarquia de permissões &#40;Mecanismo de banco de dados&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)  
  
  

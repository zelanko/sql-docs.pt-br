---
title: Determinando permissões de mecanismo de banco de dados eficiente | Microsoft Docs
ms.custom: ''
ms.date: 01/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- permissions, effective
- effective permissions
ms.assetid: 273ea09d-60ee-47f5-8828-8bdc7a3c3529
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 40f30fd646e166cc9b8db433934d22a378c907cb
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67995631"
---
# <a name="determining-effective-database-engine-permissions"></a>Determinando permissões eficientes do Mecanismo de Banco de Dados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Este artigo descreve como determinar quem tem permissões para vários objetos no Mecanismo de Banco de Dados do SQL Server. O SQL Server implementa dois sistemas de permissão para o mecanismo de banco de dados. Um sistema mais antigo de funções fixas tem permissões pré-configuradas. Está disponível, a partir do SQL Server 2005, um sistema mais flexível e preciso. (As informações neste artigo se aplicam ao SQL Server, a partir do 2005. Alguns tipos de permissões não estão disponíveis em algumas versões do SQL Server.)

> [!IMPORTANT]
>  * As permissões efetivas são a agregação dos dois sistemas de permissão. 
>  * Uma negação de permissões substitui uma concessão de permissões. 
>  * Se um usuário é um membro da função de servidor fixa sysadmin, permissões não são verificadas e, portanto, negações não são impostas. 
>  * O sistema antigo e o novo têm semelhanças. Por exemplo, associação à função fixa de servidor `sysadmin` é semelhante a ter permissão `CONTROL SERVER`. Mas os sistemas não são idênticos. Por exemplo, se um logon só tem a permissão `CONTROL SERVER` e os procedimentos armazenados verificarem a associação na função de servidor fixa `sysadmin`, a verificação de permissão falhará. O inverso também é verdadeiro. 


## <a name="summary"></a>Resumo   
* A permissão de nível de servidor pode vir da associação a funções de servidor fixas ou funções de servidor definidas pelo usuário. Todas pertencem à função de servidor fixa `public` e recebem qualquer permissão atribuída lá.   
* As permissões de nível de servidor podem vir de permissões concedidas para logons ou funções de servidor definidas pelo usuário.   
* A permissão de nível de banco de dados pode vir da associação em funções de banco de dados fixas ou funções de banco de dados definidas pelo usuário em cada banco de dados. Todas pertencem à função de banco de dados fixa `public` e recebem qualquer permissão atribuída lá.   
* As permissões de nível de banco de dados podem vir de concessões de permissão a usuários ou funções de banco de dados definidas pelo usuário em cada banco de dados.   
* As permissões podem ser recebidas do logon `guest` ou do usuário de banco de dados `guest`, se habilitado. O logon `guest` e os usuários estão desabilitados por padrão.   
* Os usuários do Windows podem ser membros de grupos do Windows que podem ter logons. O SQL Server aprende com a associação de grupo do Windows quando um usuário do Windows se conecta e apresenta um token do Windows com o identificador de segurança de um grupo do Windows. Como o SQL Server não gerencia nem receba atualizações automáticas sobre associações de grupo do Windows, o SQL Server não pode relatar, de modo confiável, as permissões de usuários do Windows que são recebidas da associação de grupo do Windows.   
* As permissões podem ser adquiridas alternando para uma função de aplicativo e fornecendo a senha.   
* As permissões podem ser adquiridas ao executar um procedimento armazenado que inclui a cláusula `EXECUTE AS`.   
* As permissões podem ser adquiridas com logons ou usuários com a permissão `IMPERSONATE`.   
* Os membros do grupo administrador do computador local sempre podem elevar seus privilégios para `sysadmin`. (Não se aplica ao Banco de Dados SQL.)  
* Os membros da função de servidor fixa `securityadmin` podem elevar muitos de seus privilégios e, em alguns casos, podem elevar os privilégios para `sysadmin`. (Não se aplica ao Banco de Dados SQL.)   
* Os administradores do SQL Server podem ver as informações sobre todos os logons e usuários. Usuários com menos privilégios geralmente veem apenas as informações de suas próprias identidades.

## <a name="older-fixed-role-permission-system"></a>Sistema de permissão de função fixa anterior

As funções de servidor fixas e as funções de banco de dados fixas têm permissões pré-configuradas que não podem ser alteradas. Para determinar quem é um membro de uma função de servidor fixa, execute a consulta a seguir:    
> [!NOTE]
>  Não se aplica ao Banco de Dados SQL ou ao SQL Data Warehouse, em que a permissão de nível de servidor não está disponível. A coluna `is_fixed_role` de `sys.server_principals` foi adicionada no SQL Server 2012. Ela não é necessária para versões anteriores do SQL Server.  
> ```sql
> SELECT SP1.name AS ServerRoleName, 
>  isnull (SP2.name, 'No members') AS LoginName   
>  FROM sys.server_role_members AS SRM
>  RIGHT OUTER JOIN sys.server_principals AS SP1
>    ON SRM.role_principal_id = SP1.principal_id
>  LEFT OUTER JOIN sys.server_principals AS SP2
>    ON SRM.member_principal_id = SP2.principal_id
>  WHERE SP1.is_fixed_role = 1 -- Remove for SQL Server 2008
>  ORDER BY SP1.name;
> ```
> [!NOTE]
>  * Todos os logons e os usuários são membros das funções públicas e não podem ser removidos. 
>  * Essa consulta verifica tabelas no banco de dados mestre, mas ela pode ser executada em qualquer banco de dados do produto local. 

Para determinar quem é membro de uma função de banco de dados fixa, execute a consulta a seguir em cada banco de dados.
```sql
SELECT DP1.name AS DatabaseRoleName, 
   isnull (DP2.name, 'No members') AS DatabaseUserName 
 FROM sys.database_role_members AS DRM
 RIGHT OUTER JOIN sys.database_principals AS DP1
   ON DRM.role_principal_id = DP1.principal_id
 LEFT OUTER JOIN sys.database_principals AS DP2
   ON DRM.member_principal_id = DP2.principal_id
 WHERE DP1.is_fixed_role = 1
 ORDER BY DP1.name;
```
Para entender as permissões concedidas a cada função, consulte as descrições de função em ilustrações nos Manuais Online ([funções de nível de servidor](../../../relational-databases/security/authentication-access/server-level-roles.md) e [funções de nível de banco de dados](../../../relational-databases/security/authentication-access/database-level-roles.md)).

## <a name="newer-granular-permission-system"></a>Novo sistema de permissão granular

Esse sistema é flexível, o que significa que ele poderá ser complicado se as pessoas que estão definindo a configuração buscarem precisão. Para simplificar, ele ajuda a criar funções, atribuir permissões a funções e adicionar grupos de pessoas para as funções. E é mais fácil se a equipe de desenvolvimento de banco de dados separar atividades por esquema e, em seguida, conceder permissões de função para um esquema inteiro em vez de tabelas individuais ou procedimentos. Cenários do mundo real são complexos e as necessidades de negócios podem criar requisitos de segurança inesperados.   

[!INCLUDE[database-engine-permissions](../../../includes/paragraph-content/database-engine-permissions.md)]


### <a name="security-classes"></a>Classes de segurança

As permissões podem ser concedidas no nível do servidor, no nível de banco de dados, no nível de esquema ou no nível de objeto, etc. Há 26 níveis (chamados de classes). A lista completa de classes em ordem alfabética é: `APPLICATION ROLE`, `ASSEMBLY`, `ASYMMETRIC KEY`, `AVAILABILITY GROUP`, `CERTIFICATE`, `CONTRACT`, `DATABASE`, `DATABASE` `SCOPED CREDENTIAL`, `ENDPOINT`, `FULLTEXT CATALOG`, `FULLTEXT STOPLIST`, `LOGIN`, `MESSAGE TYPE`, `OBJECT`, `REMOTE SERVICE BINDING`, `ROLE`, `ROUTE`, `SCHEMA`, `SEARCH PROPERTY LIST`, `SERVER`, `SERVER ROLE`, `SERVICE`, `SYMMETRIC KEY`, `TYPE`, `USER` e `XML SCHEMA COLLECTION`. (Algumas classes não estão disponíveis em alguns tipos de SQL Servers.) Para fornecer informações completas sobre cada classe é necessária uma consulta diferente.

### <a name="principals"></a>Principals

As permissões são concedidas a entidades de segurança. Entidades de segurança podem ser usuários, logons, funções de banco de dados ou funções de servidor. Os logons podem representar grupos do Windows que incluem muitos usuários do Windows. Como os grupos do Windows não são mantidos pelo SQL Server, o SQL Server nem sempre saberá que é membro de um grupo do Windows. Quando um usuário do Windows se conecta ao SQL Server, o pacote de logon contém os tokens de associação de grupo do Windows para o usuário.

Quando um usuário do Windows se conecta usando um logon baseado em um grupo do Windows, algumas atividades podem exigir que o SQL Server crie um logon ou usuário para representar o usuário do Windows individual. Por exemplo, um grupo do Windows (Engenheiros) contém os usuários (Mary, Todd, Pat) e o grupo de engenheiros têm uma conta de usuário de banco de dados. Se Mary tem permissão e cria uma tabela, um usuário (Mary) pode ser criado para ser o proprietário da tabela. Ou, se Todd tiver uma permissão negada que o restante do grupo de engenheiros tem, então, o usuário Todd deverá ser criado para acompanhar a negação de permissão.

Lembre-se de que um usuário do Windows pode ser membro de mais de um grupo do Windows (por exemplo, engenheiros e gerentes). As permissões concedidas ou negadas ao logon de engenheiros, ao logon de gerentes, concedidas ou negadas ao usuário individualmente e concedidas ou negadas a funções das quais o usuário é membro, serão agregadas e avaliadas para as permissões efetivas. A função `HAS_PERMS_BY_NAME` pode revelar se um usuário ou logon tem uma permissão específica. No entanto, não há nenhuma maneira óbvia de determinar a origem da concessão ou negação de permissão. Estude a lista de permissões e, talvez, realize testes de tentativa e erro.

## <a name="useful-queries"></a>Consultas úteis

### <a name="server-permissions"></a>Permissões de servidor

A consulta a seguir retorna uma lista das permissões concedidas ou negadas no nível do servidor. Essa consulta pode ser executada no banco de dados mestre.   
> [!NOTE]
>  As permissões de nível de servidor não podem ser concedidas ou consultadas no Banco de Dados SQL ou o SQL Data Warehouse.   
> ```sql
> SELECT pr.type_desc, pr.name, 
>  isnull (pe.state_desc, 'No permission statements') AS state_desc, 
>  isnull (pe.permission_name, 'No permission statements') AS permission_name 
>  FROM sys.server_principals AS pr
>  LEFT OUTER JOIN sys.server_permissions AS pe
>    ON pr.principal_id = pe.grantee_principal_id
>  WHERE is_fixed_role = 0 -- Remove for SQL Server 2008
>  ORDER BY pr.name, type_desc;
> ```

### <a name="database-permissions"></a>Permissões de banco de dados

A consulta a seguir retorna uma lista das permissões concedidas ou negadas no nível do banco de dados. Essa consulta pode ser executada em cada banco de dados.   
```sql
SELECT pr.type_desc, pr.name, 
 isnull (pe.state_desc, 'No permission statements') AS state_desc, 
 isnull (pe.permission_name, 'No permission statements') AS permission_name 
FROM sys.database_principals AS pr
LEFT OUTER JOIN sys.database_permissions AS pe
    ON pr.principal_id = pe.grantee_principal_id
WHERE pr.is_fixed_role = 0 
ORDER BY pr.name, type_desc;
```

Cada classe de permissão da tabela de permissões pode ser unida a outras exibições do sistema que fornecem informações relacionadas sobre essa classe de protegível. Por exemplo, a consulta a seguir fornece o nome do objeto de banco de dados que é afetado pela permissão.    
```sql
SELECT pr.type_desc, pr.name, pe.state_desc, 
 pe.permission_name, s.name + '.' + oj.name AS Object, major_id
 FROM sys.database_principals AS pr
 JOIN sys.database_permissions AS pe
   ON pr.principal_id = pe.grantee_principal_id
 JOIN sys.objects AS oj
   ON oj.object_id = pe.major_id
 JOIN sys.schemas AS s
   ON oj.schema_id = s.schema_id
 WHERE class_desc = 'OBJECT_OR_COLUMN';
```
Use a função `HAS_PERMS_BY_NAME` para determinar se um usuário específico (neste caso `TestUser`) tem uma permissão. Por exemplo:   
```sql
EXECUTE AS USER = 'TestUser';
SELECT HAS_PERMS_BY_NAME ('dbo.T1', 'OBJECT', 'SELECT');
REVERT;
```
Para obter os detalhes da sintaxe, consulte [HAS_PERMS_BY_NAME](../../../t-sql/functions/has-perms-by-name-transact-sql.md).

## <a name="see-also"></a>Consulte Também:

[Guia de Introdução às permissões do mecanismo de banco de dados](../../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)    
[Tutorial: Introdução ao Mecanismo de Banco de Dados](Tutorial:%20Getting%20Started%20with%20the%20Database%20Engine.md) 


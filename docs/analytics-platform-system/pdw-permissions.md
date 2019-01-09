---
title: Permissões no Parallel Data Warehouse | Microsoft Docs
description: Este artigo descreve os requisitos e opções para gerenciar permissões de banco de dados para o Parallel Data Warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1ac058e42b8bad4f499210835a1f85c3cc7a08a5
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52523589"
---
# <a name="managing-permissions-in-parallel-data-warehouse"></a>Gerenciar permissões no Parallel Data Warehouse
Este artigo descreve os requisitos e opções para gerenciar permissões de banco de dados para SQL Server PDW.  
  
## <a name="BackupRestoreBasics"></a>Noções básicas sobre permissões de mecanismo de banco de dados  
Permissões do mecanismo de banco de dados no SQL Server PDW são gerenciadas no nível do servidor por meio de logons e no nível do banco de dados por meio de usuários de banco de dados e funções de banco de dados definido pelo usuário.  
  
**Logons**  
Os logons são contas de usuário individuais para fazer logon no SQL Server PDW. PDW do SQL Server dá suporte a logons usando a autenticação de autenticação do Windows e SQL Server.  Logons de autenticação do Windows podem ser usuários de Windows ou grupos do Windows de qualquer domínio que seja confiável pelo SQL Server PDW. Logons de autenticação do SQL Server são definidos e são autenticados pelo SQL Server PDW e devem ser criados, especificando uma senha.  
  
Os membros a **sysadmin** função de servidor fixa (como o **sa** logon) pode se conectar a um banco de dados sem ter que está sendo mapeado para um usuário de banco de dados. Eles são mapeados para o **dbo** usuário. O proprietário do banco de dados também é mapeado como o **dbo** usuário.  
  
**Funções de servidor**  
Há quatro funções especiais de servidor com um conjunto de funções pré-configuradas que fornecem um agrupamento conveniente de permissões de nível de servidor. O **sysadmin**, **MediumRC**, **LargeRC**, e **XLargeRCfixed** funções de servidor são as funções de servidor único implementadas atualmente no SQL Server PDW. O **sa** logon é o único membro do **sysadmin** função de servidor fixa e logons adicionais não podem ser adicionados para o **sysadmin** função. Logons podem ser concedidos a **CONTROL SERVER** permissão, que é semelhante, embora não sejam idênticos, para o **sysadmin** função de servidor fixa. Use [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) para adicionar membros a outras funções de servidor. SQL Server PDW não dá suporte a funções de servidor definidas pelo usuário.  
  
**Usuários de banco de dados**  
Logons recebem acesso a um banco de dados criando um usuário de banco de dados em um banco de dados e mapeando esse usuário de banco de dados para um logon. Normalmente, o nome de usuário do banco de dados é igual ao nome de logon, mas não precisa ser o mesmo. Cada usuário de banco de dados é mapeado para um logon único. Um logon pode ser mapeado para apenas um usuário em um banco de dados, mas pode ser mapeado como um usuário de banco de dados em vários bancos de dados diferentes.  
  
**Funções de banco de dados fixa**  
Funções de banco de dados fixas são um conjunto de funções pré-configuradas que fornecem um agrupamento conveniente de permissões de nível de banco de dados. Usuários de banco de dados e funções de banco de dados definidos pelo usuário podem ser adicionadas às funções de banco de dados fixa usando o [sp_addrolemember](../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) procedimento. Para obter mais informações sobre as funções de banco de dados fixa, consulte [funções de banco de dados fixas](#fixed-database-roles).  
  
**Funções de banco de dados definido pelo usuário**  
Os usuários com o **CREATE ROLE** permissão pode criar novas funções de banco de dados definido pelo usuário para representar grupos de usuários com permissões comuns. Normalmente, as permissões são concedidas ou negadas para toda a função, simplificando o gerenciamento e o monitoramento de permissões.  
  
As permissões são concedidas a entidades de segurança (logons, usuários e funções) usando o **GRANT** instrução. As permissões são explicitamente negadas usando o **DENY** comando. Um concedida ou negada permissão anteriormente é removido usando o **REVOGAR** instrução. As permissões são cumulativas, com o usuário recebendo todas as permissões concedidas ao usuário, logon e quaisquer associações de grupo; no entanto, qualquer negação de permissão substitui todas as concessões. <!-- MISSING LINKS (For information, syntax, and available permissions with these commands, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md)).  -->  
  
Veja a seguir um exemplo que representa um método comum e recomendado de configuração de permissões.  
  
1.  Se usar a autenticação do Windows, crie um logon para cada usuário do Windows ou grupo do Windows que se conectará ao SQL Server PDW. Se usar autenticação do SQL Server, crie um logon para cada pessoa que se conectará ao SQL Server PDW.  
  
2.  Crie um usuário de banco de dados para cada logon em todos os bancos de dados necessários.  
  
3.  Crie uma ou mais funções de banco de dados definido pelo usuário, cada um representando uma função semelhante. Por exemplo, analista financeiro e analista de vendas.  
  
4.  Adicione usuários de banco de dados a uma ou mais funções de banco de dados definido pelo usuário.  
  
5.  Conceda permissões às funções de banco de dados definidas pelo usuário.  
  
Logons são objetos de nível de servidor e podem ser listados por meio da exibição [sys. server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md). Somente as permissões de nível de servidor podem ser concedidas a entidades de segurança do servidor.  
  
Usuários e funções de banco de dados são objetos de nível de banco de dados e podem ser listadas por meio da exibição [sys. database_principals](../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md). Apenas permissões de nível de banco de dados podem ser concedidas a entidades de segurança do banco de dados.  
  
## <a name="BackupTypes"></a>Permissões padrão  
A lista a seguir descreve as permissões padrão:  
  
-   Quando um logon é criado por usos **CREATE LOGIN** instrução, o logon recebe o **CONNECT SQL** permissão permitindo que o logon para conexão com o SQL Server PDW.  
  
-   Quando um usuário de banco de dados é criado usando o **criar usuário** instrução, o usuário recebe a **CONNECT ON DATABASE::**_< database_name >_ permissão, permitindo que o Faça logon para conectar-se ao banco de dados como um usuário.  
  
-   Todas as entidades, incluindo a função pública, não tem nenhuma permissão explícita ou implícita por padrão, como permissões implícitas são herdadas de permissões explícitas. Portanto, quando nenhuma permissão explícita estiverem presente, também não pode haver nenhuma permissão implícita.  
  
-   Quando um logon se torna o proprietário de um objeto ou o banco de dados, o logon sempre tem todas as permissões do objeto ou o banco de dados. As permissões de propriedade não são visíveis como as permissões explícitas. O **GRANT**, **REVOGAR**, e **DENY** instruções não têm efeito nas permissões de propriedade. Propriedade pode ser alterada usando o [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md) instrução.  
  
-   O logon sa tem todas as permissões no dispositivo. Semelhante às permissões de propriedade, as permissões de sa não podem ser alteradas e não são visíveis como as permissões explícitas. O **GRANT**, **REVOGAR**, e **DENY** instruções não têm nenhum efeito nas permissões de sa.  
  
-   A função de servidor público não recebe nenhuma permissão por padrão e não herda as permissões de outras funções de servidor. A função de servidor público pode receber permissões explícitas com o **GRANT**, **REVOGAR**, e **DENY** instruções.  
  
-   As transações não exigem permissões. Todas as entidades podem ser executados a **BEGIN TRANSACTION**, **confirmar**, e **REVERSÃO** comandos de transação. No entanto, uma entidade de segurança deve ter as permissões apropriadas para executar cada instrução na transação.  
  
-   A instrução **USE** não requer permissões. Todas as entidades podem ser executados a **uso** instrução em qualquer banco de dados, no entanto, para acessar um banco de dados, eles devem ter uma entidade de usuário no banco de dados ou o usuário convidado deve ser habilitado.  
  
### <a name="the-public-role"></a>A função pública  
Todos os novos logons de dispositivo pertencem automaticamente à função pública. A função de servidor público tem as seguintes características:  
  
-   A função de servidor público não tem permissões por padrão.  
  
-   Todas as entidades são membros da função de servidor público e a função de servidor público não é um membro de outra função de servidor.  
  
-   A função de servidor público não pode herdar permissões implícitas. Quaisquer permissões dadas a função pública devem ser concedidas explicitamente.  
  
## <a name="BackupProc"></a>Determinando permissões  
Se um logon tem permissão para executar uma ação específica depende das permissões concedidas ou negadas ao logon, usuário e funções que o usuário é membro do. Permissões de nível de servidor (como **CREATE LOGIN** e **VIEW SERVER STATE**) estão disponíveis para entidades de segurança de nível de servidor (logons). Permissões de nível de banco de dados (como **selecionar** de uma tabela ou **EXECUTE** em um procedimento) estão disponíveis para entidades de nível de banco de dados (usuários e funções de banco de dados).  
  
### <a name="implicit-and-explicit-permissions"></a>Permissões implícitas e explícitas  
Uma *permissão explícita* é uma permissão **GRANT** ou **DENY** concedida a uma entidade de segurança por uma instrução **GRANT** ou **DENY**. Permissões de nível de banco de dados são listadas na [sys. database_permissions](../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) modo de exibição. Permissões de nível de servidor são listadas na [server_permissions](../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) exibição.  
  
Uma *permissão implícita* é um **GRANT** ou **DENY** permissão herdou uma entidade de segurança (logon ou função de servidor). Uma permissão pode ser herdada das seguintes maneiras.  
  
-   Uma entidade pode herdar uma permissão de uma função se a entidade for um membro da função, mesmo se a entidade de segurança não tem um explícito **GRANT** ou **DENY** permissão.  
  
-   Uma entidade pode herdar uma permissão em um objeto subordinado (como uma tabela), se a entidade tem uma permissão em um dos objetos pai escopos (como o esquema da tabela ou a permissão no banco de dados inteiro).  
  
-   Uma entidade pode herdar uma permissão fazendo com que uma permissão que inclui uma permissão subordinada. Por exemplo o **ALTER ANY USER** permissão inclui a ambas as **CREATE USER** e o **ALTER ON USER::** _<name>_ permissões.  
  
### <a name="determining-permissions-when-performing-actions"></a>Determinando permissões ao executar ações  
O processo de determinação de qual permissão para atribuir a uma entidade de segurança é complexo. A complexidade ocorre ao determinar as permissões implícitas porque as entidades podem ser membros de várias funções e permissões podem ser passadas por meio de vários níveis na hierarquia de funções.  
  
A lista a seguir descreve regras gerais para determinar as permissões:  
  
-   Propriedade indica a permissão.  
  
    Um proprietário de objeto tem todas as permissões no objeto. Da mesma forma, um proprietário de banco de dados tem todas as permissões no banco de dados e todas as permissões nos objetos no banco de dados. Essas permissões não podem ser alteradas.  
  
-   As permissões podem ser herdadas em vários níveis na hierarquia de associações de função de servidor.  
  
    Por exemplo, suponha que você tem a seguinte situação:  
  
    -   David de logon é um membro da função de banco de dados PerfAnalysts.  
  
    -   PerfAnalysts é um membro da função de banco de dados de produção.  
  
    -   Não têm de David e PerfAnalysts **selecionar** permissão na tabela Customer. A permissão foi revogada ou nunca explicitamente concedida.  
  
    -   Tem de produção **selecionar** permissão na tabela Customer.  
  
    Nesse caso, PerfAnalysts herdará **GRANT** permissão na tabela de cliente de produção e David herdará **GRANT** permissão na tabela de cliente de produção.  
  
-   **DENY** substituições **GRANT** quando as permissões em conflito.  
  
    Por exemplo, suponha que David de logon não tem permissões na tabela de cliente e é um membro de duas funções de banco de dados-dbgroup1, que tem **DENY** permissão na tabela Customer e dbgroup2, que tem **GRANT** permissão na tabela Customer. Nesse caso, David herdarão as **DENY** permissão na tabela Customer. Esse é o caso se as funções ganhou suas permissões explicitamente ou implicitamente.  
  
### <a name="auditing-permissions"></a>Permissões de auditoria  
Para pesquisar as permissões de um usuário, verifique o seguinte.  
  
-   Execute a seguinte consulta para determinar quais logons são administradores do sistema.  
  
    ```sql  
    SELECT SPLogins.name, 'is a member of ', SPRoles.name   
    FROM sys.server_role_members AS SRM   
    JOIN sys.server_principals AS SPRoles   
        ON SRM.role_principal_id = SPRoles.principal_id   
    JOIN sys.server_principals AS SPLogins   
        ON SRM.member_principal_id = SPLogins.principal_id;  
    ```  
  
-   Execute a seguinte consulta para determinar quais logons foram concedidas permissões explícitas.  
  
    ```sql  
    SELECT name, 'has the ', state_desc , permission_name, ' permission'  
    FROM sys.server_permissions AS SP  
    JOIN sys.server_principals AS SPRoles   
        ON SP.grantee_principal_id = SPRoles.principal_id;  
    ```  
  
-   Execute a seguinte consulta em um banco de dados do usuário para determinar quais usuários de banco de dados são membros de uma função de banco de dados.  
  
    ```sql  
    SELECT DPUsers.name, 'is a member of ', DPRoles.name    
    FROM sys.database_role_members AS DRM  
    JOIN sys.database_principals AS DPRoles   
        ON DRM.role_principal_id = DPRoles.principal_id  
    JOIN sys.database_principals AS DPUsers  
        ON DRM.member_principal_id = DPUsers.principal_id;  
    ```  
  
-   Execute a seguinte consulta em um banco de dados do usuário para determinar quais usuários de banco de dados e funções concedidas ou negadas permissões específicas. Você terá a modos de exibição adicionais, como sys. Objects e sys. Schemas para identificar os itens descritos com o major_id consulta.  
  
    ```sql  
    SELECT DPUsers.name, 'has the ', permission_name,   
    'permission on the item described as class = ', class, 'id = ', major_id  
    FROM sys.database_permissions AS DP  
    JOIN sys.database_principals AS DPUsers  
        ON DP.grantee_principal_id = DPUsers.principal_id;  
    ```  
  
## <a name="RestoreProc"></a>Práticas recomendadas de permissões de banco de dados  
  
-   Conceda permissões de nível mais granular que é prático. Conceder permissões a tabela ou as permissões de nível de exibição pode se tornar impossível de gerenciar. Mas a concessão de permissões no nível do banco de dados pode ser muito permissivas. Se o banco de dados foi projetado com esquemas para definir os limites de trabalho, talvez a concessão de permissão para o esquema é um meio-termo apropriado entre o nível de tabela e o nível de banco de dados.  
  
-   Conceder permissões a funções, em vez de usuários ou logons. O gerenciamento de direitos usando funções em vez de usuários torna mais fácil conceder ou revogar um conjunto de permissões para um usuário ou logon, movendo-os dentro ou fora da função de rapidamente. Quando uma função passa de uma pessoa para outra, as permissões podem permanecer intactas no nível de função enquanto as alterações de associação de função.  
  
-   Conceder permissões a funções com base em função de trabalho e em funções do grupo de nível mais altos que combinam as funções da função de trabalho com base no grupo da empresa executando as ações.  
  
-   Cada usuário final deve ter um logon exclusivo. Não permitir que os usuários compartilhem logons. Fornecer um logon para cada usuário garante uma trilha de auditoria e simplifica o gerenciamento de permissão.  
  
## <a name="fixed-database-roles"></a>Funções de banco de dados fixas
O SQL Server fornece funções de nível de banco de dados (fixas) pré-configuradas para ajudá-lo a gerenciar as permissões em um servidor. As funções pré-configuradas são corrigidas em que você não pode alterar as permissões atribuídas a eles. Funções de banco de dados definido pelo usuário também podem ser criadas. Você pode alterar as permissões atribuídas às funções de banco de dados definido pelo usuário.  
  
Funções são entidades de segurança que agrupam outras entidades. Funções de banco de dados são todo o banco de dados no escopo de suas permissões. Usuários de banco de dados e outras funções de banco de dados podem ser adicionadas como membros das funções de banco de dados. As funções de banco de dados fixa não podem ser adicionadas ao outro. (As*funções* são como *grupos* no sistema operacional Windows.)  
  
Há funções de banco de dados fixa 9.  
  
-   **db_owner**  
  
-   **db_securityadmin**  
  
-   **db_accessadmin**  
  
-   **db_backupoperator**  
  
-   **db_ddladmin**  
  
-   **db_datawriter**  
  
-   **db_datareader**  
  
-   **db_denydatawriter**  
  
-   **db_denydatareader**  
  
### <a name="permissions-of-the-fixed-database-roles"></a>Permissões das funções de banco de dados fixa  
O sistema de funções de servidor fixas e funções de banco de dados fixa é um sistema herdado com origem no 1980's. Funções fixas ainda são suportadas e são úteis em ambientes onde há alguns usuários e as necessidades de segurança são simples. Começando com o SQL Server 2005, um sistema mais detalhado de concessão de permissão foi criado. Esse novo sistema é mais granular, oferecendo muito mais opções para conceder e negar permissões. A complexidade extra do sistema mais granular, ficará mais difícil de aprender, mas a maioria dos sistemas empresariais deve conceder permissões em vez de usar as funções fixas. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md). -->O gráfico a seguir mostra as permissões que estão associadas a cada função de banco de dados fixa. Todas as permissões neste gráfico do SQL Server não estão disponíveis (ou necessários) dos pontos de acesso.  
  
![Funções de banco de dados fixas da segurança de APS](./media/pdw-permissions/APS_security_fixed_db_roles.png "APS_security_fixed_db_roles")  
  
### <a name="related-content"></a>Conteúdo relacionado  
  
-   Para criar funções definidas pelo usuário, consulte [CREATE ROLE](../t-sql/statements/create-role-transact-sql.md).  
  
  
## <a name="fixed-server-roles"></a>Funções de servidor fixas
Funções de servidor fixas são criadas automaticamente pelo SQL Server. SQL Server PDW tem uma implementação limitada de funções de servidor fixas do SQL Server. Somente o **sysadmin** e **público** ter logons de usuário como membros. O **setupadmin** e **dbcreator** as funções são usadas internamente pelo SQL Server PDW. Membros adicionais não podem ser adicionados ou removidos de qualquer função.  
  
### <a name="sysadmin-fixed-server-role"></a>sysadmin a função de servidor fixa  
Os membros da função de servidor fixa **sysadmin** podem executar qualquer atividade no servidor. O **sa** logon é o único membro do **sysadmin** função de servidor fixa. Logons adicionais não podem ser adicionados para o **sysadmin** função de servidor fixa. Conceder a permissão **CONTROL SERVER** aproxima-se da associação à função de servidor fixa **sysadmin**. O exemplo a seguir concede a **CONTROL SERVER** permissão a um logon denominado Fay.  
  
```sql  
USE master;  
GO  
GRANT CONTROL SERVER TO Fay;  
```  
  
> [!IMPORTANT]  
> O **CONTROL SERVER** permissão fornece controle quase completa do SQL Server PDW. Sempre que possível, forneça permissões mais granulares para os logons em vez disso. Por exemplo, considere conceder a **VIEW SERVER STATE**, **ALTER ANY LOGIN**, **VIEW ANY DATABASE**, ou **CREATE ANY DATABASE** permissões.  
  
### <a name="public-server-role"></a>Função de servidor público  
Todo logon pode se conectar ao SQL Server PDW é um membro do **pública** função de servidor. Todos os logons herdam as permissões concedidas ao **pública** em qualquer objeto. Somente atribua **pública** permissões em um objeto quando você deseja que o objeto esteja disponível para todos os usuários. Você não pode alterar a associação na **pública** função.  
  
> [!NOTE]  
> **público** é implementado Diferentemente de outras funções. Porque todas as entidades de servidor são membros do público, a associação do **pública** função não estiver listada na **server_role_members** DMV.  
  
### <a name="fixed-server-roles-vs-granting-permissions"></a>Vs de funções de servidor fixas. Concedendo permissões  
O sistema de funções de servidor fixas e funções de banco de dados fixa é um sistema herdado com origem no 1980's. Funções fixas ainda são suportadas e são úteis em ambientes onde há alguns usuários e as necessidades de segurança são simples. Começando com o SQL Server 2005, um sistema mais detalhado de concessão de permissão foi criado. Esse novo sistema é mais granular, oferecendo muito mais opções para conceder e negar permissões. A complexidade extra do sistema mais granular, ficará mais difícil de aprender, mas a maioria dos sistemas empresariais deve conceder permissões em vez de usar as funções fixas. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  -->  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
- [Conceder permissões](grant-permissions.md)

<!-- MISSING LINKS
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->


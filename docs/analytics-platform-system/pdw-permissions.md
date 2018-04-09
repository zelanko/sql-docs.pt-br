---
title: Permissões de PDW (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7e271980-bec8-424b-9f68-cea11b4e64e8
caps.latest.revision: 23
ms.openlocfilehash: 95843be163714be27e6eeb7f28825e98a5371e19
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="pdw-permissions"></a>Permissões do PDW
Este tópico descreve os requisitos e opções de gerenciamento de permissões de banco de dados para SQL Server PDW.  
  
## <a name="BackupRestoreBasics"></a>Noções básicas de permissão de mecanismo de banco de dados  
Permissões do mecanismo de banco de dados no SQL Server PDW são gerenciadas no nível do servidor por meio de logon e o nível de banco de dados por meio de usuários de banco de dados e funções de banco de dados definido pelo usuário.  
  
**Logons**  
Logons são contas de usuário individuais de logon do SQL Server PDW. SQL Server PDW dá suporte a logons usando a autenticação do SQL Server e de autenticação do Windows.  Logons de autenticação do Windows podem ser usuários do Windows ou grupos do Windows de qualquer domínio confiável pelo SQL Server PDW. Logons de autenticação do SQL Server são definidos e autenticados pelo SQL Server PDW e devem ser criados, especificando uma senha.  
  
Membros do **sysadmin** função fixa de servidor (como o **sa** logon) pode se conectar a um banco de dados sem ter que está sendo mapeado para um usuário de banco de dados. Eles são mapeados para o **dbo** usuário. O proprietário do banco de dados também é mapeado como o **dbo** usuário.  
  
**Funções de servidor**  
Há quatro funções especiais de servidor com um conjunto de funções pré-configuradas que fornecem um agrupamento conveniente de permissões de nível de servidor. O **sysadmin**, **MediumRC**, **LargeRC**, e **XLargeRCfixed** funções de servidor são as funções de servidor único implementadas atualmente no SQL Servidor PDW. O **sa** logon é o único membro do **sysadmin** função de servidor fixa e logins adicionais não não possível adicionar o **sysadmin** função. Logons podem ser concedidos a **CONTROL SERVER** permissão, que é semelhante, embora não sejam idênticos, para o **sysadmin** função de servidor fixa. Use [ALTER SERVER ROLE](../t-sql/statements/alter-server-role-transact-sql.md) para adicionar membros a funções de servidor. SQL Server PDW não dá suporte a funções de servidor definidas pelo usuário.  
  
**Usuários do banco de dados**  
Logons recebem acesso a um banco de dados criando um usuário de banco de dados em um banco de dados e mapeamento desse usuário de banco de dados para um logon. Normalmente, o nome de usuário do banco de dados é igual ao nome de logon, mas não precisa ser o mesmo. Cada usuário de banco de dados é mapeado para um logon único. Um logon pode ser mapeado para apenas um usuário em um banco de dados, mas pode ser mapeado como um usuário de banco de dados em vários bancos de dados diferentes.  
  
**Funções de banco de dados fixa**  
Funções de banco de dados fixas são um conjunto de funções pré-configuradas que fornecem um agrupamento conveniente de permissões de nível de banco de dados. Os usuários do banco de dados e funções de banco de dados definidos pelo usuário podem ser adicionadas às funções de banco de dados fixa usando o [sp_addrolemember](../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) procedimento. Para obter mais informações sobre funções fixas de banco de dados, consulte [funções fixas de banco de dados](#fixed-database-roles).  
  
**Funções de banco de dados definido pelo usuário**  
Os usuários com o **Criar função** permissão pode criar novas funções de banco de dados definido pelo usuário para representar grupos de usuários com permissões comuns. Normalmente, as permissões são concedidas ou negadas para toda a função, simplificando o gerenciamento e o monitoramento de permissões.  
  
As permissões são concedidas a entidades de segurança (logons, usuários e funções) usando o **GRANT** instrução. As permissões são explicitamente negadas usando o **DENY** comando. Um concedida ou negada permissão anteriormente é removida usando o **REVOGAR** instrução. As permissões são cumulativas, com o usuário recebendo todas as permissões concedidas ao usuário, logon e quaisquer associações de grupo; no entanto, qualquer negação de permissão substitui todas as concessões. <!-- MISSING LINKS (For information, syntax, and available permissions with these commands, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md)).  -->  
  
Veja a seguir um exemplo que representa um método comum e recomendado de configuração de permissões.  
  
1.  Se a autenticação do Windows, crie um logon para cada usuário do Windows ou grupo do Windows que vai se conectar ao SQL Server PDW. Se usar autenticação do SQL Server, crie um logon para cada pessoa que se conectarão ao SQL Server PDW.  
  
2.  Crie um usuário de banco de dados para cada logon em todos os bancos de dados necessários.  
  
3.  Crie uma ou mais funções de banco de dados definido pelo usuário, cada uma representando uma função semelhante. Por exemplo, analista financeiro e analista de vendas.  
  
4.  Adicione usuários de banco de dados para uma ou mais funções de banco de dados definido pelo usuário.  
  
5.  Conceda permissões às funções de banco de dados definidas pelo usuário.  
  
Logons são objetos de nível de servidor e podem ser listados exibindo [sys. server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md). Somente as permissões de nível de servidor podem ser concedidas a entidades de segurança do servidor.  
  
Usuários e funções de banco de dados são objetos de nível de banco de dados e podem ser listadas exibindo [database_principals](../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md). Somente as permissões de nível de banco de dados podem ser concedidas aos objetos de banco de dados.  
  
## <a name="BackupTypes"></a>Permissões padrão  
A lista a seguir descreve as permissões padrão:  
  
-   Quando um logon é criado pelo usos **CREATE LOGIN** instrução, o logon recebe o **CONNECT SQL** permissão Permitir logon para conexão com o SQL Server PDW.  
  
-   Quando um usuário de banco de dados é criado usando o **CREATE USER** instrução, o usuário receberá o **CONNECT ON DATABASE:: * < nome_do_banco_de_dados >* permissão, permitindo que o logon para se conectar ao banco de dados como um usuário.  
  
-   Todas as entidades, incluindo a função pública, não têm nenhuma permissão explícita ou implícita por padrão como permissões implícitas são herdadas de permissões explícitas. Portanto, quando nenhuma permissão explícita estiverem presente, não pode também haver nenhuma permissão implícita.  
  
-   Quando um logon se torna o proprietário de um objeto ou o banco de dados, o logon sempre tem todas as permissões do objeto ou o banco de dados. As permissões de propriedade não são visíveis como permissões explícitas. O **GRANT**, **REVOGAR**, e **DENY** instruções não têm nenhum efeito nas permissões de propriedade. Propriedade pode ser alterada usando o [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md) instrução.  
  
-   O logon sa tem todas as permissões no dispositivo. Semelhante às permissões de propriedade, as permissões de sa não podem ser alteradas e não são visíveis como permissões explícitas. O **GRANT**, **REVOGAR**, e **DENY** instruções não têm nenhum efeito nas permissões de sa.  
  
-   A função de servidor público não recebe nenhuma permissão por padrão e não herda as permissões de outras funções de servidor. A função de servidor público pode receber permissões explícitas a **GRANT**, **REVOGAR**, e **DENY** instruções.  
  
-   Transações não exigem permissões. Todas as entidades de segurança podem executar o **BEGIN TRANSACTION**, **confirmar**, e **REVERSÃO** comandos de transação. No entanto, uma entidade de segurança deve ter as permissões apropriadas para executar cada instrução na transação.  
  
-   A instrução **USE** não requer permissões. Todas as entidades de segurança podem executar o **USE** instrução em qualquer banco de dados, no entanto, para acessar um banco de dados, eles devem ter uma entidade de segurança do usuário no banco de dados ou o usuário convidado deve ser habilitado.  
  
### <a name="the-public-role"></a>A função pública  
Todos os novos logons de dispositivo automaticamente pertencem à função pública. A função de servidor público tem as seguintes características:  
  
-   A função de servidor público não tem permissões por padrão.  
  
-   Todas as entidades são membros da função de servidor público e a função de servidor público não é um membro de outra função de servidor.  
  
-   A função de servidor público não pode herdar permissões implícitas. Qualquer permissões concedidas à função pública devem ser concedidas explicitamente.  
  
## <a name="BackupProc"></a>Determinando permissões  
Se um logon tem permissão para executar uma ação específica depende das permissões concedidas ou negadas ao logon, usuário e funções que o usuário é membro. Permissões de nível de servidor (como **CREATE LOGIN** e **VIEW SERVER STATE**) estão disponíveis para entidades no nível do servidor (logons). Permissões de nível de banco de dados (como **selecione** de uma tabela ou **executar** em um procedimento) estão disponíveis para objetos de nível de banco de dados (usuários e funções de banco de dados).  
  
### <a name="implicit-and-explicit-permissions"></a>Permissões implícitas e explícitas  
Uma *permissão explícita* é uma permissão **GRANT** ou **DENY** concedida a uma entidade de segurança por uma instrução **GRANT** ou **DENY**. Permissões de nível de banco de dados são listadas no [database_permissions](../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) exibição. Permissões de nível de servidor são listadas no [server_permissions](../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) exibição.  
  
Um *permissão implícita* é um **GRANT** ou **DENY** permissão foi herdada uma entidade de segurança (logon ou função de servidor). Uma permissão pode ser herdada das seguintes maneiras.  
  
-   Uma entidade pode herdar uma permissão de uma função se a entidade for um membro da função, mesmo se a entidade de segurança não tem uma explícita **GRANT** ou **DENY** permissão.  
  
-   Uma entidade pode herdar de uma permissão em um objeto subordinado (como uma tabela) se a entidade de segurança tem uma permissão em um dos escopos objetos pai (como o esquema da tabela ou a permissão no banco de dados inteiro).  
  
-   Uma entidade pode herdar de uma permissão por ter uma permissão que inclui uma permissão subordinada. Por exemplo o **ALTER ANY USER** permissão inclui a ambos o **CREATE USER** e o **ALTER ON USER:: *<name>*  permissões.  
  
### <a name="determining-permissions-when-performing-actions"></a>Determinando permissões ao executar ações  
O processo de determinação de qual permissão para atribuir a uma entidade de segurança é complexo. A complexidade ocorre quando determinando permissões implícitas porque as entidades podem ser membros de várias funções e permissões podem ser passadas por meio de vários níveis na hierarquia de funções.  
  
A lista a seguir descreve as regras gerais para determinar as permissões:  
  
-   Propriedade indica a permissão.  
  
    Um proprietário de objeto tem todas as permissões no objeto. Da mesma forma, um proprietário de banco de dados tem todas as permissões no banco de dados e todas as permissões nos objetos no banco de dados. Essas permissões não podem ser alteradas.  
  
-   As permissões podem ser herdadas em vários níveis na hierarquia de membros da função de servidor.  
  
    Por exemplo, suponha que você tem a seguinte situação:  
  
    -   David de logon é um membro da função de banco de dados PerfAnalysts.  
  
    -   PerfAnalysts é um membro da função de banco de dados de produção.  
  
    -   David e PerfAnalysts não têm **selecione** permissão na tabela de cliente. A permissão foi revogada ou nunca explicitamente concedida.  
  
    -   Produção tem **selecione** permissão na tabela de cliente.  
  
    Nesse caso, PerfAnalysts herdará **GRANT** permissão na tabela de cliente de produção e David herdará **GRANT** permissão na tabela de cliente de produção.  
  
-   **Negar** substitui **GRANT** quando as permissões estão em conflito.  
  
    Por exemplo, suponha que o logon David não tem nenhuma permissão na tabela de cliente e é um membro de duas funções de banco de dados – dbgroup1, que tem **DENY** permissão na tabela Customer e dbgroup2, que tem **GRANT** permissão na tabela de cliente. Nesse caso, David herdará o **DENY** permissão na tabela de cliente. Esse é o caso se as funções obtido suas permissões implicitamente ou explicitamente.  
  
### <a name="auditing-permissions"></a>Permissões de auditoria  
Para pesquisar as permissões de um usuário verifique o seguinte.  
  
-   Execute a consulta a seguir para determinar quais logons são administradores do sistema.  
  
    ```sql  
    SELECT SPLogins.name, 'is a member of ', SPRoles.name   
    FROM sys.server_role_members AS SRM   
    JOIN sys.server_principals AS SPRoles   
        ON SRM.role_principal_id = SPRoles.principal_id   
    JOIN sys.server_principals AS SPLogins   
        ON SRM.member_principal_id = SPLogins.principal_id;  
    ```  
  
-   Execute a consulta a seguir para determinar quais logons foram concedidas permissões explícitas.  
  
    ```sql  
    SELECT name, 'has the ', state_desc , permission_name, ' permission'  
    FROM sys.server_permissions AS SP  
    JOIN sys.server_principals AS SPRoles   
        ON SP.grantee_principal_id = SPRoles.principal_id;  
    ```  
  
-   Execute a seguinte consulta em um banco de dados de usuário para determinar quais usuários de banco de dados são membros de uma função de banco de dados.  
  
    ```sql  
    SELECT DPUsers.name, 'is a member of ', DPRoles.name    
    FROM sys.database_role_members AS DRM  
    JOIN sys.database_principals AS DPRoles   
        ON DRM.role_principal_id = DPRoles.principal_id  
    JOIN sys.database_principals AS DPUsers  
        ON DRM.member_principal_id = DPUsers.principal_id;  
    ```  
  
-   Execute a seguinte consulta em um banco de dados de usuário para determinar quais usuários de banco de dados e funções tenham sido concedidas ou negadas permissões específicas. Você terá a exibições de consulta adicionais, como sys. Objects e schemas para identificar os itens descritos com o major_id.  
  
    ```sql  
    SELECT DPUsers.name, 'has the ', permission_name,   
    'permission on the item described as class = ', class, 'id = ', major_id  
    FROM sys.database_permissions AS DP  
    JOIN sys.database_principals AS DPUsers  
        ON DP.grantee_principal_id = DPUsers.principal_id;  
    ```  
  
## <a name="RestoreProc"></a>Práticas recomendadas de permissões de banco de dados  
  
-   Conceda permissões de nível mais granular que é prático. Conceder permissões a tabela ou as permissões de nível de exibição podem se tornar incontrolável. Mas conceder permissões no nível do banco de dados podem ser muito permissivas. Se o banco de dados é projetado com esquemas para definir os limites de trabalho, talvez a concessão de permissão para o esquema é um termo apropriado entre o nível de tabela e o nível de banco de dados.  
  
-   Conceder permissões a funções, em vez da usuários ou logons. O gerenciamento de direitos usando funções em vez de usuários facilita a rapidamente conceder ou revogar um conjunto de permissões para um usuário ou logon, movendo-os para dentro ou fora de função. Quando uma função passa de uma pessoa para outra, as permissões podem permanecer intactas no nível de função enquanto as alterações de associação de função.  
  
-   Conceder permissões a funções com base na função de trabalho e em funções do grupo de nível superior que combinam as funções de função de trabalho com base no grupo de empresa executando as ações.  
  
-   Cada usuário deve ter um logon único. Não permitir que os usuários compartilhem logons. Fornecer um logon para cada usuário garante uma trilha de auditoria e simplifica o gerenciamento de permissões.  
  
## <a name="fixed-database-roles"></a>Funções de banco de dados fixas
SQL Server fornece funções de nível de banco de dados (fixas) pré-configuradas para ajudá-lo a gerenciar as permissões em um servidor. As funções pré-configuradas corrigidas em que você não pode alterar as permissões atribuídas a eles. Funções de banco de dados definido pelo usuário também podem ser criadas. Você pode alterar as permissões atribuídas às funções de banco de dados definido pelo usuário.  
  
Funções são entidades de segurança que agrupam outras entidades. Funções de banco de dados são todo o banco de dados no escopo de suas permissões. Os usuários do banco de dados e outras funções de banco de dados podem ser adicionadas como membros das funções de banco de dados. As funções de banco de dados fixa não podem ser adicionadas ao outro. (As*funções* são como *grupos* no sistema operacional Windows.)  
  
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
  
### <a name="permissions-of-the-fixed-database-roles"></a>Permissões das funções fixas de banco de dados  
O sistema de funções de servidor fixas e funções fixas de banco de dados é um sistema de herdado seja proveniente de um a 1980's. Funções fixas ainda têm suporte e são úteis em ambientes em que há alguns usuários e às necessidades de segurança são simples. Começando com o SQL Server 2005, um sistema mais detalhado de concessão de permissão foi criado. Esse novo sistema é mais granular, fornecendo muito mais opções para conceder e negando permissões. A complexidade extra do sistema mais granular torna mais difícil saber mais, mas a maioria dos sistemas corporativos deve conceder permissões em vez de usar as funções fixas. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md). -->O gráfico a seguir mostra as permissões que estão associadas a cada função de banco de dados fixa. Todas as permissões neste gráfico do SQL Server não estão disponíveis (ou necessários) em APS.  
  
![Funções de banco de dados fixas da segurança APS](./media/pdw-permissions/APS_security_fixed_db_roles.png "APS_security_fixed_db_roles")  
  
### <a name="related-content"></a>Conteúdo relacionado  
  
-   Para criar funções definidas pelo usuário, consulte [Criar função](../t-sql/statements/create-role-transact-sql.md).  
  
  
## <a name="fixed-server-roles"></a>Funções de servidor fixas
Funções de servidor fixas são criadas automaticamente pelo SQL Server. SQL Server PDW tem uma implementação limitada de funções de servidor fixas do SQL Server. Somente o **sysadmin** e **pública** ter logons de usuário como membros. O **setupadmin** e **dbcreator** são usadas internamente pelo SQL Server PDW. Membros adicionais não podem ser adicionados ou removidos de qualquer função.  
  
### <a name="sysadmin-fixed-server-role"></a>sysadmin a função de servidor fixa  
Os membros da função de servidor fixa **sysadmin** podem executar qualquer atividade no servidor. O **sa** logon é o único membro a **sysadmin** função de servidor fixa. Logons adicionais não podem ser adicionados para o **sysadmin** função de servidor fixa. Conceder a permissão **CONTROL SERVER** aproxima-se da associação à função de servidor fixa **sysadmin**. O exemplo a seguir concede a **CONTROL SERVER** permissão a um logon denominado Fay.  
  
```sql  
USE master;  
GO  
GRANT CONTROL SERVER TO Fay;  
```  
  
> [!IMPORTANT]  
> O **CONTROL SERVER** permissão fornece um controle quase completo do SQL Server PDW. Sempre que possível, forneça permissões mais granulares para os logons em vez disso. Por exemplo, considere conceder a **VIEW SERVER STATE**, **ALTER ANY LOGIN**, **VIEW ANY DATABASE**, ou **CREATE ANY DATABASE** permissões.  
  
### <a name="public-server-role"></a>Função pública de servidor  
Todo logon pode se conectar ao SQL Server PDW é um membro do **pública** função de servidor. Todos os logons herdam as permissões concedidas ao **pública** em qualquer objeto. Somente atribua **pública** permissões em um objeto quando você deseja que o objeto esteja disponível para todos os usuários. Você não pode alterar a associação a **pública** função.  
  
> [!NOTE]  
> **público** é implementado Diferentemente de outras funções. Porque todos os objetos de servidor público, a associação do **pública** função não estiver listada no **server_role_members** DMV.  
  
### <a name="fixed-server-roles-vs-granting-permissions"></a>Vs de funções de servidor fixas. Concedendo permissões  
O sistema de funções de servidor fixas e funções fixas de banco de dados é um sistema de herdado seja proveniente de um a 1980's. Funções fixas ainda têm suporte e são úteis em ambientes em que há alguns usuários e às necessidades de segurança são simples. Começando com o SQL Server 2005, um sistema mais detalhado de concessão de permissão foi criado. Esse novo sistema é mais granular, fornecendo muito mais opções para conceder e negando permissões. A complexidade extra do sistema mais granular torna mais difícil saber mais, mas a maioria dos sistemas corporativos deve conceder permissões em vez de usar as funções fixas. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  -->  
  
## <a name="related-topics"></a>Tópicos relacionados  
  
- [Conceder permissões](grant-permissions.md)

<!-- MISSING LINKS
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->


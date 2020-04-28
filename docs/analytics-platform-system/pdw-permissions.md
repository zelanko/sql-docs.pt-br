---
title: Permissões
description: Este artigo descreve os requisitos e as opções para gerenciar permissões de banco de dados para data warehouse paralelas.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 499ac56d8a462f62dac92b97654a9ace12bd356e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "79289684"
---
# <a name="managing-permissions-in-parallel-data-warehouse"></a>Gerenciando permissões em paralelo data warehouse
Este artigo descreve os requisitos e as opções para gerenciar permissões de banco de dados para SQL Server PDW.

## <a name="database-engine-permission-basics"></a><a name="BackupRestoreBasics"></a>Noções básicas de permissão Mecanismo de Banco de Dados
Mecanismo de Banco de Dados permissões em SQL Server PDW são gerenciadas no nível do servidor por meio de logons e no nível do banco de dados por meio de usuários de banco de dados e funções de banco de dados definidas pelo usuário.

**Logons** Os logons são contas de usuário individuais para fazer logon no SQL Server PDW. O SQL Server PDW dá suporte a logons usando a autenticação do Windows e a autenticação do SQL Server.  Os logons de autenticação do Windows podem ser usuários do Windows ou grupos do Windows de qualquer domínio confiável pelo SQL Server PDW. SQL Server logons de autenticação são definidos e autenticados pelo SQL Server PDW e devem ser criados especificando uma senha.

Os membros da função de servidor fixa **sysadmin** (como o logon **SA** ) podem se conectar a um banco de dados sem ter sido mapeado para um usuário de banco de dados. Eles são mapeados para o usuário **dbo** . O proprietário do banco de dados também é mapeado como o usuário **dbo** .

**Funções de servidor** Há quatro funções de servidor especiais com um conjunto de funções pré-configuradas que fornecem um grupo conveniente de permissões de nível de servidor. As funções de servidor **sysadmin**, **MediumRC**, **LargeRC**e **XLargeRCfixed** são as únicas funções de servidor atualmente implementadas no SQL Server PDW. O logon **SA** é o único membro da função de servidor fixa **sysadmin** e logons adicionais não podem ser adicionados à função **sysadmin** . Os logons podem receber a permissão **Control Server** , que é semelhante, embora não seja idêntico, à função de servidor fixa **sysadmin** . Use [ALTER Server Role](../t-sql/statements/alter-server-role-transact-sql.md) para adicionar membros a outras funções de servidor. SQL Server PDW não oferece suporte a funções de servidor definidas pelo usuário.

**Usuários de banco de dados** Os logons recebem acesso a um banco de dados criando um usuário de banco de dados em um banco de dados e mapeando esse usuário de banco de dados para um logon. Normalmente, o nome de usuário do banco de dados é igual ao nome de logon, mas não precisa ser o mesmo. Cada usuário de banco de dados é mapeado para um logon único. Um logon pode ser mapeado para apenas um usuário em um banco de dados, mas pode ser mapeado como um usuário de banco de dados em vários bancos de dados diferentes.

**Funções de banco de dados fixas** As funções de banco de dados fixas são um conjunto de funções pré-configuradas que fornecem um grupo conveniente de permissões de nível de banco de dados. Os usuários de banco de dados e as funções de banco de dados definidas pelo usuário podem ser adicionados às funções de banco de dados fixas usando o procedimento [sp_addrolemember](../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) . Para obter mais informações sobre funções de banco de dados fixas, consulte [Fixed Database Roles](#fixed-database-roles).

**Funções de banco de dados definidas pelo usuário** Os usuários com a permissão **CREATE ROLE** podem criar novas funções de banco de dados definidas pelo usuário para representar grupos de usuários com permissões comuns. Normalmente, as permissões são concedidas ou negadas para toda a função, simplificando o gerenciamento e o monitoramento de permissões.

As permissões são concedidas a entidades de segurança (logons, usuários e funções) usando a instrução **Grant** . As permissões são explicitamente negadas usando o comando **Deny** . Uma permissão concedida ou negada anteriormente é removida usando a instrução **REVOKE** . As permissões são cumulativas, com o usuário recebendo todas as permissões concedidas ao usuário, logon e quaisquer associações de grupo; no entanto, qualquer negação de permissão substitui todas as concessões. <!-- MISSING LINKS (For information, syntax, and available permissions with these commands, see [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md)).  -->

Veja a seguir um exemplo que representa um método comum e recomendado de configuração de permissões.

1.  Se você estiver usando a autenticação do Windows, crie um logon para cada usuário do Windows ou grupo do Windows que se conectará ao SQL Server PDW. Se você estiver usando a autenticação SQL Server, crie um logon para cada pessoa que se conectará ao SQL Server PDW.

2.  Crie um usuário de banco de dados para cada logon em todos os bancos de dados necessários.

3.  Crie uma ou mais funções de banco de dados definidas pelo usuário, cada uma representando uma função semelhante. Por exemplo, analista financeiro e analista de vendas.

4.  Adicione usuários de banco de dados a uma ou mais funções de banco de dados definidas pelo usuário.

5.  Conceda permissões às funções de banco de dados definidas pelo usuário.

Os logons são objetos de nível de servidor e podem ser listados exibindo [Sys. server_principals](../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md). Somente permissões de nível de servidor podem ser concedidas a entidades de servidor.

Usuários e funções de banco de dados são objetos de nível de banco de dados e podem ser listados exibindo [Sys. database_principals](../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md). Somente permissões de nível de banco de dados podem ser concedidas a entidades de banco de dados.

## <a name="default-permissions"></a><a name="BackupTypes"></a>Permissões padrão
A lista a seguir descreve as permissões padrão:

-   Quando um logon é criado usando a instrução **Create login** , o logon recebe a permissão **Connect SQL** , permitindo que o logon se conecte ao SQL Server PDW.

-   Quando um usuário de banco de dados é criado usando a instrução **Create User** , o usuário recebe a permissão **conectar no banco de dados::** _<database_name>_ , permitindo que o logon se conecte a esse banco de dados como um usuário.

-   Todas as entidades de segurança, incluindo a função pública, não têm permissões explícitas ou implícitas por padrão porque as permissões implícitas são herdadas de permissões explícitas. Portanto, quando não houver permissões explícitas, também poderá não haver Permissões implícitas.

-   Quando um logon se torna o proprietário de um objeto ou banco de dados, o logon sempre tem todas as permissões no objeto ou banco de dados. As permissões de propriedade não são visíveis como permissões explícitas. As instruções **Grant**, **REVOKE**e **Deny** não têm efeito sobre as permissões de propriedade. A propriedade pode ser alterada usando a instrução [ALTER AUTHORIZATION](../t-sql/statements/alter-authorization-transact-sql.md) .

-   O logon sa tem todas as permissões no dispositivo. Semelhante às permissões de propriedade, as permissões de sa não podem ser alteradas e não são visíveis como as permissões explícitas. As instruções **Grant**, **REVOKE**e **Deny** não têm efeito sobre as permissões SA.

-   A função de servidor público não recebe permissões por padrão e não herda permissões de outras funções de servidor. A função de servidor público pode receber permissões explícitas com as instruções **Grant**, **REVOKE**e **Deny** .

-   As transações não exigem permissões. Todas as entidades de segurança podem executar os comandos **BEGIN TRANSACTION**, **Commit**e **Rollback** Transaction. No entanto, uma entidade de segurança deve ter as permissões apropriadas para executar cada instrução dentro da transação.

-   A instrução **USE** não requer permissões. Todas as entidades de segurança podem executar a instrução **use** em qualquer banco de dados, no entanto, para acessar um banco de dados, eles devem ter uma entidade de usuário no banco de dados ou o usuário convidado deve estar habilitado.

### <a name="the-public-role"></a>A função pública
Todos os novos logons de dispositivo pertencem automaticamente à função pública. A função de servidor público tem as seguintes características:

-   A função de servidor público não tem permissões por padrão.

-   Todas as entidades são membros da função de servidor público e a função de servidor público não é membro de outra função de servidor.

-   A função de servidor público não pode herdar Permissões implícitas. Todas as permissões fornecidas para a função pública devem ser concedidas explicitamente.

## <a name="determining-permissions"></a><a name="BackupProc"></a>Determinando permissões
Se um logon ou não tem permissão para executar uma ação específica depende das permissões concedidas ou negadas ao logon, ao usuário e às funções das quais o usuário é membro. As permissões de nível de servidor (como **criar logon** e **Exibir estado do servidor**) estão disponíveis para entidades de segurança no nível do servidor (logons). As permissões em nível de banco de dados (como **selecionar** de uma tabela ou **executar** em um procedimento) estão disponíveis para entidades de segurança no nível do banco de dados (usuários e funções de banco de dados).

### <a name="implicit-and-explicit-permissions"></a>Permissões implícitas e explícitas
Uma *permissão explícita* é uma permissão **GRANT** ou **DENY** concedida a uma entidade de segurança por uma instrução **GRANT** ou **DENY**. As permissões de nível de banco de dados são listadas na exibição [Sys. database_permissions](../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md) . As permissões de nível de servidor são listadas na exibição [Sys. server_permissions](../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md) .

Uma *permissão implícita* é uma permissão **Grant** ou **Deny** que uma entidade de segurança (função de logon ou de servidor) herdou. Uma permissão pode ser herdada das seguintes maneiras.

-   Uma entidade de segurança pode herdar uma permissão de uma função se a entidade de segurança for membro da função, mesmo se a entidade não tiver uma permissão **Grant** ou **Deny** explícita.

-   Uma entidade de segurança pode herdar uma permissão em um objeto subordinado (como uma tabela) se a entidade de segurança tiver uma permissão em um dos escopos pai dos objetos (como o esquema da tabela ou a permissão no banco de dados inteiro).

-   Uma entidade de segurança pode herdar uma permissão com uma permissão que inclui uma permissão subordinada. Por exemplo, a permissão **ALTER ANY User** inclui as permissões **Create User** e **ALTER on User::** _<name>_ .

### <a name="determining-permissions-when-performing-actions"></a>Determinando permissões ao executar ações
O processo de determinar qual permissão atribuir a uma entidade de segurança é complexo. A complexidade ocorre ao determinar permissões implícitas porque as entidades podem ser membros de várias funções e as permissões podem ser passadas por vários níveis na hierarquia de função.

A lista a seguir descreve as regras gerais para determinar as permissões:

-   A propriedade implica permissão.

    Um proprietário de objeto tem todas as permissões no objeto. Da mesma forma, um proprietário de banco de dados tem todas as permissões no banco de dados e todas as permissões nos objetos no banco de dados. Essas permissões não podem ser alteradas.

-   As permissões podem ser herdadas em vários níveis na hierarquia de associações de função de servidor.

    Por exemplo, suponha que você tenha a seguinte situação:

    -   O logon David é um membro da função de banco de dados PerfAnalysts.

    -   PerfAnalysts é um membro da produção da função de banco de dados.

    -   David e PerfAnalysts não têm permissão **Select** na tabela Customer. A permissão foi revogada ou nunca foi concedida explicitamente.

    -   A produção tem a permissão **Select** na tabela Customer.

    Nesse caso, o PerfAnalysts herdará a permissão **Grant** na tabela Customer da produção e David herdará a permissão **Grant** na tabela Customer da produção.

-   **Deny** substitui a **concessão** quando as permissões entram em conflito.

    Por exemplo, suponha que o logon David não tenha permissões na tabela Customer e seja membro de duas funções de banco de dados – dbgroup1, que tem a permissão **Deny** na tabela Customer e dbgroup2, que tem a permissão **Grant** na tabela Customer. Nesse caso, David herdará a permissão **Deny** na tabela Customer. Esse é o caso se as funções obtiverem suas permissões explícita ou implicitamente.

### <a name="auditing-permissions"></a>Permissões de auditoria
Para pesquisar as permissões de um usuário, verifique o seguinte.

-   Execute a consulta a seguir para determinar quais logons são administradores do sistema.

    ```sql
    SELECT SPLogins.name, 'is a member of ', SPRoles.name 
    FROM sys.server_role_members AS SRM 
    JOIN sys.server_principals AS SPRoles 
        ON SRM.role_principal_id = SPRoles.principal_id 
    JOIN sys.server_principals AS SPLogins 
        ON SRM.member_principal_id = SPLogins.principal_id;
    ```

-   Execute a consulta a seguir para determinar quais logons receberam permissões explícitas.

    ```sql
    SELECT name, 'has the ', state_desc , permission_name, ' permission'
    FROM sys.server_permissions AS SP
    JOIN sys.server_principals AS SPRoles 
        ON SP.grantee_principal_id = SPRoles.principal_id;
    ```

-   Execute a consulta a seguir em um banco de dados de usuário para determinar quais usuários de banco de dados são membros de uma função de banco de dados.

    ```sql
    SELECT DPUsers.name, 'is a member of ', DPRoles.name  
    FROM sys.database_role_members AS DRM
    JOIN sys.database_principals AS DPRoles 
        ON DRM.role_principal_id = DPRoles.principal_id
    JOIN sys.database_principals AS DPUsers
        ON DRM.member_principal_id = DPUsers.principal_id;
    ```

-   Execute a consulta a seguir em um banco de dados de usuário para determinar quais usuários e funções de banco de dados foram concedidos ou negadas permissões específicas. Você precisará consultar modos de exibição adicionais, como sys. Objects e sys. schemas, para identificar os itens descritos com o major_id.

    ```sql
    SELECT DPUsers.name, 'has the ', permission_name, 
    'permission on the item described as class = ', class, 'id = ', major_id
    FROM sys.database_permissions AS DP
    JOIN sys.database_principals AS DPUsers
        ON DP.grantee_principal_id = DPUsers.principal_id;
    ```

## <a name="database-permissions-best-practices"></a><a name="RestoreProc"></a>Práticas recomendadas de permissões de banco de dados

-   Conceda permissões no nível mais granular que seja prático. A concessão de permissões nas permissões de tabela ou de nível de exibição pode se tornar não gerenciável. Mas a concessão de permissões no nível do banco de dados pode ser muito permissiva. Se o banco de dados for projetado com esquemas para definir limites de trabalho, talvez a concessão de permissão para o esquema seja um comprometimento apropriado entre o nível de tabela e o nível de banco de dados.

-   Conceda permissões a funções, em vez de a usuários ou logons. O gerenciamento de direitos usando funções em vez de usuários facilita a concessão ou revogação rápida de um conjunto de permissões para um usuário ou logon movendo-os para dentro ou para fora da função. Quando uma função passa de uma pessoa para outra, as permissões podem permanecer intactas no nível de função enquanto a associação de função é alterada.

-   Conceda permissões a funções com base na função de trabalho e em funções de grupo de nível superior que combinam as funções de função de trabalho com base no grupo da empresa que executa as ações.

-   Todo usuário final deve ter um logon exclusivo. Não permitir que os usuários compartilhem logons. Fornecer um logon para cada usuário garante uma trilha de auditoria e simplifica o gerenciamento de permissões.

## <a name="fixed-database-roles"></a>Funções de banco de dados fixas
O SQL Server fornece funções de nível de banco de dados pré-configuradas (fixas) para ajudá-lo a gerenciar as permissões em um servidor. As funções pré-configuradas são corrigidas, pois você não pode alterar as permissões atribuídas a elas. As funções de banco de dados definidas pelo usuário também podem ser criadas. Você pode alterar as permissões atribuídas a funções de banco de dados definidas pelo usuário.

As funções são entidades de segurança que agrupam outras entidades. As funções de banco de dados são de todo o banco de dados em seu escopo de permissões. Usuários de banco de dados e outras funções de banco de dados podem ser adicionados como membros de funções de banco de dados. As funções de banco de dados fixas não podem ser adicionadas umas às outras. (As*funções* são como *grupos* no sistema operacional Windows.)

Há 9 funções de banco de dados fixas.

-   **db_owner**

-   **db_securityadmin**

-   **db_accessadmin**

-   **db_backupoperator**

-   **db_ddladmin**

-   **db_datawriter**

-   **db_datareader**

-   **db_denydatawriter**

-   **db_denydatareader**

### <a name="permissions-of-the-fixed-database-roles"></a>Permissões das funções de banco de dados fixas
O sistema de funções de servidor fixas e de funções de banco de dados fixas é um sistema herdado originado no de 1980. As funções fixas ainda têm suporte e são úteis em ambientes em que há poucos usuários e as necessidades de segurança são simples. A partir do SQL Server 2005, um sistema mais detalhado de concessão de permissão foi criado. Esse novo sistema é mais granular, fornecendo muitas outras opções para conceder e negar permissões. A complexidade extra do sistema mais granular dificulta o aprendizado, mas a maioria dos sistemas empresariais deve conceder permissões em vez de usar as funções fixas. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md). -->O gráfico a seguir mostra as permissões associadas a cada função de banco de dados fixa. Todas as permissões neste gráfico de SQL Server não estão disponíveis (ou são necessárias) no APS.

![Funções de banco de dados fixas da segurança de APS](./media/pdw-permissions/APS_security_fixed_db_roles.png "APS_security_fixed_db_roles")

### <a name="related-content"></a>Conteúdo relacionado

-   Para criar funções definidas pelo usuário, consulte [criar função](../t-sql/statements/create-role-transact-sql.md).


## <a name="fixed-server-roles"></a>Funções de servidor fixas
As funções de servidor fixas são criadas automaticamente pelo SQL Server. SQL Server PDW tem uma implementação limitada de SQL Server funções de servidor fixas. Somente o **sysadmin** e o **público** têm logons de usuário como membros. As funções **setupadmin** e **dbcreator** são usadas internamente pelo SQL Server PDW. Membros adicionais não podem ser adicionados ou removidos de nenhuma função.

### <a name="sysadmin-fixed-server-role"></a>Função de servidor fixa sysadmin
Os membros da função de servidor fixa **sysadmin** podem executar qualquer atividade no servidor. O logon **SA** é o único membro da função de servidor fixa **sysadmin** . Logons adicionais não podem ser adicionados à função de servidor fixa **sysadmin** . Conceder a permissão **CONTROL SERVER** aproxima-se da associação à função de servidor fixa **sysadmin**. O exemplo a seguir concede a permissão **Control Server** a um logon chamado Fay.

```sql
USE master;
GO
GRANT CONTROL SERVER TO Fay;
```

> [!IMPORTANT]
> A permissão **Control Server** fornece controle quase total de SQL Server PDW. Sempre que possível, forneça permissões mais granulares para logons em vez disso. Por exemplo, considere a concessão das permissões **Exibir estado do servidor**, **alterar qualquer logon**, **exibir qualquer banco de dados**ou **criar qualquer banco de dados** .

### <a name="public-server-role"></a>Função de servidor público
Cada logon que pode se conectar a SQL Server PDW é um membro da função de servidor **público** . Todos os logons herdam as permissões concedidas a **Public** em qualquer objeto. Atribua somente permissões **públicas** em um objeto quando desejar que o objeto esteja disponível para todos os usuários. Você não pode alterar a associação na função **pública** .

> [!NOTE]
> o **público** é implementado de forma diferente de outras funções. Como todas as entidades de segurança do servidor são membros do público, a associação da função **pública** não está listada na DMV **Sys. server_role_members** .

### <a name="fixed-server-roles-vs-granting-permissions"></a>Funções de servidor fixas vs. concedendo permissões
O sistema de funções de servidor fixas e de funções de banco de dados fixas é um sistema herdado originado no de 1980. As funções fixas ainda têm suporte e são úteis em ambientes em que há poucos usuários e as necessidades de segurança são simples. A partir do SQL Server 2005, um sistema mais detalhado de concessão de permissão foi criado. Esse novo sistema é mais granular, fornecendo muitas outras opções para conceder e negar permissões. A complexidade extra do sistema mais granular dificulta o aprendizado, mas a maioria dos sistemas empresariais deve conceder permissões em vez de usar as funções fixas. <!-- MISSING LINKS The permissions are discussed and listed in the topic [Permissions: GRANT, DENY, REVOKE &#40;SQL Server PDW&#41;](../sqlpdw/permissions-grant-deny-revoke-sql-server-pdw.md).  -->

## <a name="related-topics"></a>Tópicos relacionados

- [Conceder permissões](grant-permissions.md)

<!-- MISSING LINKS
## See Also
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)
-->


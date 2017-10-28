---
title: "Guia de Introdução às permissões do mecanismo de banco de dados | Microsoft Docs"
ms.custom: 
ms.date: 01/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: get-started-article
helpviewer_keywords:
- permissions [SQL Server], getting started
ms.assetid: 051af34e-bb5b-403e-bd33-007dc02eef7b
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 01f20dd99963b0bb1be86ddc3e173aef6fb3e8b3
ms.openlocfilehash: 376e591e28bbdddbd635392b24c3d6652f3bd94d
ms.contentlocale: pt-br
ms.lasthandoff: 08/11/2017

---
# <a name="getting-started-with-database-engine-permissions"></a>Guia de Introdução às permissões do mecanismo de banco de dados
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../../includes/tsql-appliesto-ss2008-all-md.md)]

  As permissões no [!INCLUDE[ssDE](../../../includes/ssde-md.md)] são gerenciadas no nível do servidor por meio de funções de logon e de servidor, e no nível do banco de dados por meio de funções de usuários do banco de dados e funções de banco de dados. O modelo para o [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] expõe o mesmo sistema dentro de cada banco de dados, mas as permissões no nível do servidor não estão disponíveis. Este tópico examina alguns conceitos básicos de segurança e descreve uma implementação comum das permissões.  
  
## <a name="security-principals"></a>Entidades de segurança  
 Entidade de segurança é o nome oficial das identidades que usam o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e que podem receber uma permissão para executar ações. Geralmente são pessoas ou grupos de pessoas, mas podem ser outras entidades que fingem ser pessoas. As entidades de segurança podem ser criadas e gerenciadas usando os [!INCLUDE[tsql](../../../includes/tsql-md.md)] listados, ou usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
 Logons  
 Logons são contas de usuário individuais para entrada no [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] oferecem suporte a logons com base na autenticação do Windows e a logons com base na autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para saber mais sobre os dois tipos de logons, confira [Choose an Authentication Mode](../../../relational-databases/security/choose-an-authentication-mode.md).  
  
 Funções de servidor fixas  
 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], as funções de servidor fixas são um conjunto de funções pré-configuradas que fornecem um agrupamento conveniente de permissões no nível do servidor. Os logons podem ser adicionados às funções usando a instrução `ALTER SERVER ROLE ... ADD MEMBER` . Para mais informações, consulte [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-role-transact-sql.md). [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] não dá suporte a funções de servidor fixas, mas tem duas funções no banco de dados mestre (`dbmanager` e `loginmanager`) que atuam como funções de servidor.  
  
 Funções de servidor definidas pelo usuário  
 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], você pode criar suas próprias funções de servidor e atribuir a elas permissões no nível do servidor. Os logons podem ser adicionados às funções de servidor usando a instrução `ALTER SERVER ROLE ... ADD MEMBER` . Para mais informações, consulte [ALTER SERVER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-role-transact-sql.md). [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] não dá suporte às funções de servidor definidas pelo usuário.  
  
 Usuários de banco de dados  
 Os logons recebem acesso a um banco de dados por meio da criação de um usuário de banco de dados em um banco de dados, e por meio do mapeamento desse usuário de banco de dados para o logon. Normalmente, o nome de usuário do banco de dados é igual ao nome de logon, mas não precisa ser o mesmo. Cada usuário de banco de dados é mapeado para um logon único. Um logon pode ser mapeado para apenas um usuário em um banco de dados, mas pode ser mapeado como um usuário de banco de dados em vários bancos de dados diferentes.  
  
 Os usuários de banco de dados também podem ser criados em um logon correspondente. Eles são chamados de *usuários de banco de dados independente*. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] incentiva o uso de usuários de banco de dados independente, pois isso facilita a movimentação do banco de dados para um servidor diferente. Como um logon, um usuário de banco de dados independente pode usar a autenticação do Windows ou a autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Usuários de bancos de dados independentes – Tornando seu banco de dados portátil](../../../relational-databases/security/contained-database-users-making-your-database-portable.md).  
  
 Há 12 tipos de usuários com pequenas diferenças no modo como são autenticados e quem eles representam. Para ver uma lista de usuários, consulte [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md).  
  
 Funções de banco de dados fixas  
 As funções de banco de dados fixas são um conjunto de funções pré-configuradas que fornecem um agrupamento conveniente de permissões no nível do banco de dados. Os usuários de banco de dados e funções de banco de dados definidas pelo usuário podem ser adicionadas às funções de banco de dados fixas usando a instrução `ALTER ROLE ... ADD MEMBER`. Para obter mais informações, veja [ALTER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-role-transact-sql.md).  
  
 Funções de banco de dados definidas pelo usuário  
 Usuários com a permissão `CREATE ROLE` podem criar novas funções de banco de dados definidas pelo usuário para representar grupos de usuários com permissões comuns. Normalmente, as permissões são concedidas ou negadas para toda a função, simplificando o gerenciamento e o monitoramento de permissões. É possível adicionar usuários de banco de dados às funções de banco de dados usando a instrução `ALTER ROLE ... ADD MEMBER` . Para obter mais informações, veja [ALTER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-role-transact-sql.md).  
  
 Outras entidades  
 Entre as outras entidades de segurança que não são discutidas aqui estão as funções de aplicativo, logons e usuários baseados em certificados ou chaves assimétricas.  
  
 Para ver um gráfico mostrando as relações entre usuários do Windows, grupos do Windows, logons e usuários de banco de dados, confira [Create a Database User](../../../relational-databases/security/authentication-access/create-a-database-user.md).  
  
## <a name="typical-scenario"></a>Cenário típico  
 Veja a seguir um exemplo que representa um método comum e recomendado de configuração de permissões.  
  
#### <a name="in-active-directory-or-azure-active-directory"></a>No Active Directory ou no Azure Active Directory:  
  
1.  Crie um usuário do Windows para cada pessoa.  
  
2.  Crie grupos do Windows que representam as unidades de trabalho e as funções de trabalho.  
  
3.  Adicione usuários do Windows aos grupos do Windows.  
  
#### <a name="if-the-person-connecting-will-be-connecting-to-many-databases"></a>Se a pessoa que está se conectando for se conectar a muitos bancos de dados  
  
1.  Crie um logon para os grupos do Windows. (Se você estiver usando a autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , ignore as etapas do Active Directory e crie os logons de autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aqui.)  
  
2.  No banco de dados de usuário, crie um usuário de banco de dados para o logon que representa os grupos do Windows.  
  
3.  No banco de dados de usuário, crie uma ou mais funções de banco de dados definidas pelo usuário, cada uma representando uma função semelhante. Por exemplo, analista financeiro e analista de vendas.  
  
4.  Adicione os usuários do banco de dados a uma ou mais funções de banco de dados definidas pelo usuário.  
  
5.  Conceda permissões às funções de banco de dados definidas pelo usuário.  
  
#### <a name="if-the-person-connecting-will-be-connecting-to-only-one-database"></a>Se a pessoa que está se conectando for se conectar a apenas um bancos de dados  
  
1.  Crie um logon para os grupos do Windows. (Se você estiver usando a autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , ignore as etapas do Active Directory e crie os logons de autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aqui.)  
  
2.  No banco de dados de usuário, crie um usuário de banco de dados independente para o grupo do Windows. (Se você estiver usando a autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , ignore as etapas do Active Directory e crie a autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do usuário de banco de dados independente aqui.  
  
3.  No banco de dados de usuário, crie uma ou mais funções de banco de dados definidas pelo usuário, cada uma representando uma função semelhante. Por exemplo, analista financeiro e analista de vendas.  
  
4.  Adicione os usuários do banco de dados a uma ou mais funções de banco de dados definidas pelo usuário.  
  
5.  Conceda permissões às funções de banco de dados definidas pelo usuário.  
  
 O resultado mais comum neste ponto é um usuário do Windows membro de um grupo do Windows. O grupo do Windows tem um logon no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou no [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]. O logon é mapeado para uma identidade de usuário no banco de dados do usuário. O usuário é membro de uma função de banco de dados. Agora, você precisa adicionar permissões à função.  
  
## <a name="assigning-permissions"></a>Atribuição de permissões  
 A maioria das instruções de permissão tem o formato:  
  
```  
AUTHORIZATION  PERMISSION  ON  SECURABLE::NAME  TO  PRINCIPAL;  
```  
  
-   `AUTHORIZATION` deve ser `GRANT`, `REVOKE` ou `DENY`.  
  
-   O `PERMISSION` estabelece qual ação é permitida ou proibida. [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] pode especificar 230 permissões. [!INCLUDE[ssSDS](../../../includes/sssds-md.md)] tem menos permissões, pois algumas ações não são relevantes no Azure. As permissões são listadas no tópico [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../../relational-databases/security/permissions-database-engine.md) e no gráfico referenciado abaixo.  
  
-   `ON SECURABLE::NAME` é o tipo de item protegível (servidor, objeto de servidor, banco de dados ou objeto de banco de dados) e seu nome. Algumas permissões não exigem `ON SECURABLE::NAME` , pois ele não é ambíguo ou inadequado ao contexto. Por exemplo, a permissão `CREATE TABLE` não exige a cláusula `ON SECURABLE::NAME` . (Por exemplo, `GRANT CREATE TABLE TO Mary;` permite que a Maria crie tabelas.)  
  
-   `PRINCIPAL` é a entidade de segurança (logon, usuário ou função) que recebe ou perde a permissão. Conceda permissões às funções sempre que possível.  
  
 O exemplo de instrução de concessão a seguir concede a permissão `UPDATE` na tabela ou modo de exibição `Parts` contido no esquema `Production` à função chamada `PartsTeam`:  
  
```  
GRANT UPDATE ON OBJECT::Production.Parts TO PartsTeam;  
```  
  
 As permissões são concedidas a entidades de segurança (logons, usuários e funções) usando a instrução `GRANT` . As permissões são explicitamente negadas usando o comando  `DENY` . Um permissão concedida ou negada anteriormente é removida usando a instrução `REVOKE` . As permissões são cumulativas, com o usuário recebendo todas as permissões concedidas ao usuário, logon e quaisquer associações de grupo; no entanto, qualquer negação de permissão substitui todas as concessões.  
  
> [!TIP]  
>  Um erro comum é tentar remover um `GRANT` usando `DENY` em vez de `REVOKE`. Isso pode causar problemas quando um usuário recebe permissões de várias fontes, o que é bastante comum. O exemplo a seguir demonstra a entidade.  
  
 O grupo de Vendas recebe as permissões `SELECT` na tabela OrderStatus por meio da instrução `GRANT SELECT ON OBJECT::OrderStatus TO Sales;`. O usuário Ted é membro da função Vendas. Ted também recebeu a permissão `SELECT` para a tabela OrderStatus em seu próprio nome de usuário por meio da instrução  `GRANT SELECT ON OBJECT::OrderStatus TO Ted;`. Vamos supor que o administrador deseja remover `GRANT` da função Vendas.  
  
-   Se o administrador executar corretamente `REVOKE SELECT ON OBJECT::OrderStatus TO Sales;`, Ted manterá o acesso `SELECT` à tabela OrderStatus por meio de sua instrução `GRANT` individual.  
  
-   Se o administrador executar incorretamente `DENY SELECT ON OBJECT::OrderStatus TO Sales;` , Ted, como um membro da função Vendas, terá a permissão `SELECT` negada, pois `DENY` para Vendas substitui essa  `GRANT`individual.  
  
> [!NOTE]  
>  As permissões podem ser configuradas usando [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]. Encontre o item protegível no Pesquisador de Objetos, clique nele com o botão direito do mouse e clique em **Propriedades**. Selecione a página **Permissões** . Para obter ajuda sobre como usar a página de permissão, confira [Permissions or Securables Page](../../../relational-databases/security/permissions-or-securables-page.md).  
  
## <a name="permission-hierarchy"></a>Hierarquia de permissões  
 Permissões têm uma hierarquia de pai/filho. Ou seja, se você conceder a permissão `SELECT` em um banco de dados, essa permissão incluirá a permissão `SELECT` em todos os esquemas (filho) no banco de dados. Se você conceder a permissão `SELECT` em um esquema, ela incluirá a permissão `SELECT` em todas as tabelas (filho) e modos de exibição no esquema. As permissões são transitivas, ou seja, se você conceder a permissão `SELECT` em um banco de dados, ele incluirá a permissão `SELECT` em todos os esquemas (filho) e em todos os modos de exibição e tabelas (netos).  
  
 As permissões também têm permissões de cobertura. A permissão `CONTROL` em um objeto, normalmente fornece a você todas as outras permissões no objeto.  
  
 Como a hierarquia de pai/filho e a hierarquia de cobertura podem agir na mesma permissão, o sistema de permissões pode ficar complicado. Por exemplo, vamos usar uma tabela (Região) em um esquema (Clientes) em um banco de dados (SalesDB).  
  
-   `CONTROL` na tabela Região inclui todas as outras permissões na tabela Região, incluindo `ALTER`, `SELECT`, `INSERT`,  `UPDATE`, `DELETE`e algumas outras permissões.  
  
-   `SELECT` no esquema Clientes que possui a tabela Região inclui a permissão `SELECT` na tabela Região.  
  
 Então, a permissão `SELECT` na tabela Região pode ser obtida por meio de qualquer uma das seis instruções a seguir:  
  
```  
GRANT SELECT ON OBJECT::Region TO Ted;   
  
GRANT CONTROL ON OBJECT::Region TO Ted;   
  
GRANT SELECT ON SCHEMA::Customers TO Ted;   
  
GRANT CONTROL ON SCHEMA::Customers TO Ted;   
  
GRANT SELECT ON DATABASE::SalesDB TO Ted;   
  
GRANT CONTROL ON DATABASE::SalesDB TO Ted;  
```  
  
## <a name="grant-the-least-permission"></a>Concessão da permissão mínima  
 A primeira permissão listada acima (`GRANT SELECT ON OBJECT::Region TO Ted;`) é a mais granular, ou seja, essa instrução é a permissão mínima possível que concede a `SELECT`. Nenhuma permissão para subordinar objetos vem com ela. É um bom princípio conceder sempre a permissão mínima possível, mas (contradizendo isso) conceda em níveis mais altos para simplificar o sistema a concessão. Então, se o Ted precisar de permissões para o esquema inteiro, conceda `SELECT` uma vez no nível do esquema, em vez de conceder `SELECT` várias vezes no nível da tabela ou do modo de exibição. O design do banco de dados afeta bastante o quão bem-sucedida essa estratégia pode ser. Essa estratégia funcionará melhor quando o banco de dados for projetado de modo que os objetos que precisam de permissões idênticas forem incluídos em um único esquema.  
  
## <a name="list-of-permissions"></a>Lista de permissões  
 [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] tem 230 permissões. [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] tem 219 permissões. [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] tem 214 permissões. [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] tem 195 permissões. [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], [!INCLUDE[ssDW](../../../includes/ssdw-md.md)]e [!INCLUDE[ssAPS](../../../includes/ssaps-md.md)] têm menos permissões, pois expõem apenas uma parte do mecanismo de banco de dados, mas cada um tem algumas permissões que não se aplicam a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O gráfico a seguir mostra as permissões e as relações entre elas. Algumas das permissões de nível superior (como `CONTROL SERVER`) são listadas várias vezes. Neste tópico, o cartaz é pequeno demais para ser lido. Clique na imagem para baixar o **Cartaz de permissões do Mecanismo de Banco de Dados** no formato pdf.  
  
[![Permissões do Mecanismo de Banco de Dados](../../../relational-databases/security/media/database-engine-permissions.PNG)](http://go.microsoft.com/fwlink/?LinkId=229142)
 
 Para conferir um gráfico mostrando as relações entre as entidades de segurança [!INCLUDE[ssDE](../../../includes/ssde-md.md)] e o servidor e os objetos de banco de dados, consulte [Hierarquia de permissões &#40;Mecanismo de Banco de Dados&#41;](../../../relational-databases/security/permissions-hierarchy-database-engine.md).  
  
## <a name="permissions-vs-fixed-server-and-fixed-database-roles"></a>Permissões versus Funções fixas de banco de dados e de servidor  
 As permissões das funções fixas de servidor e de banco de dados são semelhantes, mas não são exatamente as mesmas que as permissões granulares. Por exemplo, membros da função de servidor fixa `sysadmin` têm todas as permissões na instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], assim como os logons com a permissão `CONTROL SERVER` . Mas a concessão da permissão `CONTROL SERVER` não torna um logon membro da função de servidor fixa sysadmin e a adição de um logon à função de servidor fixa `sysadmin` não concede explicitamente ao logon a permissão `CONTROL SERVER`. Às vezes, um procedimento armazenado verificará as permissões consultando a função fixa e não verificando a permissão granular. Por exemplo, desanexar um banco de dados exige a associação à função de banco de dados fixa `db_owner` . A permissão `CONTROL DATABASE` equivalente não é suficiente. Esses dois sistemas operam em paralelo, mas raramente interagem entre si. A Microsoft recomenda, sempre que possível, o uso do sistema de permissão granular mais recente em vez das funções fixas.
  
## <a name="monitoring-permissions"></a>Permissões de monitoramento  
 Os modos de exibição a seguir retornam informações de segurança.  
  
-   Os logons e funções de servidor definidas pelo usuário em um servidor podem ser examinadas usando o modo de exibição `sys.server_principals` . Esse modo de exibição não está disponível em [!INCLUDE[ssSDS](../../../includes/sssds-md.md)].  
  
-   Os usuários e funções definidas pelo usuário em um banco de dados podem ser examinadas usando o modo de exibição `sys.database_principals` .  
  
-   As permissões concedidas para logons e funções de servidor fixas definidas pelo usuário podem ser examinadas usando o modo de exibição `sys.server_permissions` . Esse modo de exibição não está disponível em [!INCLUDE[ssSDS](../../../includes/sssds-md.md)].  
  
-   As permissões concedidas para usuários e funções de banco de dados fixas definidas pelo usuário podem ser examinadas usando o modo de exibição `sys.database_permissions` .  
  
-   A associação à função de banco de dados pode ser examinada usando o modo de exibição `sys. sys.database_role_members` .  
  
-   A associação à função de servidor pode ser examinada usando o modo de exibição `sys.server_role_members` . Esse modo de exibição não está disponível em [!INCLUDE[ssSDS](../../../includes/sssds-md.md)].  
  
-   Para exibições relacionadas à segurança adicional, consulte [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md) .  
  
### <a name="useful-transact-sql-statements"></a>Instruções Transact-SQL úteis  
 As instruções a seguir retornam informações úteis sobre as permissões.  
  
 Para retornar as permissões explícitas concedidas ou negadas em um banco de dados ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]), execute a seguinte instrução no banco de dados.  
  
```tsql  
SELECT   
    perms.state_desc AS State,   
    permission_name AS [Permission],   
    obj.name AS [on Object],   
    dPrinc.name AS [to User Name]  
FROM sys.database_permissions AS perms  
JOIN sys.database_principals AS dPrinc  
    ON perms.grantee_principal_id = dPrinc.principal_id  
JOIN sys.objects AS obj  
    ON perms.major_id = obj.object_id;  
```  
  
 Para retornar os membros das funções de servidor (apenas[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ), execute a seguinte instrução.  
  
```tsql  
SELECT sRole.name AS [Server Role Name] , sPrinc.name AS [Members]  
FROM sys.server_role_members AS sRo  
JOIN sys.server_principals AS sPrinc  
    ON sRo.member_principal_id = sPrinc.principal_id  
JOIN sys.server_principals AS sRole  
    ON sRo.role_principal_id = sRole.principal_id;  
```  
  
 
 Para retornar os membros das funções de banco de dados ([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDS](../../../includes/sssds-md.md)]), execute a seguinte instrução no banco de dados.  
  
```tsql  
SELECT dRole.name AS [Database Role Name], dPrinc.name AS [Members]  
FROM sys.database_role_members AS dRo  
JOIN sys.database_principals AS dPrinc  
    ON dRo.member_principal_id = dPrinc.principal_id  
JOIN sys.database_principals AS dRole  
    ON dRo.role_principal_id = dRole.principal_id;  
```  
  
## <a name="next-steps"></a>Próximas etapas  
 Para conferir mais tópicos introdutórios, consulte:  
  
-   [Tutorial: introdução ao Mecanismo de Banco de Dados](../../../relational-databases/tutorial-getting-started-with-the-database-engine.md) [Criando um banco de dados &#40;Tutorial&#41;](../../../t-sql/lesson-1-1-creating-a-database.md)  
  
-   [Tutorial: SQL Server Management Studio](../../../tools/sql-server-management-studio/tutorial-sql-server-management-studio.md)  
  
-   [Tutorial: Gravando instruções Transact-SQL](../../../t-sql/tutorial-writing-transact-sql-statements.md)  
  
## <a name="see-also"></a>Consulte também  
 [Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](../../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)   
 [Funções de segurança &#40;Transact-SQL&#41;](../../../t-sql/functions/security-functions-transact-sql.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à segurança &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Exibições de catálogo de segurança &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql.md)   
 [Determinando permissões eficientes do Mecanismo de Banco de Dados](../../../relational-databases/security/authentication-access/determining-effective-database-engine-permissions.md)
  
  


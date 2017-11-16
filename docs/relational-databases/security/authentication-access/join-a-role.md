---
title: "Unir uma função | Microsoft Docs"
ms.custom: 
ms.date: 07/14/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: SQL13.SWB.DATABASEUSER.MEMBERSHIP.F1
helpviewer_keywords:
- adding a member to a role
- join a role
ms.assetid: 05c8d10d-5823-46c6-8b1a-81722da6a42b
caps.latest.revision: "13"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.openlocfilehash: 569eea78d5270e680caa81557585bfb817d3bd13
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="join-a-role"></a>unir uma função
  Este tópico descreve como atribuir funções a logons e usuários de banco de dados no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Use funções em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para gerenciar permissões de maneira eficiente. Atribua permissões a funções e adicione e remova usuários e logons de funções. Com o uso de funções, as permissões não precisam ser mantidas individualmente para cada usuário.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dá suporte a quatro tipos de função.  
  
-   Funções de servidor fixas  
  
-   Funções de servidor definidas pelo usuário  
  
-   Funções de banco de dados fixas  
  
-   Funções de banco de dados definidas pelo usuário  
  
 As funções fixas estão automaticamente disponíveis no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Funções fixas têm as permissões necessárias para realizar tarefas comuns. Para obter mais informações sobre funções fixas, consulte os links a seguir. Funções definidas pelo usuário são criadas por você e podem ser personalizadas com as permissões que você seleciona. Para obter mais informações sobre funções definidas pelo usuário, consulte os links a seguir.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para atribuir funções a logons e usuários de banco de dados, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   A alteração do nome de uma função de banco de dados não altera o número da ID, o proprietário ou as permissões da função.  
  
-   As funções de banco de dados são visíveis nas exibições do catálogo sys.database_role_members e sys.database_principals.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige a permissão **ALTER ANY ROLE** no banco de dados, a permissão **ALTER** na função ou a associação em **db_securityadmin**.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-add-a-member-to-a-fixed-server-role"></a>Para adicionar um membro a uma função de servidor fixa  
  
1.  No Pesquisador de Objetos, expanda o servidor no qual você quer editar uma função de servidor fixa.  
  
2.  Expanda a pasta **Segurança** .  
  
3.  Expanda a pasta **Funções de Servidor**  
  
4.  Clique com o botão direito do mouse na função que você deseja editar e selecione **Propriedades**.  
  
5.  Na caixa de diálogo **Propriedades de Função de Servidor –***server_role_name* , na página **Membros** , clique em **Adicionar**.  
  
6.  Na caixa de diálogo **Selecionar Logon ou Função de Servidor** , em **Digite os nomes de objeto a selecionar (exemplos)**, insira o logon ou função de servidor para adicionar a esta função de servidor. Como alternativa, clique em **Procurar...** e selecione qualquer um ou todos os objetos disponíveis na caixa de diálogo **Procurar por objetos** . Clique em **OK** para retornar à caixa de diálogo **Propriedades de Função de Servidor –***server_role_name* .  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-add-a-member-to-a-user-defined-database-role"></a>Para adicionar um membro a uma função de banco de dados definida pelo usuário  
  
1.  No Pesquisador de Objetos, expanda o servidor no qual você quer editar uma função de banco de dados definida pelo usuário.  
  
2.  Expanda a pasta **Bancos de Dados** .  
  
3.  Expanda o banco de dados no qual você quer editar uma função de banco de dados definida pelo usuário.  
  
4.  Expanda a pasta **Segurança** .  
  
5.  Expanda a pasta **Funções** .  
  
6.  Expanda a pasta **Funções de Servidor** .  
  
7.  Clique com o botão direito do mouse na função que você deseja editar e selecione **Propriedades**.  
  
8.  Na caixa de diálogo **Propriedades de Função de Banco de Dados –***database_role_name* , na página **Geral** , clique em **Adicionar**.  
  
9. Na caixa de diálogo **Selecionar Usuário ou Função do Banco de Dados** , em **Digite os nomes de objeto a selecionar (exemplos)**, insira o logon ou função de banco de dados para adicionar a esta função de banco de dados. Como alternativa, clique em **Procurar...** e selecione qualquer um ou todos os objetos disponíveis na caixa de diálogo **Procurar por objetos** . Clique em **OK** para retornar à caixa de diálogo **Propriedades de Função de Banco de Dados –***database_role_name* .  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-add-a-member-to-a-fixed-server-role"></a>Para adicionar um membro a uma função de servidor fixa  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    ALTER SERVER ROLE diskadmin ADD MEMBER [Domain\Juan] ;  
    GO  
    ```  
  
 Para obter mais informações, veja [ALTER ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-role-transact-sql.md).  
  
#### <a name="to-add-a-member-to-a-user-defined-database-role"></a>Para adicionar um membro a uma função de banco de dados definida pelo usuário  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    ALTER ROLE Marketing ADD MEMBER [Domain\Juan] ;  
    GO  
    ```  
  
 Para obter mais informações, consulte [sp_addrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
 [Funções de nível de servidor](../../../relational-databases/security/authentication-access/server-level-roles.md)   
 [Funções de nível de banco de dados](../../../relational-databases/security/authentication-access/database-level-roles.md)   
 [Funções de aplicativo](../../../relational-databases/security/authentication-access/application-roles.md)  
  
  

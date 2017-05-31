---
title: Excluir um proxy do SQL Server Agent | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- deleting SQL Server Agent proxies
- proxies [SQL Server Agent], deleting
- removing SQL Server Agent proxies
ms.assetid: 9248841d-7294-47d4-94f3-b34a0521fabc
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 8371f1b086c15881e6cfd125194038d5c8245b72
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="delete-a-sql-server-agent-proxy"></a>Excluir um proxy do SQL Server Agent
Este tópico descreve como excluir uma conta proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] ou o [!INCLUDE[tsql](../../includes/tsql_md.md)].  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Limitações e restrições](#Restrictions)  
  
    [Segurança](#Security)  
  
-   **Para excluir uma conta proxy do SQL Server Agent, usando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
    [Transact-SQL](#TsqlProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Restrictions"></a>Limitações e restrições  
  
-   Ao excluir uma conta proxy do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent, certifique-se de que o proxy não faça referência a nenhuma etapa de trabalho ativa. Para verificar se há etapas de trabalho que fazem referência ao proxy, clique com o botão direito do mouse no proxy, selecione **Propriedades**e, em seguida, na caixa de diálogo *proxy_name***Propriedades da Conta Proxy** , selecione a página **Referências** . Se excluir um proxy, você terá a opção de reatribuir todas as etapas de trabalho que o utilizam, na caixa de diálogo **Excluir Objeto** .  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent usam credenciais para armazenar informações sobre as contas de usuário do Windows. O usuário especificado na credencial deve ter a permissão "Fazer logon como trabalho em lotes" no computador que executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent verifica o acesso a subsistemas de um proxy e fornece acesso ao proxy sempre que a etapa de trabalho é executada. Se o proxy já não tiver acesso ao subsistema, a etapa de trabalho falhará. Caso contrário, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent representará o usuário especificado no proxy e executará a etapa de trabalho.  
  
-   Se o logon do usuário tiver acesso ao proxy ou se o usuário pertencer a alguma função com acesso ao proxy, ele poderá utilizá-lo em uma etapa de trabalho.  
  
### <a name="Security"></a>Segurança  
  
#### <a name="Permissions"></a>Permissões  
Somente membros da função de servidor fixa **sysadmin** podem criar, modificar ou excluir contas proxy.  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-delete-a-sql-server-agent-proxy-account"></a>Para excluir uma conta proxy do SQL Server Agent  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir um servidor que contém a conta proxy que você deseja excluir.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique no sinal de adição para expandir a pasta **Proxies** .  
  
4.  Clique no sinal de adição para expandir o subsistema que contém a conta proxy que você deseja excluir (por exemplo, **Script ActiveX)**.  
  
5.  Clique com o botão direito do mouse na conta proxy que deseja excluir e selecione **Excluir**.  
  
6.  Na caixa de diálogo **Excluir Objeto** , verifique se a conta proxy correta está selecionada. Marque a caixa de seleção **Reassign to** para reatribuir as etapas de trabalho que fazem referência dessa conta proxy para outra conta.  
  
7.  Clique em **OK**.  
  
## <a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-delete-a-sql-server-agent-proxy-account"></a>Para excluir uma conta proxy do SQL Server Agent  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- deletes the proxy "Catalog application proxy"  
    USE msdb ;  
    GO  
    EXEC dbo.sp_delete_proxy  
        @proxy_name = N'Catalog application proxy' ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_delete_proxy (Transact-SQL)](http://msdn.microsoft.com/en-us/44a1db13-b7f2-4dab-a1b5-b8dafb41737c).  
  


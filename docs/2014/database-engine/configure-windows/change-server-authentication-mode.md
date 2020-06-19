---
title: Alterar o modo de autenticação do servidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- sa account
- authentication [SQL Server], changing modes
- server authentication mode [SQL Server]
- modifying server authentication mode
ms.assetid: 79babcf8-19fd-4495-b8eb-453dc575cac0
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8bda31ca7d0c5949173a9a3e5ea656c1757c04f7
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935853"
---
# <a name="change-server-authentication-mode"></a>Alterar modo de autenticação do servidor
  Este tópico descreve como alterar o modo de autenticação de servidor no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Durante a instalação, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] é definido como **Modo de Autenticação do Windows** ou **Modo de Autenticação do SQL Server e do Windows**. Após a instalação, você pode alterar o modo de autenticação a qualquer momento.  
  
 Se **modo de Autenticação do Windows** for selecionado durante a instalação, o logon sa será desabilitado e uma senha será atribuída por meio da instalação. Se você alterar posteriormente o modo de autenticação para **Modo de Autenticação do SQL Server e do Windows**, o logon sa permanecerá desabilitado. Para usar o logon sa, use a instrução ALTER LOGIN para habilitar o logon de sa e atribuir uma nova senha. O logon sa só pode se conectar ao servidor usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para alterar o modo de autenticação de servidor usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
 A conta sa é uma conta bem conhecida do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e geralmente é visada por usuários mal-intencionados. Não habilite a conta sa, a menos que seu aplicativo exija isso. É muito importante que você use uma senha segura para o logon de sa.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-change-security-authentication-mode"></a>Alterar modo de autenticação de segurança  
  
1.  No Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , clique com o botão direito do mouse no servidor e clique em **Propriedades**.  
  
2.  Na página **Segurança** , em **Autenticação de Servidor**, selecione o novo modo de autenticação de servidor e clique em **OK**.  
  
3.  Na caixa de diálogo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , clique em **OK** para confirmar o requisito para reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  No Object Explorer, clique com o botão direito do mouse no seu servidor, e em seguida, clique em **Reiniciar**. Se o agente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver em execução, ele também deverá ser reiniciado.  
  
#### <a name="to-enable-the-sa-login"></a>Para habilitar o logon sa  
  
1.  No Pesquisador de objetos, expanda **segurança**, logons, clique com o botão direito do mouse `sa` e clique em **Propriedades**.  
  
2.  Na página **Geral** , talvez seja necessário criar e confirmar uma senha para o logon.  
  
3.  Na página **Status** , na seção **Logon** , clique em **Habilitado**e, em seguida, em **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para habilitar o logon sa**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo a seguir habilita o logon sa e define uma nova senha.  
  
    ```  
    ALTER LOGIN sa ENABLE ;  
    GO  
    ALTER LOGIN sa WITH PASSWORD = '<enterStrongPasswordHere>' ;  
    GO  
  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Senhas fortes](../../relational-databases/security/strong-passwords.md)   
 [Considerações de segurança para uma instalação do SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)   
 [Conectar-se ao SQL Server quando os administradores do sistema estão bloqueados](connect-to-sql-server-when-system-administrators-are-locked-out.md)  
  
  

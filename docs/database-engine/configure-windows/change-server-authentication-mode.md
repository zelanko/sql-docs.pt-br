---
title: Alterar o modo de autenticação do servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
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
ms.openlocfilehash: a688bae85e0ea6bd30bbde50df0151a97fd6f505
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68012993"
---
# <a name="change-server-authentication-mode"></a>Alterar modo de autenticação do servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como alterar o modo de autenticação de servidor no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Durante a instalação, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] é definido como **Modo de Autenticação do Windows** ou **Modo de Autenticação do SQL Server e do Windows**. Após a instalação, você pode alterar o modo de autenticação a qualquer momento.  
  
 Se **modo de Autenticação do Windows** for selecionado durante a instalação, o logon sa será desabilitado e uma senha será atribuída por meio da instalação. Se você alterar posteriormente o modo de autenticação para **Modo de Autenticação do SQL Server e do Windows**, o logon sa permanecerá desabilitado. Para usar o logon sa, use a instrução ALTER LOGIN para habilitar o logon de sa e atribuir uma nova senha. O logon sa só pode se conectar ao servidor usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para alterar o modo de autenticação de servidor usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
 A conta sa é uma conta bem conhecida do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e geralmente é visada por usuários mal-intencionados. Não habilite a conta sa, a menos que seu aplicativo exija isso. É muito importante que você use uma senha segura para o logon de sa.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-change-security-authentication-mode"></a>Alterar modo de autenticação de segurança  
  
1.  No Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , clique com o botão direito do mouse no servidor e clique em **Propriedades**.  
  
2.  Na página **Segurança** , em **Autenticação de Servidor**, selecione o novo modo de autenticação de servidor e clique em **OK**.  
  
3.  Na caixa de diálogo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , clique em **OK** para confirmar o requisito para reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
4.  No Pesquisador de Objetos, clique com o botão direito do mouse no servidor e clique em **Reiniciar**. Se o agente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver em execução, ele também deverá ser reiniciado.  
  
#### <a name="to-enable-the-sa-login"></a>Para habilitar o logon sa  
  
1.  No Pesquisador de Objetos, expanda **Segurança**, expanda Logons, clique com o botão direito do mouse em **sa**e clique em **Propriedades**.  
  
2.  Na página **Geral** , talvez seja necessário criar e confirmar uma senha para o logon.  
  
3.  Na página **Status** , na seção **Logon** , clique em **Habilitado**e, em seguida, em **OK**.  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para habilitar o logon sa**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole um dos exemplos a seguir na janela de consulta e clique em **Executar**. 


    -  O exemplo a seguir habilita o logon sa e define uma nova senha.  
  
       ```sql  
       ALTER LOGIN sa ENABLE ;  
       GO  
       ALTER LOGIN sa WITH PASSWORD = '<enterStrongPasswordHere>' ;  
       GO  
       ```  
    -  O exemplo a seguir altera a Autenticação do Servidor do modo misto (Windows + SQL) para somente Windows.

       ```sql
       USE [master]
       GO
       EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', 
                                 N'Software\Microsoft\MSSQLServer\MSSQLServer',      
                                 N'LoginMode', REG_DWORD, 1
       GO
       ```
  
## <a name="see-also"></a>Consulte Também  
 [Senhas fortes](../../relational-databases/security/strong-passwords.md)   
 [Considerações sobre segurança para uma instalação do SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [Conectar-se ao SQL Server quando os administradores do sistema estão bloqueados](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)  
  
  

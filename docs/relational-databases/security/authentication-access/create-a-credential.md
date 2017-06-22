---
title: Criar uma credencial | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- credentials [SQL Server], creating
- authentication [SQL Server], credentials
- logins [SQL Server], credentials
ms.assetid: c1e77e91-2a69-40d9-b8b3-97cffc710586
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 80dba3f156735179c0fb016e39f3065acd6f5ac1
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="create-a-credential"></a>Criar uma credencial
  Este tópico descreve como criar uma credencial no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 As credenciais oferecem um modo para permitir que os usuários de Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tenham uma identidade fora do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Isso é usado principalmente para executar código em Assemblies com conjunto de permissões EXTERNAL_ACCESS. As credenciais podem também ser usadas quando um usuário de Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] precisa acessar recursos de um domínio, como o local de um arquivo para armazenar um backup.  
  
 Uma credencial pode ser mapeada para vários logons de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ao mesmo tempo. Entretanto, um logon do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] só pode ser mapeado para uma credencial ao mesmo tempo. Depois que uma credencial é criada, use **Propriedades de Logon (Página Geral)** para mapear um logon para uma credencial.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar uma credencial, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Se não houver nenhuma credencial mapeada de logon para o provedor, a credencial mapeada para a conta de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] será usada.  
  
-   Um logon pode ter várias credenciais mapeadas, contanto que elas sejam usadas com provedores diferentes. Deve haver só uma credencial mapeada por provedor por logon. A mesma credencial pode ser mapeada para outros logons.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Exige permissão de ALTER ANY CREDENCIAL para criar ou modificar uma credencial e ALTER ANY LOGIN para mapear um logon para uma credencial.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-credential"></a>Para criar uma credencial  
  
1.  No Pesquisador de Objetos, expanda a pasta **Segurança** .  
  
2.  Clique com o botão direito do mouse na pasta **Credenciais** e selecione **Nova Credencial…**.  
  
3.  Na caixa de diálogo **Nova Credencial** , na caixa **Nome da Credencial** , digite um nome para a credencial.  
  
4.  Na caixa **Identidade** , digite o nome da conta usada para conexões de saída (ao deixar o contexto do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]). Normalmente, esta será uma conta de usuário do Windows, mas a identidade pode ser uma conta de outro tipo.  
  
     Como alternativa, clique nas reticências **(…)** para abrir a caixa de diálogo **Selecionar Usuário ou Grupo** .  
  
5.  Nas caixas **Senha** e **Confirmar senha** , digite a senha da conta especificada na caixa **Identidade** . Se **Identidade** for uma conta de usuário do Windows, esta será a senha Windows. A **Senha** poderá ficar em branco se nenhuma senha for requerida.  
  
6.  Selecione **Usar Provedor de Criptografia** para definir a credencial a ser verificada por um Provedor de EKM (Gerenciamento de Chave Extensível). Para obter mais informações, veja [EKM &#40;Gerenciamento de Chave Extensível&#41;](../../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando Transact-SQL  
  
#### <a name="to-create-a-credential"></a>Para criar uma credencial  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- Creates the credential called "AlterEgo.".   
    -- The credential contains the Windows user "Mary5" and a password.  
    CREATE CREDENTIAL AlterEgo WITH IDENTITY = 'Mary5',   
        SECRET = '<EnterStrongPasswordHere>';  
    GO  
    ```  
  
 Para obter mais informações, veja [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../../t-sql/statements/create-credential-transact-sql.md).  
  
  

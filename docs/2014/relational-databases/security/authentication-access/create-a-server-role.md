---
title: Criar uma função de servidor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.serverrole.members.f1
- SQL12.SWB.SERVERROLE.GENERAL.F1
- sql12.swb.serverrole.memberships.f1
helpviewer_keywords:
- SERVER ROLE, creating
ms.assetid: 74f19992-8082-4ed7-92a1-04fe676ee82d
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 0077b35c2b6017471a7a5548de54e121f7308ba1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37251788"
---
# <a name="create-a-server-role"></a>Criar uma função de servidor
  Este tópico descreve como criar uma nova função de servidor no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar uma nova função de servidor usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 As funções de servidor não podem receber permissão nos protegíveis do banco de dados. Para criar funções de banco de dados, veja [CREATE ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-role-transact-sql).  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
  
-   Exige a permissão CREATE SERVER ROLE ou associação na função de servidor fixa sysadmin.  
  
-   Também exige IMPERSONATE no *server_principal* para logons, permissão ALTER para funções de servidor usadas como o *server_principal*ou associação em um grupo do Windows que é usado como o server_principal.  
  
-   Ao usar a opção AUTHORIZATION para atribuir a propriedade de um função de servidor, as seguintes permissões também são necessárias:  
  
    -   Para atribuir a propriedade de uma função de servidor a outro logon, a permissão IMPERSONATE é necessária naquele logon.  
  
    -   Para atribuir a propriedade de uma função de servidor para outra, é necessária associação na função de servidor ou a permissão ALTER naquela função de servidor.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-new-server-role"></a>Para criar uma nova função de servidor  
  
1.  No Pesquisador de Objetos, expanda o servidor onde você deseja criar a nova função de servidor.  
  
2.  Expanda a pasta **Segurança** .  
  
3.  Clique com o botão direito do mouse na pasta **Funções de Servidor** e selecione **Nova Função de Servidor...**.  
  
4.  Na caixa de diálogo **Nova Função de Servidor –***server_role_name*, na página **Geral**, insira um nome para a nova função de servidor na caixa **Nome da função de servidor**.  
  
5.  Na caixa **Proprietário** , digite o nome da entidade de segurança de servidor que será proprietária da nova função. Como alternativa, clique nas reticências **(…)** para abrir a caixa de diálogo **Selecionar Logon ou Função de Servidor** .  
  
6.  Em **Protegíveis**, selecione um ou mais protegíveis do nível do servidor. Quando um protegível é selecionado, essa função de servidor pode receber ou ter as permissões negadas naquele protegível.  
  
7.  Na caixa **Permissões: Explícitas** , marque a caixa de seleção para conceder, conceder com concessão ou negar permissão a esta função de servidor para os protegíveis selecionados. Se uma permissão não puder ser concedida ou negada a todos os protegíveis selecionados, a permissão será representada como uma seleção parcial.  
  
8.  Na página **Membros** , use o botão **Adicionar** para adicionar logons que representam indivíduos ou grupos à nova função de servidor.  
  
9. Uma função de servidor definida pelo usuário pode ser membro de outra função de servidor. Na página **Associações** , marque uma caixa de seleção para tornar a função de servidor definida pelo usuário atual um membro de uma função de servidor selecionada.  
  
10. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-new-server-role"></a>Para criar uma nova função de servidor  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    --Creates the server role auditors that is owned the securityadmin fixed server role.  
    USE master;  
    CREATE SERVER ROLE auditors AUTHORIZATION securityadmin;  
    GO  
    ```  
  
 Para obter mais informações, veja [CREATE SERVER ROLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-role-transact-sql).  
  
  

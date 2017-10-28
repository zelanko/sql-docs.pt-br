---
title: Iniciar o SQL Server Agent automaticamente (SQL Server Management Studio) | Microsoft Docs
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
- SQL Server Agent, starting
- autostart SQL Server Agent
ms.assetid: 2ea332da-0ede-4d2b-b122-c4c10eaca191
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: d04f69be267c374559c65638d09d24ac6ef4822d
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="autostart-sql-server-agent-sql-server-management-studio"></a>Autostart SQL Server Agent (SQL Server Management Studio)
Este tópico descreve como configurar o [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent para reiniciar automaticamente caso seja interrompido de forma inesperada no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)].  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Limitações e restrições](#Restrictions)  
  
    [Segurança](#Security)  
  
-   [Para configurar o SQL Server Agent para reiniciar automaticamente usando o SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Restrictions"></a>Limitações e restrições  
O Pesquisador de Objetos só exibirá o nó [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent se você tiver permissão para usá-lo.  
  
### <a name="Security"></a>Segurança  
  
#### <a name="Permissions"></a>Permissões  
Para executar suas funções, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent deve ser configurado de modo a usar as credenciais de uma conta que seja membro da função de servidor fixa **sysadmin** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. A conta deve ter as seguintes permissões do Windows:  
  
-   Fazer logon como um serviço (SeServiceLogonRight)  
  
-   Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)  
  
-   Ignorar verificação completa (SeChangeNotifyPrivilege)  
  
-   Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)  
  
Para obter mais informações sobre as permissões do Windows necessárias para a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent, consulte [Selecionar uma conta para o serviço do SQL Server Agent](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) e [Setting Up Windows Service Accounts (Configurando as contas de serviço do Windows)](http://msdn.microsoft.com/en-us/309b9dac-0b3a-4617-85ef-c4519ce9d014).  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-configure-sql-server-agent-to-automatically-restart"></a>Para configurar o SQL Server Agent para reiniciar automaticamente  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor no qual você deseja configurar o SQL Server Agent para reiniciar automaticamente.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**e então clique em **Propriedades**.  
  
3.  Na página **Geral** , marque **Reiniciar automaticamente o SQL Server Agent se ele parar inesperadamente**.  
  


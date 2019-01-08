---
title: Iniciar o SQL Server Agent automaticamente (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, starting
- autostart SQL Server Agent
ms.assetid: 2ea332da-0ede-4d2b-b122-c4c10eaca191
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0088ef5797b258d3c765a4548e3b1cae9d5e0a14
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52782998"
---
# <a name="autostart-sql-server-agent-sql-server-management-studio"></a>Autostart SQL Server Agent (SQL Server Management Studio)
  Este tópico descreve como configurar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para reiniciar automaticamente caso seja interrompido de forma inesperada no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   [Para configurar o SQL Server Agent para reiniciar automaticamente usando o SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e Restrições  
 O Pesquisador de Objetos só exibirá o nó [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent se você tiver permissão para usá-lo.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Para executar suas funções, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser configurado de modo a usar as credenciais de uma conta que seja membro da função de servidor fixa **sysadmin** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A conta deve ter as seguintes permissões do Windows:  
  
-   Fazer logon como um serviço (SeServiceLogonRight)  
  
-   Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)  
  
-   Ignorar verificação completa (SeChangeNotifyPrivilege)  
  
-   Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)  
  
 Para obter mais informações sobre as permissões do Windows necessárias para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço do Agent, consulte [selecionar uma conta para o serviço do SQL Server Agent](select-an-account-for-the-sql-server-agent-service.md) e [configurar contas de serviço do Windows e Permissões](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-sql-server-agent-to-automatically-restart"></a>Para configurar o SQL Server Agent para reiniciar automaticamente  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor no qual você deseja configurar o SQL Server Agent para reiniciar automaticamente.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**e então clique em **Propriedades**.  
  
3.  Na página **Geral** , marque **Reiniciar automaticamente o SQL Server Agent se ele parar inesperadamente**.  
  
  

---
title: Enviar mensagens de erro do SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- messages [SQL Server], SQL Server Agent
- sending messages
- SQL Server Agent, errors
- errors [SQL Server Agent]
ms.assetid: 2597d0d7-951a-48cf-989f-abb67b9fdb36
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ffaeaf159617b5f354a32f2ac2f9a0c59ec3dce5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37196646"
---
# <a name="send-sql-server-agent-error-messages"></a>Send SQL Server Agent Error Messages
  Este tópico descreve como configurar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para enviar suas mensagens de erro via net send no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   [Para enviar mensagens de erro do SQL Server Agent usando o SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   O Pesquisador de Objetos só exibirá o nó [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent se você tiver permissão para usá-lo.  
  
-   O serviço do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Messenger deve estar em execução para o recebimento de eventos net send.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Para executar suas funções, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser configurado de modo a usar as credenciais de uma conta que seja membro da função de servidor fixa **sysadmin** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A conta deve ter as seguintes permissões do Windows:  
  
-   Fazer logon como um serviço (SeServiceLogonRight)  
  
-   Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)  
  
-   Ignorar verificação completa (SeChangeNotifyPrivilege)  
  
-   Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)  
  
 Para obter mais informações sobre as permissões do Windows necessárias para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço do Agent, consulte [selecionar uma conta para o serviço do SQL Server Agent](select-an-account-for-the-sql-server-agent-service.md) e [configurar contas de serviço do Windows e Permissões](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-send-sql-server-agent-error-messages"></a>Para enviar mensagens de erro do SQL Server Agent  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent do qual você deseja enviar mensagens de erro via net send.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent** e selecione **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do SQL Server Agent –***server_name*, em **Log de erros** na página **Geral**, digite o nome de usuário ou o nome do computador para o qual você deseja enviar mensagens de erro na caixa **Destinatário do net send**.  
  
4.  Clique em **OK**.  
  
  

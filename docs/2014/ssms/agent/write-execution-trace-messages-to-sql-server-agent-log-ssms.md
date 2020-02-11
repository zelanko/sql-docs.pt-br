---
title: Gravar mensagens de rastreamento de execução para o SQL Server Agent log de erros (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- writing trace messages
- traces [SQL Server], SQL Server Agent logs
- SQL Server Agent, errors
- errors [SQL Server Agent]
ms.assetid: 90e3731e-6fae-43db-833e-9accecdd1c03
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fd21f4b08bf53d4715f2b99eefed523f3853c033
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63245441"
---
# <a name="write-execution-trace-messages-to-the-sql-server-agent-error-log-sql-server-management-studio"></a>Write Execution Trace Messages to the SQL Server Agent Error Log (SQL Server Management Studio)
  Este tópico descreve como configurar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Agent para incluir mensagens de rastreamento de execução em seu log [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de erros [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]no usando o.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   [Para gravar mensagens de rastreamento de execução no log de erros do SQL Server Agent usando o SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   O Pesquisador de Objetos só exibirá o nó [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent se você tiver permissão para usá-lo.  
  
-   Como essa opção pode fazer com que o log de erros torne-se muito grande, somente inclua as mensagens de rastreamento de execução nos logs de erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent ao investigar um problema específico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Para executar suas funções, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser configurado de modo a usar as credenciais de uma conta que seja membro da função de servidor fixa **sysadmin** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A conta deve ter as seguintes permissões do Windows:  
  
-   Fazer logon como um serviço (SeServiceLogonRight)  
  
-   Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)  
  
-   Ignorar verificação completa (SeChangeNotifyPrivilege)  
  
-   Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)  
  
 Para obter mais informações sobre as permissões do Windows necessárias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a conta de serviço do Agent, consulte [selecionar uma conta para o serviço de SQL Server Agent](select-an-account-for-the-sql-server-agent-service.md) e [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
##  <a name="SSMSProcedure"></a>   
#### <a name="to-write-execution-trace-messages-to-the-sql-server-agent-error-log"></a>Para gravar mensagens de rastreamento de execução no log de erros do SQL Server Agent  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para o qual você deseja gravar mensagens de rastreamento de execução.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent** e selecione **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do SQL Server Agent –**_server_name_ , **em log de erros** na página **geral** , marque a caixa de seleção **incluir mensagens de rastreamento de execução** .  
  
4.  Clique em **OK**.  
  
  

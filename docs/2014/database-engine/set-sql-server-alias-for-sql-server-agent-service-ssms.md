---
title: Definir um Alias do SQL Server para o serviço do SQL Server Agent (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- aliases [SQL Server], creating
- SQL Server Agent, aliases
ms.assetid: 02d6295d-ab52-44f0-8f1b-f3910a507d8f
caps.latest.revision: 21
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f86e776b891514e69aaffbc630debdc5f1a940a8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37229616"
---
# <a name="set-a-sql-server-alias-for-the-sql-server-agent-service-sql-server-management-studio"></a>Set a SQL Server Alias for the SQL Server Agent Service (SQL Server Management Studio)
  Este tópico descreve como definir um alias do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a ser usado pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent para se conectar ao [!INCLUDE[ssDE](../includes/ssde-md.md)] usando o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Por padrão, o serviço do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent se conecta a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em pipes nomeados usando nomes dinâmicos de servidor que não exigem configuração adicional de cliente. Só será necessário configurar um alias de conexão com o servidor se você não estiver usando o transporte de rede padrão ou se estiver se conectando a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que escute em um pipe nomeado alternativo.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   [Para definir um Alias do SQL Server para o Serviço do SQL Server Agent usando o SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent não funcionará corretamente a menos que você selecione um alias referente à instância local do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   O Pesquisador de Objetos só exibirá o nó [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent se você tiver permissão para usá-lo.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Para executar suas funções, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent deve ser configurado de modo a usar as credenciais de uma conta que seja membro da função de servidor fixa **sysadmin** no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A conta deve ter as seguintes permissões do Windows:  
  
-   Fazer logon como um serviço (SeServiceLogonRight)  
  
-   Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)  
  
-   Ignorar verificação completa (SeChangeNotifyPrivilege)  
  
-   Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)  
  
 Para obter mais informações sobre as permissões do Windows necessárias para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] conta de serviço do Agent, consulte [selecionar uma conta para o serviço do SQL Server Agent](../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) e [configurar contas de serviço do Windows e Permissões](configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-set-a-sql-server-alias-for-the-sql-server-agent-service"></a>Para definir um alias do SQL Server para o serviço do SQL Server Agent  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] e expanda-a.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**e então clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do SQL Server Agent***server_name*, em **Selecionar uma página**, selecione **Conexão**, e  
  
4.  Na caixa **Servidor de host local do alias** , digite o alias do servidor ao qual o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Agent deve se conectar.  
  
5.  Clique em **OK**.  
  
  

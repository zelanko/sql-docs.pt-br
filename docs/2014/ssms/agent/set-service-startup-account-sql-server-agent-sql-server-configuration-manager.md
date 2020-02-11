---
title: Definir a conta de inicialização do serviço para SQL Server Agent (SQL Server Configuration Manager) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, service accounts
- startup accounts [SQL Server]
- service startup accounts [SQL Server Agent]
ms.assetid: 46ffe818-ebb5-43a0-840b-923f219a2472
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30c50d1f6efc44c17eac76e0e03432c2461da296
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63033629"
---
# <a name="set-the-service-startup-account-for-sql-server-agent-sql-server-configuration-manager"></a>Set the Service Startup Account for SQL Server Agent (SQL Server Configuration Manager)
  A conta de inicialização de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent define a conta do Windows como a qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é executado, bem como suas permissões de rede. Este tópico descreve como definir a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   [Para definir a conta de inicialização do serviço para SQL Server Agent usando SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não exige mais que a conta de inicialização do serviço seja membro do grupo Administradores da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . No entanto, a conta de inicialização do serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser membro da função de servidor fixa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sysadmin. A conta também deverá ser membro da função TargetServersRole do banco de dados msdb no servidor mestre se o processamento de trabalhos multisservidor for usado.  
  
-   O Pesquisador de Objetos só exibirá o nó [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent se você tiver permissão para usá-lo.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Para executar suas funções, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Agent deve ser configurado para usar as credenciais de uma conta que seja membro da função `sysadmin` de servidor fixa no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A conta deve ter as seguintes permissões do Windows:  
  
-   Fazer logon como um serviço (SeServiceLogonRight)  
  
-   Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)  
  
-   Ignorar verificação completa (SeChangeNotifyPrivilege)  
  
-   Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)  
  
 Para obter mais informações sobre as permissões do Windows necessárias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a conta de serviço do Agent, consulte [selecionar uma conta para o serviço de SQL Server Agent](select-an-account-for-the-sql-server-agent-service.md) e [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-set-the-service-startup-account-for-sql-server-agent"></a>Para definir a conta de inicialização do serviço do SQL Server Agent  
  
1.  Em **Servidores Registrados**, clique no sinal de adição para expandir **Mecanismo de Banco de Dados**.  
  
2.  Clique no sinal de adição para expandir a pasta **Grupos do Servidor Local** .  
  
3.  Clique com o botão direito do mouse na instância de servidor na qual você deseja definir a Conta de Inicialização de Serviço e selecione **SQL Server Configuration Manager...**.  
  
4.  Na caixa de diálogo **Controle de Conta de Usuário**, clique em **Sim**.  
  
5.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no painel de console, selecione **Serviços do SQL Server**.  
  
6.  No painel de detalhes, clique com o botão direito do mouse em **SQL Server Agent**_(server_name)_, em que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *server_name* é o nome da instância do agente para o qual você deseja alterar a conta de inicialização do serviço e selecione **Propriedades**.  
  
7.  Na caixa de diálogo **Propriedades** de **SQL Server Agent**_(server_name)_ , na guia **logon** , selecione uma das seguintes opções em **fazer logon como**:  
  
    -   **Conta interna**: Selecione esta opção se seus trabalhos exigirem recursos somente do servidor local. Para obter informações sobre como escolher um tipo de conta interna do Windows, consulte [Seleção de uma conta para o Serviço do SQL Server Agent.](https://msdn.microsoft.com/library/ms191543.aspx)  
  
        > [!IMPORTANT]  
        >  O serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não dá suporte à conta **Serviço Local** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
    -   **Esta conta**: Selecione esta opção se seus trabalhos exigirem recursos na rede, incluindo recursos do aplicativo; Se você quiser encaminhar eventos para outros logs de aplicativos do Windows; ou, se você quiser notificar operadores por email ou pagers.  
  
         Se você selecionar esta opção:  
  
        1.  Na caixa **Nome da Conta** , digite a conta que será usada para executar o SQL Server Agent. Opcionalmente, clique em **Procurar** para abrir a caixa de usuário **Selecionar Usuário ou Grupo** e selecione a conta a ser usada.  
  
        2.  Na caixa **Senha** , digite a senha da conta. Digite novamente a senha na caixa **Confirmar senha** .  
  
8.  Clique em **OK**.  
  
9. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, clique no botão **Fechar** .  
  
  

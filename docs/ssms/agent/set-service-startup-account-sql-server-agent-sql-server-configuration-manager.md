---
title: Defina a conta de inicialização do serviço do SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, service accounts
- startup accounts [SQL Server]
- service startup accounts [SQL Server Agent]
ms.assetid: 46ffe818-ebb5-43a0-840b-923f219a2472
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 358b9406a7f2235d710b7da4146205e62cca0c30
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33046553"
---
# <a name="set-the-service-startup-account-for-sql-server-agent-sql-server-configuration-manager"></a>Set the Service Startup Account for SQL Server Agent (SQL Server Configuration Manager)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

A conta de inicialização de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent define a conta do Windows como a qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent é executado, bem como suas permissões de rede. Este tópico descreve como definir a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Configuration Manager no [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Limitações e restrições](#Restrictions)  
  
    [Segurança](#Security)  
  
-   [Para definir a conta de inicialização de serviço para o SQL Server Agent usando o SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Restrictions"></a>Limitações e restrições  
  
-   A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)], o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent não exige mais que a conta de inicialização do serviço seja membro do grupo Administradores da [!INCLUDE[msCoName](../../includes/msconame_md.md)] . No entanto, a conta de inicialização do serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent deve ser membro da função de servidor fixa [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]sysadmin. A conta também deverá ser membro da função TargetServersRole do banco de dados msdb no servidor mestre se o processamento de trabalhos multisservidor for usado.  
  
-   O Pesquisador de Objetos só exibirá o nó [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent se você tiver permissão para usá-lo.  
  
### <a name="Security"></a>Segurança  
  
#### <a name="Permissions"></a>Permissões  
Para executar suas funções, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent deve ser configurado de modo a usar as credenciais de uma conta que seja membro da função de servidor fixa **sysadmin** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. A conta deve ter as seguintes permissões do Windows:  
  
-   Fazer logon como um serviço (SeServiceLogonRight)  
  
-   Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)  
  
-   Ignorar verificação completa (SeChangeNotifyPrivilege)  
  
-   Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)  
  
Para obter mais informações sobre as permissões do Windows necessárias para a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent, consulte [Selecionar uma conta para o serviço do SQL Server Agent](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) e [Setting Up Windows Service Accounts (Configurando as contas de serviço do Windows)](http://msdn.microsoft.com/en-us/309b9dac-0b3a-4617-85ef-c4519ce9d014).  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-set-the-service-startup-account-for-sql-server-agent"></a>Para definir a conta de inicialização do serviço do SQL Server Agent  
  
1.  Em **Servidores Registrados**, clique no sinal de adição para expandir **Mecanismo de Banco de Dados**.  
  
2.  Clique no sinal de adição para expandir a pasta **Grupos do Servidor Local** .  
  
3.  Clique com o botão direito do mouse na instância de servidor na qual você deseja definir a Conta de Inicialização de Serviço e selecione **SQL Server Configuration Manager…**.  
  
4.  Na caixa de diálogo **Controle de Conta de Usuário** , clique em **Sim**.  
  
5.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Configuration Manager, no painel de console, selecione **Serviços do SQL Server**.  
  
6.  No painel de detalhes, clique com o botão direito do mouse em **SQL Server Agent***(server_name)*, em que *server_name* é o nome da instância do Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para o qual você deseja alterar a conta de inicialização de serviço, e selecione **Propriedades**.  
  
7.  Na caixa de diálogo **Propriedades** **SQL Server Agent***(server_name)*, na guia **Logon**, selecione uma das seguintes opções em **Fazer logon como**:  
  
    -   **Conta interna**: selecione essa opção se os trabalhos precisarem somente de recursos do servidor local. Para obter informações sobre como escolher um tipo de conta interna do Windows, consulte [Seleção de uma conta para o Serviço do SQL Server Agent.](http://msdn.microsoft.com/library/ms191543.aspx)  
  
        > [!IMPORTANT]  
        > O serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent não dá suporte à conta **Serviço Local** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
    -   **Esta conta**: selecione essa opção se os trabalhos necessitarem de recursos de toda a rede, inclusive recursos de aplicativos; se desejar encaminhar eventos para outros logs de aplicativos do Windows; ou se desejar notificar operadores por meio de email ou pagers.  
  
        Se você selecionar esta opção:  
  
        1.  Na caixa **Nome da Conta** , digite a conta que será usada para executar o SQL Server Agent. Opcionalmente, clique em **Procurar** para abrir a caixa de usuário **Selecionar Usuário ou Grupo** e selecione a conta a ser usada.  
  
        2.  Na caixa **Senha** , digite a senha da conta. Digite novamente a senha na caixa **Confirmar senha** .  
  
8.  Clique em **OK**.  
  
9. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Configuration Manager, clique no botão **Fechar** .  
  

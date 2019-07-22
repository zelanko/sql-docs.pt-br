---
title: Definir a conexão do SQL Server para o Serviço SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, connections
- connections [SQL Server], SQL Server Agent service
ms.assetid: 28b6178b-0a9e-4f2c-8562-7a62d2d2a285
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3ddd99e7ab984e0093e4a7e3f136b6df2c491f99
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263069"
---
# <a name="set-the-sql-server-connection-for-the-sql-server-agent-service-sql-server-management-studio"></a>Definir a Conexão do SQL Server para o Serviço do SQL Server Agent (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como definir a conexão entre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e o [!INCLUDE[ssDE](../../includes/ssde_md.md)] no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. O serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent pode se conectar a uma instância local do SQL Server usando autenticação do Windows.  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Limitações e restrições](#Restrictions)  
  
    [Segurança](#Security)  
  
-   **Para definir a conexão do SQL Server para o SQL Server Agent, usando:**  
  
    [SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Restrictions"></a>Limitações e restrições  
  
-   O Pesquisador de Objetos só exibirá o nó [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent se você tiver permissão para usá-lo.  
  
-   A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deixou de ter suporte à autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Essa opção só está disponível para a administração de versões antigas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="Security"></a>Segurança  
  
#### <a name="Permissions"></a>Permissões  
Para executar suas funções, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser configurado de modo a usar as credenciais de uma conta que seja membro da função de servidor fixa **sysadmin** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A conta deve ter as seguintes permissões do Windows:  
  
-   Fazer logon como um serviço (SeServiceLogonRight)  
  
-   Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)  
  
-   Ignorar verificação completa (SeChangeNotifyPrivilege)  
  
-   Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)  
  
Para obter mais informações sobre as permissões do Windows necessárias para a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, consulte [Selecionar uma conta para o serviço do SQL Server Agent](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) e [Setting Up Windows Service Accounts (Configurando as contas de serviço do Windows)](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-set-the-sql-server-connection"></a>Para definir a conexão do SQL Server  
  
1.  No **Pesquisador de Objetos,** clique no sinal de mais para expandir o servidor que você deseja definir com uma conexão como seu Serviço SQL Server Agent.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent** e selecione **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do SQL Server Agent**, em **Selecionar uma página**, clique em **Conexão**.  
  
4.  Em **Conexão do SQL Server**, selecione **Usar Autenticação do Windows** para permitir que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent se conecte a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde_md.md)] com Autenticação do [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows. Conexões com bancos de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores exigem a Autenticação do Windows.  
  

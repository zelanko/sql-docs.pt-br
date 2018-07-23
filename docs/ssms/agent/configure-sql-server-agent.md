---
title: Configurar o SQL Server Agent | Microsoft Docs
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
- SQL Server Agent, configuring
- accounts [SQL Server], SQL Server Agent
- SQL Server Agent, permissions
- security [SQL Server], SQL Server Agent
ms.assetid: 2e361a62-9e92-4fcd-80d7-d6960f127900
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a8eee96e9a3551e2ac9f0f1602b05606cea079f8
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38980269"
---
# <a name="configure-sql-server-agent"></a>Configure SQL Server Agent
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como especificar algumas opções de configuração para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. O conjunto completo de opções de configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent só está disponível no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], no SMO ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Management Objects) ou em procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent.  
  
**Neste tópico**  
  
-   **Antes de começar:**  
  
    [Limitações e restrições](#Restrictions)  
  
    [Segurança](#Security)  
  
-   [Para configurar o SQL Server Agent](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Restrictions"></a>Limitações e restrições  
  
-   Clique em **SQL Server Agent** no Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] para administrar trabalhos, operadores, alertas e o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. O Pesquisador de Objetos, porém, só exibirá o nó [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent se você tiver permissão para usá-lo.  
  
-   A reinicialização automática não deverá ser habilitada para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent em instâncias de cluster de failover.  
  
### <a name="Security"></a>Segurança  
  
#### <a name="Permissions"></a>Permissões  
Para executar suas funções, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent deve ser configurado de modo a usar as credenciais de uma conta que seja membro da função de servidor fixa **sysadmin** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. A conta deve ter as seguintes permissões do Windows:  
  
-   Fazer logon como um serviço (SeServiceLogonRight)  
  
-   Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)  
  
-   Ignorar verificação completa (SeChangeNotifyPrivilege)  
  
-   Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)  
  
Para obter mais informações sobre as permissões do Windows necessárias para a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent, consulte [Selecionar uma conta para o serviço do SQL Server Agent](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) e [Setting Up Windows Service Accounts (Configurando as contas de serviço do Windows)](http://msdn.microsoft.com/309b9dac-0b3a-4617-85ef-c4519ce9d014).  
  
## <a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-configure-sql-server-agent"></a>Para configurar o SQL Server Agent  
  
1.  Clique no botão **Iniciar** e, no menu **Iniciar**  , clique em **Painel de Controle**.  
  
2.  No Painel de Controle, clique em **Sistema e Segurança**, clique em **Ferramentas Administrativas**e selecione **Política de Segurança Local**.  
  
3.  Em Política de Segurança Local, clique na divisa para expandir a pasta **Políticas Locais** e clique na pasta **Atribuição de direitos de usuários** .  
  
4.  Clique com o botão direito do mouse em uma permissão que você deseja configurar para usar com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] e selecione **Propriedades**.  
  
5.  Na caixa de diálogo de propriedades da permissão, verifique a conta sob a qual as execuções do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent estão listadas. Se não, clique em **Adicionar Usuário ou Grupo**, insira a conta sob a qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent está sendo executado na caixa de diálogo **Selecionar usuários, computadores, contas de serviço ou grupos** e clique em **OK**.  
  
6.  Repita para cada permissão que você deseja adicionar para executar com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent. Quando terminar, clique em **OK**.  
  

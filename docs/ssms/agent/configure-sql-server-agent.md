---
description: Configure SQL Server Agent
title: Configure SQL Server Agent
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, configuring
- accounts [SQL Server], SQL Server Agent
- SQL Server Agent, permissions
- security [SQL Server], SQL Server Agent
ms.assetid: 2e361a62-9e92-4fcd-80d7-d6960f127900
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3a12ed0026afa31592d4b2f5f9f5dcc1cc30ae94
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92035637"
---
# <a name="configure-sql-server-agent"></a>Configure SQL Server Agent

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> Atualmente, na [Instância Gerenciada de SQL do Azure](/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. No momento, a habilitação e a desabilitação do SQL Server Agent não é compatível com a Instância Gerenciada de SQL. O SQL Agent sempre está em execução. Confira [Diferenças entre o T-SQL da Instância Gerenciada de SQL e o SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obter detalhes.

Este tópico descreve como especificar algumas opções de configuração para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O conjunto completo de opções de configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent só está disponível no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no SMO ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects) ou em procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>Limitações e Restrições  
  
-   Clique em **SQL Server Agent** no Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para administrar trabalhos, operadores, alertas e o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. O Pesquisador de Objetos, porém, só exibirá o nó [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent se você tiver permissão para usá-lo.  
  
-   A reinicialização automática não deverá ser habilitada para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent em instâncias de cluster de failover.  
  
### <a name="security"></a><a name="Security"></a>Segurança  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissões  
Para executar suas funções, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser configurado de modo a usar as credenciais de uma conta que seja membro da função de servidor fixa **sysadmin** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A conta deve ter as seguintes permissões do Windows:  
  
-   Fazer logon como um serviço (SeServiceLogonRight)  
  
-   Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)  
  
-   Ignorar verificação completa (SeChangeNotifyPrivilege)  
  
-   Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)  
  
Para obter mais informações sobre as permissões do Windows necessárias para a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, consulte [Selecionar uma conta para o serviço do SQL Server Agent](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) e [Setting Up Windows Service Accounts (Configurando as contas de serviço do Windows)](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-configure-sql-server-agent"></a>Para configurar o SQL Server Agent  
  
1.  Clique no botão **Iniciar** e, no menu **Iniciar**  , clique em **Painel de Controle**.  
  
2.  No Painel de Controle, clique em **Sistema e Segurança**, clique em **Ferramentas Administrativas**e selecione **Política de Segurança Local**.  
  
3.  Em Política de Segurança Local, clique na divisa para expandir a pasta **Políticas Locais** e clique na pasta **Atribuição de direitos de usuários** .  
  
4.  Clique com o botão direito do mouse em uma permissão que você deseja configurar para usar com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e selecione **Propriedades**.  
  
5.  Na caixa de diálogo de propriedades da permissão, verifique a conta sob a qual as execuções do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent estão listadas. Se não, clique em **Adicionar Usuário ou Grupo**, insira a conta sob a qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent está sendo executado na caixa de diálogo **Selecionar usuários, computadores, contas de serviço ou grupos** e clique em **OK**.  
  
6.  Repita para cada permissão que você deseja adicionar para executar com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Quando terminar, clique em **OK**.  

---
title: Configurar o SQL Server Agent | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, configuring
- accounts [SQL Server], SQL Server Agent
- SQL Server Agent, permissions
- security [SQL Server], SQL Server Agent
ms.assetid: 2e361a62-9e92-4fcd-80d7-d6960f127900
caps.latest.revision: 34
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4573c48caae7793efd4565f88a255dfe4bb7b18b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118246"
---
# <a name="configure-sql-server-agent"></a>Configurar o SQL Server Agent
  Este tópico descreve como especificar algumas opções de configuração para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O conjunto completo de opções de configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent só está disponível no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no SMO ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects) ou em procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   [Para configurar o SQL Server Agent](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
  
-   Clique em **SQL Server Agent** no Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para administrar trabalhos, operadores, alertas e o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. O Pesquisador de Objetos, porém, só exibirá o nó [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent se você tiver permissão para usá-lo.  
  
-   A reinicialização automática não deverá ser habilitada para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent em instâncias de cluster de failover.  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 Para executar suas funções, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser configurado de modo a usar as credenciais de uma conta que seja membro da função de servidor fixa **sysadmin** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A conta deve ter as seguintes permissões do Windows:  
  
-   Fazer logon como um serviço (SeServiceLogonRight)  
  
-   Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)  
  
-   Ignorar verificação completa (SeChangeNotifyPrivilege)  
  
-   Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)  
  
 Para obter mais informações sobre as permissões do Windows necessários para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conta de serviço do Agent, consulte [selecionar uma conta para o serviço SQL Server Agent](select-an-account-for-the-sql-server-agent-service.md) e [configurar contas de serviço do Windows e Permissões](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-sql-server-agent"></a>Para configurar o SQL Server Agent  
  
1.  Clique no botão **Iniciar** e, no menu **Iniciar**  , clique em **Painel de Controle**.  
  
2.  No Painel de Controle, clique em **Sistema e Segurança**, clique em **Ferramentas Administrativas**e selecione **Política de Segurança Local**.  
  
3.  Em Política de Segurança Local, clique na divisa para expandir a pasta **Políticas Locais** e clique na pasta **Atribuição de direitos de usuários** .  
  
4.  Clique com o botão direito do mouse em uma permissão que você deseja configurar para usar com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e selecione **Propriedades**.  
  
5.  Na caixa de diálogo de propriedades da permissão, verifique a conta sob a qual as execuções do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent estão listadas. Se não, clique em **Adicionar Usuário ou Grupo**, insira a conta sob a qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent está sendo executado na caixa de diálogo **Selecionar usuários, computadores, contas de serviço ou grupos** e clique em **OK**.  
  
6.  Repita para cada permissão que você deseja adicionar para executar com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Quando terminar, clique em **OK**.  
  
  
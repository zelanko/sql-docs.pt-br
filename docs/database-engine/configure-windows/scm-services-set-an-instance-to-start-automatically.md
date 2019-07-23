---
title: Serviços SCM – definir uma instância para ser iniciada automaticamente | Microsoft Docs
ms.custom: ''
ms.date: 01/06/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, automatic startup
- starting SQL Server, automatically
ms.assetid: aa2b6bde-e76d-4fea-a560-54a63745d9b1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 28c13ad423cb8ba01e91c7d8810723538ec41eae
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68025654"
---
# <a name="scm-services---set-an-instance-to-start-automatically"></a>Serviços SCM – definir uma instância para ser iniciada automaticamente
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como definir uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para iniciar automaticamente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o SQL Server Configuration Manager. Durante a instalação, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente é configurado para iniciar automaticamente. Se isto não foi feito, você poderá alterar essa definição a qualquer momento.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### <a name="to-set-an-instance-of-sql-server-to-start-automatically"></a>Para configurar uma instância do SQL Server para iniciar automaticamente  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
    > [!NOTE]  
    >  Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager é um snap-in do programa Console de Gerenciamento [!INCLUDE[msCoName](../../includes/msconame-md.md)] e não um programa autônomo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager não aparece como um aplicativo nas versões mais recentes do Windows.  
    >   
    >  -   **Windows 10**:  
    >          Para abrir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, na **Página Inicial**, digite SQLServerManager13.msc (para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]). Para versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , substitua 13 por um número menor. Clicar em SQLServerManager13.msc abre o Configuration Manager. Para fixar o Configuration Manager na Página Inicial ou na Barra de Tarefas, clique com o botão direito do mouse em SQLServerManager13.msc e clique em **Abrir local do arquivo**. No Explorador de Arquivos do Windows, clique com o botão direito do mouse em SQLServerManager13.msc e clique em **Fixar na Tela Inicial** ou **Fixar na Barra de Tarefas**.  
    > -   **Windows 8**:  
    >          Para abrir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no botão **Pesquisar**, em **Aplicativos**, digite **SQLServerManager\<versão>.msc**, como **SQLServerManager13.msc** e pressione **Enter**.  
  
2.  Em **SQL Server Configuration Manager**, expanda **Serviços**e, a seguir, clique em **SQL Server**.  
  
3.  No painel de detalhes, clique com o botão direito do mouse no nome da instância que deseja que seja iniciada automaticamente e clique em **Propriedades**.  
  
4.  Na caixa de diálogo **Propriedades do SQL Server \<***instancename***>** , defina o **Modo Inicial** como **Automático**.  
  
5.  Clique em **OK**e em seguida feche o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de Configuração.  
  
## <a name="see-also"></a>Consulte Também  
 [Impedir a inicialização automática de uma instância do SQL Server &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/scm-services-prevent-automatic-startup-of-an-instance.md)   
 [Conectar-se a outro computador &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/scm-services-connect-to-another-computer.md)   
 [Configurar o WMI para mostrar o status do servidor nas ferramentas do SQL Server](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  

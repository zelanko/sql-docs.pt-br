---
title: Definir uma instância de SQL Server para iniciar automaticamente (SQL Server Configuration Manager) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
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
ms.openlocfilehash: 5c5bb930015d3b566e68a2815aea5074819803bf
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935012"
---
# <a name="set-an-instance-of-sql-server-to-start-automatically-sql-server-configuration-manager"></a>Definir uma instância do SQL Server para iniciar automaticamente (SQL Server Configuration Manager)
  Este tópico descreve como definir uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para iniciar automaticamente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o SQL Server Configuration Manager. Durante a instalação, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente é configurado para iniciar automaticamente. Se isto não foi feito, você poderá alterar essa definição a qualquer momento.  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### <a name="to-set-an-instance-of-sql-server-to-start-automatically"></a>Para configurar uma instância do SQL Server para iniciar automaticamente  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
    > [!NOTE]  
    >  Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager é um snap-in do programa Console de Gerenciamento [!INCLUDE[msCoName](../../includes/msconame-md.md)] e não um programa autônomo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager não aparece como um aplicativo nas versões mais recentes do Windows.  
    >   
    >  -   **Windows 10**:  
    >          Para abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, na **página inicial**, digite SQLServerManager12. msc (para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ). Para versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] substitua 12 por um número menor. Clique em SQLServerManager12.msc para abrir o Configuration Manager. Para fixar o Configuration Manager na página inicial ou na barra de tarefas, clique com o botão direito do mouse em SQLServerManager12. msc e clique em **abrir local do arquivo**. No explorador de arquivos do Windows, clique com o botão direito do mouse em SQLServerManager12. msc e clique em **fixar para iniciar** ou **fixar na barra de tarefas**.  
    > -   **Windows 8**:  
    >          Para abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no botão **Pesquisar** , em **aplicativos**, digite **SQLServerManager \<version> . msc** `SQLServerManager12.msc` , como e pressione **Enter**.  
  
2.  Em **SQL Server Configuration Manager**, expanda **Serviços**e, a seguir, clique em **SQL Server**.  
  
3.  No painel de detalhes, clique com o botão direito do mouse no nome da instância que deseja que seja iniciada automaticamente e clique em **Propriedades**.  
  
4.  Na caixa de diálogo ** \<***instancename***> propriedades do SQL Server** , defina o **modo de início** como **automático**.  
  
5.  Clique em **OK**e em seguida feche o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de Configuração.  
  
## <a name="see-also"></a>Consulte Também  
 [Impedir a inicialização automática de uma instância do SQL Server &#40;SQL Server Configuration Manager&#41;](scm-services-prevent-automatic-startup-of-an-instance.md)   
 [Conectar-se a outro computador &#40;SQL Server Configuration Manager&#41;](scm-services-connect-to-another-computer.md)   
 [Configurar o WMI para mostrar o status do servidor nas ferramentas do SQL Server](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  

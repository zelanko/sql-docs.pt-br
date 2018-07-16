---
title: Definir uma instância do SQL Server para iniciar automaticamente (SQL Server Configuration Manager) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- automatic SQL Server startup
- SQL Server, automatic startup
- starting SQL Server, automatically
ms.assetid: aa2b6bde-e76d-4fea-a560-54a63745d9b1
caps.latest.revision: 34
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fdb191490353e6260467b50c26f94892ff6ce83b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37254688"
---
# <a name="set-an-instance-of-sql-server-to-start-automatically-sql-server-configuration-manager"></a>Definir uma instância do SQL Server para iniciar automaticamente (SQL Server Configuration Manager)
  Este tópico descreve como definir uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para iniciar automaticamente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o SQL Server Configuration Manager. Durante a instalação, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente é configurado para iniciar automaticamente. Se isto não foi feito, você poderá alterar essa definição a qualquer momento.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### <a name="to-set-an-instance-of-sql-server-to-start-automatically"></a>Para configurar uma instância do SQL Server para iniciar automaticamente  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
    > [!NOTE]  
    >  Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager é um snap-in do programa Console de Gerenciamento [!INCLUDE[msCoName](../../includes/msconame-md.md)] e não um programa autônomo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager não aparece como um aplicativo nas versões mais recentes do Windows.  
    >   
    >  -   **Windows 10**:  
    >          Para abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no **página inicial**, digite SQLServerManager12.msc (para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]). Para versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] substitua 12 por um número menor. Clicar SQLServerManager12.msc abre o Configuration Manager. Para fixar o Configuration Manager para a página inicial ou na barra de tarefas, clique com botão direito SQLServerManager12.msc e, em seguida, clique em **abrir local do arquivo**. No Explorador de arquivos do Windows, clique com botão direito SQLServerManager12.msc e, em seguida, clique em **Fixar na tela inicial** ou **Fixar na barra de tarefas**.  
    > -   **Windows 8**:  
    >          Para abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do Configuration Manager, no **pesquisa** botão, em **aplicativos**, digite **SQLServerManager\<versão >. msc** como `SQLServerManager12.msc`, em seguida, pressione **Enter**.  
  
2.  Em **SQL Server Configuration Manager**, expanda **Serviços**e, a seguir, clique em **SQL Server**.  
  
3.  No painel de detalhes, clique com o botão direito do mouse no nome da instância que deseja que seja iniciada automaticamente e clique em **Propriedades**.  
  
4.  Na caixa de diálogo **Propriedades do SQL Server \<***instancename***>**, defina o **Modo Inicial** como **Automático**.  
  
5.  Clique em **OK**e em seguida feche o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de Configuração.  
  
## <a name="see-also"></a>Consulte também  
 [Impedir a inicialização automática de uma instância do SQL Server &#40;SQL Server Configuration Manager&#41;](scm-services-prevent-automatic-startup-of-an-instance.md)   
 [Conectar-se a outro computador &#40;SQL Server Configuration Manager&#41;](scm-services-connect-to-another-computer.md)   
 [Configurar o WMI para mostrar o status do servidor nas ferramentas do SQL Server](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  

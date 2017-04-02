---
title: "Definir uma inst&#226;ncia do SQL Server para iniciar automaticamente (SQL Server Configuration Manager) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "inicialização automática do SQL Server"
  - "SQL Server, inicialização automática"
  - "iniciando o SQL Server, automaticamente"
ms.assetid: aa2b6bde-e76d-4fea-a560-54a63745d9b1
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Definir uma inst&#226;ncia do SQL Server para iniciar automaticamente (SQL Server Configuration Manager)
  Este tópico descreve como definir uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para iniciar automaticamente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o SQL Server Configuration Manager. Durante a instalação, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente é configurado para iniciar automaticamente. Se isto não foi feito, você poderá alterar essa definição a qualquer momento.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### Para configurar uma instância do SQL Server para iniciar automaticamente  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
    > [!NOTE]  
    >  Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager é um snap-in do programa Console de Gerenciamento [!INCLUDE[msCoName](../../includes/msconame-md.md)] e não um programa autônomo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager não aparece como um aplicativo nas versões mais recentes do Windows.  
    >   
    >  -   **Windows 10**:  
    >          Para abrir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, na **Página Inicial**, digite SQLServerManager13.msc (para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]). Para versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , substitua 13 por um número menor. Clicar em SQLServerManager13.msc abre o Configuration Manager. Para fixar o Configuration Manager na Página Inicial ou na Barra de Tarefas, clique com o botão direito do mouse em SQLServerManager13.msc e clique em **Abrir local do arquivo**. No Explorador de Arquivos do Windows, clique com o botão direito do mouse em SQLServerManager13.msc e clique em **Fixar na Tela Inicial** ou **Fixar na Barra de Tarefas**.  
    > -   **Windows 8**:  
    >          Para abrir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no botão **Pesquisar**, em **Aplicativos**, digite **SQLServerManager\<versão>.msc**, como **SQLServerManager13.msc**, e pressione **Enter**.  
  
2.  Em **SQL Server Configuration Manager**, expanda **Serviços**e, a seguir, clique em **SQL Server**.  
  
3.  No painel de detalhes, clique com o botão direito do mouse no nome da instância que deseja que seja iniciada automaticamente e clique em **Propriedades**.  
  
4.  Na caixa de diálogo **Propriedades SQL Server \<***instancename***>**, defina o **Modo Inicial** como **Automático**.  
  
5.  Clique em **OK**e em seguida feche o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de Configuração.  
  
## Consulte também  
 [Impedir a inicialização automática de uma instância do SQL Server &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/scm services - prevent automatic startup of an instance.md)   
 [Conectar-se a um outro computador &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/connect-to-another-computer-sql-server-configuration-manager.md)   
 [Configurar o WMI para mostrar o status do servidor nas ferramentas do SQL Server](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
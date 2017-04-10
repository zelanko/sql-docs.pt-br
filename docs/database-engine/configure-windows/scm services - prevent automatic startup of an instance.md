---
title: "Impedir a inicializa&#231;&#227;o autom&#225;tica de uma inst&#226;ncia do SQL Server (SQL Server Configuration Manager) | Microsoft Docs"
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
  - "SQL Server, parando"
  - "SQL Server, inicialização automática"
  - "cancelando a inicialização automática"
  - "parando o SQL Server"
  - "impedindo inicializações automáticas [SQL Server]"
ms.assetid: 782663cf-f3d7-4cc6-b621-21e4550f0322
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Impedir a inicializa&#231;&#227;o autom&#225;tica de uma inst&#226;ncia do SQL Server (SQL Server Configuration Manager)
  Este tópico descreve como impedir que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicie automaticamente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o SQL Server Configuration Manager. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é normalmente configurado para iniciar automaticamente. Você pode alterar isso definindo o modo de início da instância como manual.  
  
##  <a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### Para evitar a inicialização automática de uma instância do SQL Server  
  
1.  No menu **Iniciar** , aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
    > [!NOTE]  
    >  Como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager é um snap-in do programa Console de Gerenciamento [!INCLUDE[msCoName](../../includes/msconame-md.md)] e não um programa autônomo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager não aparece como um aplicativo nas versões mais recentes do Windows.  
    >   
    >  -   **Windows 10**:  
    >          Para abrir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, na **Página Inicial**, digite SQLServerManager13.msc (para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]). Para versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , substitua 13 por um número menor. Clicar em SQLServerManager13.msc abre o Configuration Manager. Para fixar o Configuration Manager na Página Inicial ou na Barra de Tarefas, clique com o botão direito do mouse em SQLServerManager13.msc e clique em **Abrir local do arquivo**. No Explorador de Arquivos do Windows, clique com o botão direito do mouse em SQLServerManager13.msc e clique em **Fixar na Tela Inicial** ou **Fixar na Barra de Tarefas**.  
    > -   **Windows 8**:  
    >          Para abrir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, no botão **Pesquisar**, em **Aplicativos**, digite **SQLServerManager\<versão>.msc**, como **SQLServerManager13.msc**, e pressione **Enter**.  
  
2.  No SQL Server Configuration Manager, expanda **Serviços** e clique em **SQL Server**.  
  
3.  No painel detalhes, clique com o botão direito do mouse em **MSSQLServer** e clique em **Propriedades.**  
  
4.  Na caixa de diálogo **Propriedades de \<***instancename***> do SQL Server**, na caixa **Propriedades**, defina o valor de **Modo Inicial** como **Manual**.  
  
5.  Clique em **OK** para fechar a caixa de diálogo **Propriedades de \<***instancename***> do SQL Server** e feche o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
## Consulte também  
 [Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](../../database-engine/configure-windows/start, stop, pause, resume, restart sql server services.md)  
  
  
---
title: "Executar o Windows PowerShell no SQL Server Management Studio | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# Executar o Windows PowerShell no SQL Server Management Studio
  Você pode iniciar sessões do Windows PowerShell no **Pesquisador de Objetos** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] inicia o Windows PowerShell, carrega o módulo **sqlps** e define o contexto de caminho ao nó associado na árvore do **Pesquisador de Objetos**.  
  
## Antes de começar  
 Quando você especificar a execução do PowerShell para um objeto no **Pesquisador de Objetos**, o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] iniciará uma sessão do Windows PowerShell na qual os snap-ins do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell foram carregados e registrados. O caminho da sessão é predefinido no local do objeto em que você clicou com o botão direito no Pesquisador de Objetos. Por exemplo, se você clicar com o botão direito do mouse no objeto de banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] no Pesquisador de Objetos e selecionar **Iniciar PowerShell**, o caminho do Windows PowerShell será definido da seguinte forma:  
  
```  
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```  
  
## Executar o PowerShell  
 **Para executar o PowerShell no SQL Server Management Studio**  
  
1.  Abra o **Pesquisador de Objetos**.  
  
2.  Navegue até o nó do objeto que será utilizado.  
  
3.  Clique com o botão direito do mouse no objeto e selecione **Iniciar PowerShell**.  
  
## Permissões  
 Quando aberto no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], o PowerShell não é executado com privilégios de Administrador que podem impedir algumas atividades como chamadas ao WMI.  
  
## Consulte também  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
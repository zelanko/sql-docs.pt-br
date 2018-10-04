---
title: Executar o Windows PowerShell no SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cc952b88a4828ae672bd6cee2cad0754f0ef6eaf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205236"
---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>Executar o Windows PowerShell no SQL Server Management Studio
  Você pode iniciar sessões do Windows PowerShell no **Pesquisador de Objetos** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] Inicia o Windows PowerShell, carrega o `sqlps` módulo e define o contexto de caminho ao nó associado na **Pesquisador de objetos** árvore.  
  
## <a name="before-you-begin"></a>Antes de começar  
 Quando você especificar a execução do PowerShell para um objeto no **Pesquisador de Objetos**, o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] iniciará uma sessão do Windows PowerShell na qual os snap-ins do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell foram carregados e registrados. O caminho da sessão é predefinido no local do objeto em que você clicou com o botão direito no Pesquisador de Objetos. Por exemplo, se você clicar com o botão direito do mouse no objeto de banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] no Pesquisador de Objetos e selecionar **Iniciar PowerShell**, o caminho do Windows PowerShell será definido da seguinte forma:  
  
```  
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```  
  
## <a name="run-powershell"></a>Executar o PowerShell  
 **Para executar o PowerShell no SQL Server Management Studio**  
  
1.  Abra o **Pesquisador de Objetos**.  
  
2.  Navegue até o nó do objeto que será utilizado.  
  
3.  Clique com o botão direito do mouse no objeto e selecione **Iniciar PowerShell**.  
  
## <a name="permissions"></a>Permissões  
 Quando aberto no [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], o PowerShell não é executado com privilégios de Administrador que podem impedir algumas atividades como chamadas ao WMI.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  

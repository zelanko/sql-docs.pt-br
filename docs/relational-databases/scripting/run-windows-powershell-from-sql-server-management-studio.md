---
title: Executar o Windows PowerShell no SQL Server Management Studio | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: ssms
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2f3f405a8a0a64d1202918154a163bf9b397ab93
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>Executar o Windows PowerShell no SQL Server Management Studio
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Você pode iniciar sessões do Windows PowerShell no **Pesquisador de Objetos** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] inicia o Windows PowerShell, carrega o módulo **sqlps** e define o contexto de caminho ao nó associado na árvore do **Pesquisador de Objetos** .  
  
## <a name="before-you-begin"></a>Antes de começar  
 Quando você especificar a execução do PowerShell para um objeto no **Pesquisador de Objetos**, o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] iniciará uma sessão do Windows PowerShell na qual os snap-ins do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell foram carregados e registrados. O caminho da sessão é predefinido no local do objeto em que você clicou com o botão direito no Pesquisador de Objetos. Por exemplo, se você clicar com o botão direito do mouse no objeto de banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] no Pesquisador de Objetos e selecionar **Iniciar PowerShell**, o caminho do Windows PowerShell será definido da seguinte forma:  
  
```  
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```  
  
## <a name="run-powershell"></a>Executar o PowerShell  
 **Para executar o PowerShell no SQL Server Management Studio**  
  
1.  Abra o **Pesquisador de Objetos**.  
  
2.  Navegue até o nó do objeto que será utilizado.  
  
3.  Clique com o botão direito do mouse no objeto e selecione **Iniciar PowerShell**.  
  
## <a name="permissions"></a>Permissões  
 Quando aberto no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], o PowerShell não é executado com privilégios de Administrador que podem impedir algumas atividades como chamadas ao WMI.  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  

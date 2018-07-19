---
title: Remover componentes do SQL Server Data Tools | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f8ddb919-661f-4868-8c71-87c96f1f4487
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 124b4f4f591966d8dc5294f3150892091f71ba74
ms.sourcegitcommit: 2f07d285824a8982c279f3816b220e61a2d91b06
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/29/2018
ms.locfileid: "37093652"
---
# <a name="removing-sql-server-data-tools-components"></a>Removendo componentes do SQL Server Data Tools
Alguns componentes do SSDT (SQL Server Data Tools) não são removidos quando você desinstala o SSDT ou o Visual Studio.  
  
Os pacotes de instalação do Windows (.msi) a seguir não serão removidos do computador quando o SSDT ou o Visual Studio for desinstalado. A remoção destes componentes pode colocar outras versões do Visual Studio em um estado sem suporte. Se você optar por remover estes componentes, use o recurso Adicionar ou Remover Programas do Windows:  
  
-   MicrosoftSQL Server Data Tools (SSDT.msi)  
  
-   MicrosoftSQL Server Data Tools Build Utilities (SSDTBuildUtilities.msi)  
  
-   Pré-requisitos do SSDT (SSDTDBSvcExternals.msi)  
  
Os componentes compartilhados a seguir podem ser usados por outros produtos e permanecerão no computador depois que o SSDT for desinstalado.  
  
-   Estrutura de Aplicativo da Camada de Dados do SQL Server (DACFramework.msi)  
  
-   SQL Server Management Objects (SharedManagementObjects.msi)  
  
-   Serviço de linguagem do SQL ServerTransact\-SQL (TSqlLanguageService.msi)  
  
-   Tipos de CLR do MicrosoftSQL Server System para SQL Server (SQLSysClrTypes.msi)  
  
-   SQL ServerTransact\-SQL ScriptDom (SQLDom.msi)  
  
-   SQL ServerTransact\-Serviço Compilador do SQL (SQLLs.msi)  
  

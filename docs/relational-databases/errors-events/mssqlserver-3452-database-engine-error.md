---
title: MSSQLSERVER_3452 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 3452 (Database Engine error)
ms.assetid: bf838f02-7186-4b33-b01e-361b0c02de1f
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 52865b3a6a4a036acafffa97cff5d0fbc6abbbf9
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver3452"></a>MSSQLSERVER_3452
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|3452|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|REC_CHECKIDENTITY|  
|Texto da mensagem|A recuperação do banco de dados '%.*ls' (%d) detectou uma possível inconsistência do valor da identidade na ID da tabela %d. Execute DBCC CHECKIDENT ('%.\*ls').|  
  
## <a name="explanation"></a>Explicação  
Durante a atualização para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o processo para recuperar os valores de identidade no banco de dados encontrou uma inconsistência nos metadados.  
  
## <a name="user-action"></a>Ação do usuário  
Execute DBCC CHECKIDENT.  
  

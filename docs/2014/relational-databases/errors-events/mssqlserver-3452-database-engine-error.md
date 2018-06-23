---
title: MSSQLSERVER_3452 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 3452 (Database Engine error)
ms.assetid: bf838f02-7186-4b33-b01e-361b0c02de1f
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b6ef54d9a48826e67d1fbf8b3673a590a2c58962
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121036"
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
  
  
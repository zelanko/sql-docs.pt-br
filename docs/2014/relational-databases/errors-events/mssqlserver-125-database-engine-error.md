---
title: MSSQLSERVER_125 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- "125"
helpviewer_keywords:
- 125 (Database Engine error)
ms.assetid: 0f58338d-2ea0-48b8-8a20-c438b0940433
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: c2739d0dace0b1cd1180611d406abb9bc88f56a4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010696"
---
# <a name="mssqlserver125"></a>MSSQLSERVER_125
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|125|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico||  
|Texto da mensagem|As expressões Case só podem ser aninhadas no nível %d.|  
  
## <a name="explanation"></a>Explicação  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite apenas 10 níveis de aninhamento em expressões CASE.  
  
## <a name="user-action"></a>Ação do usuário  
 Reduza o nível de instruções CASE instruções para 10 ou menos.  
  
## <a name="see-also"></a>Consulte também  
 [CASE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/case-transact-sql)  
  
  

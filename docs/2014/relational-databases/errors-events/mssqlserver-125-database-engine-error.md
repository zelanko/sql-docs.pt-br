---
title: MSSQLSERVER_125 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- "125"
helpviewer_keywords:
- 125 (Database Engine error)
ms.assetid: 0f58338d-2ea0-48b8-8a20-c438b0940433
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e7a4bdbb237f9b949a8ad0b3c9a9485e07ba2b91
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37422925"
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
  
  

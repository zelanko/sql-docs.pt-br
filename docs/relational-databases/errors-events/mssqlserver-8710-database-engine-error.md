---
title: MSSQLSERVER_8710 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 8710 (Database Engine error)
ms.assetid: 78b9f9da-5489-4be0-94df-f065d86ed18c
caps.latest.revision: 8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 28b8eb71cc0e50925788596d1b23572a51064423
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver8710"></a>MSSQLSERVER_8710
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|MSSQLSERVER|  
|ID do evento|8710|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|QUERY2_CUBE_ILLEGAL_AGG_FUNC|  
|Texto da mensagem|As funções de agregação usadas com consultas CUBE, ROLLUP ou GROUPING SET devem ser fornecidas para a mesclagem de subagregações. Para corrigir esse problema, remova a função de agregação ou grave a consulta que está usando as cláusulas UNION ALL sobre GROUP BY.|  
  
## <a name="explanation"></a>Explicação  
Uma função de agregação foi usada com CUBE, ROLLUP ou GROUPING SET e não forneceu um método para mesclar subagregações.  
  
## <a name="user-action"></a>Ação do usuário  
Para corrigir esse problema, remova a função de agregação ou grave a consulta que está usando as cláusulas UNION ALL sobre GROUP BY.  
  

---
title: MSSQLSERVER_10520 | Microsoft Docs
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
- 10520 (Database Engine error)
ms.assetid: cc8799f1-5b90-4248-b209-e1d5087f9529
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 07a9561564711ce37e6e1867b81870341d7b5e45
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007707"
---
# <a name="mssqlserver10520"></a>MSSQLSERVER_10520
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|10520|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_PARAM_NOT_ALLOWED|  
|Texto da mensagem|Não é possível criar o guia de plano '%.*ls' porque @type foi especificado como '%ls' e um valor não NULL está especificado para o parâmetro '%ls'. Esse tipo requer um valor NULL para o parâmetro. Especifique um valor NULL para o parâmetro ou altere o tipo para um que permita um valor não NULL para o parâmetro.|  
  
## <a name="explanation"></a>Explicação  
 O tipo especificado em @type exige um valor NULL para o parâmetro especificado; entretanto, foi fornecido um valor não NULL.  
  
## <a name="user-action"></a>Ação do usuário  
 Especifique um valor NULL para o parâmetro ou altere o tipo para um que permita um valor não NULL para o parâmetro.  
  
## <a name="see-also"></a>Consulte também  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Guias de plano](../performance/plan-guides.md)  
  
  

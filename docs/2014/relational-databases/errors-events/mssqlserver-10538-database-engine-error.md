---
title: MSSQLSERVER_10538 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10538 (Database Engine error)
ms.assetid: 284d19b4-4979-4cbe-a9be-ac1104433c69
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: edc6abf192a3341f9b84c99e99071343cc882c3d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968106"
---
# <a name="mssqlserver_10538"></a>MSSQLSERVER_10538
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|10538|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_INVALID_PLANGUIDE_HANDLE|  
|Texto da mensagem|Não foi possível encontrar o guia de plano porque a ID do guia de plano especificada é NULL ou inválida ou você não tem permissão no objeto referenciado pelo guia de plano. Verifique se a ID do guia de plano é válida, se a sessão atual está definida com o contexto de banco de dados correto e se você tem a permissão ALTER DATABASE ou ALTER no objeto referenciado pelo guia de plano.|  
  
## <a name="explanation"></a>Explicação  
 A ID do plano de guia especificado é NULL ou inválida ou você não tem permissão no objeto referenciado pelo guia de plano.  
  
## <a name="user-action"></a>Ação do usuário  
 Verifique se a ID do guia de plano é válida, se a sessão atual está definida com o contexto de banco de dados correto e se você tem a permissão ALTER DATABASE ou ALTER no objeto referenciado pelo guia de plano.  
  
## <a name="see-also"></a>Consulte Também  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Guias de plano](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  

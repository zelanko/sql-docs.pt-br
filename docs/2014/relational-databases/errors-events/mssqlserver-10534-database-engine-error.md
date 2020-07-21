---
title: MSSQLSERVER_10534 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10534 (Database Engine error)
ms.assetid: e65bb118-99d5-4fdb-b1d5-0ec70f0a677b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 021ef5c5c7980115f5eb25792f4090774d968cef
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554121"
---
# <a name="mssqlserver_10534"></a>MSSQLSERVER_10534
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|10534|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_INVALID_PARAMS|  
|Texto da mensagem|Não é possível criar o guia de plano '%.\*ls' porque o valor especificado para `@params` é inválido. Especifique o valor no formato *parameter_name parameter_type* ou especifique NULL.|  
  
## <a name="explanation"></a>Explicação  
 O valor especificado para `@params` é inválido.  
  
## <a name="user-action"></a>Ação do usuário  
 Especifique o valor no formato *parameter_name parameter_type* ou especifique NULL.  
  
## <a name="see-also"></a>Consulte Também  
 [Guias de plano](../performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  

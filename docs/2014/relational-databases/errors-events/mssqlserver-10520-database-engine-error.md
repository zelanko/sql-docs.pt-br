---
title: MSSQLSERVER_10520 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10520 (Database Engine error)
ms.assetid: cc8799f1-5b90-4248-b209-e1d5087f9529
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c6cdc100429aa8c0cca55261679cdae1c5ebd66e
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554171"
---
# <a name="mssqlserver_10520"></a>MSSQLSERVER_10520
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|10520|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_PARAM_NOT_ALLOWED|  
|Texto da mensagem|Não é possível criar o guia de plano '%.*ls' porque @type foi especificado como '%ls' e um valor não NULL está especificado para o parâmetro '%ls'. Esse tipo requer um valor NULL para o parâmetro. Especifique um valor NULL para o parâmetro ou altere o tipo para um que permita um valor não NULL para o parâmetro.|  
  
## <a name="explanation"></a>Explicação  
 O tipo especificado em @type exige um valor NULL para o parâmetro especificado; entretanto, foi fornecido um valor não NULL.  
  
## <a name="user-action"></a>Ação do usuário  
 Especifique um valor NULL para o parâmetro ou altere o tipo para um que permita um valor não NULL para o parâmetro.  
  
## <a name="see-also"></a>Consulte Também  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [Guias de plano](../performance/plan-guides.md)  
  
  

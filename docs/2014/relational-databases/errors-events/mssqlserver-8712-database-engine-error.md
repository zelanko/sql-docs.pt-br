---
title: MSSQLSERVER_8712 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 8712 (Database Engine error)
ms.assetid: 292fb3bc-062e-41e4-a566-b5d3d0b21977
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9285d4846cac5af2dd6e87ab55d5fd0610586d07
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85031585"
---
# <a name="mssqlserver_8712"></a>MSSQLSERVER_8712
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|8712|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|USEPLAN_ERR_NO_INDEX|  
|Texto da mensagem|O índice '%.*ls', especificado na dica USE PLAN, não existe. Especifique um índice existente ou crie um índice com o nome especificado.|  
  
## <a name="explanation"></a>Explicação  
 Um índice especificado na dica USE PLAN não existe.  
  
## <a name="user-action"></a>Ação do usuário  
 Verifique se todos os índices que estão especificados na dica USE PLAN existem.  
  
## <a name="see-also"></a>Consulte Também  
 [Dicas de consulta &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [Guias de plano](../performance/plan-guides.md)  
  
  

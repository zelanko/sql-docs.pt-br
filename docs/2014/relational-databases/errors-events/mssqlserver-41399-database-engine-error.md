---
title: MSSQLSERVER_41399 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 41399 (Database Engine error)
ms.assetid: 5e5acb07-16ca-4329-8210-cd2bab0c904f
caps.latest.revision: 5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 18f6619ed33640a0659e4260a8c40dedcb225727
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37425115"
---
# <a name="mssqlserver41399"></a>MSSQLSERVER_41399
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41399|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|MAX_SORT_ROW_WIDTH_EXCEEDED|  
|Texto da mensagem|A operação de classificação é muito complexa. Consulte os manuais online do SQL Server para obter mais informações.|  
  
## <a name="explanation"></a>Explicação  
 Classificar o resultado de operações de junção e agregação aumenta a complexidade da operação de classificação aumentando o tamanho da linha no buffer de classificação. Esse erro significa que o tamanho da linha é maior que o tamanho máximo suportado pelo operador de classificação em procedimentos armazenados criados de modo nativo. Observe que o tamanho de uma linha no buffer de classificação somente é determinado pelo número de junções e o número e o tipo de funções de agregação. O tamanho das linhas nas tabelas base não afeta o tamanho da linha no buffer.  
  
## <a name="user-action"></a>Ação do usuário  
 Reduza a complexidade da consulta removendo junções ou funções de agregação.  
  
## <a name="see-also"></a>Consulte também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  

---
title: MSSQLSERVER_41396 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 41396 (Database Engine error)
ms.assetid: 4ff04042-8367-46f3-8a16-c94682d6eedb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f66a0ce65a0d16099d7371c003a813b129b3859f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62867870"
---
# <a name="mssqlserver41396"></a>MSSQLSERVER_41396
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41396|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|MAX_SORT_ROWS_EXCEEDED|  
|Texto da mensagem|A operação de classificação excedeu o limite de buffer. A execução do procedimento armazenado foi anulada. Consulte os manuais online do SQL Server para obter mais informações.|  
  
## <a name="explanation"></a>Explicação  
 Os procedimentos armazenados compilados de modo nativo executam operações de classificação na memória. Há um limite para o tamanho do buffer de classificação. Esse erro significa que o tamanho do buffer de classificação excedeu esse limite. A operação de classificação e a execução do procedimento armazenado anuladas.  
  
 O tamanho de cada linha ou entrada no buffer de classificação é determinado pelo número de linhas classificadas assim como o número de junções e o número e o tipo de funções de agregação na consulta. Ao simplificando a consulta, você poderá reduzir o tamanho de cada linha, ajustando, assim, mais linhas no buffer de classificação. O tamanho das linhas nas tabelas base não afeta o tamanho de cada linha ou entrada no buffer de classificação.  
  
## <a name="user-action"></a>Ação do usuário  
 Selecione menos linhas ou reduza a complexidade da consulta removendo junções ou funções de agregação.  
  
## <a name="see-also"></a>Consulte também  
 [OLTP in-memory &#40;Otimização na memória&#41;](../in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  

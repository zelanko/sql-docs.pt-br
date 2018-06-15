---
title: MSSQLSERVER_41396 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 41396 (Database Engine error)
ms.assetid: 4ff04042-8367-46f3-8a16-c94682d6eedb
caps.latest.revision: 8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 27799ec8daa7964bd60220c02053b24eac4af0a7
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34319907"
---
# <a name="mssqlserver41396"></a>MSSQLSERVER_41396
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
## <a name="see-also"></a>Consulte Também  
[OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  

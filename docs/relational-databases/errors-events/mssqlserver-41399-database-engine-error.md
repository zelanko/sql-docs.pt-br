---
title: MSSQLSERVER_41399 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41399 (Database Engine error)
ms.assetid: 5e5acb07-16ca-4329-8210-cd2bab0c904f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8f1dd8f616de43a0442e4110ba755cc66e397c43
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47832984"
---
# <a name="mssqlserver41399"></a>MSSQLSERVER_41399
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  
## <a name="see-also"></a>Consulte Também  
[OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  

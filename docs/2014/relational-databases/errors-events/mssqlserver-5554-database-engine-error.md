---
title: MSSQLSERVER_5554 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 5554 (Database Engine error)
ms.assetid: 7134bbe5-d240-4a98-85ce-b13cc8ae9b0e
caps.latest.revision: 11
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: a340576c20387fa0620815759aa966e59d139897
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007262"
---
# <a name="mssqlserver5554"></a>MSSQLSERVER_5554
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|MSSQLSERVER|  
|ID do evento|5554|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|FS_MINIVER_OVERFLOW|  
|Texto da mensagem|O número total de versões para um único arquivo atingiu o limite máximo definido pelo sistema de arquivos.|  
  
## <a name="explanation"></a>Explicação  
 No MARS (conjunto de resultados ativos múltiplos) ou em cenários de gatilho, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa a miniversão especificada pelo sistema operacional.  
  
## <a name="user-action"></a>Ação do usuário  
 Tente evitar atualizações repetidas nos dados da mesma transação.  
  
  
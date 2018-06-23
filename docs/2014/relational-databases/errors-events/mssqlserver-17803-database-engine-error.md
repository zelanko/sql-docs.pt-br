---
title: MSSQLSERVER_17803 | Microsoft Docs
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
- 17803 (Database Engine error)
ms.assetid: 28591a19-258d-4891-b78a-4686789bb2d7
caps.latest.revision: 14
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: b7a2ab967786eaa05c8ac393bbeaf0e42164f0f6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115672"
---
# <a name="mssqlserver17803"></a>MSSQLSERVER_17803
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|17803|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SRV_NOMEMORY|  
|Texto da mensagem|Ocorreu uma falha de alocação de memória ao estabelecer conexão. Reduce nonessential memory load, or increase system memory. A conexão foi fechada.%.*ls|  
  
## <a name="explanation"></a>Explicação  
 O servidor está sendo executado sem memória.  
  
## <a name="user-action"></a>Ação do usuário  
 Determine o motivo pelo qual o servidor está sendo executado sem memória. Etapas genéricas para a solução de problemas de memória podem ser úteis  
  
  
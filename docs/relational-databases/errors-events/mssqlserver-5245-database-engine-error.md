---
title: MSSQLSERVER_5245 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 5245 (Database Engine error)
ms.assetid: 6005c9ec-ccdd-4def-9eb4-37cdb599ddb3
caps.latest.revision: "17"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: d1ee9b94e955cd560db165e774d623dbf2796aeb
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver5245"></a>MSSQLSERVER_5245
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|5245|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC4_TABLE_LOCK_TIMEOUT_EXCEEDED|  
|Texto da mensagem|ID de objeto O_ID (objeto 'NAME'): DBCC não pôde obter um bloqueio nesse objeto porque o tempo limite da solicitação de bloqueio foi ultrapassado. Esse objeto foi ignorado e não será processado.|  
  
## <a name="explanation"></a>Explicação  
O limite de tempo do bloqueio expirou enquanto DBCC estava aguardando um bloqueio de tabela para o objeto especificado.  
  
## <a name="user-action"></a>Ação do usuário  
Execute o comando DBCC novamente.  
  

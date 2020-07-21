---
title: MSSQLSERVER_5245 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 5245 (Database Engine error)
ms.assetid: 6005c9ec-ccdd-4def-9eb4-37cdb599ddb3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2cea5c900150a26ecde783e50b953cc4a035a8ff
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551212"
---
# <a name="mssqlserver_5245"></a>MSSQLSERVER_5245
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|5245|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC4_TABLE_LOCK_TIMEOUT_EXCEEDED|  
|Texto da mensagem|ID de objeto O_ID (objeto 'NAME'): o DBCC não pôde obter um bloqueio nesse objeto porque o tempo limite da solicitação de bloqueio foi ultrapassado. Esse objeto foi ignorado e não será processado.|  
  
## <a name="explanation"></a>Explicação  
 O limite de tempo do bloqueio expirou enquanto DBCC estava aguardando um bloqueio de tabela para o objeto especificado.  
  
## <a name="user-action"></a>Ação do usuário  
 Execute o comando DBCC novamente.  
  
  

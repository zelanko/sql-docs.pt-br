---
title: MSSQLSERVER_5245 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5245 (Database Engine error)
ms.assetid: 6005c9ec-ccdd-4def-9eb4-37cdb599ddb3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c1d0c05f5439bbeea03895a4c0611b1aca6f35ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68062618"
---
# <a name="mssqlserver5245"></a>MSSQLSERVER_5245
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|5245|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC4_TABLE_LOCK_TIMEOUT_EXCEEDED|  
|Texto da mensagem|ID de objeto O_ID (objeto 'NAME'): o DBCC não pôde obter um bloqueio nesse objeto porque o tempo limite da solicitação de bloqueio foi ultrapassado. Esse objeto foi ignorado e não será processado.|  
  
## <a name="explanation"></a>Explicação  
O limite de tempo do bloqueio expirou enquanto DBCC estava aguardando um bloqueio de tabela para o objeto especificado.  
  
## <a name="user-action"></a>Ação do usuário  
Execute o comando DBCC novamente.  
  

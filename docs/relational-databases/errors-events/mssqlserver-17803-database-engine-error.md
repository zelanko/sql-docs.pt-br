---
title: MSSQLSERVER_17803 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17803 (Database Engine error)
ms.assetid: 28591a19-258d-4891-b78a-4686789bb2d7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4f9e63330cf94a3ba945a57e19d124fba8e6e458
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68131629"
---
# <a name="mssqlserver_17803"></a>MSSQLSERVER_17803
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|17803|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SRV_NOMEMORY|  
|Texto da mensagem|Ocorreu uma falha de alocação de memória ao estabelecer conexão. Reduce nonessential memory load, or increase system memory. A conexão foi fechada.%.*ls|  
  
## <a name="explanation"></a>Explicação  
O servidor está sendo executado sem memória.  
  
## <a name="user-action"></a>Ação do usuário  
Determine o motivo pelo qual o servidor está sendo executado sem memória. Etapas genéricas para a solução de problemas de memória podem ser úteis  
  

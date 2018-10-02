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
manager: craigg
ms.openlocfilehash: 9f4c8e064a92581c69a6cf2bd13fcf239749032b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47825538"
---
# <a name="mssqlserver17803"></a>MSSQLSERVER_17803
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
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
  

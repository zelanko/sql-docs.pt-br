---
title: MSSQLSERVER_7901 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 7901 (Database Engine error)
ms.assetid: 2d0d19b9-947b-4474-9ff8-7e03019ab93d
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 929eee801220874fcd5cc8ab77a27493c05deda9
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver7901"></a>MSSQLSERVER_7901
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|7901|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC2_DATABASE_IN_EMERGENCY_MODE|  
|Texto da mensagem|A instrução de correção não foi processada. Esse nível de correção não tem suporte quando o banco de dados está no modo de emergência.|  
  
## <a name="explanation"></a>Explicação  
O banco de dados está no modo de emergência e foi especificado um nível de correção diferente de REPAIR_ALLOW_DATA_LOSS. Não é possível fazer correções no modo de emergência, a menos que REPAIR_ALLOW_DATA_LOSS seja especificado.  
  
## <a name="user-action"></a>Ação do usuário  
Execute o comando novamente e especifique a opção REPAIR_ALLOW_DATA_LOSS.  
  

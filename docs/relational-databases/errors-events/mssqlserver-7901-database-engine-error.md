---
title: MSSQLSERVER_7901 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7901 (Database Engine error)
ms.assetid: 2d0d19b9-947b-4474-9ff8-7e03019ab93d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1a10e03f2dc09bb53078faaaaea36c60e313e0eb
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67951569"
---
# <a name="mssqlserver_7901"></a>MSSQLSERVER_7901
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|7901|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC2_DATABASE_IN_EMERGENCY_MODE|  
|Texto da mensagem|A instrução de correção não foi processada. Esse nível de correção não tem suporte quando o banco de dados está no modo de emergência.|  
  
## <a name="explanation"></a>Explicação  
O banco de dados está no modo de emergência e foi especificado um nível de correção diferente de REPAIR_ALLOW_DATA_LOSS. Não é possível fazer correções no modo de emergência, a menos que REPAIR_ALLOW_DATA_LOSS seja especificado.  
  
## <a name="user-action"></a>Ação do usuário  
Execute o comando novamente e especifique a opção REPAIR_ALLOW_DATA_LOSS.  
  

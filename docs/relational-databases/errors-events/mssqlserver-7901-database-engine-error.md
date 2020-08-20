---
description: MSSQLSERVER_7901
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
ms.openlocfilehash: b07f78159cc9f525255f28bdc2b9854dc0f41244
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460900"
---
# <a name="mssqlserver_7901"></a>MSSQLSERVER_7901
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
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
  

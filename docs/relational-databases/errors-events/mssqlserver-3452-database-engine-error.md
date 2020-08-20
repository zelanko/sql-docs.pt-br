---
description: MSSQLSERVER_3452
title: MSSQLSERVER_3452 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3452 (Database Engine error)
ms.assetid: bf838f02-7186-4b33-b01e-361b0c02de1f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5eaf8a280ebc3da3c1313010d336f5fa0ef67c1a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456179"
---
# <a name="mssqlserver_3452"></a>MSSQLSERVER_3452
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|3452|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|REC_CHECKIDENTITY|  
|Texto da mensagem|A recuperação do banco de dados '%.*ls' (%d) detectou uma possível inconsistência do valor da identidade na ID da tabela %d. Execute DBCC CHECKIDENT ('%.\*ls').|  
  
## <a name="explanation"></a>Explicação  
Durante a atualização para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o processo para recuperar os valores de identidade no banco de dados encontrou uma inconsistência nos metadados.  
  
## <a name="user-action"></a>Ação do usuário  
Execute DBCC CHECKIDENT.  
  

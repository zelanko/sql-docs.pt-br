---
description: MSSQLSERVER_41365
title: MSSQLSERVER_41365 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41365 (Database Engine error)
ms.assetid: 4fc7ec15-b722-4e3d-b7f9-3d39d171e96e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e370cafb16d5eceb2caed96b561862ea93b68205
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460906"
---
# <a name="mssqlserver_41365"></a>MSSQLSERVER_41365
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41365|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|HK_MERGE_SCHEDULE_ERROR|  
|Texto da mensagem|A solicitação de mesclagem para o intervalo de transações [%ld, %ld] no banco de dados %.*ls não foi agendada. Os arquivos de ponto de verificação que representam o intervalo não estão disponíveis para mesclagem ou parte de uma mesclagem contínua.|  
  
## <a name="explanation"></a>Explicação  
Os arquivos de ponto de verificação que representam o intervalo não estão disponíveis para mesclagem ou parte de uma mesclagem contínua.  
  
## <a name="user-action"></a>Ação do usuário  
Forneça um melhor intervalo de transações para mesclagem/espera antes de emitir a mesma solicitação novamente. Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte Também  
[OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  

---
description: MSSQLSERVER_10532
title: MSSQLSERVER_10532 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10532 (Database Engine error)
ms.assetid: 01da29ee-bf67-433f-8148-587a7e8d1d76
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cb404a386558bb0fb0906ca3a0bd223a47c044a9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88338842"
---
# <a name="mssqlserver_10532"></a>MSSQLSERVER_10532
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|10532|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_NO_ELIGIBLE_STMT|  
|Texto da mensagem|Não é possível criar o guia de plano “%.\*” porque o lote ou módulo especificado por **\@plan_handle** não contém uma instrução que seja qualificada para um guia de plano. Especifique um valor diferente para **\@plan_handle**.|  
  
## <a name="explanation"></a>Explicação  
O lote ou o módulo especificado por **\@plan_handle** não contém uma instrução qualificada para um guia de plano.  
  
## <a name="user-action"></a>Ação do usuário  
Especifique um valor diferente para **\@plan_handle**.  
  
## <a name="see-also"></a>Consulte Também  
[Guias de plano](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  

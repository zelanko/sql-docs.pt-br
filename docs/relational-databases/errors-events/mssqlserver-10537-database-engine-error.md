---
description: MSSQLSERVER_10537
title: MSSQLSERVER_10537 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10537 (Database Engine error)
ms.assetid: 728469a4-6523-4a37-925f-a950d75420fa
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bdceeb93a5bc468639502e64af3b39ffc90be6a9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88337952"
---
# <a name="mssqlserver_10537"></a>MSSQLSERVER_10537
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|10537|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_DUP_ENABLED|  
|Texto da mensagem|Não é possível habilitar o guia de plano '%.*ls' porque o guia de plano habilitado '%.\*ls' contém o mesmo escopo e valor de deslocamento inicial da instrução. Desabilite o guia de plano existente antes de habilitar o guia de plano especificado.|  
  
## <a name="explanation"></a>Explicação  
Um guia de plano existente contém o mesmo escopo e valor de deslocamento inicial que a instrução no guia de plano especificado.  
  
## <a name="user-action"></a>Ação do usuário  
Desabilite o guia de plano existente antes de habilitar o guia de plano especificado.  
  
## <a name="see-also"></a>Consulte Também  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Guias de plano](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  

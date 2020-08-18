---
description: MSSQLSERVER_10536
title: MSSQLSERVER_10536 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10536 (Database Engine error)
ms.assetid: 9f97b41f-0ef8-4ad2-aec0-906a5d7522ba
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a22480940730da65e3274bd9d2fd6a74d72ae479
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88338032"
---
# <a name="mssqlserver_10536"></a>MSSQLSERVER_10536
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|10536|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_TOO_MANY_STMTS|  
|Texto da mensagem|Não é possível criar o guia de plano '%.\*ls' porque o lote ou o módulo correspondente ao **\@plan_handle** especificado contém mais de 1.000 instruções qualificadas. Crie um guia de plano para cada instrução do lote ou do módulo especificando um valor **statement_start_offset** para cada instrução.|  
  
## <a name="explanation"></a>Explicação  
O lote ou o módulo correspondente ao **\@plan_handle** especificado contém mais de 1.000 instruções qualificadas.  
  
## <a name="user-action"></a>Ação do usuário  
Crie um guia de plano para cada instrução do lote ou do módulo especificando um valor **statement_start_offset** para cada instrução.  
  
## <a name="see-also"></a>Consulte Também  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Guias de plano](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  

---
title: MSSQLSERVER_10533 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10533 (Database Engine error)
ms.assetid: cc2fbdab-7b90-415f-a1f9-066824344283
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 86bd82dfd095baeacb35f8454859adb938123f52
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62916183"
---
# <a name="mssqlserver_10533"></a>MSSQLSERVER_10533
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|10533|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_NAME_TOO_BIG|  
|Texto da mensagem|Não é possível criar o guia de plano '%.*ls' porque seu nome tem mais de 124 caracteres, o número máximo permitido. Especifique um nome com menos de 125 caracteres.|  
  
## <a name="explanation"></a>Explicação  
 O nome do guia de plano tem mais de 124 caracteres, que é o número máximo permitido.  
  
## <a name="user-action"></a>Ação do usuário  
 Especifique um nome com menos de 125 caracteres.  
  
## <a name="see-also"></a>Consulte Também  
 [Guias de plano](../performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  

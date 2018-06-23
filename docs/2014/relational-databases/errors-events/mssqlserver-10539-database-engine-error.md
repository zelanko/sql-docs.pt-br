---
title: MSSQLSERVER_10539 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 10539 (Database Engine error)
ms.assetid: 49c26ff7-18b8-4f07-a087-f45f63463b3b
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 52f90cadcd7f66eebfcc1f722f3a9cc52a1eba1b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008181"
---
# <a name="mssqlserver10539"></a>MSSQLSERVER_10539
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|10539|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_NO_PLAN_FOR_STMT|  
|Texto da mensagem|Não é possível criar o guia de plano '%.*ls' a partir do cache porque um plano de consulta não está disponível para a instrução com deslocamento inicial %d. Esse problema poderá ocorrer se a instrução depender de objetos do banco de dados que ainda não foram criados. Verifique se todos os objetos de banco de dados necessários existem e execute a instrução antes de criar o guia de plano.|  
  
## <a name="explanation"></a>Explicação  
 Não há um plano de consulta disponível no cache de planos para a instrução com o deslocamento inicial especificado.  
  
## <a name="user-action"></a>Ação do usuário  
 Verifique se todos os objetos de banco de dados necessários existem e execute a instrução antes de criar o guia de plano.  
  
## <a name="see-also"></a>Consulte também  
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  

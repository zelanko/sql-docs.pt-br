---
title: MSSQLSERVER_2570 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 2570 (Database Engine error)
ms.assetid: 29800aa9-81aa-4371-992c-487dbb617f46
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 706a9fff1bed950ae6ef625ab8858ee7b86c73e3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver2570"></a>MSSQLSERVER_2570
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|2570|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_COLUMN_VALUE_OUT_OF_RANGE|  
|Texto da mensagem|Página P_ID, slot S_ID na ID de objeto O_ID, ID de índice I_ID, ID de partição PN_ID, ID de unidade de alocação A_ID (tipo TYPE). O valor de coluna COLUMN_NAME está fora do intervalo para tipo de dados "DATATYPE". Atualize a coluna para um valor válido.|  
  
## <a name="explanation"></a>Explicação  
O valor de coluna contido na coluna especificada está fora do intervalo de valores possíveis para o tipo de dados da coluna.  
  
## <a name="user-action"></a>Ação do usuário  
O erro não é reparável. Atualize a coluna com um valor que esteja dentro do intervalo para o tipo de dados da coluna e execute o comando novamente.  Para obter mais informações, consulte o artigo [923247](http://support.microsoft.com/kb/923247) da Base de Dados de Conhecimento.  
  
## <a name="see-also"></a>Consulte Também  
[UPDATE &#40;Transact-SQL&#41;](~/t-sql/queries/update-transact-sql.md)  
[Tipos de dados &#40;Transact-SQL&#41;](~/t-sql/data-types/data-types-transact-sql.md)  
  

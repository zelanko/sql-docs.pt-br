---
title: MSSQLSERVER_3417 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 3417 (Database Engine error)
ms.assetid: 005829c8-cf57-4828-818a-bbe8ee2e00f0
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d67f08ab21e634823011dd5a0e96005e97f2839c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver3417"></a>MSSQLSERVER_3417
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|3417|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|REC_BADMASTER|  
|Texto da mensagem|Não é possível recuperar o banco de dados mestre. O SQL Server não pode ser executado. Restaure o banco de dados mestre usando um backup completo, repare-o ou recrie-o. Para obter mais informações sobre como recriar o banco de dados mestre, consulte os Manuais Online do SQL Server.|  
  
## <a name="explanation"></a>Explicação  
O SQL Server não pode iniciar o banco de dados **mestre**. Se o banco de dados **master** ou **tempdb** não puderem ficar online, o SQL Server não poderá ser executado. Esse erro normalmente é precedido por outros erros. Revise os logs de erros para encontrar a causa original.  
  
## <a name="user-action"></a>Ação do usuário  
Restaure o backup do banco de dados ou repare o banco de dados.  
  

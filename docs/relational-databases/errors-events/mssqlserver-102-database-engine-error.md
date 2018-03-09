---
title: MSSQLSERVER_102 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 102 (Database Engine error)
ms.assetid: 264dc1a2-c8a0-4c89-b5f6-951baf950299
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8dea747ecad3640040dce817aaf706f90e4f63d6
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver102"></a>MSSQLSERVER_102
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|102|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|P_SYNTAXERR2|  
|Texto da mensagem|Sintaxe incorreta próxima a '%.*ls'.|  
  
## <a name="explanation"></a>Explicação  
Indica um erro de sintaxe. Informações adicionais não estão disponíveis porque o erro impede o [!INCLUDE[ssDE](../../includes/ssde-md.md)] de processar a instrução.  
  
Pode ser causado pela tentativa de criar uma chave simétrica que usa a criptografia RC4 ou RC4_128 preterido, quando fora do modo de compatibilidade 90 ou 100.  
  
## <a name="user-action"></a>Ação do usuário  
Procure os erros de sintaxe na instrução [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
Se for criar uma chave simétrica usando RC4 ou RC4_128, selecione uma criptografia mais recente, como um dos algoritmos AES. (Recomendado.) Se for necessário usar RC4, use ALTER DATABASE SET COMPATIBILITY_LEVEL para definir o banco de dados com o nível de compatibilidade 90 ou 100. (Não recomendável.)  
  

---
title: MSSQLSERVER_9532 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 9532 (Database Engine error)
ms.assetid: ab95cce8-4f97-4aea-a746-a73eea7c9aab
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 514c8efd47a7cb54397db495a268b1c9c415be58
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver9532"></a>MSSQLSERVER_9532
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|9532|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|XMLERR_COLUMNSET_CANNOT_CONVERT_FROM_TO|  
|Texto da mensagem|Na operação de consulta/DML envolvendo o conjunto de colunas '%.*ls', houve falha na conversão ao converter do tipo de dados '%ls' no tipo de dados '%ls' da coluna '%.\*ls'.|  
  
## <a name="explanation"></a>Explicação  
Um conjunto de colunas é uma representação em XML sem-tipo que combina algumas das colunas de uma tabela em uma saída estruturada. Ao inserir ou atualizar valores de coluna esparsos no conjunto de colunas XML, os valores inseridos nas colunas esparsas subjacentes são convertidos implicitamente do tipo de dados **xml**. O valor fornecido não pode ser convertido ao tipo de dados da coluna.  
  
## <a name="user-action"></a>Ação do usuário  
Como não foi possível converter implicitamente o valor fornecido, talvez seja uma entrada inválida. Corrija o erro e tente novamente. Se o valor estiver correto, modifique a instrução para usar as colunas individuais em vez do conjunto de colunas. Isso permitirá que você converta o valor explicitamente no tipo de dados correto.  
  

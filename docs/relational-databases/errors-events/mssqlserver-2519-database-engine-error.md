---
title: MSSQLSERVER_2519 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2519 (Database Engine error)
ms.assetid: 8dc6ad98-5db8-4c88-8dea-6d455e63b839
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 233d7d3a6ae29fe2e83272f36ed3e952e8bdd1dc
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68138478"
---
# <a name="mssqlserver_2519"></a>MSSQLSERVER_2519
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|2519|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_NO_EXPRESSION_EVALUATOR|  
|Texto da mensagem|Colunas computadas e tipos definidos pelo usuário não podem ter a ID do objeto O_ID (objeto "O_NAME") verificada porque o avaliador interno de expressões não pôde ser inicializado.|  
  
## <a name="explanation"></a>Explicação  
Essa mensagem informativa indica que o processador de consultas não pôde fornecer para DBCC um objeto interno que permita a avaliação de colunas computadas e de tipos CLR (Common Language Runtime) definidos pelo usuário. Isso significa que as colunas computadas e os tipos CLR definidos pelo usuário não serão verificados quanto à correção ou que não serão usados quando DBCC verificar a consistência entre índices e tabelas base.  
  
## <a name="user-action"></a>Ação do usuário  
Nenhum  
  
## <a name="see-also"></a>Consulte Também  
[MSSQLSERVER_2518](~/relational-databases/errors-events/mssqlserver-2518-database-engine-error.md)  
  

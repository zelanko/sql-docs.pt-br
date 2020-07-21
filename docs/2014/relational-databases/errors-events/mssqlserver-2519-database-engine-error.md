---
title: MSSQLSERVER_2519 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2519 (Database Engine error)
ms.assetid: 8dc6ad98-5db8-4c88-8dea-6d455e63b839
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 415657757d94d865fbea058f9d5929ec0deb0b20
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552059"
---
# <a name="mssqlserver_2519"></a>MSSQLSERVER_2519
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
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
 [MSSQLSERVER_2518](mssqlserver-2518-database-engine-error.md)  
  
  

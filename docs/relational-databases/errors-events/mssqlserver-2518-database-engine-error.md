---
title: MSSQLSERVER_2518 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2518 (Database Engine error)
ms.assetid: 54a13abc-4c33-43f0-b55d-e2e74a1381c8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 866600d2400dc84e597999eaaf88db08f65f9e89
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63045405"
---
# <a name="mssqlserver2518"></a>MSSQLSERVER_2518
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|2518|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_NO_EXPRESSION_EVAL_CLR_DISABLED|  
|Texto da mensagem|ID de Objeto O_ID (objeto "O_NAME"): colunas computadas e tipos definidos pelo usuário não podem ser verificados quanto a este objeto porque o CLR (Common Language Runtime) está desabilitado.|  
  
## <a name="explanation"></a>Explicação  
Essa mensagem informativa indica que o processador de consultas não pôde fornecer para DBCC um objeto interno que permita a avaliação de colunas computadas e de tipos CLR definidos pelo usuário. Esse problema ocorreu porque uma das colunas envolvia o CLR, mas ele não está habilitado. O objeto interno abrange todas as colunas. Por isso, a incapacidade de avaliar uma única coluna impede a criação do objeto interno. Isso significa que as colunas computadas não serão verificadas quanto à correção ou que não serão usadas quando DBCC verificar a consistência entre índices e tabelas base.  
  
## <a name="user-action"></a>Ação do usuário  
Habilite o CLR e execute a instrução DBCC novamente.  
  
## <a name="see-also"></a>Consulte Também  
[Habilitando a integração CLR](~/relational-databases/clr-integration/clr-integration-enabling.md)  
  

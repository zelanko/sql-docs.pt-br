---
title: MSSQLSERVER_2518 | Microsoft Docs
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
- 2518 (Database Engine error)
ms.assetid: 54a13abc-4c33-43f0-b55d-e2e74a1381c8
caps.latest.revision: 19
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f40eb8fe404479f5a2bcd68881aec4b2b2d84613
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012906"
---
# <a name="mssqlserver2518"></a>MSSQLSERVER_2518
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|2518|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_NO_EXPRESSION_EVAL_CLR_DISABLED|  
|Texto da mensagem|ID de Objeto O_ID (objeto "O_NAME"): colunas computadas e tipos definidos pelo usuário não podem ser verificados quanto a este objeto porque o Common Language Runtime (CLR) está desabilitado.|  
  
## <a name="explanation"></a>Explicação  
 Essa mensagem informativa indica que o processador de consultas não pôde fornecer para DBCC um objeto interno que permita a avaliação de colunas computadas e de tipos CLR definidos pelo usuário. Esse problema ocorreu porque uma das colunas envolvia o CLR, mas ele não está habilitado. O objeto interno abrange todas as colunas. Por isso, a incapacidade de avaliar uma única coluna impede a criação do objeto interno. Isso significa que as colunas computadas não serão verificadas quanto à correção ou que não serão usadas quando DBCC verificar a consistência entre índices e tabelas base.  
  
## <a name="user-action"></a>Ação do usuário  
 Habilite o CLR e execute a instrução DBCC novamente.  
  
## <a name="see-also"></a>Consulte também  
 [Habilitando a integração CLR](../clr-integration/clr-integration-enabling.md)  
  
  
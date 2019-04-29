---
title: Tipos de simultaneidade | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- locking concurrency control [ODBC]
- optimistic concurrency [ODBC]
- read-only concurrency control [ODBC]
ms.assetid: 46762ae5-17dd-4777-968e-58156f470fe1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 12891d7ee674167157bcb02300d2e4181ef51734
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63012111"
---
# <a name="concurrency-types"></a>Tipos de simultaneidade
Para resolver o problema de redução de simultaneidade em cursores, ODBC expõe quatro tipos diferentes de simultaneidade do cursor:  
  
-   **Somente leitura** o cursor pode ler dados, mas não é possível atualizar ou excluir dados. Esse é o tipo de simultaneidade padrão. Embora o DBMS podem bloquear linhas para impor a leitura repetida e níveis de isolamento serializável, ela pode usar bloqueios de leitura em vez de bloqueios de gravação. Isso resulta em maior simultaneidade porque outras transações, pelo menos, podem ler os dados.  
  
-   **Bloqueio** o cursor usa o nível mais baixo de bloqueio necessário para garantir que ele pode atualizar ou excluir linhas no conjunto de resultados. Isso geralmente resulta em níveis de simultaneidade muito baixa, especialmente em níveis de isolamento de transação Repeatable Read e Serializable.  
  
-   **Usando as versões de linha de simultaneidade otimista e simultaneidade otimista usando valores** o cursor usa a simultaneidade otimista: Ele atualiza ou exclui linhas somente se eles não foram alterados desde que eles foram lidos pela última vez. Para detectar alterações, ele compara as versões de linha ou valores. Não há nenhuma garantia de que o cursor será possível atualizar ou excluir uma linha, mas a simultaneidade for muito maior do que quando o bloqueio é usado. Para obter mais informações, consulte a seção a seguir, [simultaneidade otimista](../../../odbc/reference/develop-app/optimistic-concurrency.md).  
  
 Um aplicativo especifica qual tipo de simultaneidade ele deseja que o cursor a ser usado com o atributo de instrução SQL_ATTR_CONCURRENCY. Para determinar quais tipos têm suporte, ele chama **SQLGetInfo** com a opção SQL_SCROLL_CONCURRENCY.

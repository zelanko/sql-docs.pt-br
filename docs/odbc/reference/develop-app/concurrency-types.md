---
title: Tipos de simultaneidade | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
- locking concurrency control [ODBC]
- optimistic concurrency [ODBC]
- read-only concurrency control [ODBC]
ms.assetid: 46762ae5-17dd-4777-968e-58156f470fe1
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 737fadc881109457051cf30bfce9b493bd164f1c
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="concurrency-types"></a>Tipos de simultaneidade
Para resolver o problema de redução de simultaneidade em cursores, ODBC expõe quatro tipos diferentes de simultaneidade do cursor:  
  
-   **Somente leitura** o cursor pode ler os dados, mas não é possível atualizar ou excluir dados. Esse é o tipo de simultaneidade padrão. Embora o DBMS poderão bloquear linhas para impor os níveis de isolamento serializável e leitura repetida, ele pode usar bloqueios de leitura em vez de bloqueios de gravação. Isso resulta em maior simultaneidade porque outras transações, pelo menos, podem ler os dados.  
  
-   **Bloqueio** o cursor usa o nível mais baixo de bloqueio necessário certificar-se de que ele pode atualizar ou excluir linhas no conjunto de resultados. Geralmente, isso resulta em níveis de simultaneidade muito baixa, especialmente nos níveis de isolamento de transação Repeatable Read e Serializable.  
  
-   **Simultaneidade otimista usando versões de linha e simultaneidade otimista usando valores** o cursor usa a simultaneidade otimista: atualizar ou excluir linhas apenas se eles não foram alterados desde a última foram lidas. Para detectar alterações, ele compara valores ou versões de linha. Não há nenhuma garantia de que o cursor será capaz de atualizar ou excluir uma linha, mas a simultaneidade é muito maior do que quando o bloqueio é usado. Para obter mais informações, consulte a seção a seguir, [simultaneidade otimista](../../../odbc/reference/develop-app/optimistic-concurrency.md).  
  
 Um aplicativo especifica o tipo de simultaneidade que deseja que o cursor a ser usado com o atributo de instrução SQL_ATTR_CONCURRENCY. Para determinar quais tipos têm suporte, ele chama **SQLGetInfo** com a opção SQL_SCROLL_CONCURRENCY.


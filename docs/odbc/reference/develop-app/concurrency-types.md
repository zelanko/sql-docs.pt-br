---
title: Tipos de simultaneidade | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
manager: craigg
ms.openlocfilehash: 6b5970995d3b8f881b62556b0f12eac96d302760
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32911851"
---
# <a name="concurrency-types"></a>Tipos de simultaneidade
Para resolver o problema de redução de simultaneidade em cursores, ODBC expõe quatro tipos diferentes de simultaneidade do cursor:  
  
-   **Somente leitura** o cursor pode ler os dados, mas não é possível atualizar ou excluir dados. Esse é o tipo de simultaneidade padrão. Embora o DBMS poderão bloquear linhas para impor os níveis de isolamento serializável e leitura repetida, ele pode usar bloqueios de leitura em vez de bloqueios de gravação. Isso resulta em maior simultaneidade porque outras transações, pelo menos, podem ler os dados.  
  
-   **Bloqueio** o cursor usa o nível mais baixo de bloqueio necessário certificar-se de que ele pode atualizar ou excluir linhas no conjunto de resultados. Geralmente, isso resulta em níveis de simultaneidade muito baixa, especialmente nos níveis de isolamento de transação Repeatable Read e Serializable.  
  
-   **Simultaneidade otimista usando versões de linha e simultaneidade otimista usando valores** o cursor usa a simultaneidade otimista: atualizar ou excluir linhas apenas se eles não foram alterados desde a última foram lidas. Para detectar alterações, ele compara valores ou versões de linha. Não há nenhuma garantia de que o cursor será capaz de atualizar ou excluir uma linha, mas a simultaneidade é muito maior do que quando o bloqueio é usado. Para obter mais informações, consulte a seção a seguir, [simultaneidade otimista](../../../odbc/reference/develop-app/optimistic-concurrency.md).  
  
 Um aplicativo especifica o tipo de simultaneidade que deseja que o cursor a ser usado com o atributo de instrução SQL_ATTR_CONCURRENCY. Para determinar quais tipos têm suporte, ele chama **SQLGetInfo** com a opção SQL_SCROLL_CONCURRENCY.

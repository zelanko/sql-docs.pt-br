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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 642301d09c5aa189276db534e58aca0c5e00e3ce
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299096"
---
# <a name="concurrency-types"></a>Tipos de simultaneidade
Para resolver o problema de simultaneidade reduzida em cursores, o ODBC expõe quatro tipos diferentes de simultaneidade do cursor:  
  
-   **Somente leitura** O cursor pode ler dados, mas não pode atualizar ou excluir dados. Esse é o tipo de simultaneidade padrão. Embora o DBMS possa bloquear linhas para impor os níveis de isolamento de leitura e serializáveis repetíveis, ele pode usar bloqueios de leitura em vez de bloqueios de gravação. Isso resulta em uma simultaneidade maior porque outras transações podem, pelo menos, ler os dados.  
  
-   **Bloqueio** O cursor usa o nível mais baixo de bloqueio necessário para garantir que ele possa atualizar ou excluir linhas no conjunto de resultados. Isso geralmente resulta em níveis de simultaneidade muito baixos, especialmente nos níveis de isolamento de transação de leitura e serializáveis repetidos.  
  
-   **Simultaneidade otimista usando versões de linha e simultaneidade otimista usando valores** O cursor usa simultaneidade otimista: atualiza ou exclui linhas somente se elas não tiverem sido alteradas desde a última leitura. Para detectar alterações, ele compara as versões de linha ou valores. Não há nenhuma garantia de que o cursor poderá atualizar ou excluir uma linha, mas a simultaneidade é muito maior do que quando o bloqueio é usado. Para obter mais informações, consulte a seção a seguir, [simultaneidade otimista](../../../odbc/reference/develop-app/optimistic-concurrency.md).  
  
 Um aplicativo especifica o tipo de simultaneidade que ele deseja que o cursor use com o atributo de instrução SQL_ATTR_CONCURRENCY. Para determinar quais tipos têm suporte, ele chama **SQLGetInfo** com a opção SQL_SCROLL_CONCURRENCY.

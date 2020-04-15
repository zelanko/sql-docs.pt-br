---
title: Tipos de Concorrência | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299096"
---
# <a name="concurrency-types"></a>Tipos de simultaneidade
Para resolver o problema da concorrência reduzida em cursores, o ODBC expõe quatro tipos diferentes de concorrência cursor:  
  
-   **Somente leitura** O cursor pode ler dados, mas não pode atualizar ou excluir dados. Este é o tipo de concorrência padrão. Embora o DBMS possa bloquear linhas para impor os níveis de isolamento repetitivo de leitura e serializável, ele pode usar bloqueios de leitura em vez de bloqueios de gravação. Isso resulta em maior concorrência porque outras transações podem pelo menos ler os dados.  
  
-   **Bloqueio** O cursor usa o nível mais baixo de bloqueio necessário para garantir que ele possa atualizar ou excluir linhas no conjunto de resultados. Isso geralmente resulta em níveis de concorrência muito baixos, especialmente nos níveis de isolamento de transações de leitura e serializável repetíveis.  
  
-   **Concorrência otimista usando versões de linha e simultâneos otimistas usando valores** O cursor usa uma concorrência otimista: ele atualiza ou exclui linhas somente se não tiverem sido alteradas desde que foram lidas pela última vez. Para detectar alterações, ele compara versões ou valores de linha. Não há garantia de que o cursor será capaz de atualizar ou excluir uma linha, mas a concorrência é muito maior do que quando o bloqueio é usado. Para obter mais informações, consulte a seção a seguir, [Optimistic Concurrency](../../../odbc/reference/develop-app/optimistic-concurrency.md).  
  
 Um aplicativo especifica que tipo de simultâneo deseja que o cursor use com o atributo de declaração SQL_ATTR_CONCURRENCY. Para determinar quais tipos são suportados, ele chama **SQLGetInfo** com a opção SQL_SCROLL_CONCURRENCY.

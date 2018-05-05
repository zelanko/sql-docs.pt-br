---
title: Tipos de Cursor rolável | Microsoft Docs
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
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: dbd32576-0453-4e90-ae45-1a81cee8259d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 54acbd1010d546649b1ad92a34289fa4d04da162
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="scrollable-cursor-types"></a>Tipos de Cursor rolável
Os quatro tipos de cursores roláveis são estático, dinâmico, controlado por e misto. Cursores estáticos detectam poucas ou nenhuma alteração, mas são relativamente baratos implementar. Cursores dinâmicos detectam todas as alterações, mas são caros implementar. Cursores controlados por conjunto de chaves e mistos se encontra a média, detectando a maioria das alterações, mas com menos despesas que cursores dinâmicos.  
  
 Os seguintes termos são usados para definir as características de cada tipo de cursor rolável:  
  
-   **Possuir as inserções, atualizações e exclusões.** Atualizações, exclusões e inserções feitas por meio do cursor, com uma chamada para **SQLBulkOperations** ou **SQLSetPos** ou com um posicionadas instrução update ou delete.  
  
-   **Outros atualiza, exclui e insere.** Atualizações, exclusões e inserções não são feitas pelo cursor, incluindo aquelas feitas por outras operações na mesma transação, feitas por meio de outras transações e as feitas por outros aplicativos.  
  
-   **Associação.** O conjunto de linhas no conjunto de resultados.  
  
-   **Ordem.** A ordem na qual as linhas são retornadas pelo cursor.  
  
-   **valores.** Os valores em cada linha no conjunto de resultados.  
  
 Para obter informações sobre como atualizar, excluir e inserir dados, consulte [visão geral de atualização de dados](../../../odbc/reference/develop-app/updating-data-overview.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Cursores estáticos ODBC](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [Cursores dinâmicos ODBC](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [Cursores controlados por conjunto de chaves](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [Cursores mistos](../../../odbc/reference/develop-app/mixed-cursors.md)

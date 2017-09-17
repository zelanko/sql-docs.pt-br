---
title: "Tipos de Cursor rolável | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: dbd32576-0453-4e90-ae45-1a81cee8259d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 234da7bb8519149c78779f7920333338737b394b
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="scrollable-cursor-types"></a>Tipos de Cursor rolável
Os quatro tipos de cursores roláveis são estático, dinâmico, controlado por e misto. Cursores estáticos detectam poucas ou nenhuma alteração, mas são relativamente baratos implementar. Cursores dinâmicos detectam todas as alterações, mas são caros implementar. Cursores controlados por conjunto de chaves e mistos se encontra a média, detectando a maioria das alterações, mas com menos despesas que cursores dinâmicos.  
  
 Os seguintes termos são usados para definir as características de cada tipo de cursor rolável:  
  
-   **Possuir as inserções, atualizações e exclusões.** Atualizações, exclusões e inserções feitas por meio do cursor, com uma chamada para **SQLBulkOperations** ou **SQLSetPos** ou com um posicionadas instrução update ou delete.  
  
-   **Outros atualiza, exclui e insere.** Atualizações, exclusões e inserções não são feitas pelo cursor, incluindo aquelas feitas por outras operações na mesma transação, feitas por meio de outras transações e as feitas por outros aplicativos.  
  
-   **Associação.** O conjunto de linhas no conjunto de resultados.  
  
-   **Ordem.** A ordem na qual as linhas são retornadas pelo cursor.  
  
-   **Os valores.** Os valores em cada linha no conjunto de resultados.  
  
 Para obter informações sobre como atualizar, excluir e inserir dados, consulte [visão geral de atualização de dados](../../../odbc/reference/develop-app/updating-data-overview.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Cursores estáticos ODBC](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [Cursores dinâmicos ODBC](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [Cursores controlados por conjunto de chaves](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [Cursores mistos](../../../odbc/reference/develop-app/mixed-cursors.md)

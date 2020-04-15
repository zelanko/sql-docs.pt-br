---
title: Tipos de cursor roláveis | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: dbd32576-0453-4e90-ae45-1a81cee8259d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 63f29269ea209875a2e775cf8d523302fcb9a976
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304227"
---
# <a name="scrollable-cursor-types"></a>Tipos de cursor rolável
Os quatro tipos de cursores roláveis são estáticos, dinâmicos, orientados por keysets e misturados. Os cursores estáticos detectam poucas ou nenhuma alteração, mas são relativamente baratos de implementar. Os cursores dinâmicos detectam todas as alterações, mas são caros de implementar. Os cursores mistos e orientados por keyset estão entre eles, detectando a maioria das alterações, mas a menos gastos do que os cursores dinâmicos.  
  
 Os seguintes termos são usados para definir as características de cada tipo de cursor rolável:  
  
-   **Próprioatualizas, exclusões e inserções.** Atualizações, exclusões e inserções feitas através do cursor, seja com uma chamada para **SQLBulkOperations** ou **SQLSetPos** ou com uma instrução de atualização posicionada ou exclusão.  
  
-   **Outras atualizações, exclusões e inserções.** Atualizações, exclusões e inserções não feitas pelo cursor, incluindo as feitas por outras operações na mesma transação, aquelas feitas através de outras transações, e aquelas feitas por outros aplicativos.  
  
-   **Associação.** O conjunto de linhas no conjunto de resultados.  
  
-   **Ordem.** A ordem em que as linhas são devolvidas pelo cursor.  
  
-   **Valores.** Os valores em cada linha no conjunto de resultados.  
  
 Para obter informações sobre como atualizar, excluir e inserir dados, consulte [Visão geral de dados atualizado](../../../odbc/reference/develop-app/updating-data-overview.md).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Cursores estáticos ODBC](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [Cursores dinâmicos ODBC](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [Cursores controlados por conjunto de chaves](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [Cursores mistos](../../../odbc/reference/develop-app/mixed-cursors.md)

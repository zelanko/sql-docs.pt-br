---
title: Tipos de cursor rolável | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304227"
---
# <a name="scrollable-cursor-types"></a>Tipos de cursor rolável
Os quatro tipos de cursores roláveis são estáticos, dinâmicos, controlados por conjunto de chaves e mistos. Cursores estáticos detectam algumas ou nenhuma alteração, mas são relativamente baratos de implementar. Cursores dinâmicos detectam todas as alterações, mas são caros de implementar. Cursores mistos e controlados por conjunto de chaves estão entre, detectando a maioria das alterações, mas com menos despesas do que cursores dinâmicos.  
  
 Os termos a seguir são usados para definir as características de cada tipo de cursor rolável:  
  
-   **Próprias atualizações, exclusões e inserções.** Atualizações, exclusões e inserções feitas por meio do cursor, seja com uma chamada para **SQLBulkOperations** ou **SQLSetPos** ou com uma instrução UPDATE ou DELETE posicionada.  
  
-   **Outras atualizações, exclusões e inserções.** Atualizações, exclusões e inserções não feitas pelo cursor, incluindo aquelas feitas por outras operações na mesma transação, aquelas feitas por meio de outras transações e as feitas por outros aplicativos.  
  
-   **Participante.** O conjunto de linhas no conjunto de resultados.  
  
-   **Ordene.** A ordem na qual as linhas são retornadas pelo cursor.  
  
-   **Os.** Os valores em cada linha no conjunto de resultados.  
  
 Para obter informações sobre como atualizar, excluir e inserir dados, consulte [visão geral de atualização de dados](../../../odbc/reference/develop-app/updating-data-overview.md).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Cursores estáticos ODBC](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [Cursores dinâmicos ODBC](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [Cursores controlados por conjunto de chaves](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [Cursores mistos](../../../odbc/reference/develop-app/mixed-cursors.md)

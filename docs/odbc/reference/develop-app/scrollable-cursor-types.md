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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 210b66a800670f033508f903b18778f88ddd4c8b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68061631"
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
  
 Esta seção contém os seguintes tópicos:  
  
-   [Cursores estáticos ODBC](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [Cursores dinâmicos ODBC](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [Cursores controlados por conjunto de chaves](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [Cursores mistos](../../../odbc/reference/develop-app/mixed-cursors.md)

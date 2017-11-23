---
title: "Recuperando resultados (avançados) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- offsets [ODBC]
- result sets [ODBC], about result sets
- bind offsets [ODBC]
ms.assetid: bc00c379-71a7-407a-975c-898243f39bb6
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0f669180407ed626ae9235bd666068b6889060b8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="retrieving-results-advanced"></a>Recuperando resultados (avançados)
Um aplicativo pode especificar que um deslocamento é adicionado ao associados a endereços de buffer de dados e o comprimento/indicador correspondente buffer endereços quando **SQLBulkOperations**, **SQLFetch**,  **SQLFetchScroll**, ou **SQLSetPos** é chamado. Os resultados dessas adições determinam os endereços usados nessas operações.  
  
 Deslocamentos de ligação permitem que um aplicativo alterar associações sem chamar **SQLBindCol** para colunas associadas anteriormente. Uma chamada para **SQLBindCol** associar novamente dados altera o endereço do buffer e o ponteiro de comprimento/indicador. Reassociação com um deslocamento, por outro lado, simplesmente adiciona um deslocamento para o endereço existente de buffer de dados associados e o endereço do buffer de comprimento/indicador. Quando os deslocamentos são usados, as associações são um "modelo" de como os buffers de aplicativo são dispostos e o aplicativo pode mover esta "template" para diferentes áreas de memória, alterando o deslocamento. Um novo deslocamento pode ser especificado a qualquer momento e sempre é adicionado para os valores de limite originalmente.  
  
 Para especificar um deslocamento de associação, o aplicativo define o atributo de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR para o endereço de um buffer sqlinteger que contém. Antes do aplicativo chama uma função que usa as associações, como **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, ou **SQLSetPos**, coloca um deslocamento em bytes nesse buffer, como o endereço do buffer de dados, nem o endereço do buffer de comprimento/indicador é 0, e como a coluna associada está no conjunto de resultados. A soma do endereço e o deslocamento deve ser um endereço válido. (Isso significa que um ou ambos os o deslocamento e o endereço para o qual o deslocamento é adicionado podem ser inválidas, como soma é um endereço válido). O atributo da instrução SQL_ATTR_ROW_BIND_OFFSET_PTR é um ponteiro para que o valor de deslocamento pode ser aplicado mais de um conjunto de associação de dados, que pode ser alterado por meio da alteração de um valor de deslocamento. Um aplicativo deve se certificar de que o ponteiro permanece válido até que o cursor seja fechado.  
  
> [!NOTE]  
>  Deslocamentos de associação não são suportados pelo ODBC 2. *x* drivers.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Cursores em bloco](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [Cursores roláveis](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [A biblioteca de cursores ODBC](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [Vários resultados](../../../odbc/reference/develop-app/multiple-results.md)

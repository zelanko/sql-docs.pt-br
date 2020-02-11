---
title: Recuperando resultados (avançado) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- offsets [ODBC]
- result sets [ODBC], about result sets
- bind offsets [ODBC]
ms.assetid: bc00c379-71a7-407a-975c-898243f39bb6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22a88a96b856ba0976dcb8600d26f78b772654bd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020498"
---
# <a name="retrieving-results-advanced"></a>Recuperar resultados (avançado)
Um aplicativo pode especificar que um deslocamento seja adicionado aos endereços de buffer de dados vinculados e os endereços de buffer de comprimento/indicador correspondentes quando **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**ou **SQLSetPos** for chamado. Os resultados dessas adições determinam os endereços usados nessas operações.  
  
 Os deslocamentos de ligação permitem que um aplicativo altere as associações sem chamar **SQLBindCol** para colunas associadas anteriormente. Uma chamada para **SQLBindCol** para reassociar dados altera o endereço de buffer e o ponteiro de comprimento/indicador. A reassociação com um deslocamento, por outro lado, simplesmente adiciona um deslocamento ao endereço do buffer de dados vinculado existente e ao endereço do buffer de comprimento/indicador. Quando os deslocamentos são usados, as associações são um "modelo" de como os buffers de aplicativo são dispostos e o aplicativo pode mover esse "modelo" para diferentes áreas de memória alterando o deslocamento. Um novo deslocamento pode ser especificado a qualquer momento e sempre é adicionado aos valores associados originalmente.  
  
 Para especificar um deslocamento de ligação, o aplicativo define o atributo SQL_ATTR_ROW_BIND_OFFSET_PTR instrução como o endereço de um buffer sqlinteiro. Antes que o aplicativo chame uma função que usa as associações, como **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**ou **SQLSetPos**, ele coloca um deslocamento em bytes nesse buffer, desde que nem o endereço do buffer de dados nem o endereço do buffer de comprimento/indicador seja 0 e, desde que a coluna associada esteja no conjunto de resultados. A soma do endereço e o deslocamento devem ser um endereço válido. (Isso significa que ou tanto o deslocamento quanto o endereço para o qual o deslocamento é adicionado podem ser inválidos, desde que sua soma seja um endereço válido.) O atributo de instrução SQL_ATTR_ROW_BIND_OFFSET_PTR é um ponteiro para que o valor de deslocamento possa ser aplicado a mais de um conjunto de dados de associação, que podem ser alterados alterando-se um valor de deslocamento. Um aplicativo deve garantir que o ponteiro permaneça válido até que o cursor seja fechado.  
  
> [!NOTE]  
>  Os deslocamentos de ligação não são suportados pelo ODBC 2. drivers *x* .  
  
 Esta seção contém os seguintes tópicos:  
  
-   [Cursores em bloco](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [Cursores roláveis](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [A biblioteca de cursores ODBC](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [Vários resultados](../../../odbc/reference/develop-app/multiple-results.md)

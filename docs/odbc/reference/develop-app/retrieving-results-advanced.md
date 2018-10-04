---
title: Recuperando resultados (Avançado) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 5199fb82cbc6b2a9da644554db12dc525cc0be40
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47693515"
---
# <a name="retrieving-results-advanced"></a>Recuperar resultados (avançado)
Um aplicativo pode especificar que um deslocamento é adicionado ao associados a endereços de buffer de dados e o comprimento/indicador correspondente buffer endereços quando **SQLBulkOperations**, **SQLFetch**,  **SQLFetchScroll**, ou **SQLSetPos** é chamado. Os resultados dessas adições determinam os endereços usados nessas operações.  
  
 Deslocamentos de ligação permitem que um aplicativo alterar associações sem chamar **SQLBindCol** para colunas associadas anteriormente. Uma chamada para **SQLBindCol** reassociar dados altera o endereço do buffer e o ponteiro de comprimento/indicador. Nova associação com um deslocamento, por outro lado, simplesmente adiciona um deslocamento para o endereço de buffer de dados ligada existente e o endereço do buffer de comprimento/indicador. Quando deslocamentos são usados, as associações são um "modelo" de como os buffers do aplicativo são dispostos e o aplicativo pode mover esse "modelo" para diferentes áreas de memória, alterando o deslocamento. Um novo deslocamento pode ser especificado a qualquer momento e sempre é adicionado para os valores de limite originalmente.  
  
 Para especificar um deslocamento de ligação, o aplicativo define o atributo da instrução SQL_ATTR_ROW_BIND_OFFSET_PTR para o endereço de um buffer sqlinteger que contém. Antes do aplicativo chama uma função que usa as associações, tais como **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, ou **SQLSetPos**, ele coloca um deslocamento em bytes nesse buffer, desde que nem o endereço do buffer de dados nem o endereço do buffer de comprimento/indicador for 0, e desde que a coluna associada está no conjunto de resultados. A soma do endereço e o deslocamento deve ser um endereço válido. (Isso significa que um ou ambos os o deslocamento e o endereço ao qual o deslocamento é adicionado podem ser inválidos, desde que sua soma é um endereço válido). O atributo da instrução SQL_ATTR_ROW_BIND_OFFSET_PTR é um ponteiro para que o valor de deslocamento pode ser aplicado a mais de um conjunto de associação de dados, que pode ser alterado ao alterar um valor de deslocamento. Um aplicativo deve se certificar de que o ponteiro permanece válido até que o cursor seja fechado.  
  
> [!NOTE]  
>  Deslocamentos de associação não são suportados pelo ODBC 2. *x* drivers.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Cursores em bloco](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [Cursores roláveis](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [A biblioteca de cursores ODBC](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [Vários resultados](../../../odbc/reference/develop-app/multiple-results.md)

---
title: Recuperando resultados (avançados) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca02b4ff911c8edff06b38d5341eeaa288cc194c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294636"
---
# <a name="retrieving-results-advanced"></a>Recuperar resultados (avançado)
Um aplicativo pode especificar que uma compensação é adicionada aos endereços de buffer de dados vinculados e aos endereços de buffer de comprimento/indicador correspondentes quando **sQLBulkOperations,** **SQLFetch,** **SQLFetchScroll**ou **SQLSetPos** são chamados. Os resultados dessas adições determinam os endereços utilizados nessas operações.  
  
 As compensações de vinculação permitem que um aplicativo altere as vinculações sem chamar **sqlBindCol** para colunas vinculadas anteriormente. Uma chamada para **sqlBindCol** para revincular dados altera o endereço buffer e o ponteiro comprimento/indicador. A revinculação com um deslocamento, por outro lado, simplesmente adiciona uma compensação ao endereço de buffer de dados vinculado existente e ao endereço buffer de comprimento/indicador existente. Quando as compensações são usadas, as vinculações são um "modelo" de como os buffers do aplicativo são definidos e o aplicativo pode mover esse "modelo" para diferentes áreas de memória alterando o deslocamento. Um novo deslocamento pode ser especificado a qualquer momento e é sempre adicionado aos valores originalmente vinculados.  
  
 Para especificar uma compensação de vinculação, o aplicativo define o atributo de declaração SQL_ATTR_ROW_BIND_OFFSET_PTR para o endereço de um buffer SQLINTEGER. Antes que o aplicativo chame uma função que usa as vinculações, como **SQLBulkOperations,** **SQLFetch,** **SQLFetchScroll**ou **SQLSetPos,** ele coloca uma compensação em bytes neste buffer, desde que nem o endereço de buffer de dados nem o endereço buffer de comprimento/indicador seja 0, e enquanto a coluna vinculada estiver no conjunto de resultados. A soma do endereço e do deslocamento deve ser um endereço válido. (Isso significa que tanto o deslocamento quanto o endereço ao qual o deslocamento é adicionado podem ser inválidos, desde que sua soma seja um endereço válido.) O SQL_ATTR_ROW_BIND_OFFSET_PTR atributo de declaração é um ponteiro para que o valor de deslocamento possa ser aplicado a mais de um conjunto de dados vinculativos, todos os quais podem ser alterados alterando um valor de deslocamento. Um aplicativo deve certificar-se de que o ponteiro permanece válido até que o cursor esteja fechado.  
  
> [!NOTE]  
>  As compensações de vinculação não são suportadas pelo ODBC 2. *x* drivers.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Cursores em bloco](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [Cursors roláveis](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [A biblioteca de cursores ODBC](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [Vários resultados](../../../odbc/reference/develop-app/multiple-results.md)

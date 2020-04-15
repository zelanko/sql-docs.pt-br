---
title: Cursors de bloco, cursores roláveis e compatibilidade retrógrada | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: d9d271f6-d2d9-49b9-a365-4909ca06caae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe24362f1a49577a7fb494f768947080d0ab6e9e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292306"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>Cursores em bloco, cursores roláveis e compatibilidade com versões anteriores
A existência tanto do **SQLFetchScroll** quanto **do SQLExtendedFetch** representa a primeira divisão clara no ODBC entre a API (Application Programming Interface, interface de programação de aplicativos), que é o conjunto de funções que as chamadas de aplicativos e a Interface do Provedor de Serviços (SPI), que é o conjunto de funções que o driver implementa. Essa divisão é necessária para que o ODBC *3.x*, que usa **SQLFetchScroll,** seja alinhado com as normas e também seja compatível com o ODBC *2.x*, que usa **SQLExtendedFetch**.  
  
 A API ODBC *3.x,* que é o conjunto de funções que as chamadas do aplicativo chamam, inclui **SQLFetchScroll** e atributos de declaração relacionados. O ODBC *3.x* SPI, que é o conjunto de funções que o driver implementa, inclui **SQLFetchScroll,** **SQLExtendedFetch**e atributos de declaração relacionados. Como o ODBC não aplica formalmente essa divisão entre a API e o SPI, é possível que os aplicativos ODBC *3.x* chamem **sqlExtendedFetch** e atributos de declaração relacionados. No entanto, não há razão para a aplicação ODBC *3.x* fazer isso. Para obter mais informações sobre APIs e SPIs, consulte a introdução da [Arquitetura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Para obter informações sobre quais funções e atributos de declaração um aplicativo ODBC *3.x* deve usar com cursores de bloco e roláveis, consulte [Cursors de bloco, cursors roláveis e compatibilidade retrógrada para aplicações ODBC 3.x](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [O que o Gerenciador de Driver faz](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [O que o driver faz](../../../odbc/reference/appendixes/what-the-driver-does.md)

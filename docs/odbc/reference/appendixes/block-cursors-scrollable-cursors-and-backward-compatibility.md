---
title: Cursores de bloco, cursores roláveis e compatibilidade com versões anteriores | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292306"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>Cursores em bloco, cursores roláveis e compatibilidade com versões anteriores
A existência de **SQLFetchScroll** e **SQLExtendedFetch** representa a primeira divisão clara em ODBC entre a API (interface de programação de aplicativo), que é o conjunto de funções que o aplicativo chama e a SPI (interface do provedor de serviços), que é o conjunto de funções que o Driver implementa. Essa divisão é necessária para que o ODBC *3. x*, que usa **SQLFetchScroll**, se alinhe com os padrões e também seja compatível com ODBC *2. x*, que usa **SQLExtendedFetch**.  
  
 A API ODBC *3. x* , que é o conjunto de funções que o aplicativo chama, inclui **SQLFetchScroll** e atributos de instrução relacionados. O SPI ODBC *3. x* , que é o conjunto de funções que o Driver implementa, inclui **SQLFetchScroll**, **SQLExtendedFetch**e atributos de instrução relacionados. Como o ODBC não impõe formalmente essa divisão entre a API e o SPI, é possível que os aplicativos ODBC *3. x* chamem **SQLExtendedFetch** e atributos de instrução relacionados. No entanto, não há motivo para o aplicativo ODBC *3. x* fazer isso. Para obter mais informações sobre APIs e SPIs, consulte a introdução à [arquitetura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Para obter informações sobre quais funções e atributos de instrução um aplicativo ODBC *3. x* deve usar com cursores de bloqueio e rolagem, consulte [cursores de bloco, cursores roláveis e compatibilidade com versões anteriores para aplicativos ODBC 3. x](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [O que o Gerenciador de Driver faz](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [O que o driver faz](../../../odbc/reference/appendixes/what-the-driver-does.md)

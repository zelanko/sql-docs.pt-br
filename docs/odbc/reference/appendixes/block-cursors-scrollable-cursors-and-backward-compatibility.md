---
title: "Bloquear cursores, cursores roláveis e compatibilidade com versões anteriores | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], backward compatibility
- compatibility [ODBC], cursors
- backward compatibility [ODBC], cursors
- block cursors [ODBC]
ms.assetid: d9d271f6-d2d9-49b9-a365-4909ca06caae
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 00e83e48a76e3c9159b50eb63fe4aec657baf928
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>Cursores em bloco, cursores roláveis e compatibilidade com versões anteriores
A existência de ambos **SQLFetchScroll** e **SQLExtendedFetch** representa o primeiro clear dividido em ODBC entre o aplicativo de Interface de programação (API), que é o conjunto de funções de chamadas de aplicativo e o serviço de provedor de Interface (IDA), que é o conjunto de funções implementa o driver. Essa divisão é necessário para que ODBC 3. *x*, que usa **SQLFetchScroll**, bealigned com os padrões e também ser compatível com ODBC 2. *x*, que usa **SQLExtendedFetch**.  
  
 O ODBC 3*. x* API, que é o conjunto de funções de aplicativo chama, inclui **SQLFetchScroll** e relacionados a atributos de instrução. O ODBC 3*. x* ida, que é o conjunto de funções o driver implementa, inclui **SQLFetchScroll**, **SQLExtendedFetch**e os atributos de instrução relacionados. Como o ODBC não impõe essa divisão entre a API e o IDA formalmente, é possível para o ODBC 3*. x* aplicativos chamar **SQLExtendedFetch** e relacionados a atributos de instrução. No entanto, não há nenhum motivo para ODBC 3*. x* aplicativo para fazer isso. Para obter mais informações sobre as APIs e SPIs, consulte a introdução [arquitetura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Para obter informações sobre quais funções e a instrução de atributos um ODBC 3. *x* aplicativo deve usar com o bloco e cursores roláveis, consulte [cursores em bloco, cursores roláveis e compatibilidade com versões anteriores para os aplicativos ODBC 3. x](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [O que o Gerenciador de Driver faz](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [O que o driver faz](../../../odbc/reference/appendixes/what-the-driver-does.md)

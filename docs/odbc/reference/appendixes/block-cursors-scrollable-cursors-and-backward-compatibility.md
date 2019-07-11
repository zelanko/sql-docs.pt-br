---
title: Cursores em bloco, cursores roláveis e compatibilidade com versões anteriores | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 66b4cf0ce2b2ffc15a9e450461021a9b20b1f0c3
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794130"
---
# <a name="block-cursors-scrollable-cursors-and-backward-compatibility"></a>Cursores em bloco, cursores roláveis e compatibilidade com versões anteriores
A existência de ambos **SQLFetchScroll** e **SQLExtendedFetch** representa o limpar primeiro dividido entre o aplicativo de Interface de programação (API), que é o conjunto de funções ODBC a chamadas do aplicativo e o Service Provider Interface (SPI), que é o conjunto de funções implementa o driver. Essa divisão é necessário para que ODBC *3.x*, que usa **SQLFetchScroll**, bealigned com os padrões e também ser compatível com ODBC *2.x*, que usa **SQLExtendedFetch**.  
  
 O ODBC *3.x* API, que é o conjunto de funções o aplicativo chama, inclui **SQLFetchScroll** e relacionados a atributos de instrução. O ODBC *3.x* SPI, que é o conjunto de funções o driver implementa, inclui **SQLFetchScroll**, **SQLExtendedFetch**e relacionados a atributos de instrução. Como o ODBC não impõe formalmente essa divisão entre a API e o SPI, é possível para ODBC *3.x* aplicativos chamem **SQLExtendedFetch** e relacionados a atributos de instrução. No entanto, não há nenhum motivo para ODBC *3.x* aplicativo para fazer isso. Para obter mais informações sobre as APIs e SPIs, consulte a introdução [arquitetura ODBC](../../../odbc/reference/odbc-architecture.md).  
  
 Para obter informações sobre quais funções e a instrução atributos ODBC *3.x* aplicativo deve usar com o bloco e cursores roláveis, consulte [cursores em bloco, cursores roláveis e compatibilidade com versões anteriores para ODBC 3. x Aplicativos](../../../odbc/reference/develop-app/block-cursors-scrollable-backward-compatibility-odbc-3-x-applications.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [O que o Gerenciador de Driver faz](../../../odbc/reference/appendixes/what-the-driver-manager-does.md)  
  
-   [O que o driver faz](../../../odbc/reference/appendixes/what-the-driver-does.md)

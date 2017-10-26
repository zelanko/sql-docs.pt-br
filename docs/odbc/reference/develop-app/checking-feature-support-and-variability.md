---
title: Verificando o suporte ao recurso e a variabilidade | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: ff45f220-9b8b-4c44-82f8-a8e9913fffea
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5528f451adf12d12fe5cdb1c51f5c5d0053c9145
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="checking-feature-support-and-variability"></a>Suporte ao recurso de verificação e variabilidade
Para verificar o suporte ao recurso e a variabilidade, os aplicativos geralmente chamar **SQLGetInfo**, **SQLGetFunctions**, e **SQLGetTypeInfo**. Um bom ponto de partida é níveis de conformidade de gramática SQL e de API do driver. Eles descrevem amplo níveis de suporte ao recurso. O aplicativo pode chamar **SQLGetInfo** com outras opções para determinar o suporte ou variação dos recursos de que precisa, **SQLGetFunctions** para determinar se as funções ele precisa além retornado há suporte para o nível de conformidade, e **SQLGetTypeInfo** para determinar quais tipos de dados SQL têm suporte.  
  
 Um aplicativo pode determinar se um atributo de instrução ou conexão tem suporte chamando **SQLSetStmtAttr** ou **SQLSetConnectAttr** com esse atributo. Se a função retornará SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, há suporte para o atributo; Se ele retornar SQL_ERROR e SQLSTATE HYC00 (recurso opcional não implementado), não há suporte para o atributo.  
  
 Aplicativos também podem determinar uma quantidade limitada de informações antes de se conectar ao driver chamando **SQLDrivers**.


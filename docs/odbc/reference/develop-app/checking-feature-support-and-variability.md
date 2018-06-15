---
title: Verificando o suporte ao recurso e a variabilidade | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: ff45f220-9b8b-4c44-82f8-a8e9913fffea
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2dfea013336a98ab4e69adf79198692e336acfd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909321"
---
# <a name="checking-feature-support-and-variability"></a>Suporte ao recurso de verificação e variabilidade
Para verificar o suporte ao recurso e a variabilidade, os aplicativos geralmente chamar **SQLGetInfo**, **SQLGetFunctions**, e **SQLGetTypeInfo**. Um bom ponto de partida é níveis de conformidade de gramática SQL e de API do driver. Eles descrevem amplo níveis de suporte ao recurso. O aplicativo pode chamar **SQLGetInfo** com outras opções para determinar o suporte ou variação dos recursos de que precisa, **SQLGetFunctions** para determinar se as funções ele precisa além retornado há suporte para o nível de conformidade, e **SQLGetTypeInfo** para determinar quais tipos de dados SQL têm suporte.  
  
 Um aplicativo pode determinar se um atributo de instrução ou conexão tem suporte chamando **SQLSetStmtAttr** ou **SQLSetConnectAttr** com esse atributo. Se a função retornará SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, há suporte para o atributo; Se ele retornar SQL_ERROR e SQLSTATE HYC00 (recurso opcional não implementado), não há suporte para o atributo.  
  
 Aplicativos também podem determinar uma quantidade limitada de informações antes de se conectar ao driver chamando **SQLDrivers**.

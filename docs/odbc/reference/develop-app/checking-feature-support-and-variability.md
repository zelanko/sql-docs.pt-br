---
title: Verificando o suporte e a variabilidade do recurso | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], feature support and variability
- interoperability [ODBC], writing interoperable applications
- feature support in interoperable applications [ODBC]
- feature variability in interoperable applications [ODBC]
ms.assetid: ff45f220-9b8b-4c44-82f8-a8e9913fffea
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47f16160c05d1c410e3889f0bb857befe88df5b3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299166"
---
# <a name="checking-feature-support-and-variability"></a>Verificar o suporte ao recurso e a variabilidade
Para verificar o suporte e a variabilidade do recurso, os aplicativos geralmente chamam **SQLGetInfo**, **SQLGetFunctions**e **SQLGetTypeInfo**. Um bom ponto de partida é a API do driver e os níveis de conformidade da gramática do SQL. Elas descrevem níveis amplos de suporte a recursos. O aplicativo pode então chamar **SQLGetInfo** com outras opções para determinar o suporte ou a variabilidade dos recursos de que precisa, **SQLGetFunctions** para determinar se as funções necessárias além do nível de conformidade retornado têm suporte e **SQLGetTypeInfo** para determinar quais tipos de dados SQL têm suporte.  
  
 Um aplicativo pode determinar se há suporte para uma instrução ou um atributo de conexão chamando **SQLSetStmtAttr** ou **SQLSetConnectAttr** com esse atributo. Se a função retornar SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o atributo terá suporte; Se ele retornar SQL_ERROR e SQLSTATE HYC00 (recurso opcional não implementado), não haverá suporte para o atributo.  
  
 Os aplicativos também podem determinar uma quantidade limitada de informações antes de se conectar ao driver chamando **SQLDrivers**.

---
title: Verificando suporte e variabilidade de recursos | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299166"
---
# <a name="checking-feature-support-and-variability"></a>Verificar o suporte ao recurso e a variabilidade
Para verificar o suporte e a variabilidade dos recursos, os aplicativos geralmente chamam **SQLGetInfo,** **SQLGetFunctions**e **SQLGetTypeInfo**. Um bom local de partida são os níveis de conformidade de api e gramática SQL do driver. Estes descrevem níveis amplos de suporte a recursos. O aplicativo pode então chamar **o SQLGetInfo** com outras opções para determinar o suporte ou a variabilidade dos recursos **necessários, o SQLGetFunctions** para determinar se as funções que ele precisa além do nível de conformidade retornada são suportadas e **o SQLGetTypeInfo** para determinar quais tipos de dados SQL são suportados.  
  
 Um aplicativo pode determinar se um atributo de declaração ou conexão é suportado ligando para **SQLSetStmtAttr** ou **SQLSetConnectAttr** com esse atributo. Se a função retornar SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, o atributo será suportado; se retornar SQL_ERROR e SQLSTATE HYC00 (recurso opcional não implementado), o atributo não é suportado.  
  
 Os aplicativos também podem determinar uma quantidade limitada de informações antes de se conectar ao driver ligando para **SQLDrivers**.

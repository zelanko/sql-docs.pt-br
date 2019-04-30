---
title: Verificando o suporte ao recurso e variabilidade | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b9af2cfd73556baca4870428cdcdfcee3e07191d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63217615"
---
# <a name="checking-feature-support-and-variability"></a>Verificar o suporte ao recurso e a variabilidade
Para verificar o suporte ao recurso e variabilidade, os aplicativos geralmente chamar **SQLGetInfo**, **SQLGetFunctions**, e **SQLGetTypeInfo**. Um bom ponto de partida é níveis de conformidade de gramática SQL e a API do driver. Eles descrevem amplos níveis de suporte ao recurso. O aplicativo pode, em seguida, chamar **SQLGetInfo** com outras opções para determinar o suporte ou variação dos recursos que precisa, **SQLGetFunctions** para determinar se funções ele precisa além retornado há suporte para o nível de conformidade, e **SQLGetTypeInfo** para determinar quais tipos de dados SQL têm suporte.  
  
 Um aplicativo pode determinar se um atributo de instrução ou a conexão tem suporte por meio da chamada **SQLSetStmtAttr** ou **SQLSetConnectAttr** com esse atributo. Se a função retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO, há suporte para o atributo; Se ele retornar SQL_ERROR e SQLSTATE HYC00 (recurso opcional não implementado), não há suporte para o atributo.  
  
 Aplicativos também podem determinar uma quantidade limitada de informações antes de se conectar ao driver chamando **SQLDrivers**.

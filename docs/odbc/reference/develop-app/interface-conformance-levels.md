---
title: Níveis de conformidade de interface | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 2c470e54-0600-4b2b-b1f3-9885cb28a01a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fff555324746fcb92641126ddf11ea91ce5e3f89
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304596"
---
# <a name="interface-conformance-levels"></a>Níveis de conformidade de interface
O objetivo do nivelamento é informar o aplicativo quais recursos estão disponíveis para ele a partir do motorista. Um esquema de nivelamento baseado em funções não atinge suficientemente esse objetivo. Em ODBC 3. *x*, os drivers são classificados com base nas características que possuem. O suporte ao recurso pode incluir o suporte à função; ele também pode incluir o suporte a um campo descritor, um atributo de declaração, um valor "Y" para um tipo de informação retornado pelo **SQLGetInfo,** e assim por diante.  
  
 Para simplificar a especificação da conformidade de interface, o ODBC define três níveis de conformidade. Para atender a um determinado nível de conformidade, o motorista deve satisfazer todos os requisitos desse nível de conformidade. A conformidade com um determinado nível implica conformidade completa com todos os níveis inferiores.  
  
 Os níveis de conformidade nem sempre se dividem perfeitamente em suporte para uma lista específica de funções ODBC, mas especificam recursos suportados conforme listado nas seções a seguir. Para fornecer suporte a um recurso, um driver deve suportar algumas ou todas as formas de chamadas para determinadas funções ODBC (para obter mais informações, consulte [Conformidade de função),](../../../odbc/reference/develop-app/function-conformance.md)definindo certos atributos (ver [Conformidade de Atributos)](../../../odbc/reference/develop-app/attribute-conformance.md)e certos campos descritores (ver [Conformidade de Campo Descritor](../../../odbc/reference/develop-app/descriptor-field-conformance.md)).  
  
 O aplicativo descobre o nível de conformidade da interface do driver conectando-se a uma fonte de dados e ligando para **o SQLGetInfo** com a opção SQL_ODBC_INTERFACE_CONFORMANCE.  
  
 Os drivers são livres para implementar recursos além do nível ao qual eles reivindicam conformidade completa. Os aplicativos descobrem tais recursos adicionais ligando para **SQLGetFunctions** (para determinar quais funções oDBC estão presentes) e **SQLGetInfo** (para consultar vários outros recursos ODBC).  
  
 Existem três níveis de conformidade de interface ODBC: Núcleo, Nível 1 e Nível 2.  
  
> [!NOTE]
>  Esses níveis de conformidade têm requisitos diferentes dos níveis de conformidade da API ODBC de mesmo nome no ODBC 2 *.x*. Em particular, todos os recursos implícitos pela conformidade oDBC 2 *.x* API Nível 1 agora fazem parte do nível de conformidade da interface Core. Como resultado, muitos drivers ODBC podem relatar conformidade de interface de nível core.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Conformidade de interface de núcleo](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [Conformidade de interface nível 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [Conformidade de interface nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [Conformidade de função](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [Conformidade de atributo](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [Conformidade de campo de descritor](../../../odbc/reference/develop-app/descriptor-field-conformance.md)

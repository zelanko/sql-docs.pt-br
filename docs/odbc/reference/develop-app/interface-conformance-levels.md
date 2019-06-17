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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74d4ceb4532ee09004f035958860833aef488aaa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62446683"
---
# <a name="interface-conformance-levels"></a>Níveis de conformidade de interface
A finalidade de redistribuição é informar ao aplicativo de quais recursos estão disponíveis para ele no driver. Um esquema de redistribuição baseado em funções não suficientemente atingir esse objetivo. Em ODBC 3. *x*, drivers são classificados com base nos recursos que eles possuem. O recurso de suporte pode incluir suporte a função; Ele também pode incluir suporte a um campo de descritor, um atributo de instrução, um valor de "Y" para um tipo de informação retornado por **SQLGetInfo**e assim por diante.  
  
 Para simplificar a especificação de conformidade de interface, o ODBC define três níveis de conformidade. Para atender a um nível de conformidade específico, um driver deve satisfazer todos os requisitos desse nível de conformidade. Conformidade com um determinado nível implica conformidade completa com todos os níveis inferiores.  
  
 Níveis de conformidade não sempre dividir claramente em suporte para uma lista específica de funções ODBC, mas especificam recursos com suporte, conforme listado nas seções a seguir. Para fornecer suporte para um recurso, um driver deve oferecer suporte a alguns ou todos os formulários de chamadas para determinadas funções ODBC (para obter mais informações, consulte [conformidade com a função](../../../odbc/reference/develop-app/function-conformance.md)), configuração de determinados atributos (consulte [conformidade de atributo ](../../../odbc/reference/develop-app/attribute-conformance.md)) e determinados campos de descritor (consulte [conformidade de campo de descritor](../../../odbc/reference/develop-app/descriptor-field-conformance.md)).  
  
 O aplicativo descobre o nível de conformidade de interface de um driver se conectar a uma fonte de dados e chamando **SQLGetInfo** com a opção SQL_ODBC_INTERFACE_CONFORMANCE.  
  
 Drivers são livres para implementar recursos além do nível ao qual eles alegam conformidade completa. Aplicativos de descobrir todos esses recursos adicionais, chamando **SQLGetFunctions** (para determinar quais funções ODBC estão presentes) e **SQLGetInfo** (para consultar vários outros recursos do ODBC).  
  
 Há três níveis de conformidade de interface ODBC: Core, nível 1 e nível 2.  
  
> [!NOTE]
>  Esses níveis de conformidade têm requisitos diferentes de níveis de conformidade com a API ODBC o mesmo nome no ODBC 2 *. x*. Em particular, a todos os recursos implícito de ODBC 2 *. x* conformidade com a API nível 1 agora são parte do nível de conformidade de interface de núcleo. Como resultado, muitos drivers ODBC podem relatar a conformidade de interface de nível de núcleo.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Conformidade de interface de núcleo](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [Conformidade de interface nível 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [Conformidade de interface nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [Conformidade de função](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [Conformidade de atributo](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [Conformidade de campo de descritor](../../../odbc/reference/develop-app/descriptor-field-conformance.md)

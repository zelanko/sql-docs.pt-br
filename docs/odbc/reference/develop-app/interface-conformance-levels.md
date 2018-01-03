---
title: "Interface níveis de conformidade | Microsoft Docs"
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
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 2c470e54-0600-4b2b-b1f3-9885cb28a01a
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0abde908ca3205cc10a35c310b508c5142fcb82c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="interface-conformance-levels"></a>Níveis de conformidade de interface
A finalidade de redistribuição é informar ao aplicativo de quais recursos estão disponíveis para ele no driver. Um esquema de redistribuição com base em funções não suficientemente atingi-lo. Em ODBC 3. *x*, drivers são classificados com base nos recursos que eles possuem. O recurso de suporte pode incluir suporte a função. Ele também pode incluir um campo de descrição, um atributo de instrução, um valor de "Y" de suporte para um tipo de informação retornado por **SQLGetInfo**, e assim por diante.  
  
 Para simplificar a especificação de conformidade de interface, o ODBC define três níveis de conformidade. Para atender a um nível de conformidade específico, um driver deve atender aos requisitos de nível de conformidade. Conformidade com um determinado nível implica completa conformidade com todos os níveis inferiores.  
  
 Níveis de conformidade não sempre dividir organizado em suporte para uma lista específica de funções ODBC, mas especificar recursos com suporte, conforme listado nas seções a seguir. Para fornecer suporte para um recurso, um driver deve oferecer suporte a algumas ou todas as formas de chamadas para determinadas funções ODBC (para obter mais informações, consulte [função conformidade](../../../odbc/reference/develop-app/function-conformance.md)), definir determinados atributos (consulte [conformidade de atributo ](../../../odbc/reference/develop-app/attribute-conformance.md)) e alguns campos de descritor (consulte [conformidade de campo de descritor](../../../odbc/reference/develop-app/descriptor-field-conformance.md)).  
  
 O aplicativo descobre o nível de conformidade de interface do driver conectando-se a uma fonte de dados e chamar **SQLGetInfo** com a opção SQL_ODBC_INTERFACE_CONFORMANCE.  
  
 Drivers estão livres para implementar recursos além do nível ao qual ele alega conformidade concluída. Aplicativos descobrir todos esses recursos adicionais, chamando **SQLGetFunctions** (para determinar quais funções ODBC estão presentes) e **SQLGetInfo** (para consultar vários outros recursos do ODBC).  
  
 Há três níveis de conformidade de interface ODBC: principal, nível 1 e nível 2.  
  
> [!NOTE]  
>  Esses níveis de conformidade com requisitos diferentes de níveis de conformidade a API ODBC de mesmo nome no ODBC 2*. x*. Em particular, todos os recursos indicado pelo ODBC 2*. x* conformidade API nível 1 agora fazem parte do nível de conformidade da interface principal. Como resultado, muitos drivers ODBC podem relatar a conformidade de interface de nível de núcleo.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Conformidade de interface de núcleo](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [Conformidade de interface nível 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [Conformidade de interface nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [Conformidade de função](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [Conformidade de atributo](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [Conformidade de campo de descritor](../../../odbc/reference/develop-app/descriptor-field-conformance.md)

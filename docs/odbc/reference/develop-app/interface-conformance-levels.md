---
title: Níveis de conformidade da interface | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304596"
---
# <a name="interface-conformance-levels"></a>Níveis de conformidade de interface
A finalidade do nivelamento é informar ao aplicativo quais recursos estão disponíveis para ele do driver. Um esquema de nivelamento baseado em funções não atinge o suficiente dessa meta. No ODBC 3. *x*, os drivers são classificados com base nos recursos que possuem. O suporte ao recurso pode incluir o suporte à função; Ele também pode incluir o suporte a um campo de descritor, um atributo de instrução, um valor "Y" para um tipo de informação retornado por **SQLGetInfo**e assim por diante.  
  
 Para simplificar a especificação da conformidade da interface, o ODBC define três níveis de conformidade. Para atender a um nível de conformidade específico, um driver deve atender a todos os requisitos desse nível de conformidade. A conformidade com um determinado nível implica em conformidade total com todos os níveis inferiores.  
  
 Os níveis de conformidade nem sempre dividem-se perfeitamente no suporte para uma lista específica de funções ODBC, mas especificam os recursos com suporte, conforme listado nas seções a seguir. Para fornecer suporte a um recurso, um driver deve dar suporte a algumas ou todas as formas de chamadas para determinadas funções ODBC (para obter mais informações, consulte [conformidade da função](../../../odbc/reference/develop-app/function-conformance.md)), definindo determinados atributos (consulte [conformidade do atributo](../../../odbc/reference/develop-app/attribute-conformance.md)) e determinados campos de descritor (consulte a conformidade do [campo do descritor](../../../odbc/reference/develop-app/descriptor-field-conformance.md)).  
  
 O aplicativo descobre o nível de conformidade da interface do driver conectando-se a uma fonte de dados e chamando **SQLGetInfo** com a opção SQL_ODBC_INTERFACE_CONFORMANCE.  
  
 Os drivers são gratuitos para implementar recursos além do nível para o qual eles alegam a conformidade completa. Os aplicativos detectam quaisquer recursos adicionais chamando **SQLGetFunctions** (para determinar quais funções ODBC estão presentes) e **SQLGetInfo** (para consultar vários outros recursos ODBC).  
  
 Há três níveis de conformidade de interface ODBC: Core, nível 1 e nível 2.  
  
> [!NOTE]
>  Esses níveis de conformidade têm requisitos diferentes dos níveis de conformidade da API ODBC com o mesmo nome no ODBC 2 *. x*. Em particular, todos os recursos implícitos pelo nível 1 de conformidade da API do ODBC 2 *. x* agora fazem parte do nível de conformidade da interface principal. Como resultado, muitos drivers ODBC podem relatar a conformidade da interface de nível de núcleo.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Conformidade de interface de núcleo](../../../odbc/reference/develop-app/core-interface-conformance.md)  
  
-   [Conformidade de interface nível 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md)  
  
-   [Conformidade de interface nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)  
  
-   [Conformidade de função](../../../odbc/reference/develop-app/function-conformance.md)  
  
-   [Conformidade de atributo](../../../odbc/reference/develop-app/attribute-conformance.md)  
  
-   [Conformidade de campo de descritor](../../../odbc/reference/develop-app/descriptor-field-conformance.md)

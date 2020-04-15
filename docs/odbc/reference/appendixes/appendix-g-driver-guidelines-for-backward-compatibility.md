---
title: 'Apêndice G: Diretrizes do driver para compatibilidade retrógrada | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 911cd335-f2c0-4d03-9739-1078308a678a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1055f94cb54bba9262f210e5df5f028029aebf5b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292396"
---
# <a name="appendix-g-driver-guidelines-for-backward-compatibility"></a>Apêndice G: Diretrizes de driver para compatibilidade com versões anteriores
Este apêndice fornece informações para escritores de driver que trabalham no ODBC 3. *x* drivers que precisam suportar ODBC 2. *x* aplicações. Para obter mais informações sobre compatibilidade retrógrada, consulte [Retrocompatibilidade e Conformidade de Padrões](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Cursores de bloco, cursores roláveis e compatibilidade retrógrada para drivers ODBC 3.x](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) - Novos recursos são recursos que existem no ODBC 3. *x* e não em ODBC 2. *x*. ODBC 3. *x* drivers geralmente não tem que se preocupar com a retrocompatibilidade com novos recursos porque ODBC 2. *x* aplicativos nunca usá-los. As únicas exceções a isso são os recursos relacionados ao **SQLFetch,** **SQLFetchScroll,** **SQLSetPos**e **SQLExtendedFetch;** para obter mais informações, veja , mais tarde neste apêndice.  
  
-   [Mapeamento de funções depreciadas](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) - Recursos duplicados são recursos que são implementados de forma diferente no ODBC 3. *x* e ODBC 2. *x*. ODBC 3. *x* drivers não tem que se preocupar com a compatibilidade retrógrada com recursos duplicados porque o Driver Manager sempre mapeia ODBC 2. *x* características para ODBC 3. *x* recursos ao chamar um ODBC 3. *x* driver. Assim, um ODBC 3. *x* driver vê apenas ODBC 3. *x* características. Para obter mais informações sobre esses mapeamentos, consulte , mais tarde neste apêndice.  
  
-   [Mudanças comportamentais e Drivers ODBC 3.x](../../../odbc/reference/appendixes/behavioral-changes-and-odbc-3-x-drivers.md) - Mudanças de comportamento são características que são tratadas de forma diferente no ODBC 3. *x* e ODBC 2. *x*. ODBC 3. *x* drivers têm que se preocupar com mudanças de comportamento e agir em resposta ao SQL_ATTR_ODBC_VERSION atributo ambiente definido pelo aplicativo.

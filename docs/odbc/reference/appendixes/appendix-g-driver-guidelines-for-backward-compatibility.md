---
title: 'Apêndice G: diretrizes de driver para compatibilidade com versões anteriores | Microsoft Docs'
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292396"
---
# <a name="appendix-g-driver-guidelines-for-backward-compatibility"></a>Apêndice G: Diretrizes de driver para compatibilidade com versões anteriores
Este apêndice fornece informações para os gravadores de driver que trabalham no ODBC 3. drivers *x* que precisam dar suporte ao ODBC 2. aplicativos *x* . Para obter mais informações sobre compatibilidade com versões anteriores, consulte [compatibilidade com versões anteriores e conformidade com padrões](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Cursores de bloco, cursores roláveis e compatibilidade com versões anteriores para drivers ODBC 3. x](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) – os novos recursos são recursos que existem no ODBC 3. *x* e não no ODBC 2. *x*. ODBC 3. os drivers *x* geralmente não precisam se preocupar com a compatibilidade com versões anteriores com novos recursos, porque ODBC 2. os aplicativos *x* nunca os usam. As únicas exceções a isso são recursos relacionados a **SQLFetch**, **SQLFetchScroll**, **SQLSetPos**e **SQLExtendedFetch**; para obter mais informações, consulte, mais adiante neste apêndice.  
  
-   [Mapeando funções preteridas](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) – recursos duplicados são recursos que são implementados de modo diferente no ODBC 3. *x* e ODBC 2. *x*. ODBC 3. os drivers *x* não precisam se preocupar com a compatibilidade com versões anteriores com recursos duplicados porque o Gerenciador de driver sempre MAPEIA o ODBC 2. recursos *x* para ODBC 3. recursos *x* ao chamar um ODBC 3. Driver *x* . Portanto, um ODBC 3. *x* driver vê somente ODBC 3. recursos *x* . Para obter mais informações sobre esses mapeamentos, consulte, mais adiante neste apêndice.  
  
-   [Alterações comportamentais e drivers ODBC 3. x](../../../odbc/reference/appendixes/behavioral-changes-and-odbc-3-x-drivers.md) – alterações de comportamento são recursos que são tratados de forma diferente no ODBC 3. *x* e ODBC 2. *x*. ODBC 3. os drivers *x* precisam se preocupar com alterações de comportamento e agir em resposta ao atributo de ambiente SQL_ATTR_ODBC_VERSION definido pelo aplicativo.

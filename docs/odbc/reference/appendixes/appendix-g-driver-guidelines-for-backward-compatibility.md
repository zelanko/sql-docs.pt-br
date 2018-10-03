---
title: 'Apêndice g: diretrizes de Driver para compatibilidade com versões anteriores | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 63f999fa01623898be6561c9f5a450c6ec81487d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47654224"
---
# <a name="appendix-g-driver-guidelines-for-backward-compatibility"></a>Apêndice G: Diretrizes de driver para compatibilidade com versões anteriores
Este apêndice fornece informações para gravadores de driver trabalhando em ODBC 3. *x* drivers que precisam dar suporte a ODBC 2. *x* aplicativos. Para obter mais informações sobre compatibilidade com versões anteriores, consulte [compatibilidade com versões anteriores e em conformidade com padrões](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Cursores em bloco, cursores roláveis e compatibilidade com versões anteriores para Drivers ODBC 3.x](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) – novos recursos são recursos que existem no ODBC 3. *x* e não no ODBC 2. *x*. ODBC 3. *x* drivers geralmente não precisa se preocupar sobre a compatibilidade com versões anteriores com os novos recursos, porque o ODBC 2. *x* aplicativos nunca usá-los. As única exceções são recursos relacionados ao **SQLFetch**, **SQLFetchScroll**, **SQLSetPos**, e **SQLExtendedFetch**; para obter mais informações informações, consulte, posteriormente neste apêndice.  
  
-   [Funções preteridas de mapeamento](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) — recursos duplicado são recursos que são implementados de maneira diferente em ODBC 3. *x* e o ODBC 2. *x*. ODBC 3. *x* drivers não precisa se preocupar sobre a compatibilidade com versões anteriores com recursos duplicados porque o Gerenciador de Driver sempre mapeia ODBC 2. *x* recursos para o ODBC 3. *x* apresenta ao chamar um ODBC 3. *x* driver. Portanto, um ODBC 3. *x* driver vê apenas o ODBC 3. *x* recursos. Para obter mais informações sobre esses mapeamentos, consulte, posteriormente neste apêndice.  
  
-   [Alterações de comportamento e Drivers ODBC 3.x](../../../odbc/reference/appendixes/behavioral-changes-and-odbc-3-x-drivers.md) — as alterações de comportamento são recursos que são tratados de maneira diferente em ODBC 3. *x* e o ODBC 2. *x*. ODBC 3. *x* drivers precisam se preocupar sobre alterações de comportamento e agir em resposta ao ambiente SQL_ATTR_ODBC_VERSION atributo definido pelo aplicativo.

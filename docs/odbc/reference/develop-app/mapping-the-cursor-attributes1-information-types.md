---
title: "Mapear os tipos de informações do Cursor Attributes1 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [ODBC], mapping cursor attributes1 information types
- application upgrades [ODBC], mapping cursor attributes1 information types
- mapping cursor attributes1 information types [ODBC]
- backward compatibility [ODBC], mapping cursor attributes1 information types
- upgrading applications [ODBC], mapping cursor attributes1 information types
ms.assetid: 9f112449-ca86-45ac-a865-e6174d67f91b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1d8f72fb4246f2ccfded98e63b701b57d3229068
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="mapping-the-cursor-attributes1-information-types"></a>Mapear os tipos de informações do Cursor Attributes1
Quando um ODBC 3. *x* aplicativo chama **SQLGetInfo** em um ODBC 2*. x* driver com o tipo de informação SQL_XXXX_CURSOR_ATTRIBUTES1 (para o conjunto de chaves-driver dinâmico, somente encaminhamento, ou Cursores estáticos), a configuração dos bits retornados pelo Gerenciador de Driver depende de que o ODBC 2. *x* driver retorna para o correspondente ODBC 2. *x* tipos de informações. Os bits são definidos como mostrado na tabela a seguir.  
  
|Bit no<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|Tipo de cursor|ODBC 2. *x* informações<br /><br /> Tipo|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|Todos|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTE SQL_CA1_RELATIVE SQL_CA1_BOOKMARK|Dinâmico, o conjunto de chaves-driver, estático|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_NO_CHANGE SQL_CA1_LOCK_UNLOCK SQL_CA1_LOCK_EXCLUSIVE|Dinâmico, o conjunto de chaves-driver, estático|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_DELETE SQL_CA1_SELECT_FOR_UPDATE|Todos|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITION SQL_CA1_POS_DELETE SQL_CA1_POS_REFRESH SQL_CA1_POS_BULK_ADD|Dinâmico, o conjunto de chaves-driver, estático|SQL_POS_OPERATIONS|


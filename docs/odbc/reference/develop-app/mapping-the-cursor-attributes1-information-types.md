---
title: Mapear os tipos de informações do Cursor Attributes1 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
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
manager: craigg
ms.openlocfilehash: 90f5913eef381d2130fbe0c7eeeaa225a2587c6c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="mapping-the-cursor-attributes1-information-types"></a>Mapear os tipos de informações do Cursor Attributes1
Quando um ODBC 3. *x* aplicativo chama **SQLGetInfo** em um ODBC 2 *. x* driver com o tipo de informação SQL_XXXX_CURSOR_ATTRIBUTES1 (para o conjunto de chaves-driver dinâmico, somente encaminhamento, ou Cursores estáticos), a configuração dos bits retornados pelo Gerenciador de Driver depende de que o ODBC 2. *x* driver retorna para o correspondente ODBC 2. *x* tipos de informações. Os bits são definidos como mostrado na tabela a seguir.  
  
|Bit no<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|Tipo de cursor|ODBC 2. *x* informações<br /><br /> Tipo|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|Todos|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTE SQL_CA1_RELATIVE SQL_CA1_BOOKMARK|Dinâmico, o conjunto de chaves-driver, estático|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_NO_CHANGE SQL_CA1_LOCK_UNLOCK SQL_CA1_LOCK_EXCLUSIVE|Dinâmico, o conjunto de chaves-driver, estático|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_DELETE SQL_CA1_SELECT_FOR_UPDATE|Todos|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITION SQL_CA1_POS_DELETE SQL_CA1_POS_REFRESH SQL_CA1_POS_BULK_ADD|Dinâmico, o conjunto de chaves-driver, estático|SQL_POS_OPERATIONS|

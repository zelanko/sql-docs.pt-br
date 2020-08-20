---
description: Mapear os tipos de informações dos atributos1 de cursor
title: Mapeando os tipos de informações do cursor Attributes1 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], mapping cursor attributes1 information types
- application upgrades [ODBC], mapping cursor attributes1 information types
- mapping cursor attributes1 information types [ODBC]
- backward compatibility [ODBC], mapping cursor attributes1 information types
- upgrading applications [ODBC], mapping cursor attributes1 information types
ms.assetid: 9f112449-ca86-45ac-a865-e6174d67f91b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fcd4c1eaa6ddd2e6db4f2634cc22d3148e7977cf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461398"
---
# <a name="mapping-the-cursor-attributes1-information-types"></a>Mapear os tipos de informações dos atributos1 de cursor
Quando um ODBC 3. *x* o aplicativo chama **SQLGetInfo** em um driver ODBC 2 *. x* com o tipo de informação SQL_XXXX_CURSOR_ATTRIBUTES1 (para cursores dinâmicos, somente de encaminhamento, de conjunto de chaves ou estáticos), a configuração dos bits retornados pelo Gerenciador de driver depende do que o ODBC 2. o driver *x* retorna para o ODBC 2 correspondente. tipos de informações *x* . Os bits são definidos conforme mostrado na tabela a seguir.  
  
|Bit em<br /><br /> SQL_XXXX_CURSOR_ATTRIBUTES1|Tipo de cursor|ODBC 2. informações de *x*<br /><br /> type|  
|-----------------------------------------------|-----------------|-------------------------------------|  
|SQL_CA1_NEXT|Tudo|SQL_FETCH_DIRECTION|  
|SQL_CA1_ABSOLUTE SQL_CA1_RELATIVE SQL_CA1_BOOKMARK|Dinâmico, conjunto de chaves-Driver, estático|SQL_FETCH_DIRECTION|  
|SQL_CA1_LOCK_NO_CHANGE SQL_CA1_LOCK_UNLOCK SQL_CA1_LOCK_EXCLUSIVE|Dinâmico, conjunto de chaves-Driver, estático|SQL_LOCK_TYPES|  
|SQL_CA1_POSITIONED_UPDATE SQL_CA1_POSITIONED_DELETE SQL_CA1_SELECT_FOR_UPDATE|Tudo|SQL_POSITIONED_STATEMENTS|  
|SQL_CA1_POS_POSITION SQL_CA1_POS_DELETE SQL_CA1_POS_REFRESH SQL_CA1_POS_BULK_ADD|Dinâmico, conjunto de chaves-Driver, estático|SQL_POS_OPERATIONS|

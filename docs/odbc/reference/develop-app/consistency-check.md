---
description: Verificação de consistência
title: Verificação de consistência | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], consistency checks
- consistency checks [ODBC]
ms.assetid: deb80efa-ad1f-4ea5-b334-9817cd279e5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ad1ffe0cb7819447a3819d73cd6605347b756ede
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465898"
---
# <a name="consistency-check"></a>Verificação de consistência
Uma verificação de consistência é executada automaticamente pelo driver sempre que um aplicativo define o campo SQL_DESC_DATA_PTR de APD, ARD ou IPD. Sempre que esse campo for definido, o driver verificará se o valor do campo SQL_DESC_TYPE e os valores aplicáveis ao campo SQL_DESC_TYPE no mesmo registro são válidos e consistentes.  
  
 O campo SQL_DESC_DATA_PTR de um IPD não é normalmente definido; no entanto, um aplicativo pode fazer isso para forçar uma verificação de consistência de campos de IPD. O valor ao qual o campo SQL_DESC_DATA_PTR do IPD está definido não é realmente armazenado e não pode ser recuperado por uma chamada para **SQLGetDescField** ou **SQLGetDescRec**; a configuração é feita somente para forçar a verificação de consistência. Uma verificação de consistência não pode ser executada em um IRD.  
  
 Para obter mais informações sobre a verificação de consistência, consulte [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).

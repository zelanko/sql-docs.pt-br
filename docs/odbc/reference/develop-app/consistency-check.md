---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 419e338a5e96821606dc26a53a4fccecbc72ae3e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125536"
---
# <a name="consistency-check"></a>Verificação de consistência
Uma verificação de consistência é executada automaticamente pelo driver sempre que um aplicativo define o campo SQL_DESC_DATA_PTR de APD, ARD ou IPD. Sempre que esse campo for definido, o driver verificará se o valor do campo SQL_DESC_TYPE e os valores aplicáveis ao campo SQL_DESC_TYPE no mesmo registro são válidos e consistentes.  
  
 O campo SQL_DESC_DATA_PTR de um IPD não é normalmente definido; no entanto, um aplicativo pode fazer isso para forçar uma verificação de consistência de campos de IPD. O valor ao qual o campo SQL_DESC_DATA_PTR do IPD está definido não é realmente armazenado e não pode ser recuperado por uma chamada para **SQLGetDescField** ou **SQLGetDescRec**; a configuração é feita somente para forçar a verificação de consistência. Uma verificação de consistência não pode ser executada em um IRD.  
  
 Para obter mais informações sobre a verificação de consistência, consulte [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).

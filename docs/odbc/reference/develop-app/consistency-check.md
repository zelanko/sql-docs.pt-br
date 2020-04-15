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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: edd946ca865cd9d8d2edff2c7bedbb3b2629c97c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298996"
---
# <a name="consistency-check"></a>Verificação de consistência
Uma verificação de consistência é realizada automaticamente pelo driver sempre que um aplicativo define o campo SQL_DESC_DATA_PTR do APD, ARD ou IPD. Sempre que este campo é definido, o motorista verifica se o valor do campo SQL_DESC_TYPE e os valores aplicáveis ao campo SQL_DESC_TYPE no mesmo registro são válidos e consistentes.  
  
 O campo SQL_DESC_DATA_PTR de um IPD normalmente não está definido; no entanto, um aplicativo pode fazê-lo para forçar uma verificação de consistência dos campos IPD. O valor para o que o SQL_DESC_DATA_PTR campo do IPD está definido não é realmente armazenado e não pode ser recuperado por uma chamada para **SQLGetDescField** ou **SQLGetDescRec**; a configuração é feita apenas para forçar a verificação de consistência. Uma verificação de consistência não pode ser realizada em um IRD.  
  
 Para obter mais informações sobre a verificação de consistência, consulte [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).

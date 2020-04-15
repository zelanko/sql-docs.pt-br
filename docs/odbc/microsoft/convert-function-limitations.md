---
title: Limitações de função CONVERT | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, CONVERT function limitations
- Convert function limitations [ODBC]
ms.assetid: 3c81fc58-57f0-4dd7-be16-2b146eb15cbc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 63f4258e737327ae11f03a96cfef3cdecf133e53
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281026"
---
# <a name="convert-function-limitations"></a>Limitações da função CONVERT
As falhas de conversão de tipo resultam na configuração da coluna afetada como NULL.  
  
 Nem o tipo de dados DATE nem TIMESTAMP podem ser convertidos para outro tipo de dados (ou em si) pela função CONVERT.

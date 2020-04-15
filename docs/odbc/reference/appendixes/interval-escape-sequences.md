---
title: Seqüências de fuga de intervalo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9fe7f6941e9ec9fba8b6698faaa18a678732dd6f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304951"
---
# <a name="interval-escape-sequences"></a>Sequências de escape de intervalo
ODBC usa seqüências de fuga para literais de intervalo. A sintaxe desta seqüência de fuga é a seguinte:  
  
 {*intervalo-literal*}  
  
 Para a sintaxe BNF de *intervalo-literal,* consulte a seção [De sintaxe literal do intervalo](../../../odbc/reference/appendixes/interval-literal-syntax.md) mais tarde neste apêndice.  
  
 A seqüência de fuga literal de intervalo é suportada se os tipos de dados de intervalo forem suportados pela fonte de dados. Um aplicativo deve ligar para **o SQLGetTypeInfo** para determinar se esses tipos de dados são suportados.

---
title: Limitações de cordas | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 61f81ff3da882095a0a6c41bb5061addd497a5d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306057"
---
# <a name="string-limitations"></a>Limitações de cadeia de caracteres
O comprimento máximo de uma seqüência de declaração SQL é de 65.000 caracteres.  
  
 Quando o driver Microsoft Access é usado, apenas as constantes de seqüência SQL-92 (com aspas simples, não aspas duplas) são suportadas.  
  
 O caractere pipe (&#124;) não pode ser usado em uma seqüência de caracteres, quer o caractere esteja incluído entre aspas traseiras ou não.  
  
 Para interoperabilidade máxima, as aplicações devem passar strings em parâmetros, em vez de passar as strings citadas.

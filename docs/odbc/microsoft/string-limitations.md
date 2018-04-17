---
title: Limitações de cadeia de caracteres | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8a8e90ace4e237b7945da4a43ad869b79c657ab2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="string-limitations"></a>Limitações de cadeia de caracteres
O comprimento máximo de uma cadeia de caracteres de instrução SQL é 65.000 caracteres.  
  
 Quando o driver do Microsoft Access for usado, somente as constantes de cadeia de caracteres SQL-92 (com aspas simples, aspas duplas não) têm suporte.  
  
 O caractere de pipe (&#124;) não pode ser usado em uma cadeia de caracteres, se o caractere é colocado entre aspas back ou não.  
  
 Para interoperabilidade máxima, aplicativos devem passar cadeias de caracteres nos parâmetros, em vez de passagem de cadeias de caracteres entre aspas.

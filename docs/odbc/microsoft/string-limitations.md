---
title: "Limitações de cadeia de caracteres | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: ec1da65f-c69d-415d-bf75-8fda8aa2b39f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e6f9d8add08f80b59adaa42f02bc1da006356081
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="string-limitations"></a>Limitações de cadeia de caracteres
O comprimento máximo de uma cadeia de caracteres de instrução SQL é 65.000 caracteres.  
  
 Quando o driver do Microsoft Access for usado, somente as constantes de cadeia de caracteres SQL-92 (com aspas simples, aspas duplas não) têm suporte.  
  
 O caractere de pipe (&#124;) não pode ser usado em uma cadeia de caracteres, se o caractere é colocado entre aspas back ou não.  
  
 Para interoperabilidade máxima, aplicativos devem passar cadeias de caracteres nos parâmetros, em vez de passagem de cadeias de caracteres entre aspas.


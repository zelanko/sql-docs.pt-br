---
title: 'Jet: Data, hora e literais de carimbo de hora | Microsoft Docs'
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
- literals [ODBC], SQL grammar
- SQL grammar [ODBC], literals
- date literals [ODBC]
- timestamp literals [ODBC]
- time literals [ODBC]
ms.assetid: 37db1ae1-ca4e-4cd8-9b47-7f1a38e7fcad
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc36c46885a358e1ca453901fd72362ed1dbb32b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: Data, hora e literais de carimbo de hora
Para interoperabilidade máxima, aplicativos devem passar literais de data no formato canônico ODBC usando a sintaxe da cláusula escape:  
  
-   Para literais de data, {d '*valor*'}, onde *valor*e está no formato "aaaa-mm-dd"  
  
-   Para literais de hora, {t '*valor*'}, onde *valor*e está no formato "hh"  
  
 Para literais de carimbo de hora {ts'*valor*'}, onde *valor*e está no formato "aaaa-mm-dd hh [. f....]".

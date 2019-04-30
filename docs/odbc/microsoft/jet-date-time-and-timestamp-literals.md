---
title: 'Jet: Data, hora e literais de carimbo de hora | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- literals [ODBC], SQL grammar
- SQL grammar [ODBC], literals
- date literals [ODBC]
- timestamp literals [ODBC]
- time literals [ODBC]
ms.assetid: 37db1ae1-ca4e-4cd8-9b47-7f1a38e7fcad
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2325cd7e4a10e91f351aa2107c64c0978b843fa6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224583"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: Data, hora e literais de carimbo de data/hora
Para interoperabilidade máxima, aplicativos devem passar literais de data no formato canônico ODBC usando a sintaxe da cláusula de escape:  
  
-   Para literais de data, {1!d '*valor*'}, onde *valo*e está no formato "aaaa-mm-dd"  
  
-   Para literais de hora, {t '*valor*'}, onde *valo*e está no formato "hh"  
  
 Para literais de carimbo de hora {ts'*valor*'}, onde *valo*e está no formato "aaaa-mm-dd hh: mm ss [. f...]".

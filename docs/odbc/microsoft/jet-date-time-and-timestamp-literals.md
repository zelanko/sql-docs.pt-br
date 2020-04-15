---
title: 'Jato: Data, Hora e Carimbo de Tempo Literals | Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 372b7c1dab1ad8ff000fb88729c3b02e05d4a21c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299926"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: data, hora e literais de carimbo de data/hora
Para interoperabilidade máxima, os aplicativos devem passar literais de data no formato canônico ODBC usando sintaxe de cláusula de escape:  
  
-   Para literais de data, {d '*valor*'}, onde *valu*e está na forma "yyyy-mm-dd"  
  
-   Para literais de tempo, {t '*valor*'}, onde *valu*e está na forma "hh:mm:ss"  
  
 Para literais de carimbo de tempo {ts '*valor*'}, onde *valu*e está na forma "yyyy-mm-dd hh:mm:ss[.f...]".

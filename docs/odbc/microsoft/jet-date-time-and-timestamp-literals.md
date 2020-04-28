---
title: 'Jet: Date, time e literais de carimbo de data/hora | Microsoft Docs'
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299926"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: data, hora e literais de carimbo de data/hora
Para a interoperabilidade máxima, os aplicativos devem passar literais de data no formato ODBC canônico usando sintaxe de cláusula de escape:  
  
-   Para literais de data, {d '*Value*'}, em que *valo*e está no formato "aaaa-mm-dd"  
  
-   Para literais de tempo, {t '*Value*'}, em que *valo*e está no formato "hh: mm: SS"  
  
 Para literais de carimbo de data/hora {TS '*Value*'}, em que *valo*e está no formato "aaaa-mm-dd hh: mm: SS [. f...]".

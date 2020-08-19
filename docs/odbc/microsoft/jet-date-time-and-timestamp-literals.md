---
description: 'Jet: data, hora e literais de carimbo de data/hora'
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
ms.openlocfilehash: 02b2a7c5c633ee891dbcd962786cb1904bfd5df8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449438"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: data, hora e literais de carimbo de data/hora
Para a interoperabilidade máxima, os aplicativos devem passar literais de data no formato ODBC canônico usando sintaxe de cláusula de escape:  
  
-   Para literais de data, {d '*Value*'}, em que *valo*e está no formato "aaaa-mm-dd"  
  
-   Para literais de tempo, {t '*Value*'}, em que *valo*e está no formato "hh: mm: SS"  
  
 Para literais de carimbo de data/hora {TS '*Value*'}, em que *valo*e está no formato "aaaa-mm-dd hh: mm: SS [. f...]".

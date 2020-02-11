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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1bb7f0fb02049b6d2f1897c4f495035aee2858f6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085491"
---
# <a name="jet-date-time-and-timestamp-literals"></a>Jet: data, hora e literais de carimbo de data/hora
Para a interoperabilidade máxima, os aplicativos devem passar literais de data no formato ODBC canônico usando sintaxe de cláusula de escape:  
  
-   Para literais de data, {d '*Value*'}, em que *valo*e está no formato "aaaa-mm-dd"  
  
-   Para literais de tempo, {t '*Value*'}, em que *valo*e está no formato "hh: mm: SS"  
  
 Para literais de carimbo de data/hora {TS '*Value*'}, em que *valo*e está no formato "aaaa-mm-dd hh: mm: SS [. f...]".

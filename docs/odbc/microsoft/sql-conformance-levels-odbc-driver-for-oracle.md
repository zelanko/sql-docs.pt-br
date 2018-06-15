---
title: Níveis de conformidade do SQL (ODBC Driver for Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- ODBC driver for Oracle [ODBC], conformance levels
ms.assetid: 077a6c6a-2c57-42c9-a4fd-4cf0e65cf7e2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6124577353292209f2bcbd2ca35b6b33add34ca6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32904921"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>Níveis de conformidade do SQL (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O Driver ODBC do Oracle oferece suporte a gramática SQL mínima e a gramática de SQL do núcleo e também suporta as seguintes extensões ODBC para SQL:  
  
-   Dados de data, hora e carimbo de hora  
  
-   À esquerda e junções externas direitas  
  
-   Funções numéricas:  
  
    |||||  
    |-|-|-|-|  
    |Abs|Log|round|tan|  
    |Ceiling|Log10|second|truncate|  
    |Cos|Mod|Logon||  
    |Exp|Pi|sin||  
    |Floor|Potência|Sqrt||  
  
-   Funções de data:  
  
    |||||  
    |-|-|-|-|  
    |Curdate|DayOfWeek|MonthName|second|  
    |Curtime|Dia do ano|minute|week|  
    |Dayname|Hora|Agora|year|  
    |DayOfMonth|Month|Trimestre||  
  
-   Funções de cadeia de caracteres:  
  
    |||||  
    |-|-|-|-|  
    |ASCII|Left (à esquerda)|Certo|UCase|  
    |Char|Comprimento|RTrim||  
    |Concat|Ltrim|Soundex||  
    |Lcase|Substituir|substring||  
  
-   Função de conversão de tipo:  
  
    ||  
    |-|  
    |Converter|  
  
-   Funções do sistema:  
  
    ||  
    |-|  
    |Ifnull|  
    |Usuário|

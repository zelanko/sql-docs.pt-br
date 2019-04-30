---
title: Níveis de conformidade do SQL (Driver ODBC para Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- ODBC driver for Oracle [ODBC], conformance levels
ms.assetid: 077a6c6a-2c57-42c9-a4fd-4cf0e65cf7e2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0bf63b831dace7678f5d3fdf952a9d6d5f60aa6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313386"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>Níveis de conformidade do SQL (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O Driver ODBC para Oracle dá suporte a gramática SQL mínima e a gramática SQL principal e também suporta as seguintes extensões ODBC para SQL:  
  
-   Dados de data, hora e carimbo de hora  
  
-   À esquerda e junções externas direitas  
  
-   Funções numéricas:  
  
    |||||  
    |-|-|-|-|  
    |Abs|Log|round|tan|  
    |Ceiling|Log10|second|truncate|  
    |Cos|Mod|logon||  
    |Exp|Pi|sin||  
    |Floor|Potência|sqrt||  
  
-   Funções de data:  
  
    |||||  
    |-|-|-|-|  
    |Curdate|DayOfWeek|MonthName|second|  
    |Função Curtime|Dia do ano|minute|week|  
    |Função Dayname|Hora|Agora|year|  
    |Dia do mês|Month|Trimestre||  
  
-   Funções de cadeia de caracteres:  
  
    |||||  
    |-|-|-|-|  
    |Ascii|Left (à esquerda)|Certo|UCase|  
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
    |User|

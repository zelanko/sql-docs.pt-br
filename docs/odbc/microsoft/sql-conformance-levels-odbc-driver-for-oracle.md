---
title: "Níveis de conformidade do SQL (ODBC Driver for Oracle) | Microsoft Docs"
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
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- ODBC driver for Oracle [ODBC], conformance levels
ms.assetid: 077a6c6a-2c57-42c9-a4fd-4cf0e65cf7e2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ada0aaa75fe63313395b6e727c3bc86bf639704e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

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


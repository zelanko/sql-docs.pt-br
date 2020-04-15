---
title: Níveis de conformidade SQL (Driver ODBC para Oracle) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e283bbc13f0d0dda055b047b027f7b9816502df5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300672"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>Níveis de conformidade do SQL (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O Driver ODBC for Oracle suporta a gramática SQL mínima e a gramática SQL principal e também suporta as seguintes extensões ODBC ao SQL:  
  
-   Dados de data, hora e carimbo de hora  
  
-   Junções externas esquerda e direita  
  
-   Funções numéricas:  
  
    |||||  
    |-|-|-|-|  
    |Abs|Log|round|tan|  
    |Ceiling|Log10|second|truncate|  
    |Cos|Mod|assinar||  
    |Exp|Pi|sin||  
    |Piso|Potência|sqrt||  
  
-   Funções de data:  
  
    |||||  
    |-|-|-|-|  
    |Curdate|Dayofweek|Monthname|second|  
    |Curtime|Dia do ano|minute|week|  
    |Nome do dia|Hora|now|year|  
    |Dayofmonth|Month|trimestre||  
  
-   Funções de cadeia de caracteres:  
  
    |||||  
    |-|-|-|-|  
    |Ascii|Left (à esquerda)|direita|Ucase|  
    |Char|Comprimento|Rtrim||  
    |Concat|Ltrim|Soundex||  
    |Lcase|Substitua|substring||  
  
-   Função de conversão de tipo:  
  
    ||  
    |-|  
    |Converter|  
  
-   Funções do sistema:  
  
    ||  
    |-|  
    |Ifnull|  
    |Usuário|

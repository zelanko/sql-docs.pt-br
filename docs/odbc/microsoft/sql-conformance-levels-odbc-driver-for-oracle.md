---
description: Níveis de conformidade do SQL (Driver ODBC para Oracle)
title: Níveis de conformidade do SQL (driver ODBC para Oracle) | Microsoft Docs
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
ms.openlocfilehash: 78e98aed952ef8b15a4654be9f82e355d1b4177b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483419"
---
# <a name="sql-conformance-levels-odbc-driver-for-oracle"></a>Níveis de conformidade do SQL (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O ODBC driver for Oracle dá suporte à gramática SQL mínima e à gramática SQL básica e também dá suporte às seguintes extensões ODBC para SQL:  
  
-   Dados de data, hora e timestamp  
  
-   Junções externas esquerda e direita  
  
-   Funções numéricas:  

    :::row:::
        :::column:::
            Abs  
            Ceiling  
            Cos  
            Exp  
            Piso  
        :::column-end:::
        :::column:::
            Log  
            Log10  
            Mod  
            Pi  
            Energia  
        :::column-end:::
        :::column:::
            round  
            second  
            assinar  
            sin  
            sqrt  
        :::column-end:::
        :::column:::
            tan  
            truncate  
        :::column-end:::
    :::row-end:::
    
-   Funções de data:  

    :::row:::
        :::column:::
            Curdate  
            Curtime  
            Dayname  
            DayOfMonth  
        :::column-end:::
        :::column:::
            DayOfWeek  
            Dia do ano  
            Hora  
            Month  
        :::column-end:::
        :::column:::
            MonthName  
            minute  
            now  
            trimestre  
        :::column-end:::
        :::column:::
            second  
            week  
            year  
        :::column-end:::
    :::row-end:::

-   Funções de cadeia de caracteres:  

    :::row:::
        :::column:::
            Ascii  
            Char  
            Concat  
            Lcase  
        :::column-end:::
        :::column:::
            Esquerda  
            Tamanho  
            Ltrim  
            Substitua  
        :::column-end:::
        :::column:::
            direita  
            RTrim  
            SOUNDEX  
            substring  
        :::column-end:::
        :::column:::
            UCase  
        :::column-end:::
    :::row-end:::

-   Função de conversão de tipo:  

    Converter  

-   Funções do sistema:  
  
    Ifnull  
    Usuário

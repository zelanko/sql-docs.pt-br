---
description: Tipo de buffer de dados
title: Tipo de buffer de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], buffers
- data buffers [ODBC], types
- buffers [ODBC], data
- C data types [ODBC], buffers
ms.assetid: 58bea3e9-d552-447f-b3ad-ce1dab213b72
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a1a3edf66a8f3684fdf8389d16c08f62682907ca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429348"
---
# <a name="data-buffer-type"></a>Tipo de buffer de dados
O tipo de dados C de um buffer é especificado pelo aplicativo. Com uma única variável, isso ocorre quando o aplicativo aloca a variável. Com memória genérica – ou seja, a memória apontada por um ponteiro do tipo void-isso ocorre quando o aplicativo converte a memória para um tipo específico. O driver descobre esse tipo de duas maneiras:  
  
-   **Argumento de tipo de buffer de dados.** Os buffers usados para transferir valores de parâmetro e dados de conjunto de resultados, como o buffer associado a *TargetValuePtr* em **SQLBindCol**, geralmente têm um argumento de tipo associado, como o argumento *TargetType* em **SQLBindCol**. Nesse argumento, o aplicativo passa o identificador do tipo C que corresponde ao tipo do buffer. Por exemplo, na chamada a seguir para **SQLBindCol**, o valor SQL_C_TYPE_DATE informa ao driver que o buffer de *data* é um SQL_DATE_STRUCT:  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     Para obter mais informações sobre identificadores de tipo, consulte a seção [tipos de dados no ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md) , mais adiante nesta seção.  
  
-   **Tipo predefinido.** Os buffers usados para enviar e recuperar opções ou atributos, como o buffer apontado pelo argumento *InfoValuePtr* em **SQLGetInfo**, têm um tipo fixo que depende da opção especificada. O driver pressupõe que o buffer de dados é desse tipo; é responsabilidade do aplicativo alocar um buffer desse tipo. Por exemplo, na chamada a seguir para **SQLGetInfo**, o driver pressupõe que o buffer é um inteiro de 32 bits porque é isso que a opção SQL_STRING_FUNCTIONS requer:  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 O driver usa o tipo de dados C para interpretar os dados no buffer.

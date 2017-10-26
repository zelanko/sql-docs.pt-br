---
title: Tipo de Buffer de dados | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], buffers
- data buffers [ODBC], types
- buffers [ODBC], data
- C data types [ODBC], buffers
ms.assetid: 58bea3e9-d552-447f-b3ad-ce1dab213b72
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0c2ed3fb1d6a68737a894663e1b5c841d6cb1041
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="data-buffer-type"></a>Tipo de Buffer de dados
O tipo de dados C de um buffer é especificado pelo aplicativo. Com uma única variável, isso ocorre quando o aplicativo aloca a variável. Com memória genérica — ou seja, memória aponta para um ponteiro de tipo void – isso ocorre quando o aplicativo converte a memória para um determinado tipo. O driver detecta esse tipo de duas maneiras:  
  
-   **Argumento de tipo de buffer de dados.** Buffers usados para transferir dados do conjunto de resultados e os valores de parâmetro, como o buffer associado *TargetValuePtr* na **SQLBindCol**, geralmente têm um argumento de tipo associado, como o * TargetType* argumento **SQLBindCol**. Este argumento, o aplicativo passa o identificador de tipo de C que corresponde ao tipo de buffer. Por exemplo, na seguinte chamada para **SQLBindCol**, o valor de SQL_C_TYPE_DATE informa o driver de *data* buffer é um SQL_DATE_STRUCT:  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     Para obter mais informações sobre identificadores de tipo, consulte o [tipos de dados ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md) seção mais adiante nesta seção.  
  
-   **Tipo predefinido.** Buffers usados para enviar e recuperar opções ou atributos, como o buffer apontado pelo *InfoValuePtr* argumento **SQLGetInfo**, tem um tipo fixo que depende da opção especificada. O driver pressupõe que o buffer de dados seja desse tipo; é responsabilidade do aplicativo para alocar um buffer desse tipo. Por exemplo, na seguinte chamada para **SQLGetInfo**, o driver pressupõe que o buffer é um inteiro de 32 bits porque este é o que requer a opção SQL_STRING_FUNCTIONS:  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 O driver usa o tipo de dados C para interpretar os dados no buffer.


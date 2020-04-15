---
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
ms.openlocfilehash: 9b98ed2ab0865b98884f6dfa1ff20142540ff314
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305242"
---
# <a name="data-buffer-type"></a>Tipo de buffer de dados
O tipo de dados C de um buffer é especificado pelo aplicativo. Com uma única variável, isso ocorre quando a aplicação aloca a variável. Com memória genérica - ou seja, memória apontada por um ponteiro do tipo vazio - isso ocorre quando o aplicativo lança a memória para um tipo específico. O motorista descobre esse tipo de duas maneiras:  
  
-   **Argumento do tipo de buffer de dados.** Os buffers usados para transferir valores de parâmetros e dados de conjunto de resultados, como o buffer vinculado ao *TargetValuePtr* no **SQLBindCol,** geralmente têm um argumento de tipo associado, como o argumento *TargetType* no **SQLBindCol**. Neste argumento, o aplicativo passa o identificador de tipo C que corresponde ao tipo do buffer. Por exemplo, na seguinte chamada para **SQLBindCol,** o valor SQL_C_TYPE_DATE informa ao driver que o buffer *Date* é uma SQL_DATE_STRUCT:  
  
    ```  
    SQL_DATE_STRUCT Date;  
    SQLINTEGER  DateInd;  
    SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &Date, 0, &DateInd);  
    ```  
  
     Para obter mais informações sobre identificadores de tipos, consulte a seção Tipos de dados na seção [ODBC,](../../../odbc/reference/develop-app/data-types-in-odbc.md) mais tarde nesta seção.  
  
-   **Tipo predefinido.** Os buffers usados para enviar e recuperar opções ou atributos, como o buffer apontado pelo argumento *InfoValuePtr* no **SQLGetInfo,** têm um tipo fixo que depende da opção especificada. O driver assume que o buffer de dados é desse tipo; é responsabilidade do aplicativo alocar um buffer desse tipo. Por exemplo, na chamada a seguir para **SQLGetInfo,** o driver assume que o buffer é um inteiro de 32 bits porque é isso que a opção SQL_STRING_FUNCTIONS requer:  
  
    ```  
    SQLUINTEGER StringFuncs;  
    SQLGetInfo(hdbc, SQL_STRING_FUNCTIONS, (SQLPOINTER) &StringFuncs, 0,  
                NULL);  
    ```  
  
 O driver usa o tipo de dados C para interpretar os dados no buffer.

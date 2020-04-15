---
title: Sequências de fuga em ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC]
- SQL statements [ODBC], escape sequences
- escape sequences [ODBC], about escape sequences
ms.assetid: cf229f21-6c38-4b5b-aca8-f1be0dfeb3d0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4d41b0c03ecbe6de63cba1a28a1f39f12a42dc86
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300416"
---
# <a name="escape-sequences-in-odbc"></a>Sequências de escape no ODBC
Uma série de recursos de idioma, como as junções externas e as chamadas de função escalar, são comumente implementados por DBMSs. No entanto, as sintaxe para essas características tendem a ser específicas do DBMS, mesmo quando as sintaxes padrão são definidas pelos diversos órgãos de padrões. Por causa disso, o ODBC define seqüências de fuga que contêm sintaxes padrão para os seguintes recursos de idioma:  
  
-   Literals de data, hora, carimbo de data e intervalo de data  
  
-   Funções escalares como funções numéricas, string e data type conversion  
  
-   Como predicado personagem de fuga  
  
-   Junções externas  
  
-   Chamadas de procedimento  
  
 A seqüência de fuga usada pela ODBC é a seguinte:  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>Comentários  
 A seqüência de fuga é reconhecida e analisado por drivers, que substituem as seqüências de fuga por gramática específica do DBMS. Para obter mais informações sobre a sintaxe da seqüência de fuga, consulte [Seqüências de fuga ODBC](../../../odbc/reference/appendixes/odbc-escape-sequences.md) no apêndice C: Gramática SQL.  
  
> [!NOTE]  
>  Em ODBC 2. *x*, esta foi a sintaxe padrão da seqüência de fuga: **--(fornecedor\*(nome**_do fornecedor),_**)**_extensão_ **), product(**_product-name_ ** \*** do produto (nome do produto)--  
>   
>  Além dessa sintaxe, foi definida uma sintaxe taquigrafia da forma: **{**_extensão_**}**  
>   
>  Em ODBC 3. *x*, a forma longa da seqüência de fuga foi preterida, e a forma taquigrafia é usada exclusivamente.  
  
 Como as seqüências de fuga são mapeadas pelo driver para sintaxes específicas do DBMS, um aplicativo pode usar a seqüência de fuga ou a sintaxe específica do DBMS. No entanto, os aplicativos que usam a sintaxe específica do DBMS não serão interoperáveis. Ao usar a seqüência de fuga, os aplicativos devem certificar-se de que o atributo de declaração SQL_ATTR_NOSCAN está desligado, o que é por padrão. Caso contrário, a seqüência de fuga será enviada diretamente para a fonte de dados, onde geralmente causará um erro de sintaxe.  
  
 Os drivers suportam apenas as seqüências de fuga que podem mapear para os recursos de linguagem subjacentes. Por exemplo, se a fonte de dados não suportar aadesão externa, o driver também não. Para determinar quais seqüências de fuga são suportadas, um aplicativo chama **SQLGetTypeInfo** e **SQLGetInfo**. Para obter mais informações, consulte a próxima seção, [Data, Hora e Carimbo de Tempo Literals](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Data, hora e literais de carimbo de data/hora](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [Chamadas de função escalar](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [Caractere de escape de predicado LIKE](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [Junções Externas](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [Chamadas de procedimento](../../../odbc/reference/develop-app/procedure-calls.md)

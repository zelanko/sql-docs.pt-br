---
title: Sequências em ODBC de escape | Microsoft Docs
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
- escape sequences [ODBC]
- SQL statements [ODBC], escape sequences
- escape sequences [ODBC], about escape sequences
ms.assetid: cf229f21-6c38-4b5b-aca8-f1be0dfeb3d0
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2a62b9712801d2412385cc191b0649bae69be74
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="escape-sequences-in-odbc"></a>Sequências de escape de ODBC
Um número de recursos de idioma, como junções externas e chamadas de função escalar, geralmente é implementado por DBMSs. No entanto, sintaxes para esses recursos costumam ser DBMS específico, mesmo quando sintaxes padrão são definidos por vários corpos de padrões. Por isso, o ODBC define sequências de escape que contêm sintaxes padrão para os seguintes recursos de idioma:  
  
-   Literais de intervalo de data, hora, carimbo de hora e data e hora  
  
-   Funções escalares como numérico, cadeia de caracteres e funções de conversão de tipo de dados  
  
-   COMO o caractere de escape de predicado  
  
-   Junções externas  
  
-   Chamadas de procedimento  
  
 A sequência de escape usada pelo ODBC é o seguinte:  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>Remarks  
 A sequência de escape é reconhecida e analisada por drivers, substitua as sequências de escape a gramática de DBMS específico. Para obter mais informações sobre a sintaxe de sequência de escape, consulte [sequências de Escape ODBC](../../../odbc/reference/appendixes/odbc-escape-sequences.md) na gramática do apêndice c: SQL.  
  
> [!NOTE]  
>  No ODBC 2. *x*, essa era a sintaxe padrão da sequência de escape: **– (\*fornecedor (***nome do fornecedor***), product (***nome do produto***) * extensão*  **\*)--**  
>   
>  Além dessa sintaxe, uma sintaxe abreviada foi definida no formato: **{***extensão***}**  
>   
>  Em ODBC 3. *x*, o formato longo da sequência de escape foi preterido e a forma abreviada é usada exclusivamente.  
  
 Como as sequências de escape são mapeadas pelo driver para sintaxes de DBMS específico, um aplicativo pode usar a sequência de escape ou uma sintaxe específica de DBMS. No entanto, os aplicativos que usam a sintaxe específica do DBMS não serão interoperáveis. Ao usar a sequência de escape, aplicativos assegure-se de que o atributo de instrução SQL_ATTR_NOSCAN está desativado, que é o padrão. Caso contrário, a sequência de escape será enviada diretamente à fonte de dados, onde ele geralmente causará um erro de sintaxe.  
  
 Drivers de suportam a apenas as sequências de escape que podem ser mapeados para os recursos de linguagem subjacente. Por exemplo, se a fonte de dados não der suporte a junções externas, não será o driver. Para determinar quais sequências de escape têm suporte, um aplicativo chama **SQLGetTypeInfo** e **SQLGetInfo**. Para obter mais informações, consulte a próxima seção, [data, hora e literais de carimbo de hora](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Data, hora e literais de carimbo de data/hora](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [Chamadas de função escalar](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [Caractere de escape de predicado LIKE](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [Junções externas](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [Chamadas de procedimento](../../../odbc/reference/develop-app/procedure-calls.md)

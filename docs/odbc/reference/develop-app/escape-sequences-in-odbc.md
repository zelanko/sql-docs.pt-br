---
title: Sequências de escape no ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3866a45a2b55a5372769eacc0bb6b0eb1e5c088f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62942969"
---
# <a name="escape-sequences-in-odbc"></a>Sequências de escape no ODBC
Um número de recursos de linguagem, como junções externas e chamadas de função escalar, normalmente é implementado pelos DBMSs. No entanto, as sintaxes para esses recursos costumam ser específicos de DBMS, mesmo quando as sintaxes padrão são definidas por vários órgãos de padrões. Por isso, o ODBC define sequências de escape que contêm as sintaxes padrão para os seguintes recursos de idioma:  
  
-   Literais de intervalo de data, hora, carimbo de hora e data e hora  
  
-   Funções escalares como numérico, cadeia de caracteres e funções de conversão de tipo de dados  
  
-   COMO o caractere de escape de predicado  
  
-   Junções externas  
  
-   Chamadas de procedimento  
  
 A sequência de escape usada pelo ODBC é o seguinte:  
  
```  
  
(extension)  
  
```  
  
## <a name="remarks"></a>Comentários  
 A sequência de escape é reconhecida e analisada por drivers, que substituem as sequências de escape com gramática específica do DBMS. Para obter mais informações sobre a sintaxe de sequência de escape, consulte [sequências de Escape de ODBC](../../../odbc/reference/appendixes/odbc-escape-sequences.md) no Apêndice c: Gramática SQL.  
  
> [!NOTE]  
>  No ODBC 2. *x*, essa era a sintaxe padrão da sequência de escape: **– (\*fornecedor (**_nome do fornecedor_**), produto (** _nome do produto_**)**_extensão_  **\*) –**  
>   
>  Essa sintaxe, além de uma sintaxe abreviada foi definida no formato: **{**_extensão_**}**  
>   
>  Em ODBC 3. *x*, a forma longa da sequência de escape foi preterida e a forma abreviada é usada exclusivamente.  
  
 Como as sequências de escape são mapeadas pelo driver para sintaxes de DBMS específico, um aplicativo pode usar a sequência de escape ou a sintaxe específica de DBMS. No entanto, os aplicativos que usam a sintaxe específica de DBMS não será interoperáveis. Ao usar a sequência de escape, aplicativos assegure-se de que o atributo da instrução SQL_ATTR_NOSCAN está desativado, que é o padrão. Caso contrário, a sequência de escape será enviada diretamente para a fonte de dados, onde ele normalmente causará um erro de sintaxe.  
  
 Drivers de suportam a apenas essas sequências de escape que eles podem mapear para recursos de linguagem subjacente. Por exemplo, se a fonte de dados não oferece suporte a junções externas, nem será o driver. Para determinar se há suporte para quais sequências de escape, um aplicativo chama **SQLGetTypeInfo** e **SQLGetInfo**. Para obter mais informações, consulte a próxima seção, [data, hora e literais de carimbo de hora](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Data, hora e literais de carimbo de data/hora](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md)  
  
-   [Chamadas de função escalar](../../../odbc/reference/develop-app/scalar-function-calls.md)  
  
-   [Caractere de escape de predicado LIKE](../../../odbc/reference/develop-app/like-predicate-escape-character.md)  
  
-   [Junções externas](../../../odbc/reference/develop-app/outer-joins.md)  
  
-   [Chamadas de procedimento](../../../odbc/reference/develop-app/procedure-calls.md)

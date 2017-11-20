---
title: "Regras para conversões | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- numeric data type [ODBC], literals
- conversions with numeric literals [ODBC]
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: 89f846a3-001d-496a-9843-ac9c38dc1762
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 06baaaff03f75cbf04da86527a25ea60755a473e
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="rules-for-conversions"></a>Regras para conversões
As regras nesta seção se aplicam para conversões que envolvem literais numéricos. Para a finalidade dessas regras, os termos a seguir são definidos:  
  
-   *Armazenar atribuição:* ao enviar dados em uma coluna de tabela em um banco de dados. Isso ocorre durante as chamadas **SQLExecute**, **SQLExecDirect**, e **SQLSetPos**. Durante a atribuição de armazenamento "target" refere-se a uma coluna de banco de dados e "fonte" refere-se a dados em buffers do aplicativo.  
  
-   *Atribuição de recuperação:* ao recuperar dados do banco de dados em buffers do aplicativo. Isso ocorre durante as chamadas **SQLFetch**, **SQLGetData**, **SQLFetchScroll**, e **SQLSetPos**. Durante a atribuição de recuperação "target" refere-se aos buffers de aplicativo e "fonte" refere-se para a coluna de banco de dados.  
  
-   *CS:* o valor da fonte de caractere.  
  
-   *NT:* o valor de destino numérico.  
  
-   *NS:* o valor da fonte de numérico.  
  
-   *CT:* o valor de destino de caractere.  
  
-   Precisão de um literal numérico exato: o número de dígitos que ele contém.  
  
-   A escala de um literal numérico exato: o número de dígitos à direita do período explícitas ou implícita.  
  
-   A precisão de um literal numérico aproximado: a precisão de seu mantissa.  
  
## <a name="character-source-to-numeric-target"></a>Caractere de origem para destino numérico  
 Estas são as regras para converter de uma fonte de caractere (CS) em um destino numérico (NT):  
  
1.  Substitua CS com o valor obtido ao remover espaços à esquerda ou à direita em CS. Se CS não é válido *literal numérico*, SQLSTATE 22018 (valor de caractere inválido para especificação de coerção) será retornado.  
  
2.  Substitua CS com o valor obtido pela remoção de zeros à esquerda antes do ponto decimal, à direita zeros após o ponto decimal, ou ambos.  
  
3.  Converta CS NT. Se a conversão resulta em perda de dígitos significativos, SQLSTATE 22003 (valor numérico fora do intervalo) será retornado. Se a conversão resulta na perda de dígitos de espaços, SQLSTATE 01S07 (Truncamento fracionário) será retornado.  
  
## <a name="numeric-source-to-character-target"></a>Origem numéricos para o destino de caractere  
 Estas são as regras para converter de uma origem numéricos (NS) para um destino de caractere (CT):  
  
1.  Permitir que o LT ter o comprimento em caracteres do CT. Para a atribuição de recuperação, LT é igual ao comprimento do buffer em caracteres menos o número de bytes no caractere null de terminação para este conjunto de caracteres.  
  
2.  Casos:  
  
    -   Se NS é um tipo numérico exato, deixe YP igual a cadeia de caracteres mais curta que está de acordo com a definição de *exato numérico-literal* , de modo que a escala de YP é o mesmo que a escala de NS e o valor interpretado YP é o valor absoluto de NS.  
  
    -   Se NS é um tipo numérico aproximado, deixe YP ser uma cadeia de caracteres da seguinte maneira:  
  
         Caso:  
  
         Se NS é igual a 0, YP é 0.  
  
         Permitir que YSN ser a cadeia de caracteres mais curta que está de acordo com a definição de exatamente -*literal numérico* e cujo valor interpretado é o valor absoluto de NS. Se o comprimento de YSN é menor que (*precisão* + 1) do tipo de dados de NS, deixe YP igual YSN.  
  
         Caso contrário, YP é a cadeia de caracteres mais curta que está de acordo com a definição de *aproximado numérico-literal* cujo valor interpretado é o valor absoluto de NS e cujo *mantissa* consiste em um único *dígitos* que é não '0', seguido por um *período* e um *inteiro não assinado*.  
  
3.  Caso:  
  
    -   Se NS for menor que 0, deixe Y ser o resultado de:  
  
         '-' &#124; &#124; YP  
  
         onde ' &#124; &#124;' é o operador de concatenação de cadeia de caracteres.  
  
         Caso contrário, deixe Y igual YP.  
  
4.  Permitir que o r ter o comprimento em caracteres de Y.  
  
5.  Caso:  
  
    -   Se r é igual a longo prazo, CT é definido como Y.  
  
    -   Se r for menor que LT, CT é definido como Y estendido à direita pelo número correto de espaços.  
  
         Caso contrário (r > LT), copie os primeiros caracteres de longo prazo de Y para CT.  
  
         Caso:  
  
         Se esta for uma atribuição de armazenamento, retorna o erro SQLSTATE 22001 (dados de cadeia de caracteres, truncados à direita).  
  
         Se esta for a atribuição de recuperação, retorne o aviso SQLSTATE 01004 (dados de cadeia de caracteres, truncados à direita). Quando a cópia resulta na perda de dígitos fracionários (diferente de zeros à direita), é definido pelo driver se ocorrer um dos seguintes:  
  
         (1) o driver trunca a cadeia de caracteres em Y para uma escala apropriada (que pode ser zero também) e grava o resultado em CT.  
  
         (2) o driver Arredonda a cadeia de caracteres em Y para uma escala apropriada (que pode ser zero também) e grava o resultado em CT.  
  
         (3) o driver não trunca nem Arredonda, mas apenas copia os primeiros caracteres de longo prazo de Y CT.


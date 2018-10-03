---
title: Regras para conversões | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], literals
- conversions with numeric literals [ODBC]
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: 89f846a3-001d-496a-9843-ac9c38dc1762
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3ecee500204303dfcbcd8e179b9cb9cb0a94bae
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47706094"
---
# <a name="rules-for-conversions"></a>Regras para conversões
As regras nesta seção se aplicam para conversões que envolvem literais numéricos. Para fins dessas regras, os seguintes termos são definidos:  
  
-   *Atribuição de Store:* ao enviar dados para uma coluna de tabela em um banco de dados. Isso ocorre durante chamadas para **SQLExecute**, **SQLExecDirect**, e **SQLSetPos**. Durante a atribuição de armazenamento, "target" refere-se a uma coluna de banco de dados e "fonte" refere-se aos dados em buffers do aplicativo.  
  
-   *Atribuição de recuperação:* ao recuperar dados do banco de dados em buffers do aplicativo. Isso ocorre durante chamadas para **SQLFetch**, **SQLGetData**, **SQLFetchScroll**, e **SQLSetPos**. Durante a atribuição de recuperação "target" refere-se aos buffers de aplicativo e "fonte" refere-se para a coluna de banco de dados.  
  
-   *CS:* o valor na fonte de caractere.  
  
-   *NT:* o valor no destino numérico.  
  
-   *NS:* o valor na fonte de numérico.  
  
-   *CT:* o valor no destino de caractere.  
  
-   Precisão de um literal numérico exato: o número de dígitos que ele contém.  
  
-   A escala de um literal numérico exato: o número de dígitos à direita do período contratual ou legal.  
  
-   A precisão de um literal numérico aproximado: a precisão de seu mantissa.  
  
## <a name="character-source-to-numeric-target"></a>Caractere de origem para destino numérico  
 A seguir estão as regras de conversão de uma fonte de caractere (CS) para um destino numérico (NT):  
  
1.  Substitua o CS com o valor obtido ao remover espaços à esquerda ou à direita no CS. Se CS não é válido *literal numérico*, SQLSTATE 22018 (valor de caractere inválido para especificação de conversão) será retornado.  
  
2.  Substitua o CS com o valor obtido pela remoção de zeros à esquerda antes do ponto decimal, à direita zeros após o ponto decimal, ou ambos.  
  
3.  Converta CS NT. Se a conversão resulta em perda de dígitos significativos, SQLSTATE 22003 (valor numérico fora do intervalo) será retornado. Se a conversão resulta na perda de dígitos não significativas, SQLSTATE 01S07 (Truncamento fracionário) será retornado.  
  
## <a name="numeric-source-to-character-target"></a>Origem de numérica para o destino de caractere  
 A seguir estão as regras de conversão de uma fonte numérica (NS) para um destino de caractere (CT):  
  
1.  Permitir que o LT seja o comprimento em caracteres de CT. Para a atribuição de recuperação, LT é igual ao tamanho do buffer em caracteres menos o número de bytes no caractere nulo de terminação para esse conjunto de caracteres.  
  
2.  Casos:  
  
    -   Se NS é um tipo numérico exato, em seguida, permitir que YP igual a cadeia de caracteres mais curta que esteja de acordo com a definição de *exato numérico-literal* , de modo que a escala de YP é o mesmo que a escala de NS, e o valor interpretado YP é o valor absoluto de NS.  
  
    -   Se NS é um tipo numérico aproximado, em seguida, permitir que YP seja uma cadeia de caracteres da seguinte maneira:  
  
         Caso:  
  
         Se NS é igual a 0, YP é 0.  
  
         Permitir que o YSN seja a cadeia de caracteres mais curta que esteja de acordo com a definição de exato -*literal numérico* e cujo valor interpretado é o valor absoluto de NS. Se o comprimento de YSN é menor que (*precisão* + 1) do tipo de dados de NS, deixe YP YSN ser igual.  
  
         Caso contrário, YP é a cadeia de caracteres mais curta que esteja de acordo com a definição de *aproximado numérico-literal* cujo valor interpretado é o valor absoluto de NS e cujo *mantissa* consiste em um única *dígito* que é não '0', seguido por um *período* e um *inteiro sem sinal*.  
  
3.  Caso:  
  
    -   Se NS é menor que 0, em seguida, permitir que Y seja o resultado de:  
  
         '-' &AMP;#124; &AMP;#124; YP  
  
         em que '&#124;&#124;' é o operador de concatenação de cadeia de caracteres.  
  
         Caso contrário, deixe o Y igual YP.  
  
4.  Permitir que LY seja o comprimento em caracteres de Y.  
  
5.  Caso:  
  
    -   Se LY for igual a longo prazo, CT é definido como Y.  
  
    -   Se LY for menor que LT, CT é definido como Y estendido à direita pelo número apropriado de espaços.  
  
         Caso contrário (LY > LT), copie os primeiros caracteres LT de Y para CT.  
  
         Caso:  
  
         Se essa é uma atribuição de armazenamento, retornará o erro SQLSTATE 22001 (dados de cadeia de caracteres, truncados à direita).  
  
         Quando se trata de atribuição de recuperação, retorne o aviso SQLSTATE 01004 (dados de cadeia de caracteres, truncados à direita). Quando a cópia resulta na perda de dígitos fracionários (diferente de zeros à direita), é definido pelo driver se ocorrer um dos seguintes:  
  
         (1) o driver trunca a cadeia de caracteres em Y para uma escala apropriada (que pode ser zero também) e grava o resultado no CT.  
  
         (2) o driver Arredonda a cadeia de caracteres em Y para uma escala apropriada (que pode ser zero também) e grava o resultado no CT.  
  
         (3) o driver nem trunca nem Arredonda, mas copia apenas os primeiros caracteres LT de Y para CT.

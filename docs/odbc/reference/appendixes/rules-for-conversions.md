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
ms.openlocfilehash: 9ca64355a80ce8892f0ea0494e165d934d8d7a88
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68057096"
---
# <a name="rules-for-conversions"></a>Regras para conversões
As regras nesta seção se aplicam a conversões que envolvem literais numéricos. Para os fins dessas regras, os seguintes termos são definidos:  
  
-   *Atribuição de repositório:* Ao enviar dados para uma coluna de tabela em um banco de dado. Isso ocorre durante chamadas para **SQLExecute**, **SQLExecDirect**e **SQLSetPos**. Durante a atribuição de armazenamento, "destino" refere-se a uma coluna de banco de dados e "origem" refere-se aos seus buffers.  
  
-   *Atribuição de recuperação:* Ao recuperar dados do banco de dado em buffers de aplicativo. Isso ocorre durante chamadas para **SQLFetch**, **SQLGetData**, **SQLFetchScroll**e **SQLSetPos**. Durante a atribuição de recuperação, "destino" refere-se aos buffers de aplicativo e "origem" refere-se à coluna de banco de dados.  
  
-   *CS:* O valor na fonte de caracteres.  
  
-   *NT:* O valor no destino numérico.  
  
-   *Ns:* O valor na fonte numérica.  
  
-   *CT:* O valor no destino de caractere.  
  
-   Precisão de um literal numérico exato: o número de dígitos que ele contém.  
  
-   A escala de um literal numérico exato: o número de dígitos à direita do período expresso ou implícito.  
  
-   A precisão de um literal numérico aproximado: a precisão de seu mantissa.  
  
## <a name="character-source-to-numeric-target"></a>Origem do caractere para destino numérico  
 A seguir estão as regras para converter de uma fonte de caracteres (CS) em um destino numérico (NT):  
  
1.  Substitua CS pelo valor obtido removendo espaços à esquerda ou à direita no CS. Se CS não for um *literal numérico*válido, SQLSTATE 22018 (valor de caractere inválido para especificação de conversão) será retornado.  
  
2.  Substitua CS pelo valor obtido removendo zeros à esquerda antes do ponto decimal, com zeros à direita após o ponto decimal ou ambos.  
  
3.  Converta CS em NT. Se a conversão resultar em uma perda de dígitos significativos, o SQLSTATE 22003 (valor numérico fora do intervalo) será retornado. Se a conversão resultar na perda de dígitos não significativos, SQLSTATE 01S07 (truncamento fracionário) será retornado.  
  
## <a name="numeric-source-to-character-target"></a>Origem numérica para destino de caractere  
 A seguir estão as regras para converter de uma fonte numérica (NS) em um destino de caractere (CT):  
  
1.  Deixe o tamanho do LT ser o comprimento em caracteres de CT. Para a atribuição de recuperação, o LT é igual ao comprimento do buffer em caracteres menos o número de bytes no caractere de terminação nula para esse conjunto de caracteres.  
  
2.  Bolsas  
  
    -   Se NS for um tipo numérico exato, deixe YP igual à cadeia de caracteres mais curta que esteja em conformidade com a definição de *literal numérico-numeric* , de modo que a escala de YP seja igual à escala de ns e o valor interpretado de YP seja o valor absoluto de ns.  
  
    -   Se NS for um tipo numérico aproximado, deixe que YP seja uma cadeia de caracteres da seguinte maneira:  
  
         Capitalização:  
  
         Se NS for igual a 0, YP será 0.  
  
         Deixe que YSN seja a cadeia de caracteres mais curta que esteja de acordo com a definição de*literal numérico* Exact e cujo valor interpretado seja o valor absoluto de ns. Se o comprimento de YSN for menor que o (*precisão* + 1) do tipo de dados do NS, deixe YP igual a YSN.  
  
         Caso contrário, YP é a cadeia de caracteres mais curta que está em conformidade com a definição de *literal de numérico aproximado* cujo valor interpretado é o valor absoluto de ns e cujo *mantissa* consiste em um único *dígito* que não é ' 0 ', seguido de um *ponto* e um *inteiro não assinado*.  
  
3.  Capitalização:  
  
    -   Se NS for menor que 0, deixe que Y seja o resultado de:  
  
         '-'  &#124;&#124; YP  
  
         onde ' &#124;&#124; ' é o operador de concatenação de cadeia de caracteres.  
  
         Caso contrário, deixe Y igual a YP.  
  
4.  Deixe que LY seja o comprimento em caracteres de Y.  
  
5.  Capitalização:  
  
    -   Se LY for igual a LT, CT será definido como Y.  
  
    -   Se LY for menor que LT, CT será definido como Y estendido à direita pelo número apropriado de espaços.  
  
         Caso contrário (LY > LT), copie os primeiros caracteres de LT de Y para CT.  
  
         Capitalização:  
  
         Se essa for uma atribuição de armazenamento, retorne o erro SQLSTATE 22001 (dados de cadeia de caracteres, truncados à direita).  
  
         Se essa for uma atribuição de recuperação, retorne o aviso SQLSTATE 01004 (dados de cadeia de caracteres, truncados à direita). Quando a cópia resulta na perda de dígitos fracionários (diferentes de zeros à direita), ela é definida pelo driver se ocorrer uma das seguintes opções:  
  
         (1) o driver trunca a cadeia de caracteres em Y para uma escala apropriada (que também pode ser zero) e grava o resultado em CT.  
  
         (2) o driver Arredonda a cadeia de caracteres em Y para uma escala apropriada (que também pode ser zero) e grava o resultado em CT.  
  
         (3) o driver não trunca nem arredonda, mas apenas copia os primeiros caracteres de LT de Y em CT.

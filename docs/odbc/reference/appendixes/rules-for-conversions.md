---
title: Regras para Conversões | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c49177d62fffc3b3b5c47a25bf3fb421d7564245
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305082"
---
# <a name="rules-for-conversions"></a>Regras para conversões
As regras desta seção aplicam-se a conversões envolvendo literais numéricos. Para efeitos destas regras, são definidos os seguintes termos:  
  
-   *Atribuição da loja:* Ao enviar dados para uma coluna de tabela em um banco de dados. Isso ocorre durante as chamadas para **SQLExecute,** **SQLExecDirect**e **SQLSetPos**. Durante a atribuição do armazenamento, "destino" refere-se a uma coluna de banco de dados e "fonte" refere-se a dados em buffers de aplicativos.  
  
-   *Atribuição de recuperação:* Ao recuperar dados do banco de dados em buffers de aplicativos. Isso ocorre durante as chamadas para **SQLFetch,** **SQLGetData,** **SQLFetchScroll**e **SQLSetPos**. Durante a atribuição de recuperação, "destino" refere-se aos buffers do aplicativo e "origem" refere-se à coluna do banco de dados.  
  
-   *CS:* O valor na fonte do personagem.  
  
-   *NT:* O valor no alvo numérico.  
  
-   *NS:* O valor na fonte numérica.  
  
-   *CT:* O valor no alvo do personagem.  
  
-   Precisão de um literal numérico exato: o número de dígitos que contém.  
  
-   A escala de um literal numérico exato: o número de dígitos à direita do período expresso ou implícito.  
  
-   A precisão de um literal numérico aproximado: a precisão de sua locantes.  
  
## <a name="character-source-to-numeric-target"></a>Fonte de caractere para alvo numérico  
 A seguir estão as regras para converter de uma fonte de caracteres (CS) para um alvo numérico (NT):  
  
1.  Substitua CS pelo valor obtido removendo quaisquer espaços de liderança ou de arrasto em CS. Se CS não for um *numérico-literal*válido, SQLSTATE 22018 (valor de caractere inválido para especificação do elenco) é devolvido.  
  
2.  Substitua CS pelo valor obtido removendo zeros de liderança antes do ponto decimal, perdendo zeros após o ponto decimal, ou ambos.  
  
3.  Converta CS em NT. Se a conversão resultar em uma perda de dígitos significativos, SQLSTATE 22003 (valor numérico fora do alcance) é devolvido. Se a conversão resultar na perda de dígitos não significativos, SQLSTATE 01S07 (truncação fracionada) é devolvido.  
  
## <a name="numeric-source-to-character-target"></a>Fonte numérica para o destino do personagem  
 A seguir estão as regras para converter de uma fonte numérica (NS) para um alvo de caracteres (CT):  
  
1.  Deixe lt ser o comprimento em caracteres de CT. Para atribuição de recuperação, lt é igual ao comprimento do buffer em caracteres menos o número de bytes no caractere de rescisão nula para este conjunto de caracteres.  
  
2.  Casos:  
  
    -   Se NS é um tipo numérico exato, então deixe YP igualar a seqüência de caracteres mais curta que se conforma com a definição de *exato-numérico-literal* de tal forma que a escala de YP é a mesma que a escala de NS, e o valor interpretado de YP é o valor absoluto de NS.  
  
    -   Se NS é um tipo numérico aproximado, então deixe YP ser uma seqüência de caracteres da seguinte forma:  
  
         Capitalização:  
  
         Se NS é igual a 0, então YP é 0.  
  
         Que o YSN seja a seqüência de caracteres mais curta que se conforma com a definição de*exato-numérico-literal* e cujo valor interpretado é o valor absoluto de NS. Se o comprimento do YSN for menor que o *(precisão* + 1) do tipo de dados de NS, então deixe yP igualar YSN.  
  
         Caso contrário, YP é a seqüência de caracteres mais curta que se conforma com a definição de *aproximadamente-numérico-literal* cujo valor interpretado é o valor absoluto de NS e cuja *mantissa* consiste em um único *dígito* que não é '0', seguido por um *período* e um *inteiro não assinado*.  
  
3.  Capitalização:  
  
    -   Se NS é menor que 0, então deixe Y ser o resultado de:  
  
         '-' &#124;&#124; YP  
  
         onde '&#124;&#124;' é o operador de concatenação de cordas.  
  
         Caso contrário, deixe Y igual YP.  
  
4.  Let LY ser o comprimento em caracteres de Y.  
  
5.  Capitalização:  
  
    -   Se LY é igual a LT, então ct é definido como Y.  
  
    -   Se ly for menor que LT, então ct é definido como Y estendido à direita pelo número apropriado de espaços.  
  
         Caso contrário (LY > LT), copie os primeiros caracteres LT de Y em CT.  
  
         Capitalização:  
  
         Se isso for uma atribuição de loja, retorne o erro SQLSTATE 22001 (Dados de string, truncados à direita).  
  
         Se esta for a atribuição de recuperação, retorne o aviso SQLSTATE 01004 (dados de string, truncados à direita). Quando a cópia resulta na perda de dígitos fracionados (além de zeros de arrasto), é definido pelo driver se um dos seguintes ocorre:  
  
         (1) O motorista trunca a corda em Y para uma escala apropriada (que também pode ser zero) e grava o resultado em TC.  
  
         (2) O motorista arredonda a corda em Y para uma escala apropriada (que também pode ser zero) e grava o resultado em TOMOGRAFIA.  
  
         (3) O motorista não trunca nem arredonda, mas apenas copia os primeiros caracteres LT de Y em TC.

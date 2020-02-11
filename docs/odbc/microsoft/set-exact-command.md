---
title: Definir comando exato | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET EXACT command [ODBC]
ms.assetid: 9533d3e0-e7c1-49de-a3a3-0cc4373a91cb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 686ecc89f44bac4b219b760e55160f451a15c503
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67997731"
---
# <a name="set-exact-command"></a>Comando SET EXACT
Especifica as regras para comparar duas cadeias de caracteres de comprimentos diferentes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ATIVADO  
 Especifica que as expressões devem corresponder ao caractere para que o caractere seja equivalente. Quaisquer espaços em branco à direita nas expressões são ignorados para a comparação. Para a comparação, o menor das duas expressões é preenchido à direita com espaços em branco para corresponder ao comprimento da expressão mais longa.  
  
 OFF  
 (Padrão.) Especifica que, para ser equivalente, as expressões devem corresponder ao caractere para o caractere até que o final da expressão no lado direito seja atingido.  
  
## <a name="remarks"></a>Comentários  
 A configuração definir exato não terá efeito se ambas as cadeias de caracteres tiverem o mesmo comprimento.  
  
## <a name="string-comparisons"></a>Comparações de cadeia de caracteres  
 O Visual FoxPro tem dois operadores relacionais que testam a igualdade.  
  
 O operador = executa uma comparação entre dois valores do mesmo tipo. Esse operador é adequado para comparar dados de caractere, numéricos, de data e lógicos.  
  
 No entanto, quando você compara expressões de caracteres com o operador =, os resultados podem não ser exatamente o esperado. As expressões de caracteres são um caractere de comparação de caractere da esquerda para a direita até que uma das expressões não seja igual à outra, até que o final da expressão no lado direito do operador = seja atingido (definido como desativado) ou até que as extremidades das duas expressões sejam atingido (definir exato em).  
  
 O operador = = pode ser usado quando uma comparação exata de dados de caracteres é necessária. Se duas expressões de caracteres forem comparadas com o operador = =, as expressões em ambos os lados do operador = = deverão conter exatamente os mesmos caracteres, incluindo espaços em branco, a serem considerados iguais. A configuração definir exato é ignorada quando as cadeias de caracteres são comparadas usando = =.  
  
 A tabela a seguir mostra como a opção de operador e a configuração SET EXACT afetam as comparações. (Um sublinhado representa um espaço em branco.)  
  
|Comparação|= EXATO DESATIVADO|= EXACT EM|= = EXACT ON ou OFF|  
|----------------|------------------|-----------------|--------------------------|  
|"ABC" = "ABC"|Corresponde|Corresponde|Corresponde|  
|"AB" = "ABC"|Sem correspondência|Sem correspondência|Sem correspondência|  
|"ABC" = "AB"|Corresponde|Sem correspondência|Sem correspondência|  
|"ABC" = "ab_"|Sem correspondência|Sem correspondência|Sem correspondência|  
|"AB" = "ab_"|Sem correspondência|Corresponde|Sem correspondência|  
|"ab_" = "AB"|Corresponde|Corresponde|Sem correspondência|  
|"" = "AB"|Sem correspondência|Sem correspondência|Sem correspondência|  
|"AB" = ""|Corresponde|Sem correspondência|Sem correspondência|  
|"__" = ""|Corresponde|Corresponde|Sem correspondência|  
|"" = "___"|Sem correspondência|Corresponde|Sem correspondência|  
|TRIM ("___") = ""|Corresponde|Corresponde|Corresponde|  
|"" = TRIM ("___")|Corresponde|Corresponde|Corresponde|  
  
## <a name="see-also"></a>Consulte Também  
 [Comando SET ANSI](../../odbc/microsoft/set-ansi-command.md)

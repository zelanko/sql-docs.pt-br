---
title: Operadores em expressões (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: d22dc8b6-4353-40e7-91a1-65e8dae6325d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4499e62cf8564705b96ec74d2598c311e0097709
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47817094"
---
# <a name="operators-in-expressions-report-builder-and-ssrs"></a>Operadores em expressões (Construtor de Relatórios e SSRS)
  Um operador é um símbolo que representa ações aplicadas a um ou mais termos em uma expressão. As seguintes categorias de operadores têm suporte em uma expressão: aritmética, de comparação, de concatenação, lógica ou de bit a bit e de deslocamento de bit.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="arithmetic"></a>Aritmética  
 Os operadores aritméticos executam operações matemáticas sobre dois termos numéricos em uma expressão.  
  
|Operador|Descrição|  
|--------------|-----------------|  
|^|Eleva um número à potência de outro número.|  
|*|Multiplica dois números.|  
|/|Divide dois números e retorna um resultado de ponto flutuante.|  
|\|Divide dois números e retorna um resultado de número inteiro.|  
|Mod|Retorna o resto inteiro de uma divisão. Por exemplo, 7 Mod 5 = 2 porque o resto de 7 dividido por 5 é 2.|  
|+|Soma dois números.|  
|-|Retorna a diferença entre dois números ou indica o valor negativo de um termo numérico.|  
  
### <a name="comparison"></a>Comparação  
 Os operadores de comparação testam se duas expressões são iguais.  
  
|Operador|Descrição|  
|--------------|-----------------|  
|<|Menor que.|  
|\<=|Menor que ou igual a.|  
|>|Maior que.|  
|>=|Maior que ou igual a.|  
|=|Igual a.|  
|<>|Diferente de.|  
|Como|Determina se uma cadeia de caracteres específica corresponde a um padrão especificado. Um padrão pode incluir caracteres normais e curingas. Durante a correspondência de padrões, os caracteres normais devem corresponder exatamente aos caracteres especificados na cadeia de caracteres. No entanto, os caracteres curinga podem ser correspondidos a fragmentos arbitrários da cadeia de caracteres. O uso de caracteres curinga torna o operador LIKE mais flexível que o uso dos operadores de comparação de cadeias de caracteres = e !=.<br /><br /> A tabela a seguir lista os caracteres que podem ser usados como curingas:<br /><br /> %: qualquer cadeia de zero ou mais caracteres.<br /><br /> _: qualquer caractere único.<br /><br /> [ ]: qualquer caractere único dentro do intervalo (por exemplo, [a-f]) ou conjunto (por exemplo, [aeiou]) especificado.<br /><br /> [^]: qualquer caractere único que não esteja dentro do intervalo (por exemplo, [^a-f]) ou conjunto (por exemplo, [^aeiou]) especificado|  
|Is|Compara duas referências de objeto.|  
  
### <a name="string-concatenation"></a>Concatenação de cadeias de caracteres  
 A concatenação de cadeias de caracteres anexa a segunda cadeia de caracteres à primeira em uma expressão. Para outras operações de cadeia de caracteres, use funções internas.  
  
|Operador|Descrição|  
|--------------|-----------------|  
|&|Concatena duas cadeias de caracteres|  
|+|Concatena duas cadeias de caracteres|  
  
### <a name="logical-and-bitwise"></a>Lógico e de bit a bit  
 Os operadores lógicos e de bit a bit executam manipulações lógicas entre dois termos inteiros em uma expressão.  
  
|Operador|Descrição|  
|--------------|-----------------|  
|And|Executa uma conjunção lógica em duas expressões boolianas ou uma conjunção bit a bit em duas expressões numéricas.|  
|Not|Executa uma negação lógica em uma expressão booliana ou uma negação bit a bit em uma expressão numérica.|  
|Ou|Executa uma disjunção lógica em duas expressões boolianas ou uma disjunção bit a bit em dois valores numéricos.|  
|Xor|Executa uma operação de exclusão lógica em duas expressões boolianas ou uma exclusão bit a bit em duas expressões numéricas.|  
|AndAlso|Executa a conjunção lógica em duas expressões.|  
|OrElse|Executa a disjunção lógica em duas expressões.|  
  
### <a name="bit-shift"></a>Bit Shift  
 Os operadores bit a bit executam manipulações de bit entre dois termos inteiros em uma expressão.  
  
|Operador|Descrição|  
|--------------|-----------------|  
|<\<|Executa um deslocamento aritmético à esquerda em um padrão de bit.|  
|>>|Executa um deslocamento aritmético à direita em um padrão de bit.|  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo Expressão](http://msdn.microsoft.com/library/e6c74ccb-4594-4d4f-b958-618d710e34eb)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Caixa de diálogo Expressão &#40;Construtor de Relatórios&#41;](http://msdn.microsoft.com/library/e89c4d97-5d41-4b55-8695-79329edac15d)  
  
  

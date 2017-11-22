---
title: Identificadores (MDX) | Microsoft Docs
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords:
- formats [Analysis Services]
- Multidimensional Expressions [Analysis Services], identifiers
- identifiers [MDX]
- MDX [Analysis Services], identifiers
- delimited identifiers [MDX]
- regular identifiers [MDX]
- formats [Analysis Services], identifiers
ms.assetid: 739a8a67-bef3-4b56-961d-ee96cfc36b5b
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 00a7afcd3ff4b5c6be42f88bf4f7435ac4c20054
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="identifiers-mdx"></a>Identificadores (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Um identificador é o nome de um [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] objeto. Cada objeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] pode e deve ter um identificador. Isto inclui cubos, dimensões, hierarquias, níveis, membros e assim por diante. Use o identificador de um objeto para fazer referência ao objeto em instruções MDX.  
  
 Dependendo de como o objeto for nomeado, o identificador será um identificador normal ou delimitado.  
  
> [!NOTE]  
>  Identificadores regulares e delimitados devem conter de 1 a 100 caracteres.  
  
## <a name="using-regular-identifiers"></a>Usando identificadores normais  
 Um identificador normal é um nome de objeto que está em conformidade com as regras de formatação a seguir para identificadores normais. Um identificador normal pode ser usado com ou sem delimitadores.  
  
### <a name="formatting-rules-for-regular-identifiers"></a>Regras de formatação para identificadores normais  
  
1.  O primeiro caractere deve ser um dos seguintes:  
  
    -   Uma letra, conforme definido pelo padrão Unicode 2.0. Além dos caracteres de letras de outros idiomas, a definição de letras do Unicode inclui caracteres latinos de a até z e de A até Z.  
  
    -   O sublinhado (_).  
  
2.  Os caracteres subsequentes podem ser:  
  
    -   Letras, como definido no Unicode Standard 2.0.  
  
    -   Números decimais do latim básico ou outros scripts nacionais.  
  
    -   O sublinhado (_).  
  
3.  O identificador não deve ser uma palavra-chave MDX reservada. As palavras-chave reservadas fazem diferenciação entre maiúsculas e minúsculas em MDX. Para obter mais informações, consulte [palavras-chave reservadas &#40; Sintaxe MDX &#41; ](../mdx/reserved-keywords-mdx-syntax.md).  
  
4.  Não são permitidos espaços ou caracteres especiais.  
  
### <a name="examples-of-regular-identifiers"></a>Exemplos de identificadores normais  
 Na instrução MDX a seguir, os identificadores, `Measures`, `Product` e `Style`, estão em conformidade com as regras de formatação para identificadores normais. Esses identificadores normais não precisam de delimitadores.  
  
 `SELECT Measures.MEMBERS ON COLUMNS,`  
  
 `Product.Style.CHILDREN ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 ``  
  
 Embora não seja obrigatório, você também pode usar delimitadores com identificadores normais. Na instrução MDX a seguir, os identificadores normais `Measures`, `Product` e `Style` foram delimitados corretamente com colchetes.  
  
 `SELECT [Measures].MEMBERS ON COLUMNS,`  
  
 `[Product].[Style].CHILDREN ON ROWS`  
  
 `FROM [Adventure Works]`  
  
 ``  
  
## <a name="using-delimited-identifiers"></a>Usando identificadores delimitados  
 O identificador que não cumpre as regras de formatação dos identificadores normais deve ser sempre delimitado com colchetes ([]).  
  
> [!NOTE]  
>  Delimitadores são apenas para identificadores. Os delimitadores não podem ser utilizados para palavras-chave, estejam elas marcadas ou não como reservadas no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 Você pode usar um identificador delimitado nas seguintes situações:  
  
-   Quando o nome de um objeto ou parte do nome usar palavras reservadas.  
  
     Recomendamos que palavras-chave reservadas não sejam usadas como nomes de objeto. Bancos de dados atualizados de versões anteriores do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] podem conter identificadores que incluem palavras não reservadas na versão anterior, mas são palavras reservadas para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Até que seja possível alterar o identificador do objeto, você pode fazer referência ao objeto usando um identificador delimitado.  
  
-   Quando o nome de um objeto usa caracteres não listados como identificadores qualificados.  
  
     O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] permite um identificador delimitado use qualquer caractere na página de código atual. Porém, a utilização indiscriminada de caracteres especiais em um nome de objeto pode tornar as instruções e os scripts MDX difíceis de ler e manter.  
  
### <a name="formatting-rules-for-delimited-identifiers"></a>Regras de formatação para identificadores delimitados  
 O corpo de um identificador delimitado pode conter qualquer combinação de caracteres na página de código atual, incluindo os próprios caracteres de delimitação. Se o corpo do identificador delimitado contiver caracteres de delimitação, será necessário um tratamento especial:  
  
-   Se o corpo do identificador contiver somente um colchete esquerdo ([), não será necessária nenhuma manipulação especial.  
  
-   Se o corpo do identificador contiver um colchete direito (]), será necessário especificar dois colchetes direitos (]]).  
  
### <a name="examples-of-delimited-identifiers"></a>Exemplos de identificadores delimitados  
 Na instrução MDX hipotética a seguir, `Sales Volume`, `Sales Cube` e `select` são identificadores delimitados:  
  
 `-- The [Sales Volume] and [Sales Cube] identifiers contain a space.`  
  
 `SELECT Measures.[Sales Volume]`  
  
 `FROM [Sales Cube]`  
  
 `WHERE Product.[select]`  
  
 `-- The [select] identifier is a reserved keyword.`  
  
 Neste próximo exemplo, o nome de um objeto é `Total Profit [Domestic]`. Para fazer referência este objeto, você deve usar o seguinte identificador delimitado:  
  
 `[Total Profit [Domestic]]]`  
  
 O colchete esquerdo antes de `Domestic` não precisou ser alterado para criar o identificador delimitado. Porém, o colchete direito depois de `Domestic` precisou ser substituído por dois colchetes direitos.  
  
### <a name="delimiting-identifiers-with-multiple-parts"></a>Identificadores delimitados com várias partes  
 Quando você usar nomes de objeto qualificado, você terá que delimitar mais de um dos identificadores que compõem o nome do objeto. Por exemplo, o identificador Front Brakes no código a seguir precisa ser delimitado.  
  
 SELECT [Measures].MEMBERS ON COLUMNS,  
  
 [Product].[Product].[Front Brakes] ON ROWS  
  
 FROM [Adventure Works]  
  
 Além disso, o identificador Measures no exemplo anterior foi delimitado para demonstrar a delimitação de mais de um identificador.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de linguagem MDX &#40; MDX &#41;](../mdx/mdx-language-reference-mdx.md)   
 [Conceitos básicos de consulta MDX &#40; Analysis Services &#41;](../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)   
 [Elementos de sintaxe MDX &#40; MDX &#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  

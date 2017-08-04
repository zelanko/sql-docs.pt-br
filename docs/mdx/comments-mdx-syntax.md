---
title: "Comentários (sintaxe MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- remarks [MDX]
- MDX [Analysis Services], comments
- commenting characters
- nonexecuting text strings [MDX]
- Multidimensional Expressions [Analysis Services], comments
- comments [MDX]
ms.assetid: 9c00b30c-28f6-4f23-b812-ccc0e900daa5
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 372ef0470c32b4bb7fc6f6b2094a1e3b4d1a7013
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="comments-mdx-syntax"></a>Comments (sintaxe MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Comentários são cadeias de caracteres de texto não executáveis em código de programa. Os comentários também são conhecidos como observações. Use comentários para documentar códigos ou desabilitar temporariamente partes de instruções de linguagem MDX e scripts que estão sendo diagnosticados. Com a utilização de comentários para documentar códigos, fica mais fácil fazer a manutenção de códigos posterior. Frequentemente, os comentários são utilizados para registrar o nome do programa, o nome do autor e as datas de alterações de código principais. Use também os comentários para descrever cálculos complexos ou explicar um método de programação.  
  
 Os comentários em MDX seguem estas diretrizes:  
  
-   Todos os caracteres alfanuméricos ou símbolos podem ser usados com o comentário. [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ignora todos os caracteres dentro de um comentário.  
  
-   Não há um comprimento máximo para um comentário dentro de um script ou instrução. O comentário pode ser composto por uma ou mais linhas.  
  
 O MDX oferece suporte a três tipos de caracteres de comentário:  
  
 // (barras duplas)  
 Esses caracteres de comentário podem ser utilizados na mesma linha que o código a ser executado, ou em uma linha específica. Tudo que estiver a partir das barras duplas até o final da linha faz parte do comentário. Em um comentário de várias linhas, as barras duplas devem ser exibidas no início de cada linha de comentário. Para obter mais informações, consulte [&#40; Comentário &#41; &#40; MDX &#41; ](../mdx/comment-mdx-double-slash.md).  
  
 -- (hífens duplos)  
 Esses caracteres de comentário podem ser utilizados na mesma linha que o código a ser executado, ou em uma linha específica. Tudo que estiver a partir dos hífens duplos até o final da linha faz parte do comentário. Em um comentário de várias linhas, os hífens duplos devem ser exibidos no início de cada linha de comentário. Para obter mais informações, consulte [-&#40; Comentário &#41; &#40; MDX &#41; ](../mdx/comment-mdx-operator-reference.md).  
  
 /* ... \*/ (pares de barra e asterisco caracteres)  
 Esses caracteres de comentário podem ser usados na mesma linha de código a ser executado em linhas específicas ou mesmo dentro do código executável. Desde o par de comentário de abertura (/\*) para o par de comentário de fechamento (\*/) é considerado parte do comentário. Para um comentário de várias linhas, o par de caracteres de comentário de abertura (/\*) deve iniciar o comentário e o par de caracteres de comentário de fechamento (\*/) deve terminar o comentário. Nenhum outro caractere de comentário pode aparecer em nenhuma linha do comentário. Para obter mais informações, consulte [/ *... \*/ (Comment)](../mdx/comment-mdx.md).  
  
## <a name="example"></a>Exemplo  
 A consulta a seguir mostra exemplos dos três tipos de comentário:  
  
 `//An example of a comment using the double-forward slash`  
  
 `--An example of a comment using the double-hypen`  
  
 `/*An example of a`  
  
 `multi-line`  
  
 `comment*/`  
  
 `SELECT`  
  
 `{[Measures].[Internet Sales Amount]}`  
  
 `ON Columns,`  
  
 `[Date].[Calendar].MEMBERS`  
  
 `ON Rows`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>Consulte também  
 [Elementos de sintaxe MDX &#40; MDX &#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  


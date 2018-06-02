---
title: Comentários (sintaxe MDX) | Microsoft Docs
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c2a5c543ca5f611c671566dcbdac16f2248a59af
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34578448"
---
# <a name="comments-mdx-syntax"></a>Comments (sintaxe MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Comentários são cadeias de caracteres de texto não executáveis em código de programa. Os comentários também são conhecidos como observações. Use comentários para documentar códigos ou desabilitar temporariamente partes de instruções de linguagem MDX e scripts que estão sendo diagnosticados. Com a utilização de comentários para documentar códigos, fica mais fácil fazer a manutenção de códigos posterior. Frequentemente, os comentários são utilizados para registrar o nome do programa, o nome do autor e as datas de alterações de código principais. Use também os comentários para descrever cálculos complexos ou explicar um método de programação.  
  
 Os comentários em MDX seguem estas diretrizes:  
  
-   Todos os caracteres alfanuméricos ou símbolos podem ser usados com o comentário. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ignora todos os caracteres dentro de um comentário.  
  
-   Não há um comprimento máximo para um comentário dentro de um script ou instrução. O comentário pode ser composto por uma ou mais linhas.  
  
 O MDX oferece suporte a três tipos de caracteres de comentário:  
  
 // (barras duplas)  
 Esses caracteres de comentário podem ser utilizados na mesma linha que o código a ser executado, ou em uma linha específica. Tudo que estiver a partir das barras duplas até o final da linha faz parte do comentário. Em um comentário de várias linhas, as barras duplas devem ser exibidas no início de cada linha de comentário. Para obter mais informações, consulte [ &#40;comentário&#41; &#40;MDX&#41;](../mdx/comment-mdx-double-slash.md).  
  
 -- (hífens duplos)  
 Esses caracteres de comentário podem ser utilizados na mesma linha que o código a ser executado, ou em uma linha específica. Tudo que estiver a partir dos hífens duplos até o final da linha faz parte do comentário. Em um comentário de várias linhas, os hífens duplos devem ser exibidos no início de cada linha de comentário. Para obter mais informações, consulte [– &#40;comentário&#41; &#40;MDX&#41;](../mdx/comment-mdx-operator-reference.md).  
  
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
 [Elementos de sintaxe MDX &#40;MDX&#41;](../mdx/mdx-syntax-elements-mdx.md)  
  
  

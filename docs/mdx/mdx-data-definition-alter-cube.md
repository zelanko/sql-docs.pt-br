---
title: "ALTERAR a instrução de CUBE (MDX) | Microsoft Docs"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- Cube
- ALTER_CUBE
- ALTER CUBE
- ALTER
dev_langs: kbMDX
helpviewer_keywords:
- ALTER CUBE statement
- cubes [Analysis Services], modifying
- modifying cubes
ms.assetid: 2f0af61b-f509-4e1a-990f-20a215d22994
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 8780f95cab9d124b78d486e86b78897a2f2d6d39
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-data-definition---alter-cube"></a>Definição de dados MDX - ALTER CUBE
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Altera a estrutura de um cubo especificado, geralmente usado para oferecer suporte ao write-back de dimensão. Para obter mais informações sobre como usar o write-back em um aplicativo, consulte esta postagem de blog: [criando um aplicativo de write-back com o Analysis Services (blog)](http://go.microsoft.com/fwlink/?LinkId=394977)  
  
 Observe que os write-backs de dimensão simultâneos podem resultar em um deadlock, onde o primeiro write-back é bloqueado de uma confirmação devido ao bloqueio compartilhado mantido pelo segundo write-back. Nenhum erro é gerado nessa situação, mas nenhuma operação pode avançar. Por fim, os dois write-backs expiram e as alterações são revertidas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER CUBE  
      Cube_Name | CURRENTCUBE  
      <alter clause>   
            [ < alter clause> ...n]  
  
< alter clause> ::=   
   <create dimension member clause>   
  | <remove dimension member clause>  
  | <move dimension member clause>   
    | <update clause>   
    | <create cell calculation clause>  
  
<create dimension member clause> ::=  
CREATE DIMENSION MEMBER [ParentName.]MemberName  
    , [[KEY = Key_Value]   
    | [Property_Name = Property_Value[, ...n]]  
  
<dropping clause>::=  
DROP   
      DIMENSION MEMBER Member_Name   
            Member_Name ...n ]   
      [WITH DESCENDANTS]  
      | [ SESSION ] [ CALCULATED ] MEMBER Member_Name   
                  [ ,Member_Name,...n ]   
    | SET Set_Name  
                  [ ,Set_Name,...n ]   
    | [ SESSION ] CELL CALCULATION CellCalc_Name  
                  [ ,CellCalc_Name,...n ]   
    | ACTION Action_Name  
  
<move dimension member clause> ::=  
MOVE DIMENSION MEMBER MemberName  
        [, SKIPPED_LEVELS = Unsigned_Integer]   
      [WITH DESCENDANTS]  
    UNDER ParentName      
  
<update clause> ::=  
UPDATE   
    CUSTOM ROLLUP FOR MEMBER MemberName  
      [,MemberName, ...n] AS MDX_Expression  
   | DIMENSION Dimension_Name | Hierarchy_Name  
      , DEFAULT_MEMBER = MDX_Expression  
   | DIMENSION MEMBER MemberName AS  
   [MDX_Expression]  
   [Property_Name = Property_Value[, ...n]]  
  
<create cell calculation clause>::=  
CELL CALCULATION Calculation_Name   
   FOR Set_Expression AS MDX_Expression   
            [ [ CONDITION = 'Logical_Expression' ]   
    | [ DISABLED = { TRUE | FALSE } ]   
    | [ DESCRIPTION =String ]   
    | [ CALCULATION_PASS_NUMBER = Integer]   
    | [ CALCULATION_PASS_DEPTH = Integer]   
    | [ SOLVE_ORDER = Integer]   
    | [ Calculation_Name= Scalar_Expression ], ...n]  
```  
  
## <a name="creating-a-dimension-member"></a>Criando um membro de dimensão  
 Uma linha nova é adicionada à tabela de dimensões subjacente.  
  
### <a name="arguments"></a>Argumentos  
 *ParentName*  
 Uma expressão de cadeia de caracteres válida que fornece o nome do pai do novo membro de dimensão, a não ser que o membro esteja sendo criado na raiz.  
  
 *Nome do membro*  
 Uma expressão de cadeia de caracteres válida que fornece um nome de membro.  
  
 *Key_Value*  
 Uma expressão escalar válida que define o valor de chave do novo membro de dimensão.  
  
 *Property_Name*  
 Um identificador MDX válido que representa uma propriedade de membro.  
  
 *Property_Value*  
 Uma expressão escalar MDX válida que define o valor de propriedade do membro calculado.  
  
## <a name="dropping-a-dimension-member"></a>Descartando um membro de dimensão  
 O descarte de um membro de uma dimensão habilitada para gravação exclui o membro e a linha correspondente da tabela de dimensões subjacente.  
  
### <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Uma expressão de cadeia de caracteres válida fornecendo um nome de cubo.  
  
 *Member_Name*  
 Uma expressão de cadeia de caracteres válida que fornece um nome ou uma chave de membro.  
  
### <a name="remarks"></a>Remarks  
 Se a cláusula WITH DESCENDANTS não for utilizada, os filhos de um membro descartado se tornam filhos do pai do membro descartado. Se a cláusula WITH DESCENDENTES for utilizada, todos os descendentes e suas linhas na tabela de dimensões também serão descartados.  
  
> [!NOTE]  
>  Para obter informações sobre como descartar membros calculados, conjuntos nomeados, ações e cálculos de célula, consulte [a instrução DROP do membro &#40; MDX &#41; ](../mdx/mdx-data-definition-drop-member.md), [Remover instrução SET &#40; MDX &#41; ](../mdx/mdx-data-definition-drop-set.md), [Remover instrução ação &#40; MDX &#41; ](../mdx/mdx-data-definition-drop-action.md), e [remover instrução de CÁLCULO de CÉLULA &#40; MDX &#41; ](../mdx/mdx-data-definition-drop-cell-calculation.md).  
  
## <a name="updating-the-default-dimension-member"></a>Atualizando o membro de dimensão padrão  
 Essa cláusula atualiza o membro padrão de um cubo e é usada no script de cálculo MDX para definir um membro padrão. O membro padrão pode ser especificado para a dimensão de banco de dados, uma dimensão de cubo ou para o logon de um usuário. O membro padrão também pode ser alterado durante uma sessão.  
  
### <a name="arguments"></a>Argumentos  
 *Dimension_Name*  
 Uma cadeia de caracteres válida que fornece o nome de uma dimensão.  
  
 *MDX_Expression*  
 Uma linguagem MDX válida que retorna um único membro.  
  
### <a name="remarks"></a>Remarks  
 A linguagem MDX especificada pode ser estática ou dinâmica.  
  
## <a name="moving-a-dimension-member"></a>Movendo um membro de dimensão  
 Uma linha é modificada na tabela de dimensões subjacente.  
  
### <a name="arguments"></a>Argumentos  
 *ParentName*  
 Uma expressão de cadeia de caracteres válida que fornece o nome do novo pai do membro de dimensão que está sendo movido.  
  
 *Nome do membro*  
 Uma expressão de cadeia de caracteres válida que fornece um nome de membro.  
  
 Unsigned_*inteiro*  
 Um número válido que especifica o número de níveis a serem ignorados.  
  
 Se a cláusula WITH DESCENDENTES for especificada, a árvore inteira será movida. Se a cláusula WITH DESCENDANTS não for especificada, os filhos de um pai movido se tornam filhos do pai do membro movido. A movimentação é feita simplesmente para atualizar os valores da coluna principal de pais na tabela de dimensões subjacente.  
  
## <a name="updating-a-dimension-member"></a>Atualizando um membro de dimensão  
 A cláusula UPDATE DIMENSION MEMBER permite modificar propriedades de um membro, bem como da fórmula de membro personalizado associada a um membro.  
  
### <a name="arguments"></a>Argumentos  
 *Nome do membro*  
 Uma expressão de cadeia de caracteres válida que fornece um nome de membro.  
  
 *MDX_Expression*  
 Uma linguagem MDX válida que retorna um único membro.  
  
 *Property_Value*  
 Uma expressão MDX escalar válida que define o valor de propriedade do membro calculado.  
  
## <a name="creating-a-cell-calculation"></a>Criando um cálculo de célula  
 Para obter mais informações sobre como criar um cálculo de célula usando a instrução ALTER CUBE, consulte [instrução DROP de CÁLCULO de CÉLULA &#40; MDX &#41; ](../mdx/mdx-data-definition-drop-cell-calculation.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções de definição de dados MDX &#40; MDX &#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  

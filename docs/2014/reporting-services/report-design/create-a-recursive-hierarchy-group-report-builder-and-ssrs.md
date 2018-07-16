---
title: Criar um grupo de hierarquias recursivas (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8b830ba5-4d64-4348-a2b1-76b9338a1462
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 3c4144787ac5085c4713781569d7e6d364ff7951
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37172167"
---
# <a name="create-a-recursive-hierarchy-group-report-builder-and-ssrs"></a>Criar um grupo de hierarquia recursiva (Construtor de Relatórios e SSRS)
  Um grupo de hierarquia recursiva organiza dados de um único conjunto de dados de relatório que contém vários níveis hierárquicos, como a estrutura de subordinação para relações gerente-funcionários em uma hierarquia organizacional.  
  
 Antes de poder organizar os dados em uma tabela como um grupo de hierarquia recursiva, é preciso que haja um único conjunto de dados contendo todos os dados hierárquicos, campos separados para o item a ser agrupado e para o item pelo qual agrupar. Por exemplo, um conjunto de dados no qual você deseja agrupar os funcionários recursivamente sob o gerente pode conter um nome, um nome de funcionário, uma ID de funcionário e uma ID de gerente.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-create-a-recursive-hierarchy-group"></a>Para criar um grupo de hierarquia recursiva  
  
1.  Na exibição de Design, adicione uma tabela e arraste os campos do conjunto de dados que serão exibidos. Normalmente, o campo que você deseja mostrar como uma hierarquia está na primeira coluna.  
  
2.  Clique com o botão direito do mouse em qualquer lugar da tabela para selecioná-la. O painel Agrupamento exibe o grupo de detalhes da tabela selecionada. No painel Grupos de Linhas, clique com o botão direito do mouse no grupo **Detalhes**e clique em **Editar Grupo**. A caixa de diálogo **Propriedades do Grupo** é aberta.  
  
3.  Em **Expressões de grupo**, clique em **Adicionar**. Uma nova linha aparece na grade.  
  
4.  Na lista **Agrupar em** , digite ou selecione o campo a ser agrupado.  
  
5.  Clique em **Avançado**.  
  
6.  Na lista **Pai Recursivo** , insira ou selecione o campo pelo qual agrupar.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Execute o relatório. O relatório exibe o grupo de hierarquia recursiva, embora não haja recuo para mostrar a hierarquia.  
  
### <a name="to-format-a-recursive-hierarchy-group-with-indent-levels"></a>Para formatar um grupo de hierarquia recursiva com níveis de recuo  
  
1.  Clique na caixa de texto que contém o campo ao qual você deseja adicionar níveis de recuo para exibir um formato de hierarquia. As propriedades da caixa de texto aparecem no painel Propriedades.  
  
    > [!NOTE]  
    >  Se o painel Propriedades não for exibido, clique em **Propriedades** na guia **Exibir** .  
  
2.  No painel Propriedades, expanda o `Padding` nó, clique em **esquerda**e, na lista suspensa, selecione  **\<Expression... >**.  
  
3.  No painel Expressão, digite a seguinte expressão:  
  
     `=CStr(2 + (Level()*10)) + "pt"`  
  
     Todas as propriedades de Preenchimento requerem uma cadeia de caracteres no formato *nnyy*, sendo que *nn* é um número e *yy* é a unidade de medida. O exemplo de expressão cria uma cadeia de caracteres que usa o `Level` função para aumentar o tamanho do preenchimento com base no nível de recursão. Por exemplo, uma linha com um nível de 1 resultaria em um preenchimento de (2 + (1\*10))=12 pt, e uma linha com um nível de 3 resultaria em um preenchimento de (2 + (3\*10))=32 pt. Para obter informações sobre o `Level` , consulte [nível](report-builder-functions-level-function.md).  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Execute o relatório. O relatório exibe uma exibição hierárquica dos dados agrupados.  
  
## <a name="see-also"></a>Consulte também  
 [Criando grupos de hierarquia recursiva &#40;relatórios e SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Referência de funções de agregação &#40;relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md)   
 [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](tables-report-builder-and-ssrs.md)   
 [Matrizes &#40;Construtor de Relatórios e SSRS&#41;](create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  

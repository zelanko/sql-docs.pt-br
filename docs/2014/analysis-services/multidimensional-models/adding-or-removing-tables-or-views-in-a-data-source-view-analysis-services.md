---
title: Adicionando ou removendo tabelas ou exibições em dados (Analysis Services) de exibição da fonte | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.tablespane.f1
helpviewer_keywords:
- deleting tables
- tables [Analysis Services]
- removing tables
- adding tables
- data source views [Analysis Services], tables
- tables [Analysis Services], data source views
ms.assetid: 98307d04-6548-4d7d-9244-2371dd165249
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0ac190f75b626cf2007dee5c885c45672276ee35
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37179063"
---
# <a name="adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services"></a>Adicionando ou removendo tabelas ou exibições em uma exibição da fonte de dados (Analysis Services)
  Depois de criar uma DSV (exibição da fonte de dados) no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você pode modificá-lo no Designer da Exibição da Fonte de Dados adicionando ou removendo tabelas e colunas, inclusive tabelas e colunas de outra fonte de dados.  
  
 Para abrir a DSV no Designer da Exibição da Fonte de Dados, clique duas vezes na DSV no Gerenciador de Soluções. Após abrir a DSV, você pode usar o comando **Adicionar/Remover Tabelas** na barra de botões ou no menu para modificar ou estender a DSV. Você também pode trabalhar com os objetos no diagrama. Por exemplo, você pode selecionar um objeto e usar a tecla Delete em seu teclado para remover um objeto.  
  
> [!WARNING]  
>  Tenha cuidado ao remover uma tabela. Remover uma tabela exclui todas as colunas e as relações associadas do DSV e invalida todos os objetos associados àquela tabela.  
  
## <a name="selecting-tables-or-views-to-add-or-remove"></a>Selecionando tabelas ou exibições para adicionar ou remover  
 Usando a caixa de diálogo **Adicionar/Remover Tabelas** , é possível mover tabelas ou exibições entre as listas **Objetos disponíveis** e **Objetos incluídos** . A lista **Objetos disponíveis** inicialmente inclui todas as tabelas ou exibições da fonte de dados primária que ainda não estão na exibição da fonte de dados. Se a fonte de dados primários a `OPENROWSET` função, você também pode adicionar tabelas ou exibições de outras fontes de dados no projeto ou banco de dados.  
  
 Quando você adiciona ou remove uma tabela da DSV, também adiciona ou remove essa tabela do diagrama selecionado na DSV. Para obter mais informações sobre diagramas, consulte [Work with Diagrams in Data Source View Designer &#40;Analysis Services&#41;](work-with-diagrams-in-data-source-view-designer-analysis-services.md).  
  
 Depois de mover uma tabela para a lista **Objetos incluídos** na caixa de diálogo **Adicionar/Remover Tabelas** , você pode adicionar todas as tabelas relacionadas. Essa operação adiciona as tabelas de acordo com as restrições de chave estrangeira da fonte de dados, se existir alguma. Se não existirem restrições de chave estrangeira, você pode usar o `NameMatchingCriteria` propriedade da exibição da fonte de dados para determinar as relações especificando um critério de correspondência de nomes de coluna nas tabelas para gerar relações prováveis. Se o `NameMatchingCriteria`propriedade for especificada para a exibição da fonte de dados, clique em **adicionar tabelas relacionadas** para adicionar tabelas da fonte de dados que têm nomes de coluna correspondentes. Para obter mais informações sobre como configurar o `NameMatchingCriteria` propriedade, consulte [exibições da fonte de dados em modelos multidimensionais](data-source-views-in-multidimensional-models.md).  
  
> [!NOTE]  
>  Adicionar objetos a uma exibição da fonte de dados ou removê-los dela não afeta a fonte de dados subjacente.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições da fonte de dados em modelos multidimensionais](data-source-views-in-multidimensional-models.md)   
 [Trabalhar com diagramas em Designer de exibição de fonte de dados &#40;Analysis Services&#41;](work-with-diagrams-in-data-source-view-designer-analysis-services.md)  
  
  

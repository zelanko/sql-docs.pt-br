---
title: "Adicionando ou removendo tabelas ou exibições em dados da fonte de exibição (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.dsvdesigner.tablespane.f1
helpviewer_keywords:
- deleting tables
- tables [Analysis Services]
- removing tables
- adding tables
- data source views [Analysis Services], tables
- tables [Analysis Services], data source views
ms.assetid: 98307d04-6548-4d7d-9244-2371dd165249
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7a5a6d31373d9a7dc99015db0224de0f3703ef1e
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services"></a>Adicionando ou removendo tabelas ou exibições em uma exibição da fonte de dados (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Depois de criar uma exibição da fonte de dados (DSV) em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você pode modificá-la no Designer de exibição de fonte de dados, adicionando ou removendo tabelas e colunas, incluindo tabelas e colunas de outra fonte de dados.  
  
 Para abrir a DSV no Designer da Exibição da Fonte de Dados, clique duas vezes na DSV no Gerenciador de Soluções. Após abrir a DSV, você pode usar o comando **Adicionar/Remover Tabelas** na barra de botões ou no menu para modificar ou estender a DSV. Você também pode trabalhar com os objetos no diagrama. Por exemplo, você pode selecionar um objeto e usar a tecla Delete em seu teclado para remover um objeto.  
  
> [!WARNING]  
>  Tenha cuidado ao remover uma tabela. Remover uma tabela exclui todas as colunas e as relações associadas do DSV e invalida todos os objetos associados àquela tabela.  
  
## <a name="selecting-tables-or-views-to-add-or-remove"></a>Selecionando tabelas ou exibições para adicionar ou remover  
 Usando a caixa de diálogo **Adicionar/Remover Tabelas** , é possível mover tabelas ou exibições entre as listas **Objetos disponíveis** e **Objetos incluídos** . A lista **Objetos disponíveis** inicialmente inclui todas as tabelas ou exibições da fonte de dados primária que ainda não estão na exibição da fonte de dados. Se a fonte de dados primária der suporte à função **OPENROWSET** , também será possível adicionar tabelas e exibições de outras fontes de dados do projeto ou do banco de dados.  
  
 Quando você adiciona ou remove uma tabela da DSV, também adiciona ou remove essa tabela do diagrama selecionado na DSV. Para obter mais informações sobre diagramas, consulte [Trabalhar com diagramas em um Designer de exibição da fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md).  
  
 Depois de mover uma tabela para a lista **Objetos incluídos** na caixa de diálogo **Adicionar/Remover Tabelas** , você pode adicionar todas as tabelas relacionadas. Essa operação adiciona as tabelas de acordo com as restrições de chave estrangeira da fonte de dados, se existir alguma. Se não existirem restrições de chave estrangeira, você poderá usar a propriedade **NameMatchingCriteria** da exibição da fonte de dados para determinar as relações especificando um critério para a correspondência dos nomes de colunas das tabelas para gerar relações prováveis. Se a propriedade **NameMatchingCriteria**estiver especificada para a exibição da fonte de dados, clique em **Adicionar Tabelas Relacionadas** para adicionar tabelas da fonte de dados que com nomes de coluna correspondentes. Para obter mais informações sobre como configurar a propriedade **NameMatchingCriteria** , consulte [Exibições de fontes de dados em modelos multidimensionais](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md).  
  
> [!NOTE]  
>  Adicionar objetos a uma exibição da fonte de dados ou removê-los dela não afeta a fonte de dados subjacente.  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de fontes de dados em modelos multidimensionais](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Trabalhar com diagramas em um Designer de exibição da fonte de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)  
  
  

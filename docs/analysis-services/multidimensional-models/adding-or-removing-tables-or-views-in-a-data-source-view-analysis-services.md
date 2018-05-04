---
title: Adicionando ou removendo tabelas ou exibições em dados da fonte de exibição (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2ae4ec99ca380c0405056ac6e1ca0a296f4563dc
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="adding-or-removing-tables-or-views-in-a-data-source-view-analysis-services"></a>Adicionando ou removendo tabelas ou exibições em uma exibição da fonte de dados (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Depois de criar uma DSV (exibição da fonte de dados) no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você pode modificá-lo no Designer da Exibição da Fonte de Dados adicionando ou removendo tabelas e colunas, inclusive tabelas e colunas de outra fonte de dados.  
  
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
 [Exibições da fonte de dados em modelos multidimensionais](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Trabalhar com diagramas em Designer de exibição de fonte de dados & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/work-with-diagrams-in-data-source-view-designer-analysis-services.md)  
  
  

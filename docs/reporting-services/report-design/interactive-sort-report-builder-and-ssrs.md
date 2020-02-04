---
title: Classificação interativa (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 00cafed5-1a3c-4ce0-a1fb-ff1e2613f495
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d3f379c104b5b957fba197f9ed9317b2d5b23f16
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "65580185"
---
# <a name="interactive-sort-report-builder-and-ssrs"></a>Classificação interativa (Construtor de Relatórios e SSRS)
  É possível adicionar botões de classificação interativos para permitir que um usuário alterne entres as ordens crescente e decrescente para linhas de uma tabela ou para linhas e colunas de uma matriz. O uso mais comum da classificação interativa é adicionar um botão de classificação a todos os cabeçalhos de coluna. Assim, o usuário pode escolher a coluna pela qual classificar.  
  
 No entanto, é possível adicionar um botão de classificação interativo a qualquer caixa de texto, e não apenas a cabeçalhos de coluna. Por exemplo, em uma caixa de texto de uma linha fora de um grupo de linhas, você pode especificar uma classificação para as linhas ou as colunas do grupo pai, linhas ou colunas do grupo filho, ou linhas ou colunas detalhadas. Também é possível combinar campos em uma única expressão de grupo e classificar por vários campos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Ao adicionar uma classificação interativa, você deve especificar os itens seguintes:  
  
-   **O que classificar:** linhas ou colunas?  
  
-   **Classificar pelo quê:** um campo exibido em uma coluna de tabela? Um campo que não é exibido?  
  
-   **Em que contexto classificar:** por exemplo, é possível classificar linhas associadas a grupos; colunas associadas a grupos de colunas; linhas detalhadas; grupos filho em um grupo pai ou grupos pai e filho juntos.  
  
-   **A qual caixa de texto adicionar o botão de classificação:** ao cabeçalho de coluna ou ao cabeçalho da linha do grupo?  
  
-   **Sincronizar ou não a classificação em várias regiões de dados:** é possível criar um relatório para quando o usuário alternar a ordem de classificação; as demais regiões de dados com o mesmo ancestral também são classificadas.  
  
 Para obter instruções passo a passo, consulte [Adicionar classificação interativa a uma tabela ou matriz &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md).  
  
 A seguinte tabela resume os efeitos obtidos usando botões de classificação interativos.  
  
|Ação|O que classificar|Onde adicionar o botão de classificação|O que classificar|Escopo da classificação|  
|------------|------------------|----------------------------------|---------------------|----------------|  
|Classificar linhas detalhadas de uma tabela sem grupos|Detalhes|Cabeçalho de coluna|Campo de conjunto de dados vinculado à coluna|Região de dados|  
|Classificar instâncias de grupo de nível superior para uma matriz|Grupos|Cabeçalho de coluna|Expressão de grupo do grupo pai|Região de dados|  
|Classificar linhas detalhadas de um grupo filho em uma tabela|Detalhes|Linha do cabeçalho de grupo filho|Campo de conjunto de dados de classificação|Grupo filho|  
|Classificar linhas de vários grupos de linhas e linhas detalhadas em uma tabela|Grupos, mas você deve redefinir a expressão de grupo|Cabeçalho de coluna|Agregação do campo de conjunto de dados de classificação|Região de dados|  
|Sincronizar a ordem de classificação de várias regiões de dados|Grupos|Normalmente, cabeçalho de coluna|Expressão de grupo|Dataset|  
  
 O processador de relatório aplica a classificação interativa após a aplicação de todas as expressões da região de dados e da classificação de grupo. Para obter mais informações, consulte [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md).  
  
## <a name="adding-interactive-sort-for-multiple-groups"></a>Adicionando classificação interativa a vários grupos  
 Em uma tabela com grupos de linhas aninhados com base em um único campo de conjunto de dados, é possível adicionar um botão de classificação interativo que classifica valores de grupo pai, de grupo filho ou linhas detalhadas. No entanto, talvez você queira fornecer ao usuário a possibilidade de classificar a tabela por valores dos grupos pai e filho sem que seja necessário clicar várias vezes.  
  
 Para isso, você deve refazer a tabela para agrupar uma expressão que combina vários campos. Por exemplo, em um conjunto de dados com contagens de inventário, caso a tabela original seja agrupada por tamanho e por cor, você pode especificar um único grupo com uma expressão formada por tamanho e cor. Para obter mais informações, consulte [Adicionar classificação interativa a uma tabela ou matriz &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Classificar dados em uma região de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/sort-data-in-a-data-region-report-builder-and-ssrs.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Adicionar classificação interativa a uma tabela ou matriz &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-interactive-sort-to-a-table-or-matrix-report-builder-and-ssrs.md)  
  
  

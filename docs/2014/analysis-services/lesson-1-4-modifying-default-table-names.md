---
title: Modificando nomes de tabela padrão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: ddd97483-a76d-43c1-8b40-fc7cc57fb0c2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b6e43196f5bc318630a52073e22969dc58a0e64a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66079227"
---
# <a name="modifying-default-table-names"></a>Modificando nomes de tabela padrão
  Você pode alterar o valor da propriedade **FriendlyName** para objetos na exibição da fonte de dados para facilitar sua observação e uso.  
  
 Na tarefa a seguir, você mudará o nome de cada tabela na exibição da fonte de dados removendo os prefixos "**Dim**" e "**Fact**" dessas tabelas. Isso facilitará a observação e o uso dos objetos de cubo e dimensão (que você definirá na próxima lição).  
  
> [!NOTE]  
>  Você também pode modificar os nomes amigáveis das colunas, definir colunas calculadas e unir tabelas ou exibições na exibição da fonte de dados para facilitar o uso.  
  
### <a name="to-modify-the-default-name-of-a-table"></a>Para modificar o nome padrão de uma tabela  
  
1.  No painel **Tabelas** do **Designer de Exibição da Fonte de Dados**, clique com o botão direito do mouse na tabela **FactInternetSales** e clique em **Propriedades**.  
  
2.  Se a janela Propriedades à direita da janela do Microsoft Visual Studio não for exibida, clique no botão **Ocultar Automaticamente** na barra de títulos da janela Propriedades, de modo que essa janela permaneça visível.  
  
     É mais fácil alterar as propriedades de cada tabela na exibição da fonte de dados quando a janela Propriedades permanece aberta. Caso não configure a janela para permanecer aberta usando o botão **Ocultar Automaticamente** , a janela fechará ao clicar em um objeto diferente no painel **Diagrama** .  
  
3.  Altere a propriedade **FriendlyName** do objeto **FactInternetSales** para *`InternetSales`*.  
  
     Quando você clicar fora da célula da propriedade **FriendlyName** , a alteração será aplicada. Na próxima lição, você definirá um grupo de medidas com base nessa tabela de fatos. O nome da tabela de fatos será InternetSales em vez de FactInternetSales devido à alteração feita nessa lição.  
  
4.  Clique em **DimProduct** no painel **Tabelas** . No janela Propriedades, altere a propriedade **FriendlyName** para *`Product`*.  
  
5.  Altere a propriedade **FriendlyName** de cada tabela restante na exibição da fonte de dados da mesma forma para remover o prefixo "**Dim**".  
  
6.  Quando terminar, clique no botão **Ocultar Automaticamente** para ocultar a janela Propriedades novamente.  
  
7.  No menu **Arquivo** ou na barra de ferramentas do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique em **Salvar Tudo** para salvar as alterações feitas até este momento no projeto do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Se preferir, você pode parar o tutorial aqui e retomá-lo mais tarde.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 2: Definir e implantar um cubo](lesson-2-defining-and-deploying-a-cube.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições da fonte de dados em modelos multidimensionais](multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [Alterar propriedades em uma exibição da fonte de dados &#40;Analysis Services&#41;](multidimensional-models/change-properties-in-a-data-source-view-analysis-services.md)  
  
  

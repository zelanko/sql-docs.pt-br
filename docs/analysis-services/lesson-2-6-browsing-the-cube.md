---
title: Navegando no cubo | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5b6694f699c0f8ab3ae4f82e8a3fa71a11702dae
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="lesson-2-6---browsing-the-cube"></a>Lição 2-6-navegando no cubo
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

Depois de implantar um cubo, os dados do cubo poderão ser vistos na guia **Navegador** no Designer de Cubo e os dados de dimensão poderão ser vistos na guia **Navegador** no Designer de Dimensão. Navegar dados de cubo e de dimensão é uma maneira de verificar seu trabalho incrementalmente. Você pode verificar se as pequenas alterações em propriedades, relações e outros objetos têm o efeito desejado quando o objeto é processado. Embora a guia Navegador seja usada para exibir os dados de cubo e de dimensão, a guia fornece recursos diferentes com base no objeto que você está procurando.  
  
Para dimensões, a guia Navegador fornece um modo de exibir os membros ou navegar em uma hierarquia até o nó folha. Você pode procurar dados de dimensão em idiomas diferentes, supondo que tenha adicionado as traduções a seu modelo.  
  
Para cubos, a guia Navegador fornece duas abordagens para explorar dados. Você pode usar o Designer de Consulta MDX interno para criar consultas que retornam um conjunto de linhas bidimensional de um banco de dados multidimensional. Como alternativa, você pode usar um atalho de Excel. Quando você iniciar o Excel de dentro do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], o Excel já abre com uma Tabela Dinâmica na planilha e uma conexão predefinida para o banco de dados de espaço de trabalho do modelo.  
  
O Excel geralmente oferece uma experiência de navegação melhor porque você pode explorar dados de cubo interativamente, usando eixos horizontais e verticais para analisar as relações em seus dados. Por outro lado, o Designer de Consulta MDX é limitado a um único eixo. Além disso, como o conjunto de linhas é bidimensional, você não obtém a busca detalhada fornecida por uma Tabela Dinâmica do Excel. À medida que você adiciona mais dimensões e hierarquias a seu cubo, que você fará em lições subsequentes, o Excel será a solução preferida para procurar dados.  
  
### <a name="to-browse-the-deployed-cube"></a>Para navegar no cubo implantado  
  
1.  Alterne para o **Designer de Dimensão** para a dimensão Produto no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para fazer isso, clique duas vezes na dimensão **Produto** no nó **Dimensões** do Gerenciador de Soluções.  
  
2.  Clique na guia **Navegador** para exibir o membro **Todos** da hierarquia de atributo **Product Key** . Na lição três, você definirá uma hierarquia de usuário para a dimensão Produto que permitirá navegar pela dimensão.  
  
3.  Alterne para o **Designer de Cubo** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para fazer isso, clique duas vezes no cubo **Tutorial do Analysis Services** no nó **Cubos** do Gerenciador de Soluções.  
  
4.  Selecione a guia **Navegador** e clique no ícone **Reconectar** na barra de ferramentas do designer.  
  
    O painel esquerdo do designer mostra os objetos no cubo do Tutorial do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . À direita da guia **Navegador** , existem dois painéis: o painel superior é o painel **Filtro** e o inferior é o painel **Dados** . Em uma lição posterior, o navegador de cubos será usado para fazer análises.  
  
## <a name="next-lesson"></a>Próxima lição  
[Lição 3: Modificando medidas, atributos e hierarquias](../analysis-services/lesson-3-modifying-measures-attributes-and-hierarchies.md)  
  
## <a name="see-also"></a>Consulte também  
[Editor de Consultas MDX &#40;Analysis Services - Dados Multidimensionais&#41;](http://msdn.microsoft.com/library/777f2c23-1c1c-4b72-9d19-48a4866551f8)  
  
  
  

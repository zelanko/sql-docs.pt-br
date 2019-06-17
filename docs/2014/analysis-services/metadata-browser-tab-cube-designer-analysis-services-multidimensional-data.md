---
title: Metadados (guia navegador, Designer de cubo) (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.metadatapane.f1
ms.assetid: a1ace545-488d-4645-8330-56408a5e8abd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3e4aade575cdcb8260865d4a1fe9ab6f4b7941fe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66077853"
---
# <a name="metadata-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>Metadados (guia Navegador, Designer de Cubo) (Analysis Services - Dados Multidimensionais)
  Use o painel **Metadados** na guia **Navegador** no Designer de Cubo para navegar na estrutura do cubo, para visualizar medidas relacionadas e exibir e criar dimensões. Você executar uma busca detalhada em hierarquias, exibir uma lista de medidas disponíveis e KPIs e copiar os nomes totalmente qualificados de objetos.  
  
 Você também pode arrastar os objetos e hierarquias no painel **Metadados** para a área de compilação de consulta, para criar novas consultas ou exportar dados para navegação no Excel.  
  
## <a name="options"></a>Opções  
 **Metadados**  
 Exibe os metadados disponíveis na exibição atual. Você pode alterar a exibição (isto é, a perspectiva atualmente selecionada ou cubo) clicando no ícone de cubo e usando a caixa de diálogo **Seleção de Cubo** para escolher um novo cubo ou perspectiva. Você também pode clicar em **Grupo de Medidas**e selecionar um novo grupo de medidas na lista suspensa para filtrar os objetos que estão disponíveis no painel **Metadados** .  
  
 Arraste os itens selecionados para as áreas de filtro, dados, linhas ou colunas do controle da Tabela Dinâmica do [!INCLUDE[msCoName](../includes/msconame-md.md)] Office 11.0 no painel **Relatório** para exibir os dados do item selecionado.  
  
 **Funções**  
 Exibe uma lista de todas as funções, operadores e constantes que podem ser usados para criar consultas ou exibições de dados no **Navegador**. Para usar uma função, localize o item desejado e arraste-o para a área de consulta. A definição de sintaxe é adicionada ao texto  
  
> [!WARNING]  
>  A lista **Função** não está disponível quando você está funcionando no modo de exibição de Design gráfico.  
  
 Ao trabalhar com um modelo de tabela, a lista de funções inclui funções MDX e DAX. Caso contrário, a lista incluirá apenas MDX. Um modelo multidimensional não pode usar funções DAX diretamente, embora uma expressão DAX possa ser incluída como parte de uma definição de objeto.  
  
 Dica: As pastas que contêm funções DAX são listadas todas as letras maiusculas. Todas as outras pastas contêm MDX funções. Por exemplo, há duas pastas para funções estatísticas: **ESTATÍSTICA** contém as funções relacionadas DAX.  
  
## <a name="context-menu"></a>Menu de contexto  
 As seguintes opções estão disponíveis no menu de contexto exibido ao clicar com o botão direito do mouse em um elemento exibido no painel **Metadados** :  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Adicionar à consulta**|Clique para adicionar o objeto selecionado ao painel inferior da área de compilação da consulta.|  
|**Adicionar ao filtro**|Clique para adicionar a dimensão, atributo, hierarquia ou nível selecionado à área do **Navegador**.<br /><br /> Observação: Essa opção estará habilitada apenas se uma dimensão, atributo, hierarquia ou nível estiver selecionado.|  
|**Copiar**|Clique para adicionar o item selecionado à Área de Transferência.<br /><br /> Observação: Esta opção copia o nome totalmente qualificado do objeto.|  
  
## <a name="see-also"></a>Consulte também  
 [Barra de ferramentas &#40;guia do navegador, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Analisar no Excel &#40;guia do navegador, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md)   
 [Consulta e filtro &#40;guia do navegador, Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](query-filter-browser-cube-designer-analysis-services-multidimensional-data.md)   
 [Navegador &#40;Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)  
  
  

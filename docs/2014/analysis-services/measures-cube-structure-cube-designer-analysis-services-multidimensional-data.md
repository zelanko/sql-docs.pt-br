---
title: Medidas (guia estrutura do cubo, Designer de cubo) (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.cubeeditor.cubebuilder.measurespane.f1
ms.assetid: be70f63b-58f2-4eff-81bc-c86d8229e617
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4b81387a3eb85ca695ffd9860e09a9bf2c696ba6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118440"
---
# <a name="measures-cube-structure-tab-cube-designer-analysis-services---multidimensional-data"></a>Medidas (guia Estrutura do Cubo, Designer de Cubo) (Analysis Services - Dados Multidimensionais)
  Use o painel **Medidas** para manipular grupos de medidas e membros na guia **Estrutura do Cubo** do Designer de Cubo.  
  
## <a name="options"></a>Opções  
 medidas  
 Exibe os grupos de medidas e medidas incluídas no cubo dependendo da exibição selecionada:  
  
 trEE  
 Exibe uma exibição de árvore de grupos de medidas com medidas como nós filho.  
  
 Expanda grupos de medidas para exibir medidas. Clique em um grupo de medidas ou medida selecionada para renomear o grupo de medidas ou medida, respectivamente.  
  
 Grade  
 Exibe uma grade de medidas e as respectivas propriedades mais comumente acessadas. Clique em **Adicionar nova medida** para exibir a caixa de diálogo **Nova Medida** e adicionar uma nova medida à grade.  
  
 A grade contém as seguintes colunas:  
  
 Measure  
 Digite o nome da medida.  
  
 Grupo de Medidas  
 Exibe o grupo de medidas que contém a medida.  
  
 Tipo de Dados  
 Selecione o tipo de dados da medida.  
  
 Agregação  
 Selecione a função de agregação da medida.  
  
## <a name="context-menu"></a>Menu de contexto  
 As seguintes opções estão disponíveis no menu de contexto exibido ao clicar com o botão direito do mouse no painel **Medidas** :  
  
 **Nova medida**  
 Selecione para exibir a caixa de diálogo **Nova Medida** e adicionar uma nova medida ao grupo de medidas selecionado atualmente no painel **Medidas** .  
  
 **Novo grupo de medidas**  
 Selecione para exibir a caixa de diálogo **Novo Grupo de Medidas** e adicionar um novo grupo de medidas ao painel **Medidas** .  
  
 **Mostrar medidas em**  
 Selecione para alternar entre as seguintes opções ou selecione uma das seguintes opções para alterar a exibição do painel **Medidas** :  
  
|Opção|Definição|  
|------------|----------------|  
|**Árvore**|Exiba grupos de medidas e medidas em uma exibição de árvore.|  
|**Grade**|Exiba grupos de medidas e medidas em uma grade.|  
  
 **Renomear**  
 Selecione para renomear a medida ou grupo de medidas selecionado.  
  
 **Delete (excluir)**  
 Selecione para exibir a caixa de diálogo **Excluir Objetos** e excluir os objetos selecionados no painel **Medidas** .  
  
 **Mover para Cima**  
 Selecione para mover a medida ou grupo de medidas selecionado uma posição para cima.  
  
> [!NOTE]  
>  Esta opção estará desabilitada se o item selecionado não puder ser movido para cima.  
  
 **Mover para Baixo**  
 Selecione para mover a medida ou grupo de medidas selecionado uma posição para baixo.  
  
> [!NOTE]  
>  Esta opção estará desabilitada se o item selecionado não puder ser movido para baixo.  
  
 **Novo objeto vinculado**  
 Clique para exibir o **Assistente para Objetos Vinculados** e vincular grupos de medidas e dimensões de outros cubos, e para importar ações, KPIs e cálculos ao cubo selecionado.  
  
 **Propriedades**  
 Selecione para exibir a janela **Propriedades** do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] da medida ou grupo de medidas selecionado.  
  
## <a name="see-also"></a>Consulte também  
 [Configurar propriedades de medida](multidimensional-models/configure-measure-properties.md)   
 [Medidas e grupos de medidas](multidimensional-models/measures-and-measure-groups.md)  
  
  
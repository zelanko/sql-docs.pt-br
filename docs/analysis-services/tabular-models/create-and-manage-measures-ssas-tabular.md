---
title: Criar e gerenciar medidas | Microsoft Docs
ms.custom: ''
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: edc1a4b2-96d3-4f34-bb70-6cacec79e819
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6a695bdc842c7495beee2b6c09f98cd8205e892b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="create-and-manage-measures"></a>Criar e gerenciar medidas 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Medida é uma fórmula criada para ser usada em um relatório ou Tabela Dinâmica (ou Gráfico Dinâmico) do Excel. As medidas podem se basear em funções de agregação padrão, como COUNT ou SUM, ou é possível definir sua própria fórmula usando-se o DAX. As tarefas nesse tópico descrevem como criar e gerenciar medidas usando a Grade de Medida de uma tabela.  
  
## <a name="tasks"></a>Tarefas  
 Para criar e gerenciar medidas, você usará a grade de medida de uma tabela. Você só pode exibir a grade de medida para uma tabela no designer de modelos em Exibição de Dados. Você não pode criar medidas ou exibir a grade de medida quando estiver na Exibição de Diagrama; porém, você pode exibir medidas existentes na Exibição de Diagrama. Para mostrar a grade de medida para uma tabela, clique no menu **Tabela** e em **Mostrar Grade de Medida**.  
  
###  <a name="bkmk_create_stand"></a> Para criar uma medida usando uma fórmula de agregação padrão  
  
-   Clique na coluna para a qual você deseja criar a medida, clique no menu **Coluna** , aponte para **AutoSoma**e clique em um tipo de agregação.  
  
     A medida será criada automaticamente com um nome padrão, seguido pela fórmula na primeira célula na grade de medida diretamente abaixo da coluna.  
  
###  <a name="bkmk_create_custom"></a> Para criar uma medida usando uma fórmula personalizada  
  
-   Na grade de medida, abaixo da coluna para a qual você deseja criar a medida, clique em uma célula e, na barra de fórmula, digite um nome, seguido por dois-pontos (:), seguido por um sinal de igualdade (=), seguido pela fórmula. Pressione ENTER para aceitar a fórmula.  
  
###  <a name="bkmk_edit"></a> Para editar propriedades de medida  
  
-   Na grade de medida, clique em uma medida e, na janela **Propriedades** , digite ou selecione um valor de propriedade diferente.  
  
###  <a name="bkmk_rename"></a> Para renomear uma medida  
  
-   Na grade de medida, clique em uma medida e, na janela **Propriedades** , em **Nome da Medida**, digite um novo nome e clique em ENTER.  
  
     Você também pode renomear uma medida na barra de fórmula. O nome da medida precede a fórmula, seguido por dois-pontos.  
  
###  <a name="bkmk_delete"></a> Para excluir uma medida  
  
-   Na Grade de Medida, clique com o botão direito do mouse em uma medida e clique em **Excluir**.  
  
## <a name="see-also"></a>Consulte também  
 [Medidas](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [KPIs](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [Colunas calculadas](../../analysis-services/tabular-models/ssas-calculated-columns.md)  
  
  

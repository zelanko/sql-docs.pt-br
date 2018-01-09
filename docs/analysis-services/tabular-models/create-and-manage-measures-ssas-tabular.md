---
title: Criar e gerenciar medidas (SSAS Tabular) | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: edc1a4b2-96d3-4f34-bb70-6cacec79e819
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 799ada43cebe2f6358c88c0b4aa8719186f67823
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="create-and-manage-measures-ssas-tabular"></a>Criar e Gerenciar medidas (SSAS tabular)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]Uma medida é uma fórmula que é criada para uso em um relatório ou tabela dinâmica do Excel (ou gráfico dinâmico). As medidas podem se basear em funções de agregação padrão, como COUNT ou SUM, ou é possível definir sua própria fórmula usando-se o DAX. As tarefas nesse tópico descrevem como criar e gerenciar medidas usando a Grade de Medida de uma tabela.  
  
 Este tópico inclui as seguintes tarefas:  
  
-   [Para criar uma medida usando uma fórmula de agregação padrão](#bkmk_create_stand)  
  
-   [Para criar uma medida usando uma fórmula personalizada](#bkmk_create_custom)  
  
-   [Para editar propriedades de medida](#bkmk_edit)  
  
-   [Para renomear uma medida](#bkmk_rename)  
  
-   [Para excluir uma medida](#bkmk_delete)  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Medidas &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [KPIs &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [Colunas calculadas &#40;SSAS de Tabela&#41;](../../analysis-services/tabular-models/ssas-calculated-columns.md)  
  
  

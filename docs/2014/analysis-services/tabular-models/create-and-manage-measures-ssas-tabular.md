---
title: Criar e gerenciar medidas (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: edc1a4b2-96d3-4f34-bb70-6cacec79e819
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9dff39591aee77bcb88fea4dcea78e5018786999
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121146"
---
# <a name="create-and-manage-measures-ssas-tabular"></a>Criar e Gerenciar medidas (SSAS tabular)
  Medida é uma fórmula criada para ser usada em um relatório ou Tabela Dinâmica (ou Gráfico Dinâmico) do Excel. As medidas podem se basear em funções de agregação padrão, como COUNT ou SUM, ou é possível definir sua própria fórmula usando-se o DAX. As tarefas nesse tópico descrevem como criar e gerenciar medidas usando a Grade de Medida de uma tabela.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Medidas &#40;Tabular do SSAS&#41;](measures-ssas-tabular.md)   
 [KPIs &#40;Tabular do SSAS&#41;](kpis-ssas-tabular.md)   
 [Colunas calculadas &#40;Tabular do SSAS&#41;](ssas-calculated-columns.md)  
  
  
---
title: Criar e gerenciar medidas (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: edc1a4b2-96d3-4f34-bb70-6cacec79e819
author: minewiskan
ms.author: owend
ms.openlocfilehash: fbc0d47c523be7a6a1dd421535862ac30748168a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939807"
---
# <a name="create-and-manage-measures-ssas-tabular"></a>Criar e Gerenciar medidas (SSAS tabular)
  Medida é uma fórmula criada para ser usada em um relatório ou Tabela Dinâmica (ou Gráfico Dinâmico) do Excel. As medidas podem se basear em funções de agregação padrão, como COUNT ou SUM, ou é possível definir sua própria fórmula usando-se o DAX. As tarefas neste tópico descrevem como criar e gerenciar medidas usando a grade de medida de uma tabela.  
  
 Este tópico inclui as seguintes tarefas:  
  
-   [Para criar uma medida usando uma fórmula de agregação padrão](#bkmk_create_stand)  
  
-   [Para criar uma medida usando uma fórmula personalizada](#bkmk_create_custom)  
  
-   [Para editar propriedades de medida](#bkmk_edit)  
  
-   [Para renomear uma medida](#bkmk_rename)  
  
-   [Para excluir uma medida](#bkmk_delete)  
  
## <a name="tasks"></a>Tarefas  
 Para criar e gerenciar medidas, você usará a grade de medida de uma tabela. Você só pode exibir a grade de medida para uma tabela no designer de modelos em Exibição de Dados. Você não pode criar medidas ou exibir a grade de medida quando estiver na Exibição de Diagrama; porém, você pode exibir medidas existentes na Exibição de Diagrama. Para mostrar a grade de medida para uma tabela, clique no menu **Tabela** e em **Mostrar Grade de Medida**.  
  
###  <a name="to-create-a-measure-using-a-standard-aggregation-formula"></a><a name="bkmk_create_stand"></a>Para criar uma medida usando uma fórmula de agregação padrão  
  
-   Clique na coluna para a qual você deseja criar a medida, clique no menu **Coluna** , aponte para **AutoSoma**e clique em um tipo de agregação.  
  
     A medida será criada automaticamente com um nome padrão, seguido pela fórmula na primeira célula na grade de medida diretamente abaixo da coluna.  
  
###  <a name="to-create-a-measure-using-a-custom-formula"></a><a name="bkmk_create_custom"></a> Para criar uma medida usando uma fórmula personalizada  
  
-   Na grade de medida, abaixo da coluna para a qual você deseja criar a medida, clique em uma célula e, na barra de fórmula, digite um nome, seguido por dois-pontos (:), seguido por um sinal de igualdade (=), seguido pela fórmula. Pressione ENTER para aceitar a fórmula.  
  
###  <a name="to-edit-measure-properties"></a><a name="bkmk_edit"></a>Para editar propriedades de medida  
  
-   Na grade de medida, clique em uma medida e, na janela **Propriedades** , digite ou selecione um valor de propriedade diferente.  
  
###  <a name="to-rename-a-measure"></a><a name="bkmk_rename"></a>Para renomear uma medida  
  
-   Na grade de medida, clique em uma medida e, na janela **Propriedades** , em **Nome da Medida**, digite um novo nome e clique em ENTER.  
  
     Você também pode renomear uma medida na barra de fórmula. O nome da medida precede a fórmula, seguido por dois-pontos.  
  
###  <a name="to-delete-a-measure"></a><a name="bkmk_delete"></a>Para excluir uma medida  
  
-   Na Grade de Medida, clique com o botão direito do mouse em uma medida e clique em **Excluir**.  
  
## <a name="see-also"></a>Consulte Também  
 [Medidas &#40;&#41;de tabela do SSAS](measures-ssas-tabular.md)   
 [KPIs &#40;SSAS de tabela&#41;](kpis-ssas-tabular.md)   
 [Colunas calculadas &#40;SSAS de Tabela&#41;](ssas-calculated-columns.md)  
  
  

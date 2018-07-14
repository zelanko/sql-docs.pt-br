---
title: Editor de formulário KPI (guia KPIs, Designer de cubo) (Analysis Services - dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.kpidefinitionpane.f1
ms.assetid: 45c6453a-bbe2-4ca5-836e-c7ef11cfcb65
caps.latest.revision: 23
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 284ccc63f98624e1a64b114d31b69215d8e6b1be
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37224829"
---
# <a name="kpi-form-editor-kpis-tab-cube-designer-analysis-services---multidimensional-data"></a>Editor de Formulário KPI (guia KPIs, Designer de Cubo) (Analysis Services - Dados Multidimensionais)
  Use o painel **Editor de Formulário KPI** na guia **KPIs** do Designer de Cubo para criar ou modificar o KPI (Indicador Chave de Desempenho) selecionado.  
  
> [!NOTE]  
>  Este painel é exibido apenas na exibição de formulário.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Digite o nome do KPI.  
  
 **Grupo de medidas associado**  
 Selecione o grupo de medidas associado ao KPI. O aplicativo cliente pode usar essas informações para determinar quais dimensões estão disponíveis quando o usuário procurar esse KPI.  
  
 **Expressão de valor**  
 Expanda para exibir ou editar a expressão MDX do valor do KPI.  
  
 Digite a expressão MDX que retorna o valor do KPI.  
  
 Arraste elementos selecionados do painel **Ferramentas de Cálculo** para esta opção para incluir a sintaxe MDX para o elemento selecionado.  
  
 **Expressão de meta**  
 Expanda para exibir ou editar a expressão MDX do valor de meta do KPI.  
  
 Digite a expressão MDX que retorna o valor de meta do KPI quando o KPI é executado.  
  
 Arraste elementos selecionados do painel **Ferramentas de Cálculo** para esta opção para incluir a sintaxe MDX para o elemento selecionado.  
  
 **Status**  
 Expanda para exibir as opções **Gráfico de Status** e **Expressão de status** .  
  
 **Gráfico de status**  
 Selecione o gráfico a ser usado pelo aplicativo cliente para representar o valor de status em formulário gráfico.  
  
> [!NOTE]  
>  O aplicativo cliente pode oferecer suporte ao gráfico selecionado ou substituí-lo por uma alternativa apropriada.  
  
 **Expressão de status**  
 Digite a expressão MDX que retorna o valor de status do KPI quando o KPI é executado.  
  
 Arraste elementos selecionados do painel **Ferramentas de Cálculo** para esta opção para incluir a sintaxe MDX para o elemento selecionado.  
  
 É recomendável que essa expressão retorne um número decimal entre -1 e 1. Um número mais baixo representa uma situação negativa, enquanto um número mais alto representa uma situação positiva.  
  
> [!NOTE]  
>  Valores abaixo de -1 e acima de 1 são possíveis, mas podem não ser interpretados corretamente por aplicativos cliente de terceiros.  
  
 **Tendência**  
 Expanda para exibir as opções **Gráfico de tendência** e **Expressão de tendência** .  
  
 **Gráfico de tendência**  
 Selecione o gráfico a ser usado pelo aplicativo cliente para representar o valor de tendência em formulário gráfico.  
  
> [!NOTE]  
>  O aplicativo cliente pode oferecer suporte ao gráfico selecionado ou substituí-lo por uma alternativa apropriada.  
  
 **Expressão de tendência**  
 Digite a expressão MDX que retorna o valor de tendência do KPI.  
  
 Arraste elementos selecionados do painel **Ferramentas de Cálculo** para esta opção para incluir a sintaxe MDX para o elemento selecionado.  
  
 A base da expressão de tendência pode ser qualquer critério baseado em tempo que faça sentido em um determinado contexto comercial. É recomendável que essa expressão retorne um número decimal entre -1 e 1. Um número mais baixo representa uma tendência negativa ao longo do tempo, enquanto um número mais alto representa uma tendência positiva.  
  
> [!NOTE]  
>  Valores abaixo de -1 e acima de 1 são possíveis, mas podem não ser interpretados corretamente por aplicativos cliente de terceiros.  
  
 **Propriedades Adicionais**  
 Expanda para exibir as opções **Pasta de exibição**, **KPI Pai**, **Membro da hora atual**, **Peso**e **Descrição** .  
  
 **Pasta de exibição**  
 Digite a categorização do KPI para uso pelo aplicativo cliente para fins de exibição.  
  
 Use uma barra invertida (\\) para separar nomes de pastas em uma pasta de exibição e um ponto e vírgula (;) para separar várias pastas de exibição. Por exemplo, digite `Category\Goal\Scientific;Category\Goal\Metric`.  
  
 **KPI pai**  
 Selecione um KPI existente sob o qual categorizar o KPI para uso pelo aplicativo cliente.  
  
> [!NOTE]  
>  Se essa opção for definida como um KPI existente, a **Pasta de exibição** será ignorada.  
  
 **Membro da hora atual**  
 Digite a expressão MDX que retorna o membro que identifica o contexto temporal do KPI.  
  
 Arraste elementos selecionados do painel **Ferramentas de Cálculo** para esta opção para incluir a sintaxe MDX para o elemento selecionado.  
  
> [!IMPORTANT]  
>  A expressão MDX deve retornar o nome exclusivo de um membro dentro de uma dimensão de tempo associada ao grupo de medidas especificado em **Grupo de medidas associado**.  
  
 **Weight**  
 Expanda para exibir ou editar a expressão MDX do fator de ponderação do KPI.  
  
 Arraste elementos selecionados do painel **Ferramentas de Cálculo** para esta opção para incluir a sintaxe MDX para o elemento selecionado.  
  
 **Descrição**  
 Digite a descrição opcional do KPI.  
  
## <a name="see-also"></a>Consulte também  
 [KPIs &#40;Designer de cubo&#41; &#40;Analysis Services - dados multidimensionais&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md)  
  
  

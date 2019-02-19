---
title: Especificar o tamanho de um indicador usando uma expressão (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: ab0b86f1-4882-4258-a2b6-c612faecfa4b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5a6ded6b52da2105d324ba835f6a747eb024f97a
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56298624"
---
# <a name="specify-the-size-of-an-indicator-using-an-expression-report-builder-and-ssrs"></a>Especificar o tamanho de um indicador usando uma expressão (Construtor de Relatórios e SSRS)
  Além de cor, direção e forma, você pode usar tamanho para maximizar o impacto visual de indicadores.  
  
 Um indicador tem uma coleção de estados de indicador denominados IndicatorStates. A coleção IndicatorStates normalmente tem vários estados. Cada estado é um membro da coleção e é representado por um ícone. Juntos, os estados constituem a coleção IndicatorsStates.  
  
 Para configurar dinamicamente os tamanhos de ícones, você define propriedades de membros da coleção IndicatorsStates no painel Propriedades do Construtor de Relatórios. Se o painel **Propriedades** não estiver visível, clique na guia **Exibir** e selecione **Propriedades**.  
  
> [!NOTE]  
>  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você usa a janela **Propriedades** para definir propriedades do membro. Se a janela **Propriedades** não estiver aberta, pressione a tecla F4.  
  
 O painel **Propriedades** fornece acesso às propriedades da coleção IndicatorStates de um indicador. Você configura os ícones para terem tamanhos diferentes definindo a propriedade ScaleFactor dos membros da coleção IndicatorStates usando uma expressão. Para obter mais informações, consulte [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
 A expressão usada neste procedimento também foi usada para gerar o relatório com tamanhos diferentes de indicadores, mostrada em [Indicadores &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-the-indicator-icon-size-using-an-expression"></a>Para especificar o tamanho do ícone de indicador usando uma expressão  
  
1.  Clique no indicador que você deseja alterar.  
  
2.  No painel Propriedades, localize a propriedade IndicatorStates.  
  
     Se o painel Propriedades for organizado por categoria, você localizará IndicatorStates na categoria **Estados** .  
  
3.  Clique no botão de reticências **(...)** ao lado de IndicatorStates. A caixa de diálogo **Editor de Coleções IndicatorState** será aberta.  
  
     Selecione todos os membros da coleção.  
  
4.  Na lista **Propriedades de Multisseleção** , clique na seta para baixo ao lado de ScaleFactor e clique em **Expressão**.  
  
5.  Na caixa de diálogo **Expressão** , escreva a expressão.  
  
     A expressão de exemplo a seguir cria o ícone de um tamanho diferente com base no valor do campo **SalesYTD** .  
  
     `=IIF(Fields!SalesYTD.value = 0,0,Fields!SalesYTD.value/Max(Fields!SalesYTD.value,"Indicator"))`  
  
     Para obter mais informações, consulte [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md).  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Indicadores &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  

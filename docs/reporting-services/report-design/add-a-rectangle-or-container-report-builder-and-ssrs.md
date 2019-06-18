---
title: Adicionar um retângulo ou um contêiner (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10061"
- sql13.rtp.rptdesigner.rectangleproperties.general.f1
ms.assetid: f905c35f-754d-4d02-80f3-85e29ddda826
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2079eeb5cb871b5006ac4b2c45b60e9c8a3a3c97
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65574780"
---
# <a name="add-a-rectangle-or-container-report-builder-and-ssrs"></a>Adicionar um retângulo ou um contêiner (Construtor de Relatórios e SSRS)
  Adicione um retângulo a um relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] quando quiser que um elemento gráfico separe áreas do relatório, enfatize áreas de um relatório ou forneça uma tela de fundo para um ou mais itens de relatório. Os retângulos também são usados como contêineres para ajudar a controlar a maneira como as regiões de dados são renderizadas em um relatório. Você pode personalizar a aparência de um retângulo editando suas propriedades, como plano de fundo e cores da borda. Para obter mais informações sobre como usar um retângulo como um contêiner, consulte [Retângulos e linhas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md) e [Exibir os mesmos dados em uma matriz e um gráfico &#40;Construtor de Relatórios&#41;](../../reporting-services/report-design/display-the-same-data-on-a-matrix-and-a-chart-report-builder.md).    
   
## <a name="to-add-a-rectangle"></a>Para adicionar um retângulo    
    
1.  Na guia **Inserir** , no grupo **Itens de Relatório** , clique em **Retângulo**.    
    
2.  Na superfície de design, clique no local onde deseja exibir o canto superior esquerdo do retângulo e arraste até onde deseja colocar o canto inferior direito.    
    
     À medida que você move o cursor, “linhas de ajuste” aparecem como as linhas do cursor junto com outros objetos na superfície de design. Isso será útil se você desejar alinhar os objetos.    
    
## <a name="to-create-a-container"></a>Para criar um contêiner    
    
1.  Adicione um item de relatório retângulo ao relatório.    
    
2.  Arraste outros itens de relatório para o retângulo.    
    
    > [!NOTE]    
    >  Um retângulo é um contêiner apenas para itens que você cria no retângulo ou arrasta para dentro dele. Se você desenhar um retângulo ao redor de um item que já existe na superfície de design, o retângulo não funcionará como seu contêiner.    
    
## <a name="to-change-rectangle-properties-such-as-color-style-or-weight"></a>Para alterar propriedades de retângulo, como cor, estilo ou peso    
    
1.  Selecione o retângulo e clique nas opções de cor, estilo ou peso de linha na seção **Borda** da guia Página Inicial.    
    
2.  Clique na seta próxima ao botão **Borda** para determinar quais lados do retângulo devem ser alterados.    
    
    > [!NOTE]    
    >  Se você definir o estilo da linha como **Duplo** e a largura for 1,5 pt ou mais estreita, a linha talvez não pareça dupla quando o relatório for executado no Construtor de Relatórios, no Designer de Relatórios ou no portal da Web do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] . Ela aparecerá dupla quando você exportar o relatório para outros formatos, como Microsoft Word e Acrobat PDF.    
    
## <a name="see-also"></a>Consulte Também    
 [Retângulos e linhas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md)     
 [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)    
    
  

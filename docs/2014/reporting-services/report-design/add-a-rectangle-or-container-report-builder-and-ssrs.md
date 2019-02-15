---
title: Adicionar um retângulo ou um contêiner (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10061"
- sql12.rtp.rptdesigner.rectangleproperties.general.f1
ms.assetid: f905c35f-754d-4d02-80f3-85e29ddda826
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 2b14c42d88354660c04955ddc20e7586fdc377f1
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56291474"
---
# <a name="add-a-rectangle-or-container-report-builder-and-ssrs"></a>Adicionar um retângulo ou um contêiner (Construtor de Relatórios e SSRS)
  Adicione um retângulo a seu relatório quando quiser que um elemento gráfico separe áreas do relatório, enfatize áreas de um relatório ou forneça um plano de fundo para um ou mais itens de relatório. Os retângulos também são usados como contêineres para ajudar a controlar a maneira como as regiões de dados são renderizadas em um relatório. Você pode personalizar a aparência de um retângulo editando suas propriedades, como plano de fundo e cores da borda. Para obter mais informações sobre como usar um retângulo como um contêiner, consulte [Retângulos e linhas &#40;Construtor de Relatórios e SSRS&#41;](rectangles-and-lines-report-builder-and-ssrs.md) e [Exibir os mesmos dados em uma matriz e um gráfico &#40;Construtor de Relatórios&#41;](display-the-same-data-on-a-matrix-and-a-chart-report-builder.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-rectangle"></a>Para adicionar um retângulo  
  
1.  Na guia **Inserir** , no grupo **Itens de Relatório** , clique em **Retângulo**.  
  
2.  Na superfície de design, clique no local onde deseja exibir o canto superior esquerdo do retângulo e arraste até onde deseja colocar o canto inferior direito.  
  
     À medida que você move o cursor, “linhas de ajuste” aparecem como as linhas do cursor junto com outros objetos na superfície de design. Isso será útil se você desejar alinhar os objetos.  
  
### <a name="to-create-a-container"></a>Para criar um contêiner  
  
1.  Adicione um item de relatório retângulo ao relatório.  
  
2.  Arraste outros itens de relatório para o retângulo.  
  
    > [!NOTE]  
    >  Um retângulo é um contêiner apenas para itens que você cria no retângulo ou arrasta para dentro dele. Se você desenhar um retângulo ao redor de um item que já existe na superfície de design, o retângulo não funcionará como seu contêiner.  
  
### <a name="to-change-rectangle-properties-such-as-color-style-or-weight"></a>Para alterar propriedades de retângulo, como cor, estilo ou peso  
  
1.  Selecione o retângulo e clique nas opções de cor, estilo ou peso de linha na seção **Borda** da guia Página Inicial.  
  
2.  Clique na seta próxima ao botão **Borda** para determinar quais lados do retângulo devem ser alterados.  
  
    > [!NOTE]  
    >  Se você definir o estilo de linha como **duplas** e a largura da linha é 1 1/2 pt ou mais estreita, a linha talvez não pareça dupla quando você executa o relatório no construtor de relatórios, Designer de relatórios ou Gerenciador de relatórios. Ela parecerá dupla quando você exportar o relatório para outros formatos, como Microsoft Word e Acrobat PDF.  
  
## <a name="see-also"></a>Consulte também  
 [Retângulos e linhas &#40;Construtor de Relatórios e SSRS&#41;](rectangles-and-lines-report-builder-and-ssrs.md)   
 [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md)  
  
  

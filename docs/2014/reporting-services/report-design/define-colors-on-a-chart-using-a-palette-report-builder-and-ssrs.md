---
title: Definir cores em um gráfico usando uma paleta (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: d95efc22-5a32-43d4-9bd2-12753e7fd395
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 49feffa82a1ae20735a2b9b70982782c3562c9cf
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53370088"
---
# <a name="define-colors-on-a-chart-using-a-palette-report-builder-and-ssrs"></a>Definir cores em um gráfico usando uma paleta (Construtor de Relatórios e SSRS)
  Você pode alterar a paleta de cores para um gráfico, selecionando uma paleta predefinida ou definindo uma paleta personalizada. Paletas personalizadas são específicas para relatórios.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-colors-on-the-chart-using-a-built-in-color-palette"></a>Para alterar as cores no gráfico usando uma paleta de cores interna  
  
1.  Abra o painel Propriedades.  
  
2.  Na superfície de design, clique no gráfico. São exibidas as propriedades do objeto de gráfico no painel Propriedades.  
  
     O nome do objeto (**Chart1** por padrão) é exibido na lista suspensa na parte superior do painel Propriedades.  
  
3.  Na seção **Gráfico** , da propriedade Palette, selecione uma paleta nova na lista suspensa.  
  
    > [!NOTE]  
    >  Você não pode alterar as cores nem classificar em uma paleta predefinida.  
  
### <a name="to-define-your-own-colors-on-the-chart-using-a-custom-color-palette"></a>Para definir suas próprias cores no gráfico usando uma paleta de cores personalizada  
  
1.  Abra o painel Propriedades.  
  
2.  Na superfície de design, clique no gráfico. São exibidas as propriedades do objeto de gráfico no painel Propriedades.  
  
3.  No **gráfico** seção, para o `Palette` propriedade, selecione **personalizado**.  
  
4.  Na propriedade CustomPaletteColors, clique no botão Editar Coleção (**...**). O **Editor de Coleção ReportColorExpression** é aberto.  
  
5.  Clique em **Adicionar** para adicionar uma cor. Selecione uma cor na lista suspensa ou selecione Expressão e especifique um valor hexadecimal para uma cor específica, como ff6600 para "Laranja".  
  
     Para obter mais informações sobre valores hexadecimais, consulte [Tabela de Cores](https://go.microsoft.com/fwlink/?linkid=9258) n MSDN.  
  
6.  Clique em **Adicionar** para adicionar mais cores à paleta.  
  
7.  Após concluir, clique em **OK**.  
  
 Se você estiver usando uma paleta personalizada, poderá alterar a ordem das cores para alterar a cor de séries diferentes no gráfico.  
  
## <a name="see-also"></a>Consulte também  
 [Formatando as cores da série em um gráfico &#40;Construtor de Relatórios e SSRS&#41;](formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Especificar cores consistentes em gráficos com várias formas &#40;Construtor de Relatórios e SSRS&#41;](shape-charts-report-builder-and-ssrs.md)  
  
  

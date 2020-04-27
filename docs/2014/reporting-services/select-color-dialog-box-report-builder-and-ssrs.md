---
title: Caixa de diálogo Selecionar cor (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.selectcolor.f1
- "10090"
helpviewer_keywords:
- Select Color dialog box
ms.assetid: ac7089a3-5c7b-4f53-8348-180610e86da2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6bcbbe828da811ace5df4feea5cfdf888e1e6ca5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66101378"
---
# <a name="select-color-dialog-box-report-builder-and-ssrs"></a>Caixa de diálogo Selecionar Cor (Construtor de Relatórios SSRS)
  Use a caixa de diálogo **Selecionar Cor** para especificar as opções de cor da tela de fundo de uma única ou de várias células em uma região de dados ou de uma caixa de texto, ou para um gráfico.  
  
## <a name="options"></a>Opções  
 **Seletor de cores**  
 Escolha três opções que especificam como você quer selecionar as cores:  
  
-   **Selecionador – Círculo de cor** Escolha uma cor que use valores de cores HSB (Matiz/Saturação/Brilho).  
  
-   **Selecionador – Quadrado de cores** Escolha uma cor que usa valores de cor RGB (Vermelho/Verde/Azul).  
  
-   **Paleta – Cores padrão** Escolha uma cor de uma lista predefinida de valores de cor.  
  
 **Círculo de cores**  
 Use para as cores HSB pois são valores mapeados em um sistema cilíndrico coordenado. O matiz é a cor real, a saturação é a pureza da cor, e o brilho é o brilho ou escuridão relativa.  
  
 Ao selecionar uma cor, o centro do círculo determina a cor. Use o controle deslizante de cor para alterar o matiz. As coordenadas x e y representam respectivamente os valores da saturação e do brilho.  
  
 **Quadrado de cores**  
 Use para as cores RGB pois os valores do RGB são mapeados em um sistema Cartesiano coordenado. R é o valor para Red (Vermelho), G é o valor para Green (Verde), B é o valor para Blue (Azul).  
  
 Quando você escolhe uma cor, o centro do quadrado determina a cor. Use o controle deslizante de cor para alterar o faixa da cor escolhida. As coordenadas x e y representam as outras duas cores. Por exemplo, se selecionar o verde, o controle deslizando mostra a faixas dos valores do verde, e as coordenadas x e y representam respectivamente os valores do vermelho e do azul.  
  
 **Cor da paleta padrão**  
 Use para cores nomeadas da [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] `KnownColor` enumeração.  
  
 **Sistema de cores**  
 Especifique as cores RGB ou HSB. Esta escolha altera a exibição para mostrar os valores de RGB ou HSB, que são atualizados interativamente ao usar um circulo de cores ou um quadrado de cores para o **Selecionador de cores**.  
  
 O valor **Alpha** é exibido para algumas propriedades quando uma cor é incluída em um valor de transparência. Por exemplo, preenchimento das séries do gráfico. Para propriedades que não dão suporte transparência, este valor é desabilitado.  
  
 **Vermelho**  
 O valor decimal para a parte vermelha da cor de RGB. Use a caixa de rotação para alterar o valor ou digitar um valor entre 0 e 255.  
  
 **Verde**  
 O valor decimal para a parte verde da cor de RGB. Use a caixa de rotação para alterar o valor ou digitar um valor entre 0 e 255.  
  
 **Azul**  
 O valor decimal para a parte azul da cor de RGB. Use a caixa de rotação para alterar o valor ou digitar um valor entre 0 e 255.  
  
 **Alfa**  
 O valor decimal para o alfa ou parte de transparência da cor. Quando este valor é ativado, você pode usar a opção de controle deslizante para ajustar o grau de transparência desejado.  
  
 **Matiz**  
 O valor decimal para o matiz da cor HSB. Use a caixa de rotação para alterar o valor ou digitar um valor entre 0 e 255.  
  
 **Saturação**  
 O valor decimal para a saturação da cor HSB. Use a caixa de rotação para alterar o valor ou digitar um valor entre 0 e 255.  
  
 **Brilho**  
 O valor decimal para o brilho da cor HSB. Use a caixa de rotação para alterar o valor ou digitar um valor entre 0 e 255.  
  
 **Amostra de cor**  
 Mostra o cor atual na metade esquerda do painel e mostra interativamente a nova cor que está sendo selecionada na metade direita do painel. Se não houver nenhuma cor padrão, a metade esquerda do painel será branca. A maioria das propriedades de RDL não tem nenhuma cor padrão.  
  
## <a name="see-also"></a>Consulte Também  
 [Formatando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [Formatando texto e espaços reservados &#40;Construtor de Relatórios e SSRS&#41;](report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)  
  
  

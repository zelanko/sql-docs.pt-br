---
title: Especificar uma imagem como um ponteiro em um medidor (construtor de relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9d73b3c3-a068-4868-a2be-0cd261b6e92b
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: bce410684b433d8a444d36affa91f8134673432d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122770"
---
# <a name="specify-an-image-as-a-pointer-on-a-gauge-report-builder-and-ssrs"></a>Especificar uma imagem como um ponteiro em um medidor (Construtor de Relatórios e SSRS)
  O medidor contém três estilos internos que podem ser usados para personalizar a aparência do ponteiro. Para um medidor radial, os estilos internos são: Agulha, Marcador e Barra. Para um medidor linear, os estilos internos são: Marcador, Barra e Termômetro. Se um único ponteiro for necessário, o usuário poderá criar e especificar uma imagem que pode ser usada como um ponteiro totalmente funcional.  
  
 Quando você está especificando uma imagem para o ponteiro, sua imagem deve ter as seguintes especificações:  
  
-   A origem do ponteiro, ou centro da rotação, deve estar na parte superior da imagem.  
  
-   A extremidade do ponteiro deve estar apontando para baixo.  
  
 Uma vez que o ponteiro é uma forma irregular, você precisará especificar uma cor de transparência para ocultar as partes desnecessárias da imagem. Considere usar uma cor que normalmente seria mostrada no medidor como a cor de transparência, uma vez que as cores especificadas não serão exibidas no medidor.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-an-image-as-a-pointer-on-the-gauge"></a>Para especificar uma imagem como um ponteiro no medidor  
  
1.  No modo Design, clique no ponteiro do medidor.  
  
2.  (Opcional) Se nenhum ponteiro existir no medidor, clique no medidor e selecione **adicionar ponteiro**. Um ponteiro é adicionado ao medidor.  
  
3.  Clique o **inserir** guia na faixa de opções e clique duas vezes no ícone de imagem. A caixa de diálogo **Propriedades da Imagem** será aberta.  
  
4.  Adicione uma imagem a seu relatório. Para obter mais informações, consulte [inserir uma imagem em um relatório &#40;construtor de relatórios e SSRS&#41;](report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md).  
  
5.  Abra o painel Propriedades.  
  
6.  Na superfície de design, clique no ponteiro. As propriedades do ponteiro são exibidas no painel Propriedades.  
  
7.  Expanda o nó PointerImage.  
  
8.  Em **fonte**, selecione **inserido** na lista suspensa.  
  
    > [!NOTE]  
    >  Se sua imagem for armazenada no banco de dados ou na Web, você poderá especificar a opção adequada para essa propriedade. Para obter mais informações, consulte [caixa de diálogo de propriedades de imagem, geral &#40;construtor de relatórios e SSRS&#41;](../../2014/reporting-services/image-properties-dialog-box-general-report-builder-and-ssrs.md).  
  
9. Em **valor**, selecione o nome da imagem na lista suspensa.  
  
10. Em **TransparentColor**, escolha um valor de cor que você deseja remover da imagem. Isso criará uma aparência perfeita do ponteiro no medidor.  
  
## <a name="see-also"></a>Consulte também  
 [Formatando ponteiros de um medidor &#40;Construtor de Relatórios e SSRS&#41;](report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Adicionar um medidor a um relatório &#40;SSRS e construtor de relatórios&#41;](report-design/add-a-gauge-to-a-report-report-builder-and-ssrs.md)   
 [Formatando linhas, cores e imagens &#40;Construtor de Relatórios e SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [Medidores &#40;Construtor de Relatórios e SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md)  
  
  
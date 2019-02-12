---
title: Especificar uma imagem como um ponteiro em um medidor (construtor de relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 9d73b3c3-a068-4868-a2be-0cd261b6e92b
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: 25524aa5c7f7223f07e019ae7b8c7d6f1e3d9f7f
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56027937"
---
# <a name="specify-an-image-as-a-pointer-on-a-gauge-report-builder-and-ssrs"></a>Especificar uma imagem como um ponteiro em um medidor (Construtor de Relatórios e SSRS)
  O medidor contém três estilos internos que podem ser usados para personalizar a aparência do ponteiro. Para um medidor radial, os estilos internos são: Agulha, marcador e barra. Para um medidor linear, os estilos internos são: Marcador, Barra e Termômetro. Se um único ponteiro for necessário, o usuário poderá criar e especificar uma imagem que pode ser usada como um ponteiro totalmente funcional.  
  
 Quando você está especificando uma imagem para o ponteiro, sua imagem deve ter as seguintes especificações:  
  
-   A origem do ponteiro, ou centro da rotação, deve estar na parte superior da imagem.  
  
-   A extremidade do ponteiro deve estar apontando para baixo.  
  
 Uma vez que o ponteiro é uma forma irregular, você precisará especificar uma cor de transparência para ocultar as partes desnecessárias da imagem. Considere usar uma cor que normalmente seria mostrada no medidor como a cor de transparência, uma vez que as cores especificadas não serão exibidas no medidor.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-an-image-as-a-pointer-on-the-gauge"></a>Para especificar uma imagem como um ponteiro no medidor  
  
1.  No modo Design, clique no ponteiro do medidor.  
  
2.  (Opcional) Se nenhum ponteiro existir no medidor, clique duas vezes em medidor e selecione **adicionar ponteiro**. Um ponteiro é adicionado ao medidor.  
  
3.  Clique o **inserir** guia na faixa de opções e clique duas vezes no ícone de imagem. A caixa de diálogo **Propriedades da Imagem** será aberta.  
  
4.  Adicione uma imagem a seu relatório. Para obter mais informações, consulte [inserir uma imagem em um relatório &#40;construtor de relatórios e SSRS&#41;](report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md).  
  
5.  Abra o painel Propriedades.  
  
6.  Na superfície de design, clique no ponteiro. As propriedades do ponteiro são exibidas no painel Propriedades.  
  
7.  Expanda o nó PointerImage.  
  
8.  Na **fonte**, selecione **inserido** na lista suspensa.  
  
    > [!NOTE]  
    >  Se sua imagem for armazenada no banco de dados ou na Web, você poderá especificar a opção adequada para essa propriedade. Para obter mais informações, consulte [caixa de diálogo de propriedades de imagem, geral &#40;construtor de relatórios e SSRS&#41;](../../2014/reporting-services/image-properties-dialog-box-general-report-builder-and-ssrs.md).  
  
9. Na **valor**, selecione o nome da sua imagem na lista suspensa.  
  
10. Na **TransparentColor**, selecione um valor de cor que você deseja remover da imagem. Isso criará uma aparência perfeita do ponteiro no medidor.  
  
## <a name="see-also"></a>Consulte também  
 [Formatando ponteiros de um medidor &#40;Construtor de Relatórios e SSRS&#41;](report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Adicionar um medidor a um relatório &#40;relatórios e SSRS&#41;](report-design/add-a-gauge-to-a-report-report-builder-and-ssrs.md)   
 [Formatando linhas, cores e imagens &#40;Construtor de Relatórios e SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [Medidores &#40;Construtor de Relatórios e SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md)  
  
  

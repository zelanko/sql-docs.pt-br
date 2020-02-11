---
title: Especificar uma imagem como um ponteiro em um medidor (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 9d73b3c3-a068-4868-a2be-0cd261b6e92b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c7a57987a5d1cd0ac7984db3b716521d9c7a09af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66101152"
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
  
2.  Adicional Se não existir nenhum ponteiro no medidor, clique com o botão direito do mouse no medidor e selecione **Adicionar ponteiro**. Um ponteiro é adicionado ao medidor.  
  
3.  Clique na guia **Inserir** na faixa de faixas e clique duas vezes no ícone de imagem. A caixa de diálogo **Propriedades da Imagem** será aberta.  
  
4.  Adicione uma imagem a seu relatório. Para obter mais informações, consulte [Inserir uma imagem em um relatório &#40;Construtor de relatórios e SSRS&#41;](report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md).  
  
5.  Abra o painel Propriedades.  
  
6.  Na superfície de design, clique no ponteiro. As propriedades do ponteiro são exibidas no painel Propriedades.  
  
7.  Expanda o nó PointerImage.  
  
8.  Em **origem**, selecione **inserido** na lista suspensa.  
  
    > [!NOTE]  
    >  Se sua imagem for armazenada no banco de dados ou na Web, você poderá especificar a opção adequada para essa propriedade. Para obter mais informações, consulte [caixa de diálogo Propriedades da imagem, &#40;geral Construtor de relatórios e SSRS&#41;](../../2014/reporting-services/image-properties-dialog-box-general-report-builder-and-ssrs.md).  
  
9. Em **valor**, selecione o nome da imagem na lista suspensa.  
  
10. Em **TransparentColor**, escolha um valor de cor que você deseja remover da imagem. Isso criará uma aparência perfeita do ponteiro no medidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Formatando ponteiros de um medidor &#40;Construtor de Relatórios e SSRS&#41;](report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Adicionar um medidor a um relatório &#40;Construtor de Relatórios e SSRS&#41;](report-design/add-a-gauge-to-a-report-report-builder-and-ssrs.md)   
 [Formatando linhas, cores e imagens &#40;Construtor de Relatórios e SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [Medidores &#40;Construtor de Relatórios e SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md)  
  
  

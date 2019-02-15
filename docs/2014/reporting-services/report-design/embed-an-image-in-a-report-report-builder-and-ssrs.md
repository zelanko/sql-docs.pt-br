---
title: Inserir uma imagem em um relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.embeddedimages.f1
- "10060"
ms.assetid: aed77345-5eeb-41f0-96c9-db6b4a11ec6f
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: ca23d1dfb1b35d165959d2a249130ddf9afc7678
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56288954"
---
# <a name="embed-an-image-in-a-report-report-builder-and-ssrs"></a>Inserir uma imagem em um relatório (Construtor de Relatórios e SSRS)
  Um relatório pode conter uma imagem inserida. Inserir uma imagem garante que ela estará sempre disponível para um relatório, mas também afeta o tamanho da definição de relatório, o arquivo que define o relatório. As imagens inseridas em um relatório estão listadas no painel de dados do relatório.  
  
 Talvez você queira inserir uma imagem na definição de relatório antes de adicionar a imagem à superfície de design. Para obter mais informações, consulte [Adicionar uma imagem de tela de fundo &#40;Construtor de Relatórios e SSRS&#41;](add-a-background-image-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-embed-an-image-in-a-report"></a>Para inserir uma imagem em um relatório  
  
1.  No modo design de relatório, na guia **Inserir** , clique em **Imagem**.  
  
2.  Na superfície de design, clique e arraste uma caixa até o tamanho desejado da imagem.  
  
3.  Na página **Geral** da caixa de diálogo **Propriedades da Imagem** , digite um nome na caixa de texto **Nome** ou aceite o padrão.  
  
4.  (Opcional) Na caixa de texto **Dica de Ferramenta** , digite o texto que você deseja que apareça quando o usuário passar o mouse sobre a imagem no relatório renderizado.  
  
5.  Em **Selecione a origem da imagem**, selecione **Inserida**.  
  
6.  Clique no botão **Importar** ao lado da caixa de texto **Usar esta imagem**  
  
7.  Em **Arquivos do tipo**, selecione o tipo de arquivo de imagem, navegue até o arquivo e clique em **Abrir**.  
  
8.  Na caixa de diálogo **Propriedades da Imagem** , clique em **OK**.  
  
     A imagem é exibida na caixa que você desenhou na superfície de design, e o arquivo é exibido sob a pasta Imagens no painel de dados do relatório.  
  
    > [!NOTE]  
    >  O tipo MIME (por exemplo, bmp) será extraído automaticamente quando a imagem for importada. Para alterar o tipo MIME, consulte o procedimento a seguir.  
  
### <a name="optional-to-change-the-mime-type-of-an-imported-image"></a>(Opcional) Para alterar o tipo MIME de uma imagem importada  
  
1.  Abra o relatório no modo Design.  
  
2.  Selecione a imagem na superfície de design. O painel **Propriedades** exibe as propriedades da imagem.  
  
    > [!NOTE]  
    >  Se o painel Propriedades não estiver visível, na guia **Exibir** , clique em **Propriedades**.  
  
3.  Clique na caixa de texto próxima à propriedade **MIMEType** e selecione um novo tipo MIME na lista suspensa.  
  
## <a name="see-also"></a>Consulte também  
 [Imagens &#40;Construtor de Relatórios e SSRS&#41;](images-report-builder-and-ssrs.md)   
 [Adicionar uma imagem vinculada a dados &#40;Construtor de Relatórios e SSRS&#41;](add-a-data-bound-image-report-builder-and-ssrs.md)   
 [Caixa de diálogo Propriedades da Imagem, Geral &#40;Construtor de Relatórios e SSRS&#41;](../image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  

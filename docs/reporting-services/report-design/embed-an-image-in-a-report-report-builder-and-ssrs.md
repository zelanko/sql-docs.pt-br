---
title: "Inserir uma imagem em um relat&#243;rio (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rtp.rptdesigner.embeddedimages.f1"
  - "10060"
ms.assetid: aed77345-5eeb-41f0-96c9-db6b4a11ec6f
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Inserir uma imagem em um relat&#243;rio (Construtor de Relat&#243;rios e SSRS)
  Um relatório pode conter uma imagem inserida. Inserir uma imagem garante que ela estará sempre disponível para um relatório, mas também afeta o tamanho da definição de relatório, o arquivo que define o relatório. As imagens inseridas em um relatório estão listadas no painel de dados do relatório.  
  
 Talvez você queira inserir uma imagem na definição de relatório antes de adicionar a imagem à superfície de design. Para obter mais informações, consulte [Adicionar uma imagem de tela de fundo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-background-image-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### Para inserir uma imagem em um relatório  
  
1.  No modo design de relatório, na guia **Inserir** , clique em **Imagem**.  
  
2.  Na superfície de design, clique e arraste uma caixa até o tamanho desejado da imagem.  
  
3.  Na página **Geral** da caixa de diálogo **Propriedades da Imagem** , digite um nome na caixa de texto **Nome** ou aceite o padrão.  
  
4.  (Opcional) Na caixa de texto **Dica de Ferramenta**, digite o texto que você deseja que apareça quando o usuário passar o mouse sobre a imagem no relatório renderizado.  
  
5.  Em **Selecione a origem da imagem**, selecione **Inserida**.  
  
6.  Clique no botão **Importar** ao lado da caixa de texto **Usar esta imagem**  
  
7.  Em **Arquivos do tipo**, selecione o tipo de arquivo de imagem, navegue até o arquivo e clique em **Abrir**.  
  
8.  Na caixa de diálogo **Propriedades da Imagem** , clique em **OK**.  
  
     A imagem é exibida na caixa que você desenhou na superfície de design, e o arquivo é exibido sob a pasta Imagens no painel de dados do relatório.  
  
    > [!NOTE]  
    >  O tipo MIME (por exemplo, bmp) será extraído automaticamente quando a imagem for importada. Para alterar o tipo MIME, consulte o procedimento a seguir.  
  
### (Opcional) Para alterar o tipo MIME de uma imagem importada  
  
1.  Abra o relatório no modo Design.  
  
2.  Selecione a imagem na superfície de design. O painel **Propriedades** exibe as propriedades da imagem.  
  
    > [!NOTE]  
    >  Se o painel Propriedades não estiver visível, na guia **Exibir**, clique em **Propriedades**.  
  
3.  Clique na caixa de texto próxima à propriedade **MIMEType** e selecione um novo tipo MIME na lista suspensa.  
  
## Consulte também  
 [Imagens &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)   
 [Adicionar uma imagem vinculada a dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-data-bound-image-report-builder-and-ssrs.md)   
 [Caixa de diálogo Propriedades da Imagem, Geral &#40;Construtor de Relatórios e SSRS&#41;](../Topic/Image%20Properties%20Dialog%20Box,%20General%20\(Report%20Builder%20and%20SSRS\).md)  
  
  
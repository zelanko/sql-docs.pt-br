---
title: "Adicionar uma imagem externa (construtor de relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 81fd4a1f-79a9-4967-86d6-6229413c0995
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 291a906484a6f7d812d091252802b706d207a69e
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="add-an-external-image-report-builder-and-ssrs"></a>Adicionar uma imagem externa (Construtor de Relatórios e SSRS)
  Imagens externas podem estar em um servidor de relatório em modo nativo ou em modo Integrado do SharePoint, ou em qualquer outro site. Quando você incluir imagens externas em seu relatório, verifique se a imagem existe e se o leitor do relatório tem permissões para acessar a imagem. Para obter mais informações, consulte [Imagens &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-an-external-image"></a>Para adicionar uma imagem externa  
  
1.  No modo design de relatório, na guia **Inserir** , clique em **Imagem**.  
  
2.  Na superfície de design, clique e arraste uma caixa até o tamanho desejado da imagem.  
  
3.  Na guia **Geral** da caixa de diálogo **Propriedades da Imagem** , digite um nome na caixa de texto **Nome** ou aceite o padrão.  
  
4.  (Opcional) Na caixa de texto **Dica de Ferramenta** , digite o texto a ser exibido quando o usuário passar o mouse sobre a imagem em um relatório renderizado para HTML.  
  
5.  Em **Selecione a origem da imagem**, selecione **Externa**.  
  
     Para uma imagem que está em um servidor de relatório no modo nativo, digite um caminho relativo até a imagem na caixa **Usar esta imagem**; por exemplo, /images/image1.jpg.  
  
     Para uma imagem em um servidor de relatório no modo integrado do SharePoint, ou qualquer outro site, digite uma URL completa para a imagem de **usar essa imagem** caixa — por exemplo, http://\<SharePointservername > /\<site > / Documents/images/Image1.jpg.  
  
     Para obter mais informações, consulte [Especificando caminhos para itens externos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
6.  (Opcional) Clique em **Tamanho**, **Visibilidade**, **Ação** ou **Borda** para definir as propriedades adicionais do item de relatório da imagem.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Inserir uma imagem em um relatório &#40;Construtor de relatórios e SSR&#41;](../../reporting-services/report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [Adicionar uma imagem de tela de fundo &#40;Construtor de relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-background-image-report-builder-and-ssrs.md)   
 [Caixa de diálogo de propriedades de imagem, geral &#40;Construtor de relatórios e SSRS&#41;](http://msdn.microsoft.com/library/c2218b93-f7fe-46ef-995f-d7dadf9752ec)  
  
  

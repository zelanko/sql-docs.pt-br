---
title: Adicionar uma imagem externa (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 81fd4a1f-79a9-4967-86d6-6229413c0995
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: bbe37d01a3e503d5ffb9aa9dc326d19bb9360d63
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52506932"
---
# <a name="add-an-external-image-report-builder-and-ssrs"></a>Adicionar uma imagem externa (Construtor de Relatórios e SSRS)
  Imagens externas podem estar em um servidor de relatório em modo nativo ou em modo Integrado do SharePoint, ou em qualquer outro site. Quando você incluir imagens externas em seu relatório, verifique se a imagem existe e se o leitor do relatório tem permissões para acessar a imagem. Para obter mais informações, consulte [Imagens &#40;Construtor de Relatórios e SSRS&#41;](images-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-an-external-image"></a>Para adicionar uma imagem externa  
  
1.  No modo design de relatório, na guia **Inserir** , clique em **Imagem**.  
  
2.  Na superfície de design, clique e arraste uma caixa até o tamanho desejado da imagem.  
  
3.  Na guia **Geral** da caixa de diálogo **Propriedades da Imagem** , digite um nome na caixa de texto **Nome** ou aceite o padrão.  
  
4.  (Opcional) Na caixa de texto **Dica de Ferramenta** , digite o texto a ser exibido quando o usuário passar o mouse sobre a imagem em um relatório renderizado para HTML.  
  
5.  Em **Selecione a origem da imagem**, selecione **Externa**.  
  
     Para uma imagem que está em um servidor de relatório no modo nativo, digite um caminho relativo até a imagem na caixa **Usar esta imagem**, por exemplo, ../images/image1.jpg.  
  
     Para uma imagem em um servidor de relatório no modo integrado do SharePoint, ou qualquer outro site, digite uma URL completa para a imagem na **usar esta imagem** caixa-por exemplo, http://\<SharePointservername > /\<site > / Documents/images/Image1.jpg.  
  
     Para obter mais informações, consulte [Especificando caminhos para itens externos &#40;Construtor de Relatórios e SSRS&#41;](specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
6.  (Opcional) Clique em **Tamanho**, **Visibilidade**, **Ação**ou **Borda** para definir as propriedades adicionais do item de relatório da imagem.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Inserir uma imagem em um relatório &#40;Construtor de Relatórios e SSRS&#41;](embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [Adicionar uma imagem de tela de fundo &#40;Construtor de Relatórios e SSRS&#41;](add-a-background-image-report-builder-and-ssrs.md)   
 [Caixa de diálogo Propriedades da Imagem, Geral &#40;Construtor de Relatórios e SSRS&#41;](../image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  

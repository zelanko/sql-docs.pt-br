---
title: Exportar um relatório como outro tipo de arquivo (construtor de relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: b577568b-ecbd-44c3-be88-31dab6fc38a2
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: e1f048a91f8e20255050772f1503e6dfa387954b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56017347"
---
# <a name="export-a-report-as-another-file-type-report-builder-and-ssrs"></a>Exportar um relatório como outro tipo de arquivo (Construtor de Relatórios e SSRS)
  Você pode renderizar um relatório para outro formato de arquivo, como CSV, Imagem, PDF, [!INCLUDE[ofprword](../includes/ofprword-md.md)]ou [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)], enquanto visualiza seu relatório no Construtor de Relatórios ou no Designer de Relatórios, ou pode renderizar o relatório enquanto visualiza-o no servidor de relatórios. A renderização do relatório em um formato específico será útil se você desejar salvá-lo imediatamente como outro tipo de arquivo, sem publicar o relatório no servidor de relatório, ou se quiser ver como o design do relatórios será exibido quando ele for entregue aos leitores de relatórios em um formato específico. A renderização do relatório no servidor de relatórios é útil quando você configura assinaturas ou fornece seus relatórios por email, ou quando deseja salvar um relatório disponível no servidor de relatórios. Para obter mais informações, consulte [Assinaturas e entrega &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-export-a-report-as-another-file-type-in-report-builder"></a>Para exportar um relatório como outro tipo de arquivo no Construtor de Relatórios  
  
1.  Visualize o relatório.  
  
2.  Na faixa de opções, clique em **Exportar**.  
  
3.  Selecione o formato que você deseja usar.  
  
     A caixa de diálogo **Salvar como** é aberta. Por padrão, o nome do arquivo é o mesmo do relatório que você exportou. Opcionalmente, você pode alterar o nome do arquivo.  
  
4.  Navegue até o local em que o relatório exportado foi salvo e abra-o.  
  
> [!NOTE]  
>  Se o programa não puder abrir o relatório no formato escolhido porque você não tem um programa associado a esse tipo de arquivo, será solicitado que você salve o relatório exportado ou localize um programa online para abri-lo.  
  
### <a name="to-export-a-report-as-another-file-type-in-report-manager"></a>Para exportar um relatório como outro tipo de arquivo no Gerenciador de Relatórios  
  
1.  No Gerenciador de Relatórios, na página **inicial** , navegue até o relatório que deseja exportar.  
  
2.  Clique no relatório.  
  
     O relatório é gerado.  
  
3.  Na barra de ferramentas do Report Viewer, clique na seta suspensa **Selecionar um formato** .  
  
4.  Selecione o formato que você deseja usar.  
  
5.  Clique em **Exportar**.  
  
     Uma mensagem é exibida perguntando se deseja abrir ou salvar o arquivo.  
  
6.  Para exibir o relatório no formato de exportação selecionado, clique em **Abrir**.  
  
     \- ou –  
  
     Para salvar imediatamente o relatório no formato de exportação selecionado, clique em **Salvar**.  
  
     Usando o aplicativo associado ao formato escolhido, o relatório é exibido ou salvo. Se você clicar em **Salvar**, você será solicitado a indicar um local no qual seja possível salvar o relatório.  
  
     **Observação** Se o programa não puder abrir o relatório no formato escolhido porque você não tem um programa associado a esse tipo de arquivo, você será solicitado a salvar o relatório exportado ou a localizar um programa online para abri-lo.  
  
### <a name="to-export-a-report-as-another-file-type-in-a-sharepoint-library"></a>Para exportar um relatório como outro tipo de arquivo em uma biblioteca do SharePoint  
  
1.  Visualize o relatório.  
  
2.  Na barra de ferramentas, clique em **Ações**, aponte para **Exportar**e selecione o formato desejado.  
  
     A caixa de diálogo **Download de Arquivo** é aberta.  
  
3.  Para exibir o relatório no formato de exportação selecionado, clique em **Abrir**.  
  
     \- ou –  
  
     Para salvar imediatamente o relatório no formato de exportação selecionado, clique em **Salvar**.  
  
     Usando o aplicativo associado ao formato escolhido, o relatório é exibido ou salvo. Se você clicar em **Salvar**, você será solicitado a indicar um local no qual seja possível salvar o relatório.  
  
     Outra opção é alterar o nome do arquivo do relatório exportado.  
  
     **Observação** Se o programa não puder abrir o relatório no formato escolhido porque você não tem um programa associado a esse tipo de arquivo, você será solicitado a salvar o relatório exportado ou a localizar um programa online para abri-lo.  
  
## <a name="see-also"></a>Consulte também  
 [Exportando relatórios &#40;relatórios e SSRS&#41;](report-builder/export-reports-report-builder-and-ssrs.md)   
 [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Funcionalidade interativa para extensões de renderização de relatório diferentes &#40;relatórios e SSRS&#41;](report-builder/interactive-functionality-different-report-rendering-extensions.md)  
  
  

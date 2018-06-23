---
title: Imprimir relatórios de outros aplicativos (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a5560581-fd57-4a45-b7ea-43b21a8a7419
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: cc94d80dd6ba01575ac60319d8a453afb97d6b06
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121439"
---
# <a name="print-reports-from-other-applications-report-builder-and-ssrs"></a>Imprimir relatórios de outros aplicativos (Construtor de Relatórios e SSRS)
  O Construtor de Relatórios apresenta uma opção de exportação que permite exibir facilmente um relatório em outros aplicativos. O `Export` comando está disponível na barra de ferramentas relatório que aparece na parte superior de um relatório quando você abri-lo em um navegador ou aplicativo baseado na Web. Exportar um relatório o exibe em um aplicativo diferente (por exemplo, exportar um relatório para o Excel o abre no [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)]). Para fins de impressão, a exportação de um relatório só é recomendada caso o aplicativo tenha recursos de impressão específicos que você queira usar.  
  
 Para exportar um relatório para outro aplicativo, esse outro aplicativo deve estar instalado. Por exemplo, você deve ter o Adobe Acrobat Reader instalado no computador para que possa exportar para o formato PDF (Acrobat). Caso opte por exportar um relatório para o formato TIFF, o servidor de relatório o coloca em um aplicativo de exibição associado ao tipo de arquivo TIFF. Embora o aplicativo usado dependa da versão do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, essa ferramenta normalmente é o Visualizador de Imagens e Fax do Windows. A resolução padrão corresponde a uma resolução de tela de 96 DPI (pontos por polegada). É possível aumentar a resolução do Visualizador de Imagens e Fax do Windows para 300 ou 600 DPI de acordo com as capacidades da impressora. Para obter mais informações sobre como ajustar a resolução, consulte a documentação de produto do Windows.  
  
 Caso você escolha um arquivo da Web (também conhecido como MHTML), o relatório é exportado para o navegador padrão. Imprimir usando o navegador pode resultar na adição das informações de caminho do relatório à parte inferior de todas as páginas. Na maioria dos casos, você pode definir as opções do navegador para omitir as informações de caminho em uma página impressa. Para obter mais informações, consulte a documentação de produto do navegador que você está usando.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Imprimir um relatório &#40;Construtor de Relatórios e SSRS&#41;](print-a-report-report-builder-and-ssrs.md)   
 [Imprimir relatórios em um navegador com o controle de impressão &#40;Construtor de Relatórios e SSRS&#41;](print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs.md)   
 [Exportando relatórios &#40;SSRS e construtor de relatórios&#41;](export-reports-report-builder-and-ssrs.md)   
 [Exportar um relatório como outro tipo de arquivo &#40;Construtor de Relatórios e SSRS&#41;](../export-a-report-as-another-file-type-report-builder-and-ssrs.md)   
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
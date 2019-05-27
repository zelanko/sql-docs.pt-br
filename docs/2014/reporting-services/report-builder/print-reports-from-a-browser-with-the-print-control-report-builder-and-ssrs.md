---
title: Imprimir relatórios em um navegador com o controle de impressão (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 10054250-d915-4bcb-8a1d-26837db4e932
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d80d59759befa0a6d7b601509a99c7cc6e22fbf0
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66107762"
---
# <a name="print-reports-from-a-browser-with-the-print-control-report-builder-and-ssrs"></a>Imprimir relatórios em um navegador com o controle de impressão (Construtor de Relatórios e SSRS)
  Embora um navegador seja o aplicativo cliente mais usado para exibir um relatório, a funcionalidade de impressão do navegador não é ideal para imprimir relatórios. A funcionalidade de impressão de um navegador foi projetada para imprimir páginas da Web. Normalmente, as páginas impressas em um navegador incluem todos os elementos visuais presentes em uma página da Web, além das informações de cabeçalho e rodapé que identificam a página ou o site. Imprimir em um navegador imprime o conteúdo da janela atual. Em um relatório com várias páginas, o navegador normalmente imprime a primeira ou menos caso a página do relatório exceda as dimensões de uma página impressa.  
  
 Para melhorar a qualidade de impressão dos relatórios exibidos em um navegador e imprimir várias páginas, é possível usar a funcionalidade de impressão de cliente fornecida no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. A impressão do lado do cliente fornece uma caixa de diálogo **Imprimir** padrão, que pode ser usada para selecionar uma impressora, especificar páginas e margens e visualizar o relatório antes da impressão. Ela destina-se a ser usada no lugar do comando **Imprimir** no menu **Arquivo** de um navegador. Quando você usa a impressão de cliente, o relatório é impresso como foi criado, sem os elementos adicionais exibidos em impressões de páginas da Web.  
  
 Para usar a impressão do lado do cliente, você precisa instalar um controle ActiveX do [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obter mais informações, consulte [Habilitar e desabilitar a impressão do lado do cliente para Reporting Services](../report-server/enable-and-disable-client-side-printing-for-reporting-services.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="print-options"></a>Opções de impressão  
 Para configurar as propriedades de impressão do relatório, na caixa de diálogo **Imprimir** , clique no botão **Propriedades** . O**tamanho do papel** é determinado pela altura e pela largura padrão do tamanho da página do relatório, conforme estabelecido na definição do relatório. Os valores disponíveis dependem do tipo de impressora e de seus recursos. Largura e altura usam valores padrão, conforme a determinação dos drivers de impressão configurados no computador. Alterar esses valores faz com que o relatório seja impresso usando as novas dimensões. A largura e a altura da página são determinadas pela **Orientação**, que é definida como **Retrato** ou **Paisagem**. A orientação padrão exibida depende da largura e da altura da página do relatório.  
  
> [!NOTE]  
>  A caixa de diálogo **Imprimir** e as configurações de impressora padrão para largura, altura e orientação de página são determinadas pela definição do relatório.  
  
### <a name="print-preview"></a>Visualizar Impressão  
 Para visualizar um relatório, na caixa de diálogo **Imprimir** , clique no botão **Visualizar** . Clicar na visualização abre a primeira página do relatório em uma janela de visualização separada. Páginas adicionais ficam disponíveis quando o relatório é processado no servidor de relatórios. Um relatório visualizado é processado em formato EMF. É possível navegar até a página anterior ou a próxima chegando até a última, e o botão **Avançar** é desabilitado.  
  
### <a name="adjusting-print-margins"></a>Ajustando margens de impressão  
 É possível modificar as margens de impressão no relatório EMF processado antes de imprimi-lo. Para isso, na caixa de diálogo **Imprimir** , clique no botão **Visualizar** . Na parte superior da página de visualização, clique no botão **Margens** . A caixa de diálogo Margens é exibida. Configure as margens superior, inferior, direita e esquerda conforme desejado. [!INCLUDE[clickOK](../../includes/clickok-md.md)] A caixa de diálogo é fechada, e as configurações são armazenadas para a renderização da visualização e da impressão.  
  
## <a name="see-also"></a>Consulte também  
 [Imprimir relatórios &#40;Construtor de Relatórios e SSRS&#41;](print-reports-report-builder-and-ssrs.md)   
 [Imprimir um relatório &#40;Construtor de Relatórios e SSRS&#41;](print-a-report-report-builder-and-ssrs.md)  
  
  

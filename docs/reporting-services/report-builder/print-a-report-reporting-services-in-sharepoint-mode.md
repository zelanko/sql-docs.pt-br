---
title: Imprimir um relatório (Reporting Services no modo do SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-builder
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- printing reports, SharePoint Web application
- printing reports
ms.assetid: 026784f7-8cb4-4351-93ee-230b2ab0f8f5
caps.latest.revision: 11
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 07e50f3dcc37738206fe396b8a68105fd4ac1c87
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33020023"
---
# <a name="print-a-report-reporting-services-in-sharepoint-mode"></a>Imprimir um relatório (Reporting Services no modo do SharePoint)
  Para um servidor de relatório que é executado no modo do SharePoint, há três maneiras de imprimir um relatório em um aplicativo Web do SharePoint:  
  
-   **Em um site do SharePoint,** escolha **Imprimir** no menu **Ações** que é exibido na barra de ferramentas do relatório quando você abre o relatório. Isso oferece a funcionalidade de impressão do Reporting Services, que inclui uma caixa de diálogo padrão para **Imprimir** usada para selecionar uma impressora, especificar páginas e margens e visualizar o relatório. Esse recurso de impressão destina-se a ser usado no lugar do comando Imprimir do menu Arquivo de um navegador. Quando você imprime relatórios dessa maneira, eles são impressos como foram criados, sem os elementos adicionais que aparecem em impressões de páginas da Web.  
  
-   **Em um navegador** Os recursos de impressão de um navegador funcionam melhor com relatórios HTML que cabem em uma única página. Normalmente, as páginas impressas em um navegador incluem todos os elementos visuais presentes em uma página da Web, além das informações de cabeçalho e rodapé que identificam a página ou o site. Quando você imprime a partir de um navegador, somente o conteúdo da janela atual é impresso. Se o relatório for longo, o navegador imprime apenas uma parte do relatório (normalmente apenas a primeira página).  
  
-   **Em um aplicativo de destino** Você pode exportar um relatório para usar os recursos de impressão de um aplicativo de destino, como o Microsoft Office Excel ou Adobe Acrobat Reader. Alguns formatos de aplicativos, como TIFF ou PDF, são ideais para a impressão de relatórios de várias páginas. Quando você exporta um relatório para um aplicativo de desktop, pode usar quaisquer recursos de impressão especializados fornecidos pelo aplicativo. Para exportar um relatório, escolha **Exportar** no menu **Ações** exibido na barra de ferramentas do relatório quando ele é aberto.  
  
> [!NOTE]  
>  Para imprimir um relatório, você deve ter permissão para exibi-lo.  
  
 Para obter melhores resultados ao imprimir um relatório a partir de uma página da Web, use **Imprimir** no menu **Ações** . A ação **Imprimir** está associada a um controle de impressão do cliente que é baixado do servidor de relatório. O download ocorre uma vez, na primeira vez que você seleciona **Imprimir**.  
  
 Os autores de relatórios podem criar relatórios especialmente para saída de impressão ou para um formato de aplicativo específico. Em virtude da forma como a paginação é implementada para diferentes formatos de aplicativo, talvez você não consiga obter resultados de saída de impressão otimizados para todos os relatórios em todos os formatos de exportação. Em contraste com relatórios que são criados para saída de impressão, as páginas de relatório na tela são criadas para acomodar quantidades variáveis de dados. Por exemplo, os relatórios que incluem uma matriz podem fazer com que uma página cresça tanto horizontal quanto verticalmente, dependendo de como você expande as linhas e colunas. Ao imprimir um relatório de tamanho variável, um usuário que não expandir uma matriz obterá resultados de impressão diferentes do um usuário que a expandir. Para a maioria dos relatórios exportados, as impressões de relatório incluem tudo que é visível no relatório, conforme visualizado pelo usuário em um monitor de computador.  
  
### <a name="how-to-print-reports-from-the-actions-menu"></a>Como imprimir relatórios no menu Ações  
  
1.  Abra o relatório.  
  
2.  No menu **Ações** , clique em **Imprimir**. Se você não visualizar o menu **Ações** , isso significa que a barra de ferramentas do relatório está oculta e você não poderá usar os recursos que ela fornece. Se o menu **Ações** aparecer, mas sem **Imprimir** , isso significa que a funcionalidade de impressão foi desabilitada no servidor de relatório e você não pode usá-la.  
  
3.  Na caixa de diálogo **Imprimir** , selecione a impressora e as configurações que deseja usar e clique em **OK**.  
  
     Para modificar as configurações padrão, clique no botão **Propriedades** . O tamanho da página é determinado pela altura e pela largura padrão do tamanho da página do relatório, conforme estabelecido na definição de relatório. Os recursos da impressora sendo usada determina o quanto você pode alterar as dimensões de página.  
  
     Para exibir o relatório antes de imprimi-lo, clique no botão **Visualizar** . A primeira página do relatório é aberta em uma janela de visualização separada. Páginas adicionais ficam disponíveis quando o relatório é processado no servidor de relatórios. Um relatório visualizado é processado em formato EMF. É possível navegar até a página anterior ou a próxima chegando até a última, e o botão **Avançar** é desabilitado. Para modificar as margens de impressão na página de visualização, clique no botão **Margens** . A caixa de diálogo **Margens** será exibida. Configure as margens superior, inferior, direita e esquerda e clique em **OK**. A caixa de diálogo é fechada, e as configurações são armazenadas para a renderização da visualização e da impressão.  
  
## <a name="see-also"></a>Consulte Também  
 [Habilitar e desabilitar a impressão do lado do cliente para Reporting Services](../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)  
  
  

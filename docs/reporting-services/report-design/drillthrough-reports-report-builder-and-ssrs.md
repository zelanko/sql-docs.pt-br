---
title: Relatórios de detalhamento (Construtor de Relatórios) | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 938a6450-67c1-4eef-80b4-8fdaefeed584
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 117b3cb90970c03c836964d47d91c37f0e65a294
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "77080462"
---
# <a name="drillthrough-reports-report-builder-and-ssrs"></a>Relatórios detalhados (Construtor de Relatórios e SSRS)
  Um relatório detalhado é um relatório que pode ser aberto pelo usuário quando ele clicar em um link dentro de outro relatório. Os relatórios detalhados normalmente contêm detalhes sobre um item que está em um relatório de resumo original. Por exemplo, nesta ilustração, o relatório de resumo de vendas lista ordens e totais de vendas. Quando um usuário clica em um número de ordem na lista de resumo, outro relatório é aberto, exibindo os detalhes da ordem.  
  
 ![rs_DrillThru](../../reporting-services/report-design/media/rs-drillthru.gif "rs_DrillThru")  
  
 Os dados no relatório detalhado não serão recuperados até que o usuário clique no link no relatório principal que abre o relatório detalhado. Se for necessário recuperar os dados do relatórios principal e do relatório detalhado ao mesmo tempo, considere usar um sub-relatório. Para obter mais informações, consulte [Sub-relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  Ao trabalhar no Construtor de Relatórios, você deve estar conectado a um servidor de relatório para exibir o relatório detalhado que é aberto quando clica no link de detalhamento no relatório principal.  
  
 Para começar rapidamente nos relatórios detalhados, confira o [Tutorial: Criar relatórios principal e de detalhamento &#40;Construtor de Relatórios&#41;](../../reporting-services/tutorial-creating-drillthrough-and-main-reports-report-builder.md). 
   
## <a name="parameters-in-drillthrough-reports"></a>Parâmetros em relatórios detalhados  
 Geralmente, o relatório detalhado contém parâmetros que são passados para ele pelo relatório de resumo. No exemplo de relatório de resumo de vendas, o relatório inclui o campo [OrderNumber] na caixa de texto de uma célula da tabela. O relatório detalhado contém um parâmetro que usa o número do pedido como um valor. Ao definir o link do relatório detalhado na caixa de texto de [OrderNumber], defina também o parâmetro do relatório de destino como [OrderNumber]. Quando o usuário clica no número da ordem no relatório de resumo, o relatório de detalhes de destino é aberto e exibe as informações desse número de ordem. Para exibir instruções sobre como personalizar relatórios de detalhamento com base nos valores de parâmetro, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md) e [Função InScope &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-inscope-function.md).  
  
## <a name="designing-the-drillthrough-report"></a>Criando o relatório detalhado  
 Para criar um relatório detalhado, você deve criar o relatório detalhado antes de criar a ação de detalhamento no relatório principal.  
  
 Um relatório detalhado pode ser qualquer relatório. Normalmente, o relatório detalhado aceita um ou mais parâmetros para especificar os dados que serão mostrados com base no link disponível no relatório principal. Por exemplo, se o link do relatório principal for definido para uma ordem de venda, o número da ordem de venda será transmitido para o relatório detalhado.  
  
## <a name="creating-a-drillthrough-action-in-the-main-report"></a>Criando uma ação de detalhamento no relatório principal  
 Você pode adicionar links de detalhamento a caixas de texto (inclusive texto nas células de uma tabela ou matriz), imagens, gráficos, medidores e qualquer outro item de relatório que tenha uma página de propriedade de Ação. Para obter mais informações, consulte [Adicionar uma ação de detalhamento a um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md).  
  
 É possível criar a ação de detalhamento no relatório principal como uma ação de relatório ou de URL. Para uma ação de relatório, o relatório detalhado deve existir no mesmo servidor de relatório que o relatório principal. Para uma ação de URL, o relatório deve existir no local da URL totalmente qualificada. O modo como você especifica um relatório talvez seja diferente para um servidor de relatório ou um site do SharePoint integrado a um servidor de relatório. Se o servidor de relatório estiver configurado em modo integrado do SharePoint, somente as ações de URL serão suportadas.  
  
 Para obter mais informações, consulte [Adicionar uma ação de detalhamento a um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md) e [Especificando caminhos para itens externos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
## <a name="viewing-a-drillthrough-report"></a>Exibindo um relatório detalhado  
 Para exibir um relatório de resumo com links de detalhamento após sua publicação, é preciso verificar se os relatórios detalhados estão no mesmo servidor do relatório de resumo. Em todas as situações, o usuário deve ter permissões no relatório detalhado para exibi-lo.  
  
## <a name="see-also"></a>Consulte Também  
 [Detalhamento, busca detalhada, sub-relatórios e regiões de dados aninhadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)  
  
  

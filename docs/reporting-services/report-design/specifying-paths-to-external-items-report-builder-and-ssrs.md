---
title: Especificando caminhos para itens externos (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4fe513da-f3c5-479c-9fec-8662b91a0d6d
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e1389b60c7aac94cddea21765c41bb715063fc0c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33024643"
---
# <a name="specifying-paths-to-external-items-report-builder-and-ssrs"></a>Especificando caminhos para itens externos (Construtor de Relatórios e SSRS)
  Você especifica caminhos nas propriedades de item de relatório para referenciar itens, como relatórios detalhados, sub-relatórios e arquivos de imagem, que são externos ao arquivo de definição de relatório e armazenados em um servidor de relatório.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
> [!NOTE]  
>  No Construtor de Relatórios, os caminhos para itens devem especificar itens em um servidor de relatório. Não há suporte para caminhos para itens em um sistema de arquivos. Você somente poderá visualizar um relatório que usa esses itens se estiver conectado ao servidor de relatório em que os itens estão localizados.  
  
 Quando você especifica um caminho para um item externo em uma caixa de diálogo para ações, sub-relatórios ou imagens, pode navegar diretamente até o servidor de relatório e selecionar esse item. Navegar até o item e selecioná-lo diretamente é a maneira recomendada de especificar um relatório detalhado ou sub-relatório. Dessa forma, os nomes de parâmetro corretos estarão disponíveis em uma lista suspensa quando você especificar parâmetros de relatório ou sub-relatório. Ao alterar o caminho de um item para apontar para um item diferente, você deverá atualizar manualmente os nomes de parâmetro corretos e valores conforme necessário.  
  
 Em um servidor de relatório configurado no modo nativo, especifique um nome de relatório detalhado sem a extensão de arquivo .rdl.  
  
 Em um servidor de relatório configurado no modo integrado do SharePoint, você deve incluir a extensão de arquivo .rdl. O caminho pode ser um dos seguintes:  
  
-   **Um caminho relativo para o item do relatório principal.** Por exemplo, ../AllSubreports/Subreport1. Neste exemplo, o **..** indica a pasta acima da pasta em que o relatório principal está localizado.  
  
    > [!NOTE]  
    >  Caminhos relativos não são suportados quando o relatório é executado dentro de Construtor de Relatórios. Para exibir um relatório que use caminhos relativos a itens externos, salve o relatório no servidor de relatório e execute o relatório de lá  
  
-   **Um caminho completo para o item.**  
  
    -   **Em um servidor de relatório:** o caminho começa com **/**, a pasta Base. Por exemplo, ../Reports/AllSubreports/Subreport1.  
  
    -   **Em um site do SharePoint:** você deve especificar o nome do relatório em uma expressão, com a URL completa do item e a extensão de arquivo .rdl. Por exemplo, `="http://server/site/library/folder/Report1.rdl"`.  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar uma imagem externa &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-an-external-image-report-builder-and-ssrs.md)   
 [Adicionar um sub-relatório e parâmetros &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-subreport-and-parameters-report-builder-and-ssrs.md)   
 [Adicionar uma ação de detalhamento a um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-drillthrough-action-on-a-report-report-builder-and-ssrs.md)  
  
  

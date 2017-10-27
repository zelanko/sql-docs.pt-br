---
title: "Subrelatórios (construtor de relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ab5bea3a-109e-4c25-92d9-494df7c52dd8
caps.latest.revision: 10
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8deb7c183ab46007fb0d4c4aee17762676963c4d
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="subreports-report-builder-and-ssrs"></a>Sub-relatórios (Construtor de Relatórios e SSRS)
  Um sub-relatório é um item de relatório que exibe outro relatório dentro do principal corpo de conteúdo de um relatório. Conceitualmente, um sub-relatório em um relatório é semelhante a um quadro em uma página da Web. É usado para inserir um relatório dentro de um relatório. Qualquer relatório pode ser usado como um sub-relatório. O relatório exibido pelo sub-relatório é armazenado em um servidor de relatório, normalmente na mesma pasta do relatório pai. Você pode designar o relatório pai para transmitir parâmetros ao sub-relatório. Um sub-relatório pode ser repetido em regiões de dados, usando um parâmetro para filtrar dados em cada instância do sub-relatório.  
  
> [!NOTE]  
>  Se um sub-relatório for usado em uma região de dados tablix, ele e seus parâmetros serão processados para cada linha na região de dados. Se houver muitas linhas, avalie se um relatório detalhado é mais adequado.  
  
 ![rs_Subreport](../../reporting-services/report-design/media/rs-subreport.gif "rs_Subreport")  
  
 Nesta ilustração, as informações de contato exibidas no relatório de Ordem de Venda principal vêm de um sub-relatório Contatos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="comparing-subreports-and-nested-data-regions"></a>Comparando sub-relatórios e regiões de dados aninhados  
 Se você estiver pensando em usar os sub-relatórios para exibir grupos de dados separados, considere o uso de regiões de dados como tabelas, matrizes, listas e gráficos. Os relatórios com regiões de dados podem executar melhor apenas os relatórios que incluem sub-relatórios.  
  
 Use as regiões de dados para aninhar grupos de dados a partir da mesma fonte de dados dentro de uma região de dados simples. Use os sub-relatórios para aninhar os grupos de dados de diferentes fontes de dados dentro de uma região de dados simples, reutilizar um sub-relatório em vários relatórios pai ou exibir um relatório autônomo dentro de outro relatório. Por exemplo, você pode criar um "livro-síntese" posicionando vários sub-relatórios dentro de outro relatório.  
  
 As regiões de dados fornecem muito da funcionalidade e flexibilidade de sub-relatórios, mas com melhor desempenho. Como o servidor de relatório processa cada instância de um sub-relatório como um relatório separado, pode haver impacto no desempenho. Para obter mais informações, consulte [Regiões de dados aninhadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/nested-data-regions-report-builder-and-ssrs.md).  
  
## <a name="using-parameters-in-subreports"></a>Usando parâmetros em sub-relatórios  
 Para passar os parâmetros do relatório pai para o sub-relatório, defina um parâmetro de relatório no relatório que está sendo usado como o sub-relatório. Ao inserir o sub-relatório no relatório pai, você poderá selecionar o parâmetro de relatório e um valor que poderão ser passados do relatório pai para o parâmetro de relatório no sub-relatório.  
  
> [!NOTE]  
>  O parâmetro que você seleciona no sub-relatório é um parâmetro de relatório, não um parâmetro de consulta.  
  
 O sub-relatório pode ser colocado no corpo principal do relatório ou em uma região de dados. Se o sub-relatório for posicionado em uma região de dados, ele será repetido em cada instância do grupo ou da linha na região de dados. Para passar um valor a partir de um grupo ou uma linha para o sub-relatório, na propriedade de valor do sub-relatório, use uma expressão de campo para o campo que contém o valor que deseja passar para o parâmetro de sub-relatório.  
  
 Para obter mais informações sobre como trabalhar com sub-relatórios, consulte [Adicionar um sub-relatório e parâmetros &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-a-subreport-and-parameters-report-builder-and-ssrs.md).  
  
## <a name="specifying-subreport-names-and-locations"></a>Especificando nomes e locais de sub-relatório  
 É possível criar um relatório principal para especificar um sub-relatório em outra pasta no mesmo servidor de relatório.  
  
 A sintaxe a ser usada para especificar o sub-relatório dependerá do modo em que estará o servidor de relatório, ou seja, no modo nativo ou no modo integrado do SharePoint. Para obter mais informações, consulte [Especificando caminhos para itens externos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
 No Construtor de Relatórios, para visualizar um sub-relatório em um relatório principal, os dois relatórios devem estar localizados no mesmo servidor de relatório ou você deve especificar um caminho completo para o sub-relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Detalhamento, busca detalhada, sub-relatórios e regiões de dados aninhadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/drillthrough-drilldown-subreports-and-nested-data-regions.md)  
  
  


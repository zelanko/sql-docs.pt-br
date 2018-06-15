---
title: Conexão de modelo de relatório (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-data
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: da880fb8-13cc-4d5f-b992-91ed0ec3ca7d
caps.latest.revision: 11
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: ef0da61aaa868cafbb95b2db4618ce9e3a6763b3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33022963"
---
# <a name="report-model-connection-ssrs"></a>Conexão de modelo de relatório (SSRS)
  Para incluir dados de um modelo de relatório, é necessário ter um conjunto de dados baseado em um modelo de relatório como uma fonte de dados. Diferentemente de outras fontes de dados de relatório, não há nenhuma extensão de dados para um modelo de relatório. No Construtor de Relatórios, procure e selecione o modelo diretamente no servidor de relatório. Em Designer de Relatórios, você especifica a URL para o modelo de relatório.  
  
 Use as informações deste tópico para criar uma fonte de dados. Para obter instruções passo a passo, consulte [Adicionar e verificar uma conexão de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadeia de Conexão  
 Você não precisa de uma cadeia de conexão para usar um modelo de relatório como uma fonte de dados. Para conectar-se a um modelo de relatório, navegue até um servidor de relatório ou um site do SharePoint e selecione um modelo publicado. Em um site do SharePoint, a extensão do nome do arquivo de modelo de relatório é .smdl.  
  
 Para obter mais exemplos de cadeias de conexão, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34).  
  
  
##  <a name="Credentials"></a> Credenciais  
 As credenciais são necessárias para executar consultas, visualizar o relatório localmente e visualizá-lo no servidor de relatório.  
  
 Após a publicação do relatório, talvez seja necessário alterar as credenciais da fonte de dados para que, quando o relatório for executado no servidor de relatório, as permissões recuperadas sejam válidas.  
  
 Para obter mais informações, consulte [Especificar as credenciais no Construtor de Relatórios](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53).  
  
  
##  <a name="Query"></a> Consultas  
 Use o designer de consulta de modelo de relatório para especificar interativamente entidades, campos e um filtro para a consulta. As entidades e os campos do modelo se transformam na coleção de campos do conjunto de dados exibida no painel de dados do relatório.  
  
  
##  <a name="Parameters"></a> Parâmetros  
 Para adicionar um parâmetro de relatório, crie um filtro com uma solicitação no Designer de Consultas de Modelo de Relatório.  
  
 Os parâmetros de relatório são criados com valores de propriedade padrão que talvez precisem ser modificados. Por padrão, cada parâmetro de relatório é do tipo de dados **Texto**. Se os dados subjacentes forem de outro tipo de dados, será necessário alterar o tipo de dados de parâmetro.  
  
 Para obter mais informações, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
  
##  <a name="Remarks"></a> Comentários  
 Nem todos os modos de entrega de relatório são suportados por esse provedor de dados. Não há suporte para a entrega de relatórios através de assinaturas controladas por dados para essa extensão de processamento de dados. Para obter mais informações, consulte [Usar uma fonte de dados externa para obter dados de assinante &#40;Assinatura controlada por dados&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md).  
  
  
##  <a name="HowTo"></a> Tópicos de instruções  
 Esta seção contém instruções passo a passo para trabalhar com conexões de dados, fontes de dados e conjuntos de dados.  
  
 [Adicionar e verificar uma conexão de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Criar um conjunto de dados compartilhado ou um conjunto de dados inserido &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Adicionar um filtro a um conjunto de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> Seções relacionadas  
 Estas seções da documentação fornecem informações conceituais detalhadas sobre dados de relatório, bem como informações de procedimentos sobre como definir, personalizar e usar partes de um relatório relacionadas aos dados.  
  
 [Conjuntos de dados de relatório &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 Fornece uma visão geral de como acessar dados de seu relatório.  
  
 [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 Fornece informações sobre conexões de dados e fontes de dados.  
  
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Fornece informações sobre conjuntos de dados inseridos e compartilhados.  
  
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 Fornece informações sobre a coleção de campos de conjuntos de dados gerada pela consulta.  
  
 [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online](http://go.microsoft.com/fwlink/?linkid=121312) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Fornece informações detalhadas sobre suporte à plataforma e à versão para cada extensão de dados.  
  
  
## <a name="see-also"></a>Consulte Também  
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  

---
title: Tipo de conexão do Teradata (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: b02779c2-a6b9-453c-815f-adad53353952
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 236f883056ccfd7c66701f5126b313ccbe2361b9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48074556"
---
# <a name="teradata-connection-type-ssrs"></a>Tipo de conexão Teradata (SSRS)
  Para incluir dados de um banco de dados relacional Teradata no seu relatório, é necessário ter um conjunto de dados baseado na fonte de dados do relatório do tipo Teradata. Esse tipo de fonte de dados interna é baseado na extensão de processamento de dados do Provedor Gerenciados do .NET para Teradata.  
  
 Use as informações deste tópico para criar uma fonte de dados. Para obter instruções passo a passo, consulte [adicionar e verificar uma Conexão de dados ou uma fonte de dados &#40;construtor de relatórios e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadeia de Conexão  
 Contate o administrador do banco de dados para obter informações sobre a conexão e as credenciais que devem ser usadas para se conectar à fonte de dados. O exemplo de cadeia de conexão seguinte define um banco de dados Teradata no servidor especificado com um endereço IP:  
  
```  
data source=<IP Address>  
```  
  
 Para obter mais exemplos de cadeias de conexão, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
##  <a name="Credentials"></a> Credenciais  
 As credenciais são necessárias para executar consultas, visualizar o relatório localmente e visualizá-lo no servidor de relatório.  
  
 Após a publicação do relatório, talvez seja necessário alterar as credenciais da fonte de dados para que, quando o relatório for executado no servidor de relatório, as permissões recuperadas sejam válidas.  
  
 Para obter mais informações, consulte [conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) ou [especificar as credenciais no construtor de relatórios](../specify-credentials-in-report-builder.md).  
  
 ![Ícone de seta usado com o link Voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
##  <a name="Remarks"></a> Comentários  
 Para que você possa se conectar a uma fonte de dados Teradata, o administrador do sistema deve ter instalado a versão do Provedor de Dados .NET para Teradata que dá suporte à recuperação de dados do banco de dados Teradata. O provedor de dados deve ser instalado no mesmo computador que o Construtor de Relatórios e também no servidor de relatório.  
  
 Nem todos os modos de entrega de relatório são suportados por esse provedor de dados. Não há suporte para a entrega de relatórios através de assinaturas controladas por dados para essa extensão de processamento de dados. Para obter mais informações, consulte [Usar uma fonte de dados externa para obter dados de assinante &#40;Assinatura controlada por dados&#41;](../subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md) na documentação do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] nos [Manuais Online](http://go.microsoft.com/fwlink/?linkid=121312) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 ![Ícone de seta usado com o link Voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
##  <a name="Models"></a> Modelos de relatório  
 Para criar um conjunto de dados de um modelo de relatório baseado em uma fonte de dados Teradata, o modelo deve ser criado em Designer Modelo em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] e deve ser publicado em um servidor de relatório.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
##  <a name="Related"></a> Seções relacionadas  
 Estas seções da documentação fornecem informações conceituais detalhadas sobre dados de relatório, bem como informações de procedimentos sobre como definir, personalizar e usar partes de um relatório relacionadas aos dados.  
  
 [Adicionar dados a um relatório &#40;relatórios e SSRS&#41;](report-datasets-ssrs.md)  
 Fornece uma visão geral de como acessar dados de seu relatório.  
  
 [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 Fornece informações sobre conexões de dados e fontes de dados.  
  
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Fornece informações sobre conjuntos de dados inseridos e compartilhados.  
  
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 Fornece informações sobre a coleção de campos gerada pela consulta do conjunto de dados.  
  
 [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) na documentação do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] nos [Manuais Online](http://go.microsoft.com/fwlink/?linkid=121312) do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
 Fornece informações detalhadas sobre suporte à plataforma e à versão para cada extensão de dados.  
  
 [Usando o SQL Server 2008 Reporting Services com o Provedor de Dados do .NET Framework para Teradata](http://go.microsoft.com/fwlink/?LinkID=130848)  
 Fornece informações detalhadas sobre como trabalhar com esta extensão de dados.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início")[Voltar ao início](#BackToTop)  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  

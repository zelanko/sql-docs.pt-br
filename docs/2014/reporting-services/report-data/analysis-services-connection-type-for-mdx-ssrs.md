---
title: Tipo de conexão do Analysis Services para MDX (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: bd2e7148-3124-4e07-9734-22333127c3be
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dbd62eff94b1a885198c62a9a36cb8eef7ba57c7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68892121"
---
# <a name="analysis-services-connection-type-for-mdx-ssrs"></a>Tipo de conexão Analysis Services para MDX (SSRS)
  Para incluir dados de um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cubo em seu relatório, você deve ter um conjunto de dados com base em uma fonte de dado de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]relatório do tipo. Esse tipo de fonte de dados interna é baseado na extensão de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Você pode recuperar metadados sobre dimensões, hierarquias, níveis, KPIs (indicadores chave de desempenho), medidas e atributos de um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cubo para uso como dados de relatório.  
  
 Essa extensão de processamento de dados dá suporte a parâmetros de vários valores, a agregações de servidor e a credenciais gerenciadas separadamente da cadeia de conexão.  
  
 Use as informações deste tópico para criar uma fonte de dados. Para obter instruções detalhadas, consulte [Adicionar e verificar uma &#40;de conexão de dados ou fonte de dados Construtor de relatórios e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a>Cadeia de conexão  
 Ao se conectar a um cubo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , você está se conectando ao objeto de banco de dados em uma instância do Analysis Services em um servidor. O banco de dados pode ter vários cubos. Especifique o cubo no designer de consulta ao criar a consulta. O exemplo a seguir mostra uma cadeia de conexão:  
  
```  
data source=<server name>;initial catalog=<database name>  
```  
  
 Para obter mais exemplos de cadeias de conexão, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
  
  
##  <a name="Credentials"></a>Fornecidas  
 As credenciais são necessárias para executar consultas, visualizar o relatório localmente e visualizá-lo no servidor de relatório.  
  
 Após a publicação do relatório, talvez seja necessário alterar as credenciais da fonte de dados para que, quando o relatório for executado no servidor de relatório, as permissões recuperadas sejam válidas.  
  
 Em um cliente de criação de relatório, as seguintes opções estão disponíveis para especificar credenciais:  
  
-   Usuário atual do Windows (também conhecido como segurança integrada).  
  
-   Usar um nome de usuário e senha armazenados.  
  
-   Solicitar credenciais ao usuário. Esta opção somente dá suporte à segurança integrada do Windows.  
  
-   Nenhuma credencial é necessária. Para usar essa opção, você deve ter a conta de execução autônoma configurada no servidor de relatório. Para obter mais informações, consulte [Configurar a conta de execução autônoma &#40;Gerenciador de Configurações do SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) na [documentação do Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) em msdn.microsoft.com.  
  
 Para obter mais informações, consulte [conexões de dados, fontes de dados e cadeias de conexão em Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) ou [especificar credenciais no construtor de relatórios](../specify-credentials-in-report-builder.md).  
  
  
  
##  <a name="Query"></a>Procura  
 Depois de se conectar a uma fonte de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , você pode criar um conjunto de dados e definir uma consulta MDX que especifique quais dados devem ser recuperados do cubo. Use o designer de consulta gráfica MDX procurando e selecionando a partir das estruturas de dados subjacentes na fonte de dados.  
  
 Você pode especificar uma consulta das seguintes formas:  
  
-   Crie uma consulta interativamente. O Designer de Consulta MDX do Analysis Services oferece suporte aos seguintes modos de exibição:  
  
    -   **Modo Design** Arraste dimensões, membros, propriedades do membro, medidas e KPIs do navegador de metadados para o painel de **dados** para criar uma consulta MDX. Arraste os membros calculados do painel CalculatedMembers até o painel Dados para definir campos adicionais para o conjunto de dados.  
  
    -   **Visualização da consulta** Arraste dimensões, membros, propriedades do membro, medidas e KPIs do navegador de metadados para o painel de consulta para criar uma consulta MDX. Você pode editar o texto MDX diretamente no painel Consulta. Arraste os membros calculados do painel CalculatedMembers até o painel Consulta para definir campos adicionais para o conjunto de dados.  
  
     Para obter mais informações, consulte [Interface do usuário do Designer de Consultas MDX do Analysis Services &#40;Construtor de Relatórios&#41;](../analysis-services-mdx-query-designer-user-interface-report-builder.md).  
  
-   Importe uma consulta MDX existente de um relatório. Use o botão de consulta **Importar** para procurar um arquivo .rdl e importar uma consulta. Você pode importar uma consulta de um relatório que contém um conjunto de dados inserido baseado em uma fonte de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Não há suporte para a importação de uma consulta MDX diretamente a partir de um arquivo .mdx.  
  
 No momento do design, execute a consulta para exibir um conjunto de resultados. Os resultados da consulta são automaticamente recuperados como um conjunto de linhas bidimensional. As colunas no conjunto de resultados para uma consulta populam a coleção de campos para um conjunto de dados. Depois que você criar uma consulta, visualize a coleta de campos do conjunto de dados gerada a partir dos metadados no painel de dados do relatório. Quando o relatório é executado, os dados reais são retornados da fonte de dados externa.  
  
 A extensão de processamento de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dá suporte às propriedades estendidas de campo do conjunto de dados. Estes são valores que estão disponíveis a partir da fonte de dados externa, mas que não são exibidos no painel de dados do relatório. Você pode usar as propriedades de campo ampliadas suportadas pela extensão de processamento de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em seu relatório por meio da coleção de `Fields` interna. Para as propriedades com valores na fonte de dados, você pode acessar os valores de propriedade predefinidos como `FormattedValue`, `Color` ou `UniqueName`. Para obter mais informações, consulte [Propriedades de campos estendidos para um banco de dados do Analysis Services &#40;SSRS&#41;](extended-field-properties-for-an-analysis-services-database-ssrs.md).  
  
  
  
##  <a name="Parameters"></a> Parâmetros  
 Para incluir parâmetros de consulta, crie um filtro na área de filtros no designer de consultas e marque o filtro como um parâmetro. Para cada filtro, um conjunto de dados é criado automaticamente para fornecer os valores disponíveis. Por padrão, esses conjuntos de dados não são exibidos no painel de dados do relatório. Para obter mais informações, consulte [Definir parâmetros no Designer de Consulta MDX para o Analysis Services &#40;Construtor de Relatórios e SSRS&#41;](define-parameters-in-the-mdx-query-designer-for-analysis-services.md) e [Mostrar conjuntos de dados ocultos para obter valores de parâmetro para dados multidimensionais &#40;Construtor de Relatórios e SSRS&#41;](show-hidden-datasets-for-parameter-values-multidimensional-data.md).  
  
 Por padrão, cada parâmetro de relatório tem o tipo de dados **Text**. Depois que os parâmetros de relatório forem criados, talvez seja necessário alterar os valores padrão. Para obter mais informações, consulte [parâmetros de relatório &#40;Construtor de relatórios e Report Designer&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
  
  
##  <a name="Remarks"></a> Comentários  
 A extensão de dados do Analysis Services é baseada no protocolo XMLA (XML for Analysis). Os conjuntos de resultados de cubos são recuperados por meio do protocolo XMLA como um conjunto de linhas plano. Não há suporte para hierarquias desbalanceadas. Para obter mais informações, consulte [Hierarquias desbalanceadas](https://docs.microsoft.com/analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies).  
  
 Você também pode recuperar os dados de um cubo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] do tipo de fonte de dados OLE DB. Para obter mais informações, consulte [Tipo de conexão OLE DB &#40;SSRS&#41;](ole-db-connection-type-ssrs.md).  
  
 Para obter mais informações sobre o suporte à versão, consulte [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) na documentação do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] no Manual Online[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [ do ](https://go.microsoft.com/fwlink/?linkid=121312).  
  
  
  
##  <a name="Related"></a>Seções relacionadas  
 Estas seções da documentação fornecem informações conceituais detalhadas sobre dados de relatório, bem como informações de procedimentos sobre como definir, personalizar e usar partes de um relatório relacionadas aos dados.  
  
 [Adicionar dados a um relatório &#40;Construtor de Relatórios e SSRS&#41;](report-datasets-ssrs.md)  
 Fornece uma visão geral de como acessar dados de seu relatório.  
  
 [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 Fornece informações sobre conexões de dados e fontes de dados.  
  
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Fornece informações sobre conjuntos de dados inseridos e compartilhados.  
  
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 Fornece informações sobre a coleção de campos de conjuntos de dados gerada pela consulta.  
  
 [Propriedades de campo estendidas para um banco de dados Analysis Services &#40;SSRS&#41;](extended-field-properties-for-an-analysis-services-database-ssrs.md)  
 Fornece informações sobre campos adicionais disponíveis por meio do provedor de dados XMLA.  
  
 [Fontes de dados com suporte pelo Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) na [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] documentação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do nos [manuais online](https://go.microsoft.com/fwlink/?linkid=121312)do.  
 Fornece informações detalhadas sobre suporte à plataforma e à versão para cada extensão de dados.  
  
  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  

---
title: Tipo de conexão do Hyperion Essbase (SSRS) | Microsoft Docs
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
ms.assetid: 108a00b6-799f-4066-b796-da59e95c09fd
caps.latest.revision: 10
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 4856d84a8ee9cc8917ca6791260ca13fa083320e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="hyperion-essbase-connection-type-ssrs"></a>Tipo de conexão Hyperion Essbase (SSRS)
  Para incluir dados de uma fonte de dados externa do [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] no relatório, você deve ter um conjunto de dados baseado em uma fonte de dados do relatório do tipo [!INCLUDE[extEssbase](../../includes/extessbase-md.md)]. Esse tipo de fonte de dados interna se baseia na extensão de dados do [!INCLUDE[extEssbase](../../includes/extessbase-md.md)], que permite recuperar dados multidimensionais de uma fonte de dados externa do [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] .  
  
 Use as informações deste tópico para criar uma fonte de dados. Para obter instruções passo a passo, consulte [Adicionar e verificar uma conexão de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadeia de Conexão  
 O exemplo de cadeia de conexão a seguir especifica uma fonte de dados do [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] em um servidor que usa porta 13080 e XML no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (XMLA) para Internet usando SOAP, conectando-se a um catálogo de exemplo:  
  
```  
Data Source=http://localhost:13080/aps/XMLA; Initial Catalog=Sample  
```  
  
 Para obter mais informações sobre exemplos de cadeias de conexão, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34).  
  
  
##  <a name="Credentials"></a> Credenciais  
 As credenciais são necessárias para executar consultas, visualizar o relatório localmente e visualizá-lo no servidor de relatório.  
  
 Após a publicação do relatório, talvez seja necessário alterar as credenciais da fonte de dados para que, quando o relatório for executado no servidor de relatório, as permissões recuperadas sejam válidas.  
  
 Para obter mais informações, consulte [Conexões de dados, fontes de dados e cadeias de conexão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) ou [Especificar as credenciais no Construtor de Relatórios](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53).  
  
  
##  <a name="Query"></a> Consultas  
 Você pode especificar uma consulta das seguintes formas:  
  
-   Crie uma consulta interativamente. Use o designer de consultas gráficas no modo de Design ou de Consulta para procurar os metadados na fonte de dados externa e gerar uma consulta em sintaxe de expressão MDX.  
  
    -   **Modo de exibição de Design** Arraste as dimensões, os membros, as propriedades de membros, as medidas e os KPIs do navegador de metadados para o painel **Dados** para criar uma consulta MDX. Arraste os membros calculados do painel CalculatedMembers até o painel Dados para definir campos adicionais para o conjunto de dados.  
  
    -   **Visualização da Consulta** Arraste as dimensões, os membros, as propriedades de membros, as medidas e os KPIs do navegador de metadados até o painel Consulta para criar uma consulta MDX. Você pode editar o texto MDX diretamente no painel Consulta. Arraste os membros calculados do painel CalculatedMembers até o painel Consulta para definir campos adicionais para o conjunto de dados.  
  
     Para obter mais informações, consulte [Interface do usuário do Designer de Consultas do Hyperion Essbase &#40;Construtor de Relatórios&#41;](http://msdn.microsoft.com/library/d89a6773-dbe5-48e5-bda9-db0e67100696).  
  
-   Importe uma consulta MDX existente de um relatório. Use o botão de consulta **Importar** para procurar um arquivo .rdl e importar uma consulta. Você pode importar uma consulta de um relatório que contém um conjunto de dados inserido baseado em uma fonte de dados do [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] . Não há suporte para a importação de uma consulta MDX diretamente a partir de um arquivo .mdx.  
  
 No momento do design, execute a consulta para exibir um conjunto de resultados. Depois que você criar uma consulta, visualize a coleta de campos do conjunto de dados gerada a partir dos metadados no painel de dados do relatório. Quando o relatório é executado, os dados reais são retornados da fonte de dados externa.  
  
 A extensão de processamento de dados do [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] dá suporte às propriedades estendidas de campo do conjunto de dados. Estes são valores que estão disponíveis a partir da fonte de dados externa, mas que não são exibidos no painel de dados do relatório. Para obter mais informações, consulte [Propriedades de campo estendidas](#Extended) , mais adiante neste tópico.  
  
  
##  <a name="Parameters"></a> Para incluir parâmetros de consulta, crie um filtro na área de filtros no designer de consultas e marque o filtro como um parâmetro. Para cada filtro, um conjunto de dados é criado automaticamente para fornecer os valores disponíveis. Por padrão, esses conjuntos de dados não são exibidos no painel de dados do relatório. Para obter mais informações, consulte [Mostrar conjuntos de dados ocultos para obter valores de parâmetros para dados multidimensionais &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/show-hidden-datasets-for-parameter-values-multidimensional-data.md).  
  
 Por padrão, cada parâmetro de relatório tem o tipo de dados **Text**. Depois que os parâmetros de relatório forem criados, talvez seja necessário alterar os valores padrão. Para obter mais informações, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
  
##  <a name="Extended"></a> Propriedades de campo estendidas  
 A extensão de processamento de dados do [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] oferece suporte às propriedades de campo estendidas. As propriedades de campo estendidas são propriedades adicionais a **Value** e **IsMissing** definidas para um campo de conjunto de dados pela extensão do processamento de dados. As propriedades estendidas incluem propriedades predefinidas e propriedades personalizadas. As propriedades predefinidas são propriedades comuns para várias fontes de dados. As propriedades personalizadas são exclusivas para cada fonte de dados.  
  
 As propriedades de campo estendidas não são exibidas no painel de dados do relatório como itens que você pode arrastar em seu layout de relatório. Em vez disso, você arrasta o campo pai da propriedade para o relatório e altera a propriedade padrão de **Value** para a propriedade que você quer usar.  
  
 O nome de uma propriedade de campo estendida aparece na Dica de Ferramenta quando você para o mouse sobre um campo no painel Metadados no designer de consulta. Para obter mais informações sobre o designer de consultas que você pode usar para explorar os dados subjacentes, consulte [Interface do usuário do Designer de Consultas do Hyperion Essbase](../../reporting-services/report-data/hyperion-essbase-query-designer-user-interface.md).  
  
> [!NOTE]  
>  Os valores para essas propriedades de campo estendidas passarão a existir somente se eles forem incluídos na expressão MDX e a fonte de dados fornecer esses valores quando você executar e recuperar os dados de seus conjuntos de dados. Você poderá consultar esses valores da propriedade **Field** por meio de qualquer expressão usando a sintaxe descrita na seção a seguir. Entretanto, como esses campos são específicos para esse provedor de dados e não faz parte da linguagem de definição de relatório, as alterações que forem feitas nesse valor não serão salvas com a definição de relatório.  
  
  
### <a name="predefined-field-properties"></a>Propriedades de campo predefinidas  
 Propriedades de campo predefinidas para as quais normalmente existe suporte de vários provedores de dados e que aparecem na consulta MDX subjacente a um conjunto de dados de relatório. Por exemplo, a propriedade de dimensão MDX MEMBER_UNIQUE_NAME é mapeada para a propriedade de campo predefinida do conjunto de dados de relatório **UniqueName**. Para incluir o valor de nome exclusivo em uma caixa de texto, use a expressão `=Fields!`*\<FieldName>*`.UniqueName`.  
  
 A tabela a seguir fornece uma lista das propriedades de campo predefinidas que você pode usar para a fonte de dados do [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] .  
  
|**Propriedade**|**Tipo**|**Descrição ou valor esperado**|  
|------------------|--------------|---------------------------------------|  
|**Value**|**Objeto**|Especifica o valor de dados do campo.<br /><br /> Em uma propriedade de dimensão, é mapeada para MEMBER_CAPTION. Em uma medida, é mapeada para um valor de dados.|  
|**IsMissing**|**Booliano**|Indica se o campo foi encontrado no conjunto de dados resultante.|  
|**FormattedValue**|**String**|Retorna um valor formatado para o número chave.<br /><br /> Mapeada a partir de FORMATTED_VALUE na expressão MDX.|  
|**BackgroundColor**|**String**|Retorna a cor do segundo plano definida no banco de dados para o campo.<br /><br /> Mapeada a partir de BACK_COLOR na expressão MDX.|  
|**Color**|**String**|Retorna a cor do primeiro plano definida no banco de dados para o item.<br /><br /> Mapeada a partir de FORE_COLOR na expressão MDX.|  
|**UniqueName**|**String**|Retorna o nome totalmente qualificado de um nível.<br /><br /> Mapeada a partir de MEMBER_UNIQUE_NAME na expressão MDX.|  
  
 Para obter mais informações sobre como usar campos e propriedades de campo em uma expressão, consulte [Coleções internas em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md).  
  
  
### <a name="custom-properties"></a>Propriedades personalizadas  
 Propriedades de campo personalizadas para as quais existe suporte de um provedor de dados e que aparecem na consulta MDX subjacente a um conjunto de dados de relatório, mas não aparecem no painel Conjuntos de Dados de relatório como campos daquele conjunto de dados. Por exemplo, **Nomes Longos** é uma propriedade do membro definida para um nível de dimensão. Para incluir o valor em uma caixa de texto, use a expressão `=Fields!`*\<FieldName>*`("Long Names")`. Os nomes de campo na expressão fazem distinção de maiúsculas e minúsculas.  
  
 Use a sintaxe a seguir para consultar as propriedades estendidas personalizadas em uma expressão:  
  
-   *Fields!FieldName("PropertyName")*  
  
 A tabela a seguir mostra a propriedade de campo personalizada que você pode usar para uma fonte de dados do [!INCLUDE[extEssbase](../../includes/extessbase-md.md)] .  
  
|**Propriedade**|**Tipo**|**Descrição ou valor esperado**|  
|------------------|--------------|---------------------------------------|  
|**FORMAT_STRING**|**String**|Definida em uma medida, este é o **FormattedValue** disponível como um tipo String.|  
  
  
##  <a name="Remarks"></a> Comentários  
 Nem todos os modos de entrega de relatório são suportados por esse provedor de dados. Não há suporte para a entrega de relatórios através de assinaturas controladas por dados para essa extensão de processamento de dados. Para obter mais informações, consulte [Usar uma fonte de dados externa para obter dados de assinante &#40;Assinatura controlada por dados&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md) na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online](http://go.microsoft.com/fwlink/?linkid=121312) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obter mais informações, consulte [Usando o SQL Server 2005 Reporting Services com Hyperion Essbase](http://go.microsoft.com/fwlink/?LinkId=81970).  
  
  
##  <a name="HowTo"></a> Tópicos de instruções  
 Esta seção contém instruções passo a passo para trabalhar com conexões de dados, fontes de dados e conjuntos de dados:  
  
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
 Fornece informações sobre a coleção de campos gerada pela consulta do conjunto de dados.  
  
 [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online](http://go.microsoft.com/fwlink/?linkid=121312) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Fornece informações detalhadas sobre suporte à plataforma e à versão para cada extensão de dados.  
  
 [Usando o SQL Server 2005 Reporting Services com Hyperion Essbase](http://go.microsoft.com/fwlink/?LinkId=81970)  
 Fornece informações detalhadas sobre como trabalhar com esta extensão de dados.  
  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  

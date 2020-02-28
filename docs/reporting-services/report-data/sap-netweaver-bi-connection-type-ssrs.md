---
title: Tipo de conexão SAP NetWeaver BI | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: f985856b-31d5-4e56-844b-8a8ee38da67e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1c9edca5b50403f47b82cd2e69d51eb568c66f8a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "77081780"
---
# <a name="sap-netweaver-bi-connection-type-ssrs"></a>Tipo de conexão SAP NetWeaver BI (SSRS)
  Para incluir dados de uma fonte de dados externa do SAP NetWeaver® Business Intelligence em seu relatório, você deve ter um conjunto de dados baseado em uma fonte de dados de relatório do tipo [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)]. Esse tipo de fonte de dados interna tem como base a extensão de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework Data Provider 1.0 para [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)].  
  
 Essa extensão de dados permite que você recupere dados multidimensionais de InfoCubes, MultiProviders (InfoCubes virtuais) e consultas habilitadas para a Web que sejam definidos em uma fonte de dados externa do [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] .  
  
 Use as informações deste tópico para criar uma fonte de dados. Para obter instruções passo a passo, consulte [Adicionar e verificar uma conexão de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadeia de Conexão  
 Contate o administrador do banco de dados para obter informações sobre a conexão e as credenciais que devem ser usadas para se conectar à fonte de dados. O exemplo de cadeia de conexão a seguir especifica uma fonte de dados do [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] em um servidor usando uma porta 8000 e um XML do Analysis Services (XMLA) na Internet usando SOAP:  
  
```  
DataSource=https://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla  
```  
  
 Para ver mais exemplos de cadeias de conexão, confira [Criar cadeias de conexão de dados – Construtor de Relatórios e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
  
##  <a name="Credentials"></a> Credenciais  
 As credenciais são necessárias para executar consultas, visualizar o relatório localmente e visualizá-lo no servidor de relatório.  
  
 Após a publicação do relatório, talvez seja necessário alterar as credenciais da fonte de dados para que, quando o relatório for executado no servidor de relatório, as permissões recuperadas sejam válidas.  
  
 Para obter mais informações, consulte [Especificar informações de credenciais e de conexão para fontes de dados de relatório](specify-credential-and-connection-information-for-report-data-sources.md).  
  
  
##  <a name="Query"></a> Consultas  
 É possível usar o designer de consultas gráfico no modo de Design ou de Consulta para criar uma consulta MDX. Para isso, localize as estruturas de dados subjacentes na fonte de dados. Durante a criação, você pode executar uma consulta interativamente usando o designer de consultas para ver os resultados. A consulta criada define os campos do conjunto de dados. Durante a execução, os dados reais são retornados da fonte de dados. Use o designer de consultas gráficas para executar as seguintes ações:  
  
-   No modo de Design, arraste dimensões, membros, propriedades de membros e imagens chave da fonte de dados para um painel Dados a fim de criar uma consulta de linguagem MDX. Arraste os membros calculados do painel Membros Calculados até o painel Dados para definir campos adicionais para o conjunto de dados.  
  
-   No modo de Consulta, arraste dimensões, membros, propriedades de membros e imagens chave para o painel Consulta ou digite o texto MDX diretamente no painel Consulta. Arraste os membros calculados do painel Membros Calculados até o painel Dados para definir campos adicionais para o conjunto de dados.  
  
 À medida que você vai criando consultas, o designer de consulta adiciona as propriedades padrão automaticamente à consulta MDX. Para incluir propriedades que não sejam as propriedades padrão, modifique a consulta MDX manualmente.  
  
 Para obter mais informações sobre como trabalhar com esse designer de consulta, consulte [Interface do usuário do Designer de Consulta do SAP NetWeaver BI &#40;Construtor de Relatórios&#41;](https://msdn.microsoft.com/library/8edda06d-1608-498b-bd50-10905e54f6ce).  
  
  
##  <a name="Extended"></a> Propriedades de campo estendidas  
 A fonte de dados do [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] dá suporte a propriedades de campo estendidas. As propriedades de campo estendidas são propriedades adicionais a **Value** e **IsMissing** definidas para um campo de conjunto de dados pela extensão do processamento de dados. As propriedades estendidas incluem propriedades predefinidas e propriedades personalizadas. As propriedades predefinidas são propriedades comuns para várias fontes de dados. As propriedades personalizadas são exclusivas para cada fonte de dados.  
  
### <a name="working-with-field-properties"></a>Trabalhando com propriedades de campo  
 As propriedades de campo estendidas não são exibidas no painel de dados do relatório como itens que você pode arrastar em seu layout de relatório. Em vez disso, você arrasta o campo pai da propriedade para o relatório e altera a propriedade padrão de **Value** para a propriedade que você quer usar. Por exemplo, se o nome do campo **Ano Calendário/Nível Mensal 01** é criado em um designer de consulta MDX, soltando um nível do painel Metadados para o painel Consulta, consulte a propriedade estendida personalizada **Nome Longo** em uma expressão usando a sintaxe a seguir:  
  
 `=Fields!Calendar_Year_Month_Level_01("Long Name")`  
  
 O nome de uma propriedade de campo estendida é exibido na Dica de Ferramenta quando você para o mouse sobre um campo no painel Metadados. Para obter mais informações sobre os designers de consultas que você pode usar para explorar os dados subjacentes, consulte [Interface do usuário do Designer de Consulta do SAP NetWeaver BI](../../reporting-services/report-data/sap-netweaver-bi-query-designer-user-interface.md).  
  
> [!NOTE]  
>  Os valores para essas propriedades de campo estendidas passarão a existir somente se a fonte de dados fornecer esses valores quando você executar e recuperar os dados de seus conjuntos de dados. Dessa forma, você poderá consultar esses valores da propriedade **Field** por meio de qualquer expressão usando a sintaxe descrita a seguir. Entretanto, como esses campos são específicos para esse provedor de dados e não faz parte da linguagem de definição de relatório, as alterações que forem feitas nesse valor não serão salvas com a definição de relatório.  
  
 Use uma das seguintes sintaxes para consultar as propriedades estendidas predefinidas em uma expressão:  
  
-   *Fields!FieldName.PropertyName*  
  
-   *Fields!FieldName("PropertyName")*  
  
 Use a sintaxe a seguir para consultar as propriedades estendidas personalizadas em uma expressão:  
  
-   *Fields!FieldName("PropertyName")*  
  
  
### <a name="predefined-field-properties"></a>Propriedades de campo predefinidas  
 A tabela a seguir fornece uma lista das propriedades de campo predefinidas que você pode usar para uma fonte de dados do [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] .  
  
|**Propriedade**|**Tipo**|**Descrição ou valor esperado**|  
|------------------|--------------|---------------------------------------|  
|**Valor**|**Objeto**|Especifica o valor de dados do campo.|  
|**IsMissing**|**Booliano**|Indica se o campo foi encontrado no conjunto de dados resultante.|  
|**FormattedValue**|**Cadeia de caracteres**|Retorna um valor formatado para o número chave.|  
|**BackgroundColor**|**Cadeia de caracteres**|Retorna a cor do segundo plano definida no banco de dados para o campo.|  
|**Color**|**Cadeia de caracteres**|Retorna a cor do primeiro plano definida no banco de dados para o item.|  
|**Chave**|**Objeto**|Retorna a chave para um nível.|  
|**LevelNumber**|**Inteiro**|Para hierarquias pai-filho, retorna o nível ou o número de dimensões.|  
|**ParentUniqueName**|**Cadeia de caracteres**|Para hierarquias pai-filho, retorna um nome totalmente qualificado do nível pai.|  
|**UniqueName**|**Cadeia de caracteres**|Retorna o nome totalmente qualificado de um nível. Por exemplo, o valor **UniqueName** para um funcionário pode ser *[0D_Company].[10D_Department].[11]* .|  
  
 Para obter mais informações sobre como usar campos e propriedades de campo em uma expressão, consulte [Coleções internas em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md).  
  
  
##  <a name="Remarks"></a> Comentários  
 Nem todos os modos de entrega de relatório são suportados por esse provedor de dados. Não há suporte para a entrega de relatórios através de assinaturas controladas por dados para essa extensão de processamento de dados. Para obter mais informações, consulte [Usar uma fonte de dados externa para obter dados de assinante &#40;Assinatura controlada por dados&#41;](../../reporting-services/subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md).  
  
 Para obter mais informações, consulte [Usando o Reporting Services do SQL Server 2008 com o SAP NetWeaver Business Intelligence](https://go.microsoft.com/fwlink/?LinkId=167352).  
  
  
##  <a name="HowTo"></a> Tópicos de instruções  
 Esta seção contém instruções passo a passo para trabalhar com conexões de dados, fontes de dados e conjuntos de dados.  
  
 [Adicionar e verificar uma conexão de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Criar um conjunto de dados compartilhado ou um conjunto de dados inserido &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Adicionar um filtro a um conjunto de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> Seções relacionadas  
 Estas seções da documentação fornecem informações conceituais detalhadas sobre dados de relatório, bem como informações de procedimentos sobre como definir, personalizar e usar partes de um relatório relacionadas aos dados.  
  
 [Conjuntos de dados de relatório &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 Fornece uma visão geral de como acessar dados de seu relatório.  
  
 [Criar cadeias de conexão de dados – Construtor de Relatórios e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
 Fornece informações sobre conexões de dados e fontes de dados.  
  
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Fornece informações sobre conjuntos de dados inseridos e compartilhados.  
  
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 Fornece informações sobre a coleção de campos de conjuntos de dados gerada pela consulta.  
  
 [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  
 Fornece informações detalhadas sobre suporte à plataforma e à versão para cada extensão de dados.  
  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  

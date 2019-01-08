---
title: Tipo de conexão do SAP NetWeaver BI (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f985856b-31d5-4e56-844b-8a8ee38da67e
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: af69191452137761cfaa49d6add0ad39ad3ccdde
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53363658"
---
# <a name="sap-netweaver-bi-connection-type-ssrs"></a>Tipo de conexão SAP NetWeaver BI (SSRS)
  Para incluir dados de uma fonte de dados externa do SAP NetWeaver® Business Intelligence em seu relatório, você deve ter um conjunto de dados baseado em uma fonte de dados de relatório do tipo [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)]. Esse tipo de fonte de dados interna tem como base a extensão de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework Data Provider 1.0 para [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)].  
  
 Essa extensão de dados permite que você recupere dados multidimensionais de InfoCubes, MultiProviders (InfoCubes virtuais) e consultas habilitadas para a Web que sejam definidos em uma fonte de dados externa do [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] .  
  
 Use as informações deste tópico para criar uma fonte de dados. Para obter instruções passo a passo, consulte [adicionar e verificar uma Conexão de dados ou uma fonte de dados &#40;construtor de relatórios e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="support"></a> Versões com suporte  
 O provedor de dados foi desenvolvido para e testado com SAP BW 3.5 e 7.0.  
  
-   Suporte para pacote de 20 para SAP BW 3.5 e 7.0  
  
 Para a autenticação integrada do Windows, o provedor foi desenvolvido e testado com os sistemas a seguir.  
  
-   Pacote 20 de suporte de portas 6.40 do SAP  
  
-   Pacote de suporte de portais 7.0 11 do SAP  
  
-   SAP Duet 1.0  
  
##  <a name="Connection"></a> Cadeia de Conexão  
 Contate o administrador do banco de dados para obter informações sobre a conexão e as credenciais que devem ser usadas para se conectar à fonte de dados. O exemplo de cadeia de conexão a seguir especifica uma fonte de dados do [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] em um servidor usando uma porta 8000 e um XML do Analysis Services (XMLA) na Internet usando SOAP:  
  
```  
DataSource=http://mySAPNetWeaverBIServer:8000/sap/bw/xml/soap/xmla  
```  
  
 Para obter mais exemplos de cadeias de conexão, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
  
  
##  <a name="Credentials"></a> Credenciais  
 As credenciais são necessárias para executar consultas, visualizar o relatório localmente e visualizá-lo no servidor de relatório.  
  
 Após a publicação do relatório, talvez seja necessário alterar as credenciais da fonte de dados para que, quando o relatório for executado no servidor de relatório, as permissões recuperadas sejam válidas.  
  
 Para obter mais informações, consulte [conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) ou [especificar as credenciais no construtor de relatórios](../specify-credentials-in-report-builder.md).  
  
  
  
##  <a name="Query"></a> Consultas  
 É possível usar o designer de consultas gráfico no modo de Design ou de Consulta para criar uma consulta MDX. Para isso, localize as estruturas de dados subjacentes na fonte de dados. Durante a criação, você pode executar uma consulta interativamente usando o designer de consultas para ver os resultados. A consulta criada define os campos do conjunto de dados. Durante a execução, os dados reais são retornados da fonte de dados. Use o designer de consultas gráficas para executar as seguintes ações:  
  
-   No modo de Design, arraste dimensões, membros, propriedades de membros e imagens chave da fonte de dados para um painel Dados a fim de criar uma consulta de linguagem MDX. Arraste os membros calculados do painel Membros Calculados até o painel Dados para definir campos adicionais para o conjunto de dados.  
  
-   No modo de Consulta, arraste dimensões, membros, propriedades de membros e imagens chave para o painel Consulta ou digite o texto MDX diretamente no painel Consulta. Arraste os membros calculados do painel Membros Calculados até o painel Dados para definir campos adicionais para o conjunto de dados.  
  
 À medida que você vai criando consultas, o designer de consulta adiciona as propriedades padrão automaticamente à consulta MDX. Para incluir propriedades que não sejam as propriedades padrão, modifique a consulta MDX manualmente.  
  
 Para obter mais informações sobre como trabalhar com esse designer de consulta, consulte [Interface do usuário do Designer de Consulta do SAP NetWeaver BI &#40;Construtor de Relatórios&#41;](../sap-netweaver-bi-query-designer-user-interface-report-builder.md).  
  
  
  
##  <a name="Extended"></a> Propriedades de campo estendidas  
 A fonte de dados do [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] dá suporte a propriedades de campo estendidas. As propriedades de campo estendidas são propriedades adicionais a `Value` e `IsMissing` definidas para um campo de conjunto de dados pela extensão de processamento de dados. As propriedades estendidas incluem propriedades predefinidas e propriedades personalizadas. As propriedades predefinidas são propriedades comuns para várias fontes de dados. As propriedades personalizadas são exclusivas para cada fonte de dados.  
  
### <a name="working-with-field-properties"></a>Trabalhando com propriedades de campo  
 As propriedades de campo estendidas não são exibidas no painel de dados do relatório como itens que você pode arrastar em seu layout de relatório. Em vez disso, você arrasta o campo pai da propriedade para o relatório e altera a propriedade padrão de `Value` para a propriedade que você deseja usar. Por exemplo, se o nome do campo **Ano Calendário/Nível Mensal 01** é criado em um designer de consulta MDX, soltando um nível do painel Metadados para o painel Consulta, consulte a propriedade estendida personalizada **Nome Longo** em uma expressão usando a sintaxe a seguir:  
  
 `=Fields!Calendar_Year_Month_Level_01("Long Name")`  
  
 O nome de uma propriedade de campo estendida é exibido na Dica de Ferramenta quando você para o mouse sobre um campo no painel Metadados. Para obter mais informações sobre os designers de consultas que você pode usar para explorar os dados subjacentes, consulte [Interface do usuário do Designer de Consulta do SAP NetWeaver BI](sap-netweaver-bi-query-designer-user-interface.md).  
  
> [!NOTE]  
>  Os valores para essas propriedades de campo estendidas passarão a existir somente se a fonte de dados fornecer esses valores quando você executar e recuperar os dados de seus conjuntos de dados. Dessa forma, você poderá consultar esses valores da propriedade `Field` a partir de qualquer expressão usando a sintaxe descrita a seguir. Entretanto, como esses campos são específicos para esse provedor de dados e não faz parte da linguagem de definição de relatório, as alterações que forem feitas nesse valor não serão salvas com a definição de relatório.  
  
 Use uma das seguintes sintaxes para consultar as propriedades estendidas predefinidas em uma expressão:  
  
-   *Fields!FieldName.PropertyName*  
  
-   *Fields!FieldName("PropertyName")*  
  
 Use a sintaxe a seguir para consultar as propriedades estendidas personalizadas em uma expressão:  
  
-   *Fields!FieldName("PropertyName")*  
  
  
  
### <a name="predefined-field-properties"></a>Propriedades de campo predefinidas  
 A tabela a seguir fornece uma lista das propriedades de campo predefinidas que você pode usar para uma fonte de dados do [!INCLUDE[SAP_DPE_BW_1](../../includes/sap-dpe-bw-1-md.md)] .  
  
|**Propriedade**|**Tipo**|**Descrição ou valor esperado**|  
|------------------|--------------|---------------------------------------|  
|`Value`|`Object`|Especifica o valor de dados do campo.|  
|`IsMissing`|`Boolean`|Indica se o campo foi encontrado no conjunto de dados resultante.|  
|`FormattedValue`|`String`|Retorna um valor formatado para o número chave.|  
|`BackgroundColor`|`String`|Retorna a cor do segundo plano definida no banco de dados para o campo.|  
|`Color`|`String`|Retorna a cor do primeiro plano definida no banco de dados para o item.|  
|`Key`|`Object`|Retorna a chave para um nível.|  
|`LevelNumber`|`Integer`|Para hierarquias pai-filho, retorna o nível ou o número de dimensões.|  
|`ParentUniqueName`|`String`|Para hierarquias pai-filho, retorna um nome totalmente qualificado do nível pai.|  
|`UniqueName`|`String`|Retorna o nome totalmente qualificado de um nível. Por exemplo, o `UniqueName` valor de um funcionário pode ser *[0D_Company]. [ 10D_Department]. [11]* .|  
  
 Para obter mais informações sobre como usar campos e propriedades de campo em uma expressão, consulte [Coleções internas em expressões &#40;Construtor de Relatórios e SSRS&#41;](../report-design/built-in-collections-in-expressions-report-builder.md).  
  
  
  
##  <a name="Remarks"></a> Comentários  
 Nem todos os modos de entrega de relatório são suportados por esse provedor de dados. Não há suporte para a entrega de relatórios através de assinaturas controladas por dados para essa extensão de processamento de dados. Para obter mais informações, consulte [Usar uma fonte de dados externa para obter dados de assinante &#40;Assinatura controlada por dados&#41;](../subscriptions/use-an-external-data-source-for-subscriber-data-data-driven-subscription.md).  
  
 Para obter mais informações, consulte [Usando o Reporting Services do SQL Server 2008 com o SAP NetWeaver Business Intelligence](https://go.microsoft.com/fwlink/?LinkId=167352).  
  
  
  
##  <a name="HowTo"></a> Tópicos de instruções  
 Esta seção contém instruções passo a passo para trabalhar com conexões de dados, fontes de dados e conjuntos de dados.  
  
 [Adicionar e verificar uma Conexão de dados ou uma fonte de dados &#40;relatórios e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Criar um conjunto de dados compartilhado ou um conjunto de dados inserido &#40;Construtor de Relatórios e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Adicionar um filtro a um conjunto de dados &#40;Construtor de Relatórios e SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
  
##  <a name="Related"></a> Seções relacionadas  
 Estas seções da documentação fornecem informações conceituais detalhadas sobre dados de relatório, bem como informações de procedimentos sobre como definir, personalizar e usar partes de um relatório relacionadas aos dados.  
  
 [Adicionar dados a um relatório &#40;relatórios e SSRS&#41;](report-datasets-ssrs.md)  
 Fornece uma visão geral de como acessar dados de seu relatório.  
  
 [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 Fornece informações sobre conexões de dados e fontes de dados.  
  
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Fornece informações sobre conjuntos de dados inseridos e compartilhados.  
  
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 Fornece informações sobre a coleção de campos de conjuntos de dados gerada pela consulta.  
  
 [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)  
 Fornece informações detalhadas sobre suporte à plataforma e à versão para cada extensão de dados.  
  
 
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  

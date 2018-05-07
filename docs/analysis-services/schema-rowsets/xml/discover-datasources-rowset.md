---
title: Conjunto de linhas DISCOVER_DATASOURCES | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6ebbc52708591c54f9236aabcd2404c01a65e81f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="discoverdatasources-rowset"></a>Conjunto de linhas DISCOVER_DATASOURCES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Retorna uma lista das fontes de dados de provedor de XMLA (XML for Analysis) disponível no servidor ou no serviço Web. As fontes dos dados publicados são retornadas de uma URL do servidor da Web de aplicativo. O cliente pode conectar a uma das fontes de dados desta lista.  
  
 Se você chamar o [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método com o **DISCOVER_DATASOURCES** valor de enumeração no [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) elemento, o **Discover** método retorna o **DISCOVER_DATASOURCES** conjunto de linhas.  
  
 **Aplica-se a:** modelos de tabela, modelos multidimensionais  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O cliente seleciona uma fonte de dados, definindo o **DataSourceInfo** propriedade o [propriedades](../../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md) elemento que é enviado junto com o [comando](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md) elemento o [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método. Um cliente não deve criar o conteúdo da propriedade **DataSourceInfo** a ser enviada ao servidor. Em vez disso, ele deverá usar o método **Discover** para localizar as fontes de dados às quais o provedor oferece suporte. O cliente envia de volta o mesmo valor da propriedade **DataSourceInfo** obtido do conjunto de linhas **DISCOVER_DATASOURCES** .  
  
 O conjunto de linhas **DISCOVER_DATASOURCES** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Restrição|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**DataSourceName**|**DBTYPE_WSTR**|Sim|O nome da fonte de dados, como **Adventure Works**.|  
|**DataSourceDescription**|**DBTYPE_WSTR**||A descrição da fonte de dados inserida pelo editor.<br /><br /> Pode retornar **NULL**.|  
|**URL**|**DBTYPE_WSTR**|Sim|O caminho exclusivo que mostra onde invocar os métodos XMLA (XML for Analysis para a fonte de dados.<br /><br /> Pode retornar **NULL**.|  
|**DataSourceInfo**|**DBTYPE_WSTR**||Uma cadeia de caracteres que contém informações adicionais necessárias para a conexão à fonte de dados.<br /><br /> Pode retornar **NULL**.|  
|**ProviderName**|**DBTYPE_WSTR**|Sim|O o nome do provedor para a fonte de dados.<br /><br /> Exemplo: `"MSOLAP"`<br /><br /> Pode retornar **NULL**.|  
|**ProviderType**|**DBTYPE_WSTR**|Sim|Os tipos de dados suportados pelo provedor. Esta matriz pode incluir um ou mais dos seguintes tipos:<br /><br /> **MDP**: provedor de dados multidimensional.<br /><br /> **TDP**: provedor de dados tabular.<br /><br /> **DMP**: provedor de mineração de dados (implementa a especificação OLE DB para mineração de dados).|  
|**authenticationMode**|**DBTYPE_WSTR**|Sim|Uma especificação do tipo de modo de segurança usado pela fonte de dados. Pode conter um dos seguintes valores:<br /><br /> **Unauthenticated**: nenhuma ID de usuário ou senha deve ser enviada.<br /><br /> **Authenticated**: a ID de usuário e a senha devem ser incluídas nas informações necessárias para a conexão à fonte de dados.<br /><br /> **Integrado**: A fonte de dados usa a segurança subjacente para determinar a autorização, como segurança integrada fornecida pelo [!INCLUDE[msCoName](../../../includes/msconame-md.md)] serviços de informações da Internet (IIS).|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
> [!IMPORTANT]  
>  O conjunto de linhas **DISCOVER_DATASOURCES** não pode ser consultado por meio de consultas DMV e da sintaxe do comando SELECT. No entanto, o **DISCOVER_DATASOURCES** conjunto de linhas pode ser consultado usando <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|06c03d41-f66d-49f3-b1b8-987f7af4cf18|  
|ADOMDNAME|DataSources|  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis conjuntos de linhas de esquema](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

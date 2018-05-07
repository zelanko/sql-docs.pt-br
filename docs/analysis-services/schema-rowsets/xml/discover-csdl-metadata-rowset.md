---
title: Conjunto de linhas DISCOVER_CSDL_METADATA | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4aa7b3a15309e8ba57604112f3813b7d2d56cec7
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="discovercsdlmetadata-rowset"></a>Conjunto de linhas DISCOVER_CSDL_METADATA
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Retorna informações sobre um modelo de dados (de tabela ou multidimensional) do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] , fornecendo a definição do modelo no formato da CSDLBI (Linguagem de Definição de Esquema Conceitual com anotações de BI). A CSDLBI se baseia na CSDL, um esquema XML usado pela Estrutura de Dados de Entidade que é utilizada para comunicação entre um servidor [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e o cliente [!INCLUDE[ssCrescent](../../../includes/sscrescent-md.md)] . As anotações de BI (Business Intelligence) fornecem metadados adicionais sobre modelos de tabela e os objetos neles. Para obter mais informações sobre modelos de dados de tabela, consulte [CSDLBI &#40;Anotações CSDL para Business Intelligence&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md).  
  
 O contexto de segurança do comando afeta o conjunto de linhas que é retornado. São requeridas permissões de leitura instância do Analysis Services para obter a definição CSDL do servidor.  
  
 O identificador de idioma do cliente que emite a solicitação de conjunto de linhas é incluído na cadeia de conexão para o comando e afeta o idioma exibido em várias propriedades que são retornadas como parte do conjunto de linhas.  Para obter informações sobre propriedades e descrição que podem ser afetados pelo identificador de idioma, consulte a seção Comentários.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_CSDL_METADATA** contém as colunas a seguir.  
  
|**Nome da coluna**|**Indicador de tipo**|**Restrição**|**Descrição**|  
|---------------------|------------------------|---------------------|---------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|Sim|Especifica o nome do banco de dados para o qual a descrição CSDLBI é solicitada. Se ele for omitido, o banco de dados atual será usado.<br /><br /> Essa restrição é necessária para todos os tipos de modelo.|  
|**PERSPECTIVE_ID**|**DBTYPE_WSTR**|Sim|Especifica a ID de uma perspectiva que foi definida no modelo especificado por CATALOG_NAME.<br /><br /> Uma restrição opcional. Aplica-se a todos os tipos de modelo.|  
|**PERSPECTIVE_NAME**|**DBTYPE_WSTR**|Sim|Especifica o nome de uma perspectiva que foi definida no modelo especificado por CATALOG_NAME.<br /><br /> Essa restrição é necessária quando o modelo de tabela inclui perspectivas ou quando uma solução multidimensional inclui vários cubos ou perspectivas.|  
|**METADATA**|**DBTYPE_WSTR**|não|Uma cadeia de caracteres que contém a definição XML de uma fonte de dados e suas propriedades, de acordo com o esquema da CSDLBI.|  
|**CUBE_ID**|**DBTYPE_WSTR**|Sim|Um identificador de cadeia de caracteres.<br /><br /> Essa restrição é opcional para bancos de dados multidimensionais. Se vários cubos estiverem disponíveis e a restrição for omitida, será retornado o cubo padrão.|  
  
## <a name="remarks"></a>Comentários  
 DISCOVER_CSDL_METADATA tem os seguintes requisitos:  
  
-   A solicitação DISCOVER falhará se um banco de dados não for especificado usando a restrição CATALOG_NAME.  
  
-   Em um modelo de tabela, uma ID de perspectiva será exigida se houver mais de uma perspectiva no modelo.  
  
-   Em modelos multidimensionais, o nome do catálogo e o nome do cubo (perspectiva) são necessários.  
  
-   Se uma perspectiva for fornecida como uma restrição, o mesmo conjunto de linhas de CSDL será retornado para o modelo. No entanto, todos os objetos que presentes no modelo, mas não estão incluídos na perspectiva especificada, são marcados como **Hidden** = True.  
  
-   Para tabelas e colunas, a solicitação DISCOVER gera sempre um valor da dimensão de cubo. Se a propriedade de dimensão de cubo não for definida, a solicitação retornará o valor da dimensão.  
  
-   A solicitação DISCOVER não pode retornar qualquer medida nem colunas calculadas contendo um erro semântico.  
  
-   A solicitação DISCOVER não retornará informações para objetos sem valores de propriedade. A solicitação DISCOVER também não retornará valores para atributos que usam o valor padrão.  
  
 A cadeia de caracteres XML que é retornada no conjunto de linhas pode incluir as propriedades ou valores a seguir, específicos do idioma. Por exemplo, se você emitir a solicitação de conjunto de linhas de um cliente que tem o LCID de 0403 (espanhol catalão), a propriedade retornará os valores a seguir como apropriados para espanhol catalão. Se traduções não estiverem disponíveis no servidor, a cadeia de caracteres para o idioma padrão do servidor será retornada.  
  
-   Caption  
  
-   Qualificador  
  
-   SortDirection  
  
-   IsRightToLeft  
  
## <a name="example"></a>Exemplo  
 **Tabela**  
  
 A consulta XMLA a seguir retorna a representação CSDL do exemplo de modelo de tabela da AdventureWorks 2012. Cada solução de tabela pode conter apenas um modelo, de modo que a restrição PERSPECTIVE_NAME pode ser deixada em branco. No entanto, esse modelo contém várias perspectivas.  
  
```  
  
<Discover  xmlns="urn:schemas-microsoft-com:xml-analysis">  
     <RequestType>DISCOVER_CSDL_METADATA</RequestType>  
         <Restrictions>  
            <RestrictionList>  
                <CATALOG_NAME>AdventureWorks2012Tabular</CATALOG_NAME>  
                <PERSPECTIVE_NAME>EMPLOYEE</PERSPECTIVE_NAME>  
                <VERSION>2.0</VERSION>  
            </RestrictionList>  
         </Restrictions>  
         <Properties>  
                <PropertyList>  
                </PropertyList>  
         </Properties>  
</Discover>  
  
```  
  
## <a name="example"></a>Exemplo  
 **Multidimensional**  
  
 A consulta XMLA a seguir retorna as representações CSDLBI do cubo Operações da Contoso. A restrição VERSION é necessária para consultar um banco de dados multidimensional. O banco de dados Varejo da Contoso contém dois cubos, de modo que o cubo Operações é referenciado usando a restrição PERSPECTIVE_NAME.  
  
```  
  
<Discover  xmlns="urn:schemas-microsoft-com:xml-analysis">  
     <RequestType>DISCOVER_CSDL_METADATA</RequestType>  
         <Restrictions>  
            <RestrictionList>  
                <CATALOG_NAME>Contoso_Retail</CATALOG_NAME>  
                <PERSPECTIVE_NAME>Operation</PERSPECTIVE_NAME>  
                <VERSION>2.0</VERSION>  
            </RestrictionList>  
         </Restrictions>  
         <Properties>  
                <PropertyList>  
                </PropertyList>  
         </Properties>  
 </Discover>  
  
```  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|3444B255-171E-4cb9-AD98-19E57888A75F|  
|ADOMDNAME|Csdl|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas do esquema do Analysis Services](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)   
 [Anotações CSDL para Business Intelligence & #40; CSDLBI & #41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
  

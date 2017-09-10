---
title: Conceitos da CSDLBI | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 2fbdf621-a94d-4a55-a088-3d56d65016ac
caps.latest.revision: 28
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0b38e5f9de0860c75c0262c2e9684cc5440ba22d
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="csdlbi-concepts"></a>Conceitos da CSDLBI

[!INCLUDE[ssas-appliesto-sqlas-all](../../includes/ssas-appliesto-sqlas-all.md)]

  A CSDLBI (Linguagem de Definição de Esquema Conceitual com anotações de BI) baseia-se na Estrutura de Dados de Entidade, que é uma abstração para representar dados de modo a permitir que conjuntos de dados discrepantes sejam acessados, consultados ou exportados de modo programático. A CSDLBI é usada para representar modelos de dados criados com o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], pois ele oferece suporte a aplicativos e relatórios avançados orientados a dados.  
  
 Esta seção explica como a representação CSDLBI é mapeada para modelos de dados (de tabela e multidimensionais) do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], juntamente com exemplos de cada tipo de modelo.  
  
 Exemplos obtidos no banco de dados de exemplo AdventureWorks são usados para ilustrar esses conceitos, disponíveis em Codeplex. Para obter mais informações sobre os exemplos, consulte [exemplos do Adventure Works para SQL Server](http://go.microsoft.com/fwlink/?linkID=220093).  
  
## <a name="structure-of-a-tabular-model-in-csdlbi"></a>Estrutura de um modelo de tabela na CSDLBI  
 Um documento CSDLBI que descreve um modelo de relatório e seus dados começa com a instrução xsd, seguida pela definição de um modelo.  
  
 O modelo é um namespace, que contém as seguintes entidades, associações e propriedades principais:  
  
-   O **EntityContainer** lista as tabelas no modelo.  
  
-   Cada tabela é listada com o **EntityContainer** como um **EntitySet**.  
  
-   Cada relação entre duas tabelas é descrita como um **AssociationSet** que define os pontos de extremidade de relação e as funções de relação.  
  
-   O **EntityType** elemento é estendido para BISM a fim de fornecer detalhes adicionais sobre as tabelas e colunas neles, inclusive propriedades de classificação e fins de exibição.  
  
-   O **medidas** elemento define cálculos que podem ser usados no modelo. Uma medida pode ser convertida em um KPI, adicionando um conjunto de atributos de exibição especiais, usando o novo **KPI** elemento.  
  
-   Não há nenhuma representação separada de perspectivas. Colunas e tabelas que não estão incluídas em uma perspectiva estão presentes na CSDL, mas sinalizadas com o **Hidden** atributo.  
  
### <a name="entities-entitysets-and-entitytypes"></a>Entities, EntitySets e EntityTypes  
 A noção de uma entidade na Estrutura de Dados de Entidade é estendida para representar colunas e tabelas do modelo de dados. O trecho a seguir mostra a lista de **EntitySet** elementos em uma simples que contém apenas três tabelas de modelo.  
  
```  
<EntityContainer Name="SimpleModel">  
<EntitySet Name="DimCustomer"EntityType="SimpleModel.DimCustomer">  
     <bi:EntitySet />  
   </EntitySet>  
<EntitySet Name="DimDate" EntityType="SimpleModel.DimDate">  
     <bi:EntitySet />  
   </EntitySet>  
<EntitySet Name="DimGeography" EntityType="SimpleModel.DimGeography">  
     <bi:EntitySet />  
   </EntitySet> />  
  
```  
  
 O **EntitySet** não contém informações sobre colunas ou dados na tabela. A descrição detalhada das colunas e suas propriedades é fornecida no elemento EntityType.  
  
 O **EntitySet** elemento para cada entidade (tabela) inclui uma coleção de propriedades que definem a coluna de chave, o tipo de dados e o comprimento da coluna, nulidade, o comportamento de classificação e assim por diante. Por exemplo, o trecho CSDL a seguir descreve três colunas da tabela Customer. A primeira coluna é uma coluna oculta especial usada internamente pelo modelo.  
  
```  
<EntityType Name="Customer">  
  <Key>  
     <PropertyRef Name="RowNumber" />  
  </Key>  
    <Property Name="RowNumber" Type="Int64" Nullable="false">  
     <bi:Property Hidden="true" Contents="RowNumber"  
       Stability="RowNumber" />  
    </Property>  
    <Property Name="CustomerKey" Type="Int64" Nullable="false">  
      <bi:Property />  
    </Property>  
     <Property Name="FirstName" Type="String" MaxLength="Max" FixedLength="false">  
       <bi:Property />  
      </Property>  
  
```  
  
 Para limitar o tamanho do documento CSDLBI gerado, as propriedades que aparecem mais de uma vez em uma entidade são especificadas por uma referência a uma propriedade existente, para que a propriedade precise ser listada apenas uma vez para o **EntityType**. O aplicativo cliente pode obter o valor da propriedade localizando o **EntityType** que corresponde a **OriginEntityType**.  
  
### <a name="relationships"></a>Relações  
 Na estrutura de dados de entidade, as relações são definidas como *associações* entre entidades.  
  
 As associações sempre têm exatamente duas extremidades, cada uma apontando para um campo ou uma coluna em uma tabela. Portanto, várias relações são possíveis entre duas tabelas, se as relações tiverem pontos de extremidade diferentes. Um nome de função é atribuído aos pontos de extremidade da associação e indica como a associação é usada no contexto do modelo de dados. Um exemplo de um nome de função pode ser **ShipTo**, quando aplicado a uma ID de cliente que está relacionada à ID de cliente em uma tabela Orders.  
  
 A representação CSDLBI do modelo também contém atributos na associação que determinam como as entidades são mapeadas umas às outras em termos do *multiplicidade* da associação. A multiplicidade indica se o atributo ou a coluna no ponto de extremidade de uma relação entre tabelas está em um dos lados de uma relação ou nos vários lados. Não há nenhum valor separado para relações um para um. As anotações da CSDLBI oferecem suporte à multiplicidade 0 (o que significa que a entidade não está associada a nada) ou 0..1 (o que significa uma relação um para um ou um para muitos).  
  
 O exemplo a seguir representa a saída da CSDLBI de uma relação entre as tabelas Date e ProductInventory, na qual as duas tabelas são unidas na coluna DateAlternateKey. Observe que, por padrão, o nome do **AssociationSet** é o nome totalmente qualificado das colunas que estão envolvidos na relação. Porém, você pode alterar esse comportamento ao criar o modelo, para usar um formato de nomenclatura diferente.  
  
```  
<AssociationSet Name="ProductInventory_Date_DateKey" Association="Model.ProductInventory_Date_DateKey">  
              <End EntitySet="ProductInventory" />  
              <End EntitySet="Date" />  
              <bi:AssociationSet />  
            </AssociationSet>  
  
```  
  
### <a name="visualization-and-navigation-properties"></a>Visualização e propriedades de navegação  
 Uma parte importante das anotações da CSDLBI são as propriedades para definição da apresentação na camada de relatório e para navegação nas relações entre entidades. Normalmente, ao criar um modelo de dados, você não considera importante controlar como os dados são ordenados ou agrupados, ou qual pode ser o valor padrão, pressupondo que o aplicativo cliente especificará ordenação e outros detalhes da apresentação. No entanto, os modelos de tabela do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] foram projetados para integração ao cliente de relatório do [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], e incluem propriedades e atributos que oferecem suporte à apresentação de entidades do modelo de dados na superfície de design do relatório.  
  
 As extensões de visualização incluem atributos que especificam a agregação padrão a ser usada com dados numéricos, indicam que um campo de texto aponta para a URL de uma imagem ou especificam o campo usado para classificar o campo atual.  
  
### <a name="name-properties-and-naming-conventions"></a>Propriedades de nome e convenções de nomenclatura  
 O esquema da CSDLBI informa que cada entidade tem um nome exclusivo e um identificador que podem ser usados como uma chave. Além disso, algumas entidades podem ter legendas usadas para fins de exibição, e nomes contextuais que são alterados, dependendo do local em que a entidade é usada.  
  
 O **documentação** elemento fornece a oportunidade para designers de relatório fornecerem uma descrição da entidade, para ajudar os usuários empresariais a compreenderem o significado dos dados. Algumas entidades também permitem um ou mais **anotação** atributos, que fornecem metadados extras para consumo pelo aplicativo ou pelos clientes.  
  
 Quando você gera um modelo para as ferramentas do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], os nomes criados para objetos seguem as convenções do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para nomeação de objeto e exclusividade de nome. No entanto, como a CSDLBI se baseia na EDF (Estrutura de Dados de Entidade), que requer que os nomes obedeçam às convenções dos identificadores C#, quando o servidor cria a saída de CSDLBI para um modelo, o servidor adota os nomes usados no esquema do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e cria automaticamente novos nomes de objeto em conformidade com os requisitos da EDF. A tabela a seguir descreve as operações através das quais os novos nomes são gerados.  
  
|Regra|Ação|  
|----------|------------|  
|Nenhum caractere proibido|Os caracteres proibidos são substituídos pelo sublinhado.|  
|Os nomes devem ser exclusivos|Se duas cadeias de caracteres forem iguais, uma se tornará exclusiva através do acréscimo de um sublinhado e um número|  
  
> [!WARNING]  
>  Legendas e qualificadores têm traduções e, em um determinado idioma, um ou outro poderia estar presente. Isso significa que, nos casos em que um qualificador e um nome ou um qualificador e uma legenda são concatenados, as cadeias de caracteres poderiam estar em dois idiomas diferentes.  
  
## <a name="additions-to-support-multidimensional-models"></a>Adições para oferecer suporte aos modelos multidimensionais  
 A versão 1.0 das anotações da CSDLBI oferecia suporte apenas a modelos de tabela. Na versão 1.1, foi adicionado suporte para modelos multidimensionais (cubos OLAP) criados usando ferramentas tradicionais de desenvolvimento de BI. Portanto, agora você pode emitir uma solicitação XML para um modelo multidimensional e receber uma definição CSDLBI do modelo, para uso em relatórios.  
  
 **Cubos:** um SQL Server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados de tabela pode conter apenas um modo. Em contraposição, cada banco de dados multidimensional pode conter vários cubos e cada banco de dados é associado a um cubo padrão. Desse modo, ao emitir uma solicitação XML em um servidor multidimensional, é necessário especificar o cubo. Caso contrário, o XML do cubo padrão será retornado.  
  
 De qualquer forma, a representação de um cubo é muito semelhante a de um banco de dados modelo de tabela. O nome do cubo e o cubo correspondem ao nome do banco de dados de tabela e ao identificador do banco de dados.  
  
 **Dimensões:** uma dimensão é representada na CSDLBI como uma entidade (tabela) com colunas e propriedades. Observe que, mesmo que não são incluídas em uma perspectiva, uma dimensão que está incluída no modelo será representada na saída da CSDL, marcada como **Hidden**.  
  
 **Perspectivas:** um cliente pode solicitar CSDL para perspectivas individuais. Para obter mais informações, consulte [linhas DISCOVER_CSDL_METADATA](../../analysis-services/schema-rowsets/xml/discover-csdl-metadata-rowset.md).  
  
 **Hierarquias:** hierarquias têm suporte e representadas na CSDLBI como um conjunto de níveis.  
  
 **Membros:** suporte para o membro padrão foi adicionado e valores padrão são automaticamente adicionados à saída da CSDLBI.  
  
 **Membros calculados:** modelos multidimensionais dão suporte a membros calculados para filhos de **todos os** com um único membro real.  
  
 **Atributos de dimensão:** na saída da CSDLBI, atributos de dimensão têm suporte e automaticamente marcados como não agregável.  
  
 **KPIs:** KPIs tinham suporte na versão 1.1 da CSDLBI, mas a representação foi alterada. Antes, um KPI era uma propriedade de uma medida. Na versão 1.1, o elemento KPI pode ser adicionado a uma medida  
  
 **Novas propriedades:** atributos adicionais foram adicionados para dar suporte a modelos DirectQuery.  
  
 **Limitações:** não há suporte para a segurança da célula.  
  
## <a name="see-also"></a>Consulte também  
 [Anotações CSDLBI &#40;CSDL para Business Intelligence&#41;](../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/csdl-annotations-for-business-intelligence-csdlbi.md)  
  
  

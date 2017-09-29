---
title: O que &#39; s novos no SQL Server de 2017 Analysis Services | Microsoft Docs
ms.custom: 
ms.date: 09/21/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1eb6afc9-76ed-45a2-a188-374a4fc23224
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: c75d1ec210f3511408e2c976df28f9db22d7272f
ms.contentlocale: pt-br
ms.lasthandoff: 09/22/2017

---

# <a name="what39s-new-in-sql-server-2017-analysis-services"></a>O que &#39; s novos no SQL Server de 2017 Analysis Services
[!INCLUDE[ssas-appliesto-sql2017](../includes/ssas-appliesto-sql2017.md)]

SQL Server 2017 Analysis Services vê algumas das melhorias mais importantes desde o SQL Server 2012. Aproveitando o sucesso do modo de tabela (introduzido no SQL Server 2012 Analysis Services), esta versão torna mais eficiente do que nunca modelos de tabela.

Modo multidimensional e PowerPivot para o modo do SharePoint são um grampeamento de muitas implantações do Analysis Services. Ciclo de vida do produto do Analysis Services, esses modos estão maduros. Não há recursos novos para ambos os modos nesta versão. No entanto, correções e melhorias de desempenho são incluídas.

Os recursos descritos aqui são incluídos no SQL Server de 2017 Analysis Services. Mas para tirar proveito deles, você também deve usar as versões mais recentes de [SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md) (SSDT) e [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md) (SSMS). SSDT e SSMS é atualizado mensalmente com novos e aprimorados que normalmente recursos conincide com a nova funcionalidade no SQL Server.  

Embora seja divertido para levar os wrappers desativar todos os novos recursos, também é importante saber o que está sendo substituído e descontinuados nesta versão e versões futuras. Certifique-se de check-out [compatibilidade com versões anteriores (SQL Server 2017 Analysis Services)](analysis-services-backward-compatibility-sql2017.md).

Vamos dar uma olhada em alguns dos principais novos recursos nesta versão.

## <a name="1400-compatibility-level-for-tabular-models"></a>Nível de Compatibilidade 1400; para modelos de tabela
  Para aproveitar muitos dos novos recursos e funcionalidade descrita aqui, modelos de tabela novos ou existentes devem ser definidos ou atualizados para o nível de compatibilidade 1400. Os modelos no nível de compatibilidade 1400 não podem ser implantados no SQL Server 2016 SP1 ou anterior nem ter o downgrade para níveis de compatibilidade inferiores. Para obter mais informações, consulte [nível de compatibilidade para modelos de tabela do Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).
  
No SSDT, é possível selecionar o novo nível de compatibilidade 1400 ao criar novos projetos de modelo de tabela. 

![AS_NewTabular1400Project](../analysis-services/media/as-newtabular1400project.png)


Para atualizar um modelo tabular existente no SSDT, no Gerenciador de soluções, clique com botão direito **Model.bim**e, em seguida, em **propriedades**, defina o **nível de compatibilidade** propriedade ** SQL Server 2017 (1400)**. 

![AS_Model_Properties](../analysis-services/media/as-model-properties.png)

É importante ter em mente, depois de atualizar um modelo existente para 1400, você não pode fazer o downgrade. Certifique-se de manter um backup de seu banco de dados de modelo de 1200.

## <a name="modern-get-data-experience"></a>Experiência moderna do recurso Obter Dados
Quando se trata de ingestão de dados de fontes de dados em seus modelos de tabela, o SQL Server Data Tools (SSDT) apresenta a moderna **obter dados** experiência para modelos no nível de compatibilidade de 1400. Esse novo recurso se baseia em uma funcionalidade semelhante no Power BI Desktop e Microsoft Excel 2016. A experiência de obter dados moderna fornece recursos de mashup de dados e transformação de dados grandes usando o construtor de consultas de obter dados e expressões de M.

Obter dados modernos experiência de suporte fornecido para uma ampla gama de fonte de dados adicional. Atualizações futuras dará suporte a fontes de dados adicionais.

![AS_Get_Data_in_SSDT](../analysis-services/media/as-get-data-in-ssdt.png)

 Uma interface do usuário poderosa e intuitiva facilitar a seleção de seus dados e recursos de transformação/mashup de dados muito mais fácil.

![Mashup avançada](../analysis-services/media/as-get-data-advanced.png)


Experiência moderna obter dados e recursos de mashup M não se aplicam a ugraded de modelos de tabela existente de nível de compatibilidade 1200 para 1400. A nova experiência só se aplica a novos modelos criados no nível de compatibilidade de 1400.

## <a name="encoding-hints"></a>Dicas de codificação
Esta versão apresenta dicas de codificação, um recurso avançado, usado para otimizar o processamento (atualização de dados) grandes de memória de modelos de tabela. Para entender melhor codificação, consulte [desempenho de ajuste de modelos de tabela no SQL Server 2012 Analysis Services](https://msdn.microsoft.com/library/dn393915.aspx) white paper para entender melhor a codificação.

* Codificação de valor fornece melhor desempenho de consulta para colunas que normalmente são usados somente para agregações.

* Codificação de hash é preferível Agrupar por colunas (geralmente valores de tabela de dimensões) e chaves estrangeiras. Colunas de cadeia de caracteres sempre são codificado de hash.

Colunas numéricas podem usar qualquer um desses métodos de codificação. Quando o Analysis Services inicia o processamento de uma tabela, se a tabela estiver vazia (com ou sem partições) ou uma operação de processamento de tabela completa está sendo executada, os valores de exemplos são obtidos para cada coluna numérica determinar se deve aplicar o valor ou codificação de hash . Por padrão, o valor de codificação é escolhido quando o exemplo de valores distintos na coluna é grande o suficiente, caso contrário, a codificação de hash geralmente fornece melhor compactação. É possível para o Analysis Services alterar o método de codificação depois que a coluna é parcialmente processada com base em obter mais informações sobre a distribuição de dados e reiniciar o processo de codificação. Obviamente, isso aumenta o tempo de processamento e é ineficiente. Ajuste de desempenho white paper aborda a codificação novamente em mais detalhes e descreve como detectá-lo usando o SQL Server Profiler.

Dicas de codificação permitem Modelador especificar uma preferência para o método de codificação que recebe o conhecimento prévio de criação de perfil de dados e/ou em resposta a codificação novamente os eventos de rastreamento. Desde que a agregação em colunas codificado de hash é mais lenta do que o valor codificado colunas, o valor de codificação pode ser especificado como uma dica para essas colunas. Não há garantia de que a preferência será aplicada; Portanto, é uma dica em vez de uma configuração. Para especificar uma dica de codificação, defina a propriedade EncodingHint na coluna. Os valores possíveis são "Padrão", "Valor" e "Hash". O trecho a seguir de metadados com base em JSON do arquivo Model.bim Especifica o valor de codificação para a coluna valor das vendas.

```
{
    "name": "Sales Amount",
    "dataType": "decimal",
    "sourceColumn": "SalesAmount",
    "formatString": "\\$#,0.00;(\\$#,0.00);\\$#,0.00",
    "sourceProviderType": "Currency",
    "encodingHint": "Value"
}
```

## <a name="ragged-hierarchies"></a>Hierarquias desbalanceadas
Em modelos de tabela, você pode modelar hierarquias pai-filho. Hierarquias com um número diferente de níveis costumam ser chamadas de hierarquias desbalanceadas. Por padrão, as hierarquias desbalanceadas são exibidas com espaços em branco para níveis abaixo do filho mais baixo. Este é um exemplo de uma hierarquia desbalanceada em um organograma:

![AS_Ragged_Hierarchy](../analysis-services/media/as-ragged-hierarchy.png)

Essa versão introduz a propriedade **Ocultar Membros** . É possível definir a propriedade **Ocultar Membros** de uma hierarquia como **Ocultar membros em branco**.

![AS_Hide_Blank_Members](../analysis-services/media/as-hide-blank-members.png)

 >[!NOTE]
 > Os membros em branco no modelo são representados por um valor em branco do DAX, não por uma cadeia de caracteres vazia.

Quando é definida como **Ocultar membros em branco**, e o modelo é implantado, uma versão da hierarquia mais fácil de ser lida é mostrada em clientes de relatório como o Excel.

![AS_Non_Ragged_Hierarchy](../analysis-services/media/as-non-ragged-hierarchy.png)


## <a name="detail-rows"></a>Linhas de Detalhes
Agora é possível definir um conjunto de linhas personalizadas que contribui com um valor de medida. Linhas de Detalhes são semelhantes à ação de detalhamento padrão em modelos multidimensionais. Isso permite que os usuários finais exibam informações mais detalhadamente do que o nível de agregação. 

A Tabela Dinâmica a seguir mostra o Total de Vendas pela Internet por ano com base no modelo de tabela de exemplo do Adventure Works. Clique com o botão direito do mouse em uma célula com um valor de agregação na medida e clique em **Mostrar Detalhes** para exibir as linhas de detalhes.

![AS_Show_Details](../analysis-services/media/as-show-details.png)

Por padrão, os dados associados na tabela Vendas pela Internet são exibidos. Normalmente, esse comportamento limitado não é significativo para o usuário, pois a tabela poderá não ter as colunas necessárias para mostrar informações úteis, como nome do cliente e informações de pedido. Com as Linhas de Detalhes, você poderá especificar uma propriedade **Expressão de Linhas de Detalhes** para medidas.

#### <a name="detail-rows-expression-property-for-measures"></a>Propriedade Expressão de Linhas de Detalhes para medidas
A propriedade **Expressão de Linhas de Detalhes** para medidas permite que os autores do modelo personalizem as colunas e as linhas retornadas ao usuário final.

![AS_Detail_Rows_Expression_Property](../analysis-services/media/as-detail-rows-expression-property.png)

A função DAX [SELECTCOLUMNS](https://msdn.microsoft.com/library/mt761759.aspx) será normalmente usada em uma Expressão de Linhas de Detalhes. O seguinte exemplo define as colunas a serem retornadas para as linhas na tabela Vendas pela Internet no modelo de tabela de exemplo do Adventure Works:

```
SELECTCOLUMNS(
    'Internet Sales',
    "Customer First Name", RELATED( Customer[Last Name]),
    "Customer Last Name", RELATED( Customer[First Name]),
    "Order Date", 'Internet Sales'[Order Date],
    "Internet Total Sales", [Internet Total Sales]
)
```

Com a propriedade definida e o modelo implantado, um conjunto de linhas personalizadas é retornado quando o usuário seleciona **Mostrar Detalhes**. Ele respeita automaticamente o contexto de filtro da célula selecionada. Neste exemplo, somente as linhas do valor 2010 são exibidas:

![AS_Detail_Rows](../analysis-services/media/as-detail-rows.png)

#### <a name="default-detail-rows-expression-property-for-tables"></a>Propriedade Expressão de Linhas de Detalhes Padrão para tabelas
Além de medidas, as tabelas também têm uma propriedade para definir uma expressão de linhas de detalhes. A propriedade **Expressão de Linhas de Detalhes Padrão** atua como o padrão para todas as medidas na tabela. Medidas que não têm sua própria expressão definida herdarão a expressão da tabela e mostrarão o conjunto de linhas definido para a tabela. Isso permite a reutilização de expressões, e novas medidas adicionadas à tabela mais tarde herdarão a expressão automaticamente.

![AS_Default_Detail_Rows_Expression](../analysis-services/media/as-default-detail-rows-expression.png)
 
#### <a name="detailrows-dax-function"></a>Função DETAILROWS DAX
Uma nova função DAX `DETAILROWS` que retorna o conjunto de linhas definido pela expressão de linhas de detalhes é incluída nessa versão. Ela funciona da mesma forma que a instrução `DRILLTHROUGH` no MDX, que também é compatível com as expressões de linhas de detalhes definidas em modelos de tabela.

A consulta DAX a seguir retorna o conjunto de linhas definido pela expressão de linhas de detalhes para a medida ou tabela. Se nenhuma expressão for definida, os dados da tabela Vendas pela Internet serão retornados, pois eles são a tabela que contém a medida.

```
EVALUATE DETAILROWS([Internet Total Sales])
```

## <a name="object-level-security"></a>Segurança em nível de objeto
Esta versão apresenta [segurança em nível de objeto](../analysis-services/tabular-models/object-level-security.md) para tabelas e colunas. Além de restringir o acesso a dados de tabela e coluna, nomes de tabela e coluna confidenciais podem ser protegidos. Isso ajuda a impedir que um usuário mal-intencionado descubra uma tabela desse tipo.

Segurança em nível de objeto deve ser definida usando a metadados com base em JSON, a linguagem de script de modelo Tabular (TMSL) ou o modelo de objeto de tabela (TOM). 

Por exemplo, o código a seguir ajuda a proteger a tabela Produtos no modelo de tabela de exemplo Adventure Works, definindo a propriedade **MetadataPermission** da classe **TablePermission** como **Nenhum**.

```
//Find the Users role in Adventure Works and secure the Product table
ModelRole role = db.Model.Roles.Find("Users");
Table productTable = db.Model.Tables.Find("Product");
if (role != null && productTable != null)
{
    TablePermission tablePermission;
    if (role.TablePermissions.Contains(productTable.Name))
    {
        tablePermission = role.TablePermissions[productTable.Name];
    }
    else
    {
        tablePermission = new TablePermission();
        role.TablePermissions.Add(tablePermission);
        tablePermission.Table = productTable;
    }
    tablePermission.MetadataPermission = MetadataPermission.None;
}
db.Update(UpdateOptions.ExpandFull);
```

## <a name="dynamic-management-views-dmvs"></a>DMVs (exibições de gerenciamento dinâmico)
[DMVs](../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md) são consultas que retornam informações sobre operações do servidor local e a integridade do servidor no SQL Server Profiler.
Esta versão inclui aperfeiçoamentos para [exibições de gerenciamento dinâmico](https://docs.microsoft.com/sql/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services) (DMV) para modelos de tabela nos níveis de compatibilidade 1200 e 1400.

[DISCOVER_CALC_DEPENDENCY](../analysis-services/schema-rowsets/xml/discover-calc-dependency-rowset.md) agora funciona com modelos de tabela 1200 e 1400. Modelos de tabela 1400 mostram as dependências entre partições M, M expressões e fontes de dados estruturados. Para obter mais informações, consulte o [blog do Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2017/07/17/whats-new-in-sql-server-2017-rc1-for-analysis-services/).

[MDSCHEMA_MEASUREGROUP_DIMENSIONS](../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroup-dimensions-rowset.md) melhorias foram incluídas para esse DMV, que é usada por várias ferramentas de cliente para mostrar a dimensionalidade de medida. Por exemplo, o recurso de explorar em tabelas dinâmicas do Excel permite que o usuário entre-análise de dimensões relacionadas para as medidas selecionadas. Esta versão corrige as colunas de cardinalidade, que anteriormente eram mostrando valores incorretos.

## <a name="dax-enhancements"></a>Melhorias do DAX
Esta versão inclui suporte para novas funções de DAX e funcionalidade. Para tirar proveito, você precisa usar a versão mais recente do SSDT. Para obter mais informações, consulte [funções DAX novas](https://msdn.microsoft.com/library/mt704075.aspx).

Uma das partes mais importantes da nova funcionalidade DAX é a nova [operador IN / função CONTAINSROW](https://msdn.microsoft.com/library/mt842621.aspx) para expressões DAX. Isso é semelhante ao operador [`TSQL IN`](https://msdn.microsoft.com/library/ms177682.aspx) geralmente usado para especificar vários valores em uma cláusula `WHERE` .

Anteriormente, era comum especificar filtros de vários valores usando o operador lógico `OR` , como na seguinte expressão de medida:

```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
                 'Product'[Color] = "Red"
            || 'Product'[Color] = "Blue"
            || 'Product'[Color] = "Black"
    )
```

Isso é simplificado com o operador `IN` :
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales], 'Product'[Color] IN { "Red", "Blue", "Black" }
    )
```

Nesse caso, o operador `IN` se refere a uma tabela de coluna única com três linhas: uma para cada uma das cores especificadas. Observe que a sintaxe do construtor de tabela usa chaves.

O operador `IN` é funcionalmente equivalente à função `CONTAINSROW` :
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales], CONTAINSROW({ "Red", "Blue", "Black" }, 'Product'[Color])
    )
```

O operador `IN` também pode ser usado de modo efetivo com construtores de tabela. Por exemplo, a seguinte medida filtra por combinações de cores e categorias do produto:
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
        FILTER( ALL('Product'),
              ( 'Product'[Color] = "Red"   && Product[Product Category Name] = "Accessories" )
         || ( 'Product'[Color] = "Blue"  && Product[Product Category Name] = "Bikes" )
         || ( 'Product'[Color] = "Black" && Product[Product Category Name] = "Clothing" )
        )
    )
```

Usando o novo operador `IN` , a expressão de medida acima agora é equivalente à mostrada abaixo:
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
        FILTER( ALL('Product'),
            ('Product'[Color], Product[Product Category Name]) IN
            { ( "Red", "Accessories" ), ( "Blue", "Bikes" ), ( "Black", "Clothing" ) }
        )
    )
```

## <a name="additional-improvements"></a>Melhorias adicionais
Além de todos os novos recursos, Analysis Services, o SSDT e SSMS também incluem os seguintes aprimoramentos:

* Reutilização de hierarquia e de coluna são apresentados em locais mais úteis na lista de campos do Power BI.
* Relações de data para facilmente criar relações com as dimensões de data com base em campos de data.
* Opção de instalação padrão para o Analysis Services agora é para o modo tabular.
* Novas fontes de dados de obter dados (Power Qery).
* Editor DAX do SSDT.
* Suportam a fontes de dados DirectQuery existentes para milhão de consultas.
* Aprimoramentos do SSMS, como exibir, editar e scripts de suporte para fontes de dados estruturados.



## <a name="see-also"></a>Consulte também
[Notas de versão do SQL Server de 2017](../sql-server/sql-server-2017-release-notes.md)   
[Novidades no SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)


---
title: O que &#39; s novos no SQL Server de 2017 Analysis Services | Microsoft Docs
ms.custom: 
ms.date: 07/27/2017
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
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 572af6f86f015c88141bb6e78b781b5825be155c
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="what39s-new-in-sql-server-2017-analysis-services"></a>O que &#39; s novos no SQL Server de 2017 Analysis Services
[!INCLUDE[tsql-appliesto-ssvNxt-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]


## <a name="sql-server-2017-analysis-services-rc2"></a>Serviços de análise do SQL Server de 2017 RC2
Não há recursos novos nesta versão. Melhorias nesta versão incluem correções de bugs e desempenho.

## <a name="sql-server-2017-analysis-services-rc1"></a>Serviços de análise do SQL Server de 2017 RC1
Não há novos recursos nesta versão, no entanto, esta versão inclui aprimoramentos adicionais para [exibições de gerenciamento dinâmico](https://docs.microsoft.com/sql/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services) (DMV) para modelos de tabela nos níveis de compatibilidade 1200 e 1400.

DISCOVER_CALC_DEPENDENCY agora funciona com modelos de tabela 1200 e 1400. Modelos de tabela 1400 mostram as dependências entre partições M, M expressões e fontes de dados estruturados. Para obter mais informações, consulte o [blog do Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/).

Melhorias de MDSCHEMA_MEASUREGROUP_DIMENSIONS são incluídas para esse DMV, que é usada por várias ferramentas de cliente para mostrar a dimensionalidade de medida. Por exemplo, o recurso de explorar em tabelas dinâmicas do Excel permite que o usuário entre-análise de dimensões relacionadas para as medidas selecionadas. Esta versão corrige as colunas de cardinalidade, que anteriormente eram mostrando valores incorretos.

## <a name="sql-server-analysis-services-ctp-21"></a>SQL Server Analysis Services CTP 2.1
Não há recursos novos nesta versão. Aperfeiçoamentos nesta versão incluem correções de bugs e desempenho e melhorias para [exibições de gerenciamento dinâmico](https://docs.microsoft.com/sql/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services) (DMV). DMVs são consultas que retornam informações sobre operações do servidor local e a integridade do servidor no SQL Server Profiler. Para obter mais detalhes, consulte o [blog do Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/).

## <a name="sql-server-analysis-services-ctp-20"></a>SQL Server Analysis Services CTP 2.0
Esta versão contém vários aprimoramentos novos para o modelo de tabela, incluindo:

* Segurança do nível de objeto para proteger os metadados dos modelos de tabela.
* Melhorias de desempenho de transação para uma experiência de desenvolvedor mais ágil na resposta.
* Aprimoramentos de exibição de gerenciamento dinâmicos para modelos 1200 e 1400 habilitar análise de dependência e emissão de relatórios.
* Melhorias para a experiência de criação para expressões de linhas de detalhes.
* Hierarquia e a coluna ser reutilizado para ser apresentados em locais mais úteis na lista de campos do Power BI.
* Relações de data para facilmente criar relações com as dimensões de data com base em campos de data.
* Opção de instalação padrão para o Analysis Services agora é para o modo tabular.
* Novas fontes de dados de obter dados (Power Qery).
* Editor DAX do SSDT.
* Suportam a fontes de dados DirectQuery existentes para milhão de consultas.
* Aprimoramentos do SSMS, como exibir, editar e scripts de suporte para fontes de dados estruturados.

Para obter mais detalhes sobre essa versão CTP 2.0, consulte o [blog do Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/).

## <a name="sql-server-analysis-services-on-windows-ctp-14"></a>SQL Server Analysis Services no Windows CTP 1.4
[SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/sql-server-data-tools-ssdt-release-candidate) e [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms-release-candidate) versões de visualização coincidirem com as versões de visualização de 2017 do SQL Server. Certifique-se de usar a versão mais recente para obter novos recursos. Para obter mais informações, consulte o [blog do Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/).



## <a name="sql-server-analysis-services-on-windows-ctp-13"></a>SQL Server Analysis Services no Windows CTP 1.3

### <a name="encoding-hints"></a>Dicas de codificação

Esta versão apresenta dicas de codificação, um recurso avançado, usado para otimizar o processamento (atualização de dados) grandes de memória de modelos de tabela. Para entender melhor codificação, consulte [desempenho de ajuste de modelos de tabela no SQL Server 2012 Analysis Services](https://msdn.microsoft.com/library/dn393915.aspx) white paper para entender melhor a codificação. O processo de codificação descrito aqui se aplica no CTP 1.3.

* Codificação de valor fornece melhor desempenho de consulta para colunas que normalmente são usados somente para agregações.

* Codificação de hash é preferível Agrupar por colunas (geralmente valores de tabela de dimensões) e chaves estrangeiras. Colunas de cadeia de caracteres sempre são codificado de hash.

Colunas numéricas podem usar qualquer um desses métodos de codificação. Quando o Analysis Services inicia o processamento de uma tabela, se a tabela estiver vazia (com ou sem partições) ou uma operação de processamento de tabela completa está sendo executada, os valores de exemplos são obtidos para cada coluna numérica determinar se deve aplicar o valor ou codificação de hash . Por padrão, o valor de codificação é escolhido quando o exemplo de valores distintos na coluna é grande o suficiente, caso contrário, a codificação de hash geralmente fornece melhor compactação. É possível para o Analysis Services alterar o método de codificação depois que a coluna é parcialmente processada com base em obter mais informações sobre a distribuição de dados e reiniciar o processo de codificação. Obviamente, isso aumenta o tempo de processamento e é ineficiente. Ajuste de desempenho white paper aborda a codificação novamente em mais detalhes e descreve como detectá-lo usando o SQL Server Profiler.

Dicas de codificação no CTP 1.3 permitem Modelador especificar uma preferência para o método de codificação que recebe o conhecimento prévio de criação de perfil de dados e/ou em resposta a codificação novamente os eventos de rastreamento. Desde que a agregação em colunas codificado de hash é mais lenta do que o valor codificado colunas, o valor de codificação pode ser especificado como uma dica para essas colunas. Não há garantia de que a preferência será aplicada; Portanto, é uma dica em vez de uma configuração. Para especificar uma dica de codificação, defina a propriedade EncodingHint na coluna. Os valores possíveis são "Padrão", "Valor" e "Hash". No momento da gravação, a propriedade não é exposta ainda no SSDT, portanto, deve ser definida usando a metadados com base em JSON, a linguagem de script de modelo Tabular (TMSL) ou o modelo de objeto de tabela (TOM). O trecho a seguir de metadados com base em JSON do arquivo Model.bim Especifica o valor de codificação para a coluna valor das vendas.

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

### <a name="extended-events-not-working-in-ctp-13"></a>Não está funcionando no CTP 1.3 de eventos estendidos
Eventos estendidos do SSAS não funcionam no CTP 1.3. Uma correção está planejada para o próximo CTP.

## <a name="sql-server-analysis-services-on-windows-ctp-12"></a>SQL Server Analysis Services no Windows CTP 1.2

Não há recursos novos nesta versão. As melhorias incluem correções de bug e desempenho.

A versão de visualização mais recente do SQL Server dados Tools (SSDT), que coincide com o SQL Server de 2017 CTP 1.2, aprimora a nova experiência moderna obter dados introduzida no CTP 1.1 com o novo menu do editor de consulta e a funcionalidade de acesso rápido. 

## <a name="sql-server-analysis-services-on-windows-ctp-11"></a>SQL Server Analysis Services no Windows CTP 1.1 

Esta versão introduz melhorias para modelos de tabela. 

### <a name="1400-compatibility-level-for-tabular-models"></a>Nível de Compatibilidade&1400; para modelos de tabela
  Para aproveitar os recursos e a funcionalidade descritos neste artigo, os modelos de tabela novos ou existentes devem ser definidos como o nível de compatibilidade 1400. Os modelos no nível de compatibilidade 1400 não podem ser implantados no SQL Server 2016 SP1 ou anterior nem ter o downgrade para níveis de compatibilidade inferiores.
  
  Para criar ou atualizar projetos de modelo de tabela novos ou existentes para o nível de compatibilidade 1400, baixe e instale uma **versão prévia** do [SSDT (SQL Server Data Tools) 17.0 RC2](https://go.microsoft.com/fwlink?LinkId=837939). 
  
No SSDT, é possível selecionar o novo nível de compatibilidade 1400 ao criar novos projetos de modelo de tabela. 

![AS_NewTabular1400Project](../analysis-services/media/as-newtabular1400project.png)

>[!NOTE]
> O espaço de trabalho integrado na versão de dezembro do SSDT (SQL Server Data Tools) dá suporte ao nível de compatibilidade 1400. Se você criar novos projetos de modelo de tabela em uma instância de servidor do Espaço de Trabalho, essa instância ou qualquer instância implantada deverá ser o [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 1.1. 

Para atualizar um modelo tabular existente no SSDT, no Gerenciador de soluções, clique com botão direito **Model.bim**e, em seguida, em **propriedades**, defina o **nível de compatibilidade** propriedade  **SQL Server 2017 (1400)**. 

![AS_Model_Properties](../analysis-services/media/as-model-properties.png)

### <a name="modern-get-data-experience"></a>Experiência moderna do recurso Obter Dados
A última versão prévia do SSDT (SQL Server Data Tools), que coincide com a versão do [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 1.1, apresenta uma experiência moderna do recurso **Obter Dados** para modelos de tabela no nível de compatibilidade 1400. Esse novo recurso se baseia em uma funcionalidade semelhante no Power BI Desktop e Microsoft Excel 2016.

![AS_Get_Data_in_SSDT](../analysis-services/media/as-get-data-in-ssdt.png)

>[!NOTE]
> Para esta versão, há suporte para um número limitado de fontes de dados. As atualizações futuras darão suporte a funcionalidade e fontes de dados adicionais.

Para saber mais sobre a experiência moderna do recurso Obter Dados, confira o [Blog da Equipe do Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2016/12/16/introducing-a-modern-get-data-experience-for-sql-server-2017-on-windows-ctp-1-1-for-analysis-services/).

## <a name="ragged-hierarchies"></a>Hierarquias desbalanceadas
Em modelos de tabela, você pode modelar hierarquias pai-filho. Hierarquias com um número diferente de níveis costumam ser chamadas de hierarquias desbalanceadas. Por padrão, as hierarquias desbalanceadas são exibidas com espaços em branco para níveis abaixo do filho mais baixo. Este é um exemplo de uma hierarquia desbalanceada em um organograma:

![AS_Ragged_Hierarchy](../analysis-services/media/as-ragged-hierarchy.png)

Essa versão introduz a propriedade **Ocultar Membros** . É possível definir a propriedade **Ocultar Membros** de uma hierarquia como **Ocultar membros em branco**.

![AS_Hide_Blank_Members](../analysis-services/media/as-hide-blank-members.png)

 >[!NOTE]
 > Os membros em branco no modelo são representados por um valor em branco do DAX, não por uma cadeia de caracteres vazia.

Quando é definida como **Ocultar membros em branco**, e o modelo é implantado, uma versão da hierarquia mais fácil de ser lida é mostrada em clientes de relatório como o Excel.

![AS_Non_Ragged_Hierarchy](../analysis-services/media/as-non-ragged-hierarchy.png)

### <a name="detail-rows"></a>Linhas de Detalhes
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

## <a name="dax-enhancements"></a>Melhorias do DAX
Esta versão inclui um operador `IN` para expressões DAX. Isso é semelhante ao operador [`TSQL IN`](https://msdn.microsoft.com/library/ms177682.aspx) geralmente usado para especificar vários valores em uma cláusula `WHERE` .

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


## <a name="table-level-security"></a>Segurança em nível de tabela
Esta versão introduz a segurança em nível de tabela. Além de restringir o acesso aos dados de tabela, nomes de tabela confidenciais podem ser protegidos. Isso ajuda a impedir que um usuário mal-intencionado descubra uma tabela desse tipo.

A segurança em nível de tabela deve ser definida usando metadados baseados em JSON, TMSL (Linguagem de Script de Modelo de Tabela) ou TOM (Modelo de Objeto de Tabela). 

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



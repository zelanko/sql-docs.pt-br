---
title: Grupos de cálculo em Analysis Services modelos de tabela | Microsoft Docs
ms.date: 07/24/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: af63f41555a021fc720c7d1e15778265fe7de500
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419529"
---
# <a name="calculation-groups-preview"></a>Grupos de cálculo (visualização)
 
[!INCLUDE[ssas-appliesto-sql2019-aas](../../includes/ssas-appliesto-sql2019-aas.md)]

Os grupos de cálculo podem reduzir significativamente o número de medidas redundantes agrupando expressões de medida comuns como *itens de cálculo*. Os grupos de cálculo têm suporte em modelos de tabela Azure Analysis Services e SQL Server Analysis Services 2019 no [nível de compatibilidade](compatibility-level-for-tabular-models-in-analysis-services.md)1470 e superior. Modelos no nível de compatibilidade 1470 estão em **Visualização**no momento.  

Este artigo descreve: 

> [!div class="checklist"]
> * Benefícios 
> * Como funcionam os grupos de cálculo
> * Cadeias de caracteres de formato dinâmico
> * Ordenação
> * Precedência
> * Ferramentas
> * Limitações



## <a name="benefits"></a>Benefícios

Os grupos de cálculo abordam um problema em modelos complexos em que pode haver uma proliferação de medidas redundantes usando os mesmos cálculos – mais comuns com cálculos de inteligência de tempo. Por exemplo, um analista de vendas deseja exibir os totais de vendas e os pedidos por mês-até-data (MTD), trimestre acumulado (QTD.), ano até a data, pedidos desde o ano anterior (PY) e assim por diante. O modelador de dados precisa criar medidas separadas para cada cálculo, o que pode levar a dezenas de medidas. Para o usuário, isso pode significar ter que classificar apenas quantas medidas e aplicá-las individualmente ao relatório. 

Vamos primeiro dar uma olhada em como os grupos de cálculo aparecem para os usuários em uma ferramenta de relatório como Power BI. Em seguida, vamos dar uma olhada no que compõe um grupo de cálculo e como eles são criados em um modelo.

Grupos de cálculos são mostrados em clientes de relatório como uma tabela com uma única coluna. A coluna não é como uma coluna ou dimensão típica, mas representa um ou mais cálculos reutilizáveis ou *itens de cálculo* que podem ser aplicados a qualquer medida já adicionada ao filtro de valores para uma visualização.

Na animação a seguir, um usuário está analisando dados de vendas por anos 2012 e 2013. Antes de aplicar um grupo de cálculo, as **vendas** da medida de base comum calculam uma soma do total de vendas para cada mês. Em seguida, o usuário deseja aplicar cálculos de inteligência de tempo para obter os totais de vendas do mês até a data, trimestre até a data, desde o início do ano e assim por diante. Sem grupos de cálculo, o usuário teria que selecionar medidas individuais de inteligência de tempo.

Com um grupo de cálculo, neste exemplo denominado **inteligência de tempo**, quando o usuário arrasta o item de **cálculo de tempo** para a área de filtro de **colunas** , cada item de cálculo aparece como uma coluna separada. Os valores para cada linha são calculados a partir da medida base, **vendas**.  

![Grupo de cálculo sendo aplicado no Power BI](media/calculation-groups/calc-groups-pbi.gif)


Grupos de cálculo funcionam  com medidas Dax explícitas. Neste exemplo, **Sales** é uma medida explícita já criada no modelo. Os grupos de cálculo não funcionam com medidas DAX implícitas. Por exemplo, em Power BI medidas implícitas são criadas quando um usuário arrasta colunas para visuais para exibir valores agregados, sem criar uma medida explícita. Neste momento, Power BI gera DAX para medidas implícitas escritas como cálculos DAX embutidos, o que significa que as medidas implícitas não funcionam com grupos de cálculo. Uma nova propriedade de modelo visível no modelo de objeto de tabela (TOM) foi introduzida, **DiscourageImplicitMeasures**. No momento, para criar grupos de cálculo, essa propriedade deve ser definida como **true**. Quando definido como true, Power BI Desktop no modo Live Connect desabilita a criação de medidas implícitas.

## <a name="how-they-work"></a>Como funcionam

Agora que você viu como os grupos de cálculo beneficiam os usuários, vamos dar uma olhada em como o exemplo de grupo de cálculo de inteligência de tempo mostrado é criado.

Antes de entrarmos nos detalhes, vamos introduzir algumas novas funções DAX especificamente para grupos de cálculo: 

[SELECTEDMEASURE](https://docs.microsoft.com/dax/selectedmeasure-function-dax) – usado por expressões para itens de cálculo para referenciar a medida que está atualmente no contexto. Neste exemplo, a medida Sales.

[SELECTEDMEASURENAME](https://docs.microsoft.com/dax/selectedmeasurename-function-dax) – usado por expressões para itens de cálculo para determinar a medida que está no contexto por nome.

[ISSELECTEDMEASURE](https://docs.microsoft.com/dax/isselectedmeasure-function-dax) – usado por expressões para itens de cálculo para determinar a medida que está no contexto é especificada em uma lista de medidas.

[SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasureformatstring-function-dax) – usado por expressões para itens de cálculo para recuperar a cadeia de caracteres de formato da medida que está no contexto.

### <a name="time-intelligence-example"></a>Exemplo de inteligência de tempo

Nome da tabela- **inteligência de tempo**   
Nome da coluna- **cálculo de tempo**   
Precedência- **20**   

#### <a name="time-intelligence-calculation-items"></a>Itens de cálculo de inteligência de tempo

**Current**

```dax
SELECTEDMEASURE()
```

**MTD**

```dax
CALCULATE(SELECTEDMEASURE(), DATESMTD(DimDate[Date]))
```

**QTD**

```dax
CALCULATE(SELECTEDMEASURE(), DATESQTD(DimDate[Date]))
```

**YTD**

```dax
CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date]))
```

**AJ**

```dax
CALCULATE(SELECTEDMEASURE(), SAMEPERIODLASTYEAR(DimDate[Date]))
```

**PY MTD**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "MTD"
)
```

**QTD. DO PY**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "QTD"
)
```

**AJ POR ANO**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "YTD"
)
```

**YOY**

```dax
SELECTEDMEASURE() –
CALCULATE(
    SELECTEDMEASURE(),
    'Time Intelligence'[Time Calculation] = "PY"
)
```

**YOY**

```dax
DIVIDE(
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="YOY"
    ),
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="PY"
    ),
)
```

Para testar esse grupo de cálculo, você pode executar uma consulta DAX no SSMS ou no [Dax Studio](http://daxstudio.org/)de código aberto. YOY e YOY% são omitidos deste exemplo de consulta.

#### <a name="time-intelligence-query"></a>Consulta de inteligência de tempo

```dax
EVALUATE
CALCULATETABLE (
    SUMMARIZECOLUMNS (
        DimDate[CalendarYear],
        DimDate[EnglishMonthName],
        "Current", CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "Current" ),
        "QTD",     CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "QTD" ),
        "YTD",     CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "YTD" ),
        "PY",      CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "PY" ),
        "PY QTD",  CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "PY QTD" ),
        "PY YTD",  CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "PY YTD" )
    ),
    DimDate[CalendarYear] IN { 2012, 2013 }
)
```

#### <a name="time-intelligence-query-return"></a>Retorno de consulta de inteligência de tempo

A tabela de retorno mostra os cálculos para cada item de cálculo aplicado. Por exemplo, você pode ver QTD para março de 2012 é a soma de Janeiro, fevereiro e 2012 de março.

![Retorno de consulta](media/calculation-groups/calc-groups-query-return.png)


## <a name="dynamic-format-strings"></a>Cadeias de caracteres de formato dinâmico

*Cadeias de formato dinâmico* com grupos de cálculo permitem a aplicação condicional de cadeias de caracteres de formato a medidas sem forçá-las a retornar cadeias de caracteres

Os modelos de tabela dão suporte à formatação dinâmica de medidas usando a função de [formato](https://docs.microsoft.com/dax/format-function-dax) Dax. No entanto, a função FORMAT tem a desvantagem de retornar uma cadeia de caracteres, forçando medidas que, de outra forma, seriam numéricas também para serem retornadas como uma cadeia de caracteres. Isso pode ter algumas limitações, como não trabalhar com a maioria dos Power BI visuais, dependendo dos valores numéricos, como gráficos.

### <a name="dynamic-format-strings-for-time-intelligence"></a>Cadeias de caracteres de formato dinâmico para inteligência de tempo

Se observarmos o exemplo de inteligência de tempo mostrado acima, todos os itens de cálculo, exceto **yoy%** , devem usar o formato da medida atual no contexto. Por exemplo,  calculado acumulado na medida de base de vendas deve ser moeda. Se esse fosse um grupo de cálculo para algo como uma medida base de pedidos, o formato seria numérico. **Yoy%** , no entanto, deve ser uma porcentagem, independentemente do formato da medida base.

Para **yoy%** , podemos substituir a cadeia de caracteres de formato definindo a propriedade Format String Expression como **0,00%;-0,00%; 0,00%** . Para saber mais sobre propriedades de expressão de cadeia de caracteres de formato, consulte [Propriedades da célula MDX – conteúdo da cadeia de caracteres de formato](../multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md#numeric-values).

Neste visual de matriz no Power BI, você vê **Sales Current/yoy** e **Orders Current/yoy** retêm suas respectivas cadeias de caracteres de formato de medida base. **Sales yoy%** e **Orders yoy%** , no entanto, substitui a cadeia de caracteres de formato para usar o formato de *porcentagem* .

![Inteligência de tempo no Visual de matriz](media/calculation-groups/calc-groups-dynamicstring-timeintel.png)

### <a name="dynamic-format-strings-for-currency-conversion"></a>Cadeias de caracteres de formato dinâmico para conversão de moeda

Cadeias de caracteres de formato dinâmico fornecem uma conversão de moeda fácil. Considere o modelo de dados do Adventure Works a seguir. Ele é modelado para conversão de moeda de *um para muitos* , conforme definido por [tipos de conversão](../currency-conversions-analysis-services.md#conversion-types).

![Taxa de moeda no modelo de tabela](media/calculation-groups/calc-groups-currency-conversion.png)

Uma coluna **FormatString** é adicionada à tabela **DimCurrency** e preenchida com cadeias de caracteres de formato para as respectivas moedas.

![Coluna de cadeia de caracteres de formato](media/calculation-groups/calc-groups-formatstringcolumn.png)

Neste exemplo, o seguinte grupo de cálculo é definido como:

### <a name="currency-conversion-example"></a>Exemplo de conversão de moeda

Nome da tabela- **conversão de moeda**   
Nome da coluna – **cálculo de conversão**   
Precedência- **5**   

#### <a name="calculation-items-for-currency-conversion"></a>Itens de cálculo para conversão de moeda

**Sem conversão**

```dax
SELECTEDMEASURE()
```

**Moeda convertida**

```dax
IF(
    //Check one currency in context & not US Dollar, which is the pivot currency:
    SELECTEDVALUE( DimCurrency[CurrencyName], "US Dollar" ) = "US Dollar",
    SELECTEDMEASURE(),
    SUMX(
        VALUES(DimDate[Date]),
        CALCULATE( DIVIDE( SELECTEDMEASURE(), MAX(FactCurrencyRate[EndOfDayRate]) ) )
    )
)
```

Expressão de cadeia de caracteres de formato

```dax
SELECTEDVALUE(
    DimCurrency[FormatString],
    SELECTEDMEASUREFORMATSTRING()
)
```
A expressão de cadeia de caracteres de formato deve retornar uma cadeia de caracteres escalar. Ele usa a nova função [SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasureformatstring-function-dax) para reverter para a cadeia de caracteres de formato de medida base se houver várias moedas no contexto de filtro.

A animação a seguir mostra a conversão de moeda de formato dinâmico da medida **vendas** em um relatório.

![Cadeia de caracteres de formato dinâmico de conversão de moeda aplicada](media/calculation-groups/calc-groups-dynamic-format-string.gif)

## <a name="precedence"></a>Precedência

Precedência é uma propriedade definida para um grupo de cálculo. Especifica a ordem de avaliação quando há mais de um grupo de cálculo. Um número mais alto indica maior precedência, o que significa que ele será avaliado antes dos grupos de cálculo com precedência mais baixa.

Para este exemplo, usaremos o mesmo modelo que o exemplo de inteligência de tempo acima, mas também adicionamos  um grupo de cálculo de médias. O grupo de cálculo de médias contém cálculos médios que são independentes da inteligência de tempo tradicional, pois eles não alteram o contexto de filtro de data. eles simplesmente aplicam cálculos médios dentro dele.

Neste exemplo, um cálculo de média diária é definido. Cálculos como a média de cilindros de óleo por dia são comuns em aplicativos de petróleo e gás. Outros exemplos de negócios comuns incluem média de vendas da loja no varejo.

Embora esses cálculos sejam calculados independentemente dos cálculos de inteligência de tempo, pode haver um requisito para combiná-los. Por exemplo, um usuário pode querer ver cilindros de óleo por dia até exibir a taxa diária de óleo desde o início do ano até a data atual. Nesse cenário, a precedência deve ser definida para itens de cálculo.

### <a name="averages-example"></a>Exemplo de médias

O nome da tabela é a **média**.   
O nome da coluna é **cálculo médio**.   
A precedência é **10**.   

#### <a name="calculation-items-for-averages"></a>Itens de cálculo para médias

**Sem média**

```dax
SELECTEDMEASURE()
```

**Média diária**

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

Aqui está um exemplo de uma consulta DAX e a tabela de retorno:

#### <a name="averages-query"></a>Consulta de médias

```dax
EVALUATE
    CALCULATETABLE (
        SUMMARIZECOLUMNS (
        DimDate[CalendarYear],
        DimDate[EnglishMonthName],
        "Sales", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "Current",
            'Averages'[Average Calculation] = "No Average"
        ),
        "YTD", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "YTD",
            'Averages'[Average Calculation] = "No Average"
        ),
        "Daily Average", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "Current",
            'Averages'[Average Calculation] = "Daily Average"
        ),
        "YTD Daily Average", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "YTD",
            'Averages'[Average Calculation] = "Daily Average"
        )
    ),
    DimDate[CalendarYear] = 2012
)
```

#### <a name="averages-query-return"></a>Retorno de consulta de médias

![Retorno de consulta](media/calculation-groups/calc-groups-ytd-daily-avg.png)

A tabela a seguir mostra como os valores de março de 2012 são calculados.


|Nome da coluna  |Cálculo |
|---------|---------|
|YTD     |    Soma de vendas para Jan, Fev, mar 2012<br />= 495.364 + 506.994 + 373.483     |
|Média diária    |     Vendas para mar 2012 divididas por n º de dias em março<br />= 373.483/31       |
|Média diária acumulada no ano     | No ano para mar 2012 dividido por n º de dias em Jan, fev e mar<br />= 1.375.841/(31 + 29 + 31)       |

Aqui está a definição do item de cálculo do ano, aplicada com a precedência de **20**.

```dax
CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date]))
```

Aqui está a média diária, aplicada com uma precedência de **10**.

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

Como a precedência do grupo de cálculo de inteligência de tempo é maior do que a do grupo de cálculo de médias, ela é aplicada o mais amplamente possível. O cálculo da média diária no ano se aplica ao ano até o numerador e o denominador (contagem de dias) do cálculo da média diária.

Isso é equivalente à seguinte expressão:

```dax
CALCULATE(DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate)), DATESYTD(DimDate[Date]))
```

Não é esta expressão:

```dax
DIVIDE(CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date])), COUNTROWS(DimDate)))
```

## <a name="sideways-recursion"></a>Recursão lateral

No exemplo de inteligência de tempo acima, alguns dos itens de cálculo referem-se a outros no mesmo grupo de cálculo. Isso é chamado de *recursão lateral*. Por exemplo, **yoy%** faz referência a **yoy** e **py**.

```dax
DIVIDE(
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="YOY"
    ),
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="PY"
    ),
)
```

Nesse caso, ambas as expressões são avaliadas separadamente porque estão usando diferentes instruções Calculate. Não há suporte para outros tipos de recursão.

## <a name="single-calculation-item-in-filter-context"></a>Item de cálculo único no contexto de filtro

No nosso exemplo de inteligência de tempo, o item de cálculo de **py no ano** tem uma única expressão Calculate:

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "YTD"
)
```

O argumento do ano para a função CALCULATE () substitui o contexto do filtro para reutilizar a lógica já definida no item de cálculo do ano. Não é possível aplicar PY e no ano em uma única avaliação. Os grupos de cálculo são *aplicados somente* se um único item de cálculo do grupo de cálculo estiver no contexto de filtro.

## <a name="mdx-support"></a>Suporte a MDX

Os grupos de cálculo dão suporte a consultas MDX (multidimensional data Expressions). Isso significa que os usuários do Microsoft Excel, que consultam modelos de dados tabulares usando MDX, podem aproveitar ao máximo os grupos de cálculo em gráficos e tabelas dinâmicas de planilha.

## <a name="tools"></a>Ferramentas

Os grupos de cálculo ainda não têm suporte no SQL Server Data Tools, no Visual Studio com extensões de Analysis Services. No entanto, os grupos de cálculo podem ser criados usando TMSL (linguagem de script de modelo de tabela) ou o [Editor de tabela](https://github.com/otykier/TabularEditor)de código aberto.

## <a name="limitations"></a>Limitações

[Segurança em nível de objeto](object-level-security.md) (OLS) definido em tabelas de grupo de cálculo não tem suporte. No entanto, OLS pode ser definido em outras tabelas no mesmo modelo. Se um item de cálculo se referir a um objeto OLS protegido, um erro genérico será retornado.

[Segurança em nível de linha](roles-ssas-tabular.md#bkmk_rowfliters) (RLS) não é suportado. Você pode definir a RLS em tabelas no mesmo modelo, mas não nos próprios grupos de cálculo (direta ou indiretamente).

## <a name="see-also"></a>Confira também  

[DAX em modelos de tabela](understanding-dax-in-tabular-models-ssas-tabular.md)   
[Referência DAX](https://docs.microsoft.com/dax/data-analysis-expressions-dax-reference)  

---
title: Grupos de cálculos em modelos de tabela do Analysis Services | Microsoft Docs
ms.date: 06/09/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: abc1f51d21613676fd94271f931e1a7692cc1efc
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822696"
---
# <a name="calculation-groups-preview"></a>Grupos de cálculo (visualização)
 
[!INCLUDE[ssas-appliesto-sql2019-aas](../../includes/ssas-appliesto-sql2019-aas.md)]

Grupos de cálculo podem reduzir significativamente o número de medidas com redundância de expressões de medida comum como de agrupamento *itens de cálculo*. Grupos de cálculo têm suporte no Azure Analysis Services e SQL Server Analysis Services 2019 tabulares de modelos no 1470 e acima [nível de compatibilidade](compatibility-level-for-tabular-models-in-analysis-services.md). Modelos de nível de compatibilidade 1470 estão atualmente em **visualização**.  

Este artigo descreve: 

> [!div class="checklist"]
> * Benefícios 
> * Como funcionam os grupos de cálculo
> * Cadeias de caracteres de formato dinâmico
> * Precedência
> * Ferramentas
> * Limitações



## <a name="benefits"></a>Benefícios

Grupos de cálculo de resolver um problema em modelos complexos, onde pode haver uma proliferação de medidas redundantes usando os mesmos cálculos - mais comuns com cálculos de inteligência de tempo. Por exemplo, um analista de vendas quer exibir totais de vendas e pedidos por month-to-date (MTD) quarter-to-date (QTD), year-to-date (acumulado no ano), ordena year-to-date para o ano anterior (Aj) e assim por diante. O Modelador de dados tem que criar medidas separadas para cada cálculo, que pode levar a dezenas de medidas. Para o usuário, isso pode significar que com a classificação de tantos apenas medidas e aplicá-los individualmente aos seus relatórios. 

Vamos primeiro dar uma olhada em como os grupos de cálculo aparecem para os usuários em uma ferramenta de relatório como o Power BI. Em seguida, vamos dar uma olhada em como o que compõe um grupo de cálculo e como eles são criados em um modelo.

Grupos de cálculos são mostrados em clientes de relatório como uma tabela com uma única coluna. A coluna não é como uma coluna típica ou dimensão, em vez disso, ele representa um ou mais cálculos reutilizáveis, ou *itens de cálculo* que podem ser aplicadas a qualquer medida já adicionada ao filtro de valores para uma visualização.

Na animação a seguir, um usuário está analisando dados de vendas por anos, 2012 e 2013. Antes de aplicar um grupo de cálculo, a medida de base comum **vendas** calcula uma soma do total de vendas para cada mês. O usuário deseja, em seguida, aplicar cálculos de inteligência de tempo para obter totais de vendas para o mês, trimestre até a data, ano e assim por diante. Sem grupos de cálculo, o usuário precisa selecionar medidas de inteligência de tempo individuais.

Com um grupo de cálculo, neste exemplo denominado **inteligência de tempo**, quando o usuário arrasta o **cálculo do tempo** item para o **colunas** área, cada item de cálculo de filtro é exibida como uma coluna separada. Valores para cada linha são calculados a partir a medida base, **vendas**.  

![Grupo de cálculo que está sendo aplicado no Power BI](media/calculation-groups/calc-groups-pbi.gif)


Funcionam com os grupos de cálculo **explícita** medidas DAX. Neste exemplo, **vendas** é uma medida explícita já criada no modelo. Grupos de cálculo não funcionam com as medidas implícitas DAX. Por exemplo, no Power BI medidas implícitas são criadas quando um usuário arrasta colunas para elementos visuais para exibir valores agregados, sem criar uma medida explícita. Neste momento, o Power BI gera o DAX para medidas implícitas escritas como embutido cálculos de DAX – que significa que as medidas implícitas não podem trabalhar com grupos de cálculo. Uma nova propriedade de modelo visível no objeto de modelo de TOM (Tabular) foi introduzida, **DiscourageImplicitMeasures**. Atualmente, a fim de criar grupos de cálculo essa propriedade deve ser definida como **verdadeira**. Quando definido como true, o Power BI Desktop no Live Connect modo desabilita a criação de medidas implícitas.

## <a name="how-they-work"></a>Como eles funcionam

Agora que você já viu como grupos de cálculo se beneficiar os usuários, vamos dar uma olhada em como o exemplo de grupo de cálculo de inteligência de tempo mostrado é criado.

Antes de entrarmos em detalhes, vamos apresentar algumas novas funções DAX especificamente para grupos de cálculo: 

[SELECTEDMEASURE](https://docs.microsoft.com/dax/selectedmeasure-function-dax) - usado pelas expressões para itens de cálculo referenciar a medida que está atualmente no contexto. Neste exemplo, a medida Sales.

[SELECTEDMEASURENAME](https://docs.microsoft.com/dax/selectedmeasurename-function-dax) - usado pelas expressões para itens de cálculo determinar a medida que está no contexto pelo nome.

[ISSELECTEDMEASURE](https://docs.microsoft.com/dax/isselectedmeasure-function-dax) - usado pelas expressões para itens de cálculo determinar a medida que está no contexto é especificada em uma lista de medidas.

[SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasurefromatstring-function-dax) - usado pelas expressões para itens de cálculo recuperar a cadeia de caracteres de formato da medida que está no contexto.

### <a name="time-intelligence-example"></a>Exemplo de inteligência de tempo

Nome da tabela - **inteligência de tempo**   
Nome da coluna - **cálculo do tempo**   
Precedência - **20**   

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

**PY**

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

**AJ QTD**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "QTD"
)
```

**PY YTD**

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

**YOY%**

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

Para testar esse grupo de cálculo, você pode executar uma consulta DAX no SSMS ou o código-fonte aberto [Studio DAX](http://daxstudio.org/). Ano a ano e YOY % são omitidas deste exemplo de consulta.

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

#### <a name="time-intelligence-query-return"></a>Consulta de inteligência de tempo de retorno

A tabela de retorno mostra cálculos para cada cálculo item aplicado. Por exemplo, você pode ver que Qtd para março de 2012 é a soma de janeiro, fevereiro e março de 2012.

![Retorno de consulta](media/calculation-groups/calc-groups-query-return.png)


## <a name="dynamic-format-strings"></a>Cadeias de caracteres de formato dinâmico

*Cadeias de caracteres de formato dinâmico* com cálculo de grupos permitem que aplicativos condicional de cadeias de caracteres de formato para medidas sem forçá-los para retornar cadeias de caracteres.

Modelos de tabela oferecem suporte à formatação dinâmica de medidas por meio do DAX [formato](https://docs.microsoft.com/dax/format-function-dax) função. No entanto, a função de formato tem a desvantagem de retornar uma cadeia de caracteres, forçando a medidas que podem ser numéricas também sejam retornados como uma cadeia de caracteres. Isso pode ter algumas limitações, como não trabalhar com a maioria dos visuais do Power BI, dependendo dos valores numéricos, como gráficos.

### <a name="dynamic-format-strings-for-time-intelligence"></a>Cadeias de caracteres de formato dinâmico para inteligência de tempo

Se observarmos o exemplo de inteligência de tempo mostrado acima, o cálculo todos os itens, exceto **% de YOY** deve usar o formato da medida atual no contexto. Por exemplo, **YTD** calculado na medida vendas a base deve ser moeda. Se esse fosse um grupo de cálculo para algo como uma medida de base de pedidos, o formato seria numérico. **% De YOY de**, no entanto, deve ser uma porcentagem, independentemente do formato da medida base.

Para **% de YOY**, podemos substituir a cadeia de caracteres de formato, definindo a propriedade de expressão de cadeia de caracteres de formato **0,00%;-0.00%; % 0,00**. Para saber mais sobre as propriedades de expressão de cadeia de caracteres de formato, consulte [propriedades de célula MDX – conteúdo de cadeia de caracteres de formato](../multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md#numeric-values).

Nesta matriz visual no Power BI, você deve ver **vendas atual/YOY** e **pedidos atual/YOY** reter suas cadeias de caracteres de formato respectivo medida base. **% De YOY de venda** e **ordena % de YOY**, no entanto, substitui a cadeia de caracteres de formato para usar *porcentagem* formato.

![Inteligência de tempo no visual de matriz](media/calculation-groups/calc-groups-dynamicstring-timeintel.png)

### <a name="dynamic-format-strings-for-currency-conversion"></a>Cadeias de caracteres de formato dinâmico para conversão de moeda

Cadeias de caracteres de formato dinâmico fornecem conversão de moeda fácil. Considere o seguinte modelo de dados do Adventure Works. Ela é modelada para *um-para-muitos* conversão de moeda, conforme definido pela [tipos de conversão](../currency-conversions-analysis-services.md#conversion-types).

![Taxa de câmbio no modelo de tabela](media/calculation-groups/calc-groups-currency-conversion.png)

Um **FormatString** coluna é adicionada para o **DimCurrency** de tabela e populados com cadeias de caracteres de formato para as respectivas moedas.

![Coluna de cadeia de caracteres de formato](media/calculation-groups/calc-groups-formatstringcolumn.png)

Neste exemplo, o seguinte grupo de cálculo, em seguida, é definido como:

### <a name="currency-conversion-example"></a>Exemplo de conversão de moeda

Nome da tabela - **conversão de moeda**   
Nome da coluna - **cálculo de conversão**   
Precedência - **5**   

#### <a name="calculation-items-for-currency-conversion"></a>Itens de cálculo para conversão de moeda

**Nenhuma conversão**

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
A expressão de cadeia de caracteres de formato deve retornar uma cadeia de caracteres de escalar. Ele usa o novo [SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasurefromatstring-function-dax) função para reverter para a cadeia de caracteres de formato de medida base, se houver várias moedas no contexto de filtro.

A animação a seguir mostra a conversão de moeda de um formato dinâmico a **vendas** medidas em um relatório.

![Cadeia de formato dinâmica de conversão de moeda aplicada](media/calculation-groups/calc-groups-dynamic-format-string.gif)

## <a name="precedence"></a>Precedência

A precedência é uma propriedade definida para um grupo de cálculo. Ele especifica a ordem de avaliação quando há mais de um grupo de cálculo. Um número mais alto indica uma precedência maior, que significa que ele será avaliado antes de grupos de cálculo com menor precedência.

Neste exemplo, vamos usar o mesmo modelo como o exemplo de inteligência de tempo acima, mas também adicionar uma **médias** grupo de cálculo. O grupo de cálculo de médias contém cálculos médios que são independentes da inteligência de tempo tradicional, em que eles não alterarem o contexto de filtro de data - eles apenas aplicarem cálculos médios dentro dele.

Neste exemplo, um cálculo de média diário é definido. Cálculos como barris média de óleo por dia são comuns em aplicativos de petróleo e gás. Outros exemplos de negócios comuns incluem a média de vendas de repositório no varejo.

Enquanto esses cálculos são calculados independentemente dos cálculos de inteligência de tempo, pode haver um requisito para combiná-los. Por exemplo, um usuário pode querer ver barris de petróleo por dia até a presente data para exibir a taxa diária de petróleo desde o início do ano até a data atual. Nesse cenário, a precedência deve ser definida para itens de cálculo.

### <a name="averages-example"></a>Exemplo de médias

Nome da tabela **médias**.   
Nome da coluna é **cálculo de média**.   
A precedência é **10**.   

#### <a name="calculation-items-for-averages"></a>Itens de cálculo para médias

**Não há média**

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

#### <a name="averages-query-return"></a>Consulta de médias retornada

![Retorno de consulta](media/calculation-groups/calc-groups-ytd-daily-avg.png)

A tabela a seguir mostra como os valores de março de 2012 são calculados.


|Nome da coluna  |Cálculo |
|---------|---------|
|YTD     |    Soma das vendas de Jan, Feb, Mar de 2012<br />= 495,364 + 506,994 + 373,483     |
|Média diária    |     Vendas para o Mar dividido pelo número de dias em março de 2012<br />= 373,483 / 31       |
|Média diária da acumulados no ano     | Acumulado no ano para o Mar dividido pelo número de dias em janeiro, fevereiro e março de 2012<br />=  1,375,841 / (31 + 29 + 31)       |

Aqui está a definição do item de cálculo acumulado no ano, aplicada com a precedência dos **20**.

```dax
CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date]))
```

Aqui está o diário médio, aplicada com uma precedência de **10**.

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

Como a precedência do grupo de cálculo de inteligência de tempo é mais alta do que o grupo de cálculo de médias, ela é aplicada como amplamente quanto possível. O cálculo de média diária da acumulados no ano se aplica a acumulado no ano para o numerador e o denominador (contagem de dias) do cálculo de média diário.

Isso é equivalente à expressão a seguir:

```dax
CALCULATE(DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate)), DATESYTD(DimDate[Date]))
```

Não esta expressão:

```dax
DIVIDE(CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date])), COUNTROWS(DimDate)))
```

## <a name="sideways-recursion"></a>Para os lados recursão

O exemplo de inteligência de tempo acima, alguns dos itens de cálculo se referir a outras pessoas no mesmo grupo de cálculo. Isso é chamado *recursão para os lados*. Por exemplo, **% de YOY** faz referência aos **YOY** e **PY**.

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

Nesse caso, ambas as expressões são avaliadas separadamente porque eles estão usando diferentes calcular instruções. Não há suporte para outros tipos de recursão.

## <a name="single-calculation-item-in-filter-context"></a>Item de cálculo única no contexto de filtro

Em nosso exemplo de inteligência de tempo, o **YTD PY** item de cálculo, que tem um único calcular expressão:

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "YTD"
)
```

O argumento da acumulados no ano para a função CALCULATE() substitui o contexto de filtro para reutilizar a lógica já definida no item de cálculo da acumulados no ano. Não é possível aplicar PY e acumulado no ano em uma única avaliação. Os grupos de cálculo são *aplicadas apenas* se um item único de cálculo do grupo de cálculo está no contexto de filtro.

## <a name="mdx-support"></a>Suporte MDX

Grupos de cálculo dão suporte a consultas de dados MDX (Multidimensional Expressions). Isso significa, os usuários do Microsoft Excel, quais modelos de dados tabulares de consulta usando MDX, pode aproveitar ao máximo de grupos de cálculo na planilha de tabelas dinâmicas e gráficos.

## <a name="tools"></a>Ferramentas

Grupos de cálculo ainda não têm suporte no SQL Server Data Tools, Visual Studio com extensões do Analysis Services. No entanto, os grupos de cálculo podem ser criados usando a linguagem de script de modelo Tabular (TMSL) ou de software livre [Editor de tabelas](https://github.com/otykier/TabularEditor).

## <a name="limitations"></a>Limitações

[Segurança em nível de objeto](object-level-security.md) (ferramentas) definidos no cálculo não há suporte para tabelas de grupos. No entanto, as ferramentas podem ser definidas em outras tabelas no mesmo modelo. Se um item de cálculo se refere a um objeto protegido de ferramentas, é retornado um erro genérico.

[Segurança em nível de linha](roles-ssas-tabular.md#bkmk_rowfliters) (RLS) não tem suporte. Você pode definir o RLS em tabelas no mesmo modelo, mas não em grupos de cálculo em si (direta ou indiretamente).

[Expressões de linhas de detalhe](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md) não são compatíveis com grupos de cálculo.

## <a name="see-also"></a>Confira também  

[DAX em modelos de tabela](understanding-dax-in-tabular-models-ssas-tabular.md)   
[Referência de DAX](https://docs.microsoft.com/dax/data-analysis-expressions-dax-reference)  

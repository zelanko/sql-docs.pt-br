---
title: DAX em modelos de tabela | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 00799aeaa59ca6dce27816f4cd4344a75a84b3bf
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/08/2018
---
# <a name="dax-in-tabular-models"></a>DAX em modelos de tabela 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Expressões DAX (Data Analysis) é uma linguagem de fórmula usada para criar cálculos personalizados no Analysis Services, Power BI Desktop e Power Pivot no Excel. As fórmulas DAX incluem funções, operadores e valores para executar cálculos avançados em dados em tabelas e colunas.  
  
 Enquanto o DAX é usado no Analysis Services, Power BI Desktop e Power Pivot no Excel, este tópico se aplica mais aos projetos de modelo de tabela do Analysis Services criados no SQL Server Data Tools (SSDT).  
  
##  <a name="bkmk_DAX"></a> Fórmulas DAX em colunas calculadas, medidas e filtros de linha  
 Para modelos de tabela criados no SSDT, fórmulas DAX são usadas em colunas calculadas, medidas e filtros de linha.  
  
### <a name="calculated-columns"></a>Colunas calculadas  
 Uma coluna calculada é uma coluna que você adiciona a uma tabela existente (no designer de modelo) e, em seguida, crie uma fórmula DAX que define os valores da coluna. 
  
> [!NOTE]  
>  As colunas calculadas não têm suporte para modelos que recuperam dados de uma fonte de dados relacional usando o modo DirectQuery.  
  
 Quando uma coluna calculada contém uma fórmula DAX válida, são calculados valores para cada linha assim que a fórmula é inserida. Os valores são então armazenados no banco de dados. Por exemplo, em uma tabela de Data, quando a fórmula `=[Calendar Year] & " Q" & [Calendar Quarter]` é inserida na barra de fórmulas, um valor para cada linha na tabela é calculado usando os valores da coluna Ano Calendário (na mesma tabela de Data), adicionando-se um espaço e o Q maiúsculo e depois os valores da coluna Trimestre Calendário (na mesma tabela Data). O resultado de cada linha na coluna calculada é calculado imediatamente e aparece, por exemplo, como **2010 Q1**. Só serão recalculados valores de coluna se os dados forem reprocessados.  
  
 Para obter mais informações, consulte [Colunas calculadas](../../analysis-services/tabular-models/ssas-calculated-columns.md).  
  
### <a name="measures"></a>Medidas  
 Medidas são fórmulas dinâmicas onde os resultados são alterados dependendo de contexto. Medidas são usadas em formatos que dão suporte a combinação e filtragem de dados de modelo usando vários atributos, como um relatório do Power BI ou gráfico dinâmico ou tabela dinâmica do Excel de relatório. Medidas são definidas pelo autor do modelo usando a grade de medida (e a barra de fórmulas) no designer de modelo no SSDT.  
  
 Uma fórmula em uma medida pode usar funções de agregação padrão automaticamente criadas pelo recurso AutoSoma, como COUNT ou SUM ou você pode definir sua própria fórmula usando o DAX. Quando você define uma fórmula para uma medida na barra de fórmulas, um recurso de Dica de ferramenta mostra uma visualização rápida do que os resultados seriam para o total no contexto atual, mas, do contrário, os resultados não são produzidos imediatamente em qualquer lugar. Outros detalhes de medida também aparecem no painel **Propriedades** .  
  
 A razão pela qual você não pode consultar os resultados filtrados do cálculo imediatamente é que o resultado de uma medida não pode ser determinado sem contexto. Para avaliar uma medida, é necessário um aplicativo cliente de relatório que pode fornecer o contexto necessário para recuperar os dados relevantes para cada célula e, em seguida, avaliar a expressão para cada célula. Cliente pode ser uma tabela dinâmica do Excel ou gráfico dinâmico, um relatório do Power BI ou uma consulta MDX. Independentemente do cliente de relatório, uma consulta separada é executada para cada célula nos resultados. Ou seja, cada combinação de cabeçalhos de linha e coluna em uma tabela dinâmica, ou cada seleção de segmentação de dados e filtros em um relatório do Power BI, gera um subconjunto diferente de dados sobre os quais a medida é calculada. Por exemplo, em uma medida com a fórmula, `Total Sales:=SUM([Sales Amount])`, quando um usuário coloca a medida TotalSales na janela valores em uma tabela dinâmica e, em seguida, coloca a coluna DimProductCategory de uma tabela DimProduct na janela filtros, a soma da quantidade de vendas calculada e exibida para cada categoria de produto.  
  
 Diferentemente de colunas calculadas e filtros de linha, a sintaxe para uma medida inclui o nome da medida que precede a fórmula. No exemplo que acabamos de fornecer, o nome **Total de Vendas:** : aparece antes da fórmula. Depois que você criou uma medida, o nome e sua definição aparecem na Lista de Campos do aplicativo de cliente de relatório e, dependendo das perspectivas e funções, está disponível para todos os usuários do modelo dependendo das perspectivas e das funções.  
  
 Para obter mais informações, consulte [Medidas](../../analysis-services/tabular-models/measures-ssas-tabular.md).  
  
### <a name="row-filters"></a>Filtros de linha  
 Os filtros de linha definem quais linhas em uma tabela são visíveis a membros de uma função específica. Os filtros de linha podem ser criados para cada tabela em um modelo usando fórmulas DAX. Filtros de linha são criados para uma função específica usando o Gerenciador de funções no SSDT. Filtros de linha também podem ser definidos para um modelo implantado usando as propriedades de função no SQL Server Management Studio (SSMS).  
  
 Em um filtro de linha, uma fórmula DAX, que deve ser avaliada como uma condição booliana TRUE/FALSE, define quais as linhas que poderão ser retornadas pelos resultados de uma consulta por membros dessa função específica. As linhas não incluídas na fórmula DAX não poderão ser retornadas. Por exemplo, para membros da função Vendas, a tabela de Clientes com a seguinte fórmula DAX: `=Customers[Country] = “USA”`somente poderá exibir dados para clientes nos EUA e agregações, como SUM, são retornadas apenas para clientes nos EUA.  
  
 Quando você define um filtro de linha usando a fórmula do DAX, está criando um conjunto de linha permitido. Isto não nega acesso a outras linhas; em vez disso, elas simplesmente não são retornadas como parte do conjunto de linha permitido. Outras funções podem permitir acesso às linhas excluídas pela fórmula do DAX. Se um usuário for membro de outra função, e os filtros de linha dessa função permitirem acesso àquele conjunto de linha específico, o usuário poderá exibir os dados para aquela linha.  
  
 Os filtros de linha aplicam-se às linhas especificadas e também a linhas relacionadas. Quando uma tabela tiver várias relações, os filtros aplicam segurança para a relação que está ativa. Os filtros de linha serão intersectados com outros filtros de linha definidos para tabelas relacionadas.  
  
 Para obter mais informações, consulte [funções](../../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
##  <a name="bkmk_DAX_datatypes"></a> Tipos de dados DAX  
 É possível importar para um modelo de diversas fontes de dados diferentes que podem dar suporte a diferentes tipos de dados. Quando você importa os dados em um modelo, os dados são convertidos em um dos tipos de dados de modelo de tabela. Quando os dados de modelo são usados em um cálculo, os dados são convertidos em um tipo de dados DAX para a duração e a saída do cálculo. Quando você cria uma fórmula DAX, os termos usados na fórmula determinarão o tipo de dados de valor retornado automaticamente.  
  
 Modelos de tabela e DAX oferecem suporte aos seguintes tipos de dados:  
  
|Tipo de dados em modelo|Tipos de dados em DAX|Description|  
|------------------------|----------------------|-----------------|  
|Número Inteiro|Um valor inteiro de 64 bits (oito bytes) <sup>1, 2</sup>|Números sem casas decimais. Inteiros podem ser números positivos ou negativos, mas devem ser números inteiros entre -9.223.372.036.854.775.808 (-2^63) e 9.223.372.036.854.775.807 (2^63-1).|  
|Número Decimal|Um número real de 64 bits (oito bytes) <sup>1, 2</sup>|Números reais são números que podem ter casas decimais. Os números reais abrangem uma grande variedade de valores:<br /><br /> Valores negativos de -1,79E +308 a -2,23E -308<br /><br /> Zero<br /><br /> Valores positivos de 2,23E -308 a 1,79E + 308<br /><br /> No entanto, o número de dígitos significativos está limitado a 17 dígitos decimais.|  
|Boolean|Booliano|Um valor True ou False.|  
|Texto|Cadeia de caracteres|Uma cadeia de caracteres de dados de caractere Unicode. Podem ser cadeias de caracteres, números ou datas representados em um formato de texto.|  
|Data|Data/hora|Datas e horas em uma representação de data-hora aceita.<br /><br /> As datas válidas são todas as datas depois de 1º de março de 1900.|  
|Moeda|Moeda|O tipo de dados de moeda permite valores entre -922.337.203.685.477,5808 e 922.337.203.685.477,5807 com quatro dígitos decimais de precisão fixa.|  
|N/A|Em branco|Um espaço em branco é um tipo de dados no DAX que representa e substitui nulos SQL. É possível criar um espaço em branco usando a função BLANK e testar se há espaços em branco usando a função lógica, ISBLANK.|  
  
 Os modelos de tabela também incluem o tipo de dados como a entrada ou a saída para muitas funções DAX. Por exemplo, a função FILTER usa uma tabela como entrada e gera outra tabela que contém apenas as linhas que atendam às condições do filtro. Ao combinar funções de tabela com funções de agregação, você pode executar cálculos complexos em conjuntos de dados definidos de forma dinâmica.  
  
 Embora os tipos de dados em geral sejam definidos automaticamente, é importante entendê-los e saber como se aplicam, em particular, a fórmulas DAX. Erros em fórmulas ou resultados inesperados, por exemplo, são causados frequentemente pelo uso de um operador específico que não pode ser usado com um tipo de dados especificado em um argumento. Por exemplo, a fórmula `= 1 & 2`retorna um resultado de cadeia de caracteres de 12. A fórmula `= “1” + “2”`, no entanto, retorna um resultado de inteiro de 3.  
  
 Para obter informações detalhadas sobre os tipos de dados em modelos de tabela e conversões explícitas e implícitas de tipos de dados no DAX, consulte [tipos de dados com suporte](../../analysis-services/tabular-models/data-types-supported-ssas-tabular.md).  
  
##  <a name="bkmk_DAX_opertors"></a> Operadores DAX  
 A linguagem DAX usa quatro tipos diferentes de operadores de cálculo em fórmulas:  
  
-   Operadores de comparação para comparar valores e retornar um valor TRUE\FALSE lógico.  
  
-   Operadores aritméticos para executar cálculos aritméticos que retornam valores numéricos.  
  
-   Operadores de concatenação de texto para unir duas ou mais cadeias de caracteres de texto.  
  
-   Operadores lógicos que combinam duas ou mais expressões para retornar um único resultado.  
  
 Para obter informações detalhadas sobre operadores usados em fórmulas DAX, consulte [Referência de operador DAX](http://msdn.microsoft.com/en-us/1befbddc-6178-472c-8bc4-05dafd62207e).  
  
##  <a name="bkmk_DAX_Formulas"></a> Fórmulas DAX  
 As fórmulas DAX são essenciais para criar cálculos em colunas calculadas e medidas e proteger seus dados usando filtros de nível de linha. Para criar fórmulas para colunas calculadas e medidas, você usará a barra de fórmulas ao longo da parte superior da janela do designer de modelo ou o Editor DAX. Para criar fórmulas para filtros de linha, você usará a caixa de diálogo Gerenciador de Funções. As informações nesta seção têm o objetivo de proporcionar a você o entendimento dos fundamentos das fórmulas DAX.  
  
###  <a name="basics"></a> Fundamentos de fórmula  
 O DAX permite que os autores de modelos de tabela definam cálculos personalizados em ambas as tabelas de modelo, como parte de colunas calculadas, e como medidas associadas a tabelas, mas não aparecendo diretamente nelas. O DAX também permite que os autores de modelo protejam dados, criando cálculos que retornam um valor booliano que define quais linhas em uma tabela específica ou relacionada podem ser consultadas por usuários membros da função associada.  
  
 As fórmulas DAX podem ser muito simples ou bastante complexas. A tabela a seguir mostra alguns exemplos de fórmulas simples que poderiam ser usadas em uma coluna calculada.  
  
|||  
|-|-|  
|Fórmula|Description|  
|`=TODAY()`|Insere a data de hoje em cada linha da coluna.|  
|`=3`|Insere o valor 3 em cada linha da coluna.|  
|`=[Column1] + [Column2]`|Adiciona os valores na mesma linha de [Column1] e [Column2], além de colocar os resultados na coluna calculada da mesma linha.|  
  
 Se a fórmula que você criar for simples ou complexa, você poderá usar as etapas seguintes ao compilar uma fórmula:  
  
1.  Cada fórmula deve começar com um sinal de igualdade.  
  
2.  É possível digitar ou selecionar um nome de função ou digitar uma expressão.  
  
3.  Comece digitando as primeiras letras da função ou do nome desejado; o recurso Preenchimento Automático exibirá uma lista das funções, tabelas e colunas disponíveis. Pressione TAB para adicionar um item da lista Preenchimento Automático à fórmula.  
  
     Você também pode clicar no botão **Fx** para exibir uma lista das funções disponíveis. Para selecionar uma função na lista suspensa, use as teclas de direção para realçar o item e clique em **OK** para adicionar a função à fórmula.  
  
4.  Forneça os argumentos à função selecionando-os em uma lista suspensa de possíveis tabelas e colunas, ou digitando valores.  
  
5.  Verifique se há erros de sintaxe: verifique se todos os parênteses estão fechados, e se colunas, tabelas e valores estão referenciados corretamente.  
  
6.  Pressione ENTER para aceitar a fórmula.  
  
> [!NOTE]  
>  Em uma coluna calculada, assim que você insere a fórmula e a fórmula é validada, a coluna é preenchida com valores. Em uma medida, pressionar ENTER salva a definição da medida ma grade de medida com a tabela. Se uma fórmula estiver inválida, um erro será exibido.  
  
 Neste exemplo, nós examinaremos uma fórmula mais complexa em uma medida chamada Dias do Trimestre Atual:  
  
```  
Days in Current Quarter:=COUNTROWS( DATESBETWEEN( 'Date'[Date], STARTOFQUARTER( LASTDATE('Date'[Date])), ENDOFQUARTER('Date'[Date])))  
```  
  
 Essa medida é usada para criar uma taxa de comparação entre um período incompleto e o período anterior. A fórmula deve levar em conta a proporção do período decorrido e compará-la à mesma proporção do período anterior. Nesse caso, [Dias – Trimestre Atual até Hoje]/[Dias do Trimestre Atual] fornece a proporção decorrida no período atual.  
  
 Essa fórmula contém os seguintes elementos:  
  
|Elemento Formula|Description|  
|---------------------|-----------------|  
|`Days in Current Quarter:=`|O nome da medida.|  
|`=`|O sinal de igualdade (=) inicia a fórmula.|  
|`COUNTROWS`|A [função COUNTROWS (DAX)](http://msdn.microsoft.com/en-us/830dd659-5405-4e0a-8d26-01ae9d5e5e9a) conta o número de linhas na tabela de Data|  
|`()`|Os parênteses de abertura e fechamento especificam argumentos.|  
|`DATESBETWEEN`|A função DATESBETWEEN retorna as datas entre a última data de cada valor na coluna Data na tabela de Data.|  
|`'Date'`|Especifica a tabela de Data. As tabelas estão entre aspas simples.|  
|`[Date]`|Especifica a coluna Data na tabela de Data. As colunas estão entre colchetes.|  
|`,`||  
|`STARTOFQUARTER`|A função STARTOFQUARTER retorna a data do início do trimestre.|  
|`LASTDATE`|A função LASTDATE retorna a última data do início do trimestre.|  
|`'Date'`|Especifica a tabela de Data.|  
|`[Date]`|Especifica a coluna Data na tabela de Data.|  
|`,`||  
|`ENDOFQUARTER`|A função ENDOFQUARTER|  
|`'Date'`|Especifica a tabela de Data.|  
|`[Date]`|Especifica a coluna Data na tabela de Data.|  
  
#### <a name="using-formula-autocomplete"></a>Usando o Preenchimento Automático de fórmulas  
 A barra de fórmulas no designer de modelos e a janela Filtros de Linha da fórmula na caixa de diálogo Gerenciador de Funções fornecem um recurso de Preenchimento Automático. O Preenchimento Automático o ajuda a inserir uma sintaxe de fórmula válida fornecendo opções para cada elemento na fórmula.  
  
-   É possível usar a opção AutoCompletar Fórmula no meio de uma fórmula existente com funções aninhadas. O texto pouco antes do ponto de inserção é usado para exibir valores na lista suspensa, e todo o texto depois do ponto de inserção permanece inalterado.  
  
-   O Preenchimento Automático não adiciona parênteses de fechamento das funções, nem compara parênteses automaticamente. Você deve verificar se cada função está sintaticamente correta; caso contrário, não poderá salvar nem usar a fórmula.  
  
#### <a name="using-multiple-functions-in-a-formula"></a>Usando várias funções em uma fórmula  
 Você pode aninhar funções, o que significa que você usa os resultados de uma função como um argumento de outra função. Você pode aninhar até 64 níveis de funções em colunas calculadas. Entretanto, o aninhamento pode dificultar a criação ou a solução de problemas em fórmulas.  
  
 Muitas funções destinam-se ao uso somente como funções aninhadas. Essas funções retornam uma tabela, que não pode ser salva diretamente como um resultado; mas deve ser fornecida como entrada para uma função de tabela. Por exemplo, as funções SUMX, AVERAGEX e MINX requerem uma tabela como o primeiro argumento.  
  
> [!NOTE]  
>  Alguns limites são aplicados dentro de medidas no aninhamento de funções, para garantir que o desempenho não seja afetado pelos diversos cálculos necessários para as dependências entre colunas.  
  
##  <a name="bkmk_DAX_functions"></a> Funções DAX  
 Esta seção fornece uma visão geral dos *tipos* de funções que têm o suporte da linguagem DAX. Para obter mais informações, consulte [Referência de Função DAX](http://msdn.microsoft.com/en-us/4dbb28a1-dd1a-4fca-bcd5-e90f74864a7b).  
  
 O DAX fornece diversas funções que você pode usar para executar cálculos usando datas e horas ou criar valores condicionais, trabalhar com cadeias de caracteres, executar pesquisas com base em relacionamentos e a capacidade de iterar em uma tabela para realizar cálculos recursivos. Se você estiver familiarizado com fórmulas do Excel, muitas dessas funções parecerão muito similares; porém, as fórmulas DAX são diferentes dos seguintes modos importantes:  
  
-   Uma função DAX sempre referencia uma coluna completa ou uma tabela. Para usar apenas valores específicos de uma tabela ou coluna, você pode adicionar filtros à fórmula.  
  
-   Se for necessário personalizar os cálculos linha por linha, o DAX fornecerá funções que permitem usar o valor da linha atual ou um valor relacionado como um tipo de parâmetro, para executar cálculos que variam de acordo com o contexto. Para entender como funcionam essas funções, consulte [Contexto em fórmulas DAX](../../analysis-services/tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md#bkmk_context) , posteriormente neste tópico.  
  
-   O DAX inclui muitas funções que retornam uma tabela, em vez de um valor. A tabela não é exibida em um cliente de relatório, mas é usada para fornecer entrada para outras funções. Por exemplo, você pode recuperar uma tabela e contar os valores distintos nele ou calcular somas dinâmicas em tabelas filtradas ou colunas.  
  
-   Funções DAX incluem uma variedade de *inteligência de tempo* funções. Estas funções permitem definir ou selecionar intervalos de datas e executar cálculos dinâmicos com base nestas datas ou intervalos. Por exemplo, você pode comparar somas em períodos paralelos.  
  
### <a name="date-and-time-functions"></a>Funções de data e hora  
 As funções de data e hora na DAX são semelhantes às funções de data e hora do Microsoft Excel. No entanto, as funções DAX se baseiam nos tipos de dados **datetime** usados pelo Microsoft SQL Server. Para obter mais informações, consulte [Funções de data e hora (DAX)](http://msdn.microsoft.com/en-us/9fc9214a-fcd6-40c0-bf51-0c95637c6ffb).  
  
### <a name="filter-functions"></a>Funções de filtro  
 As funções de filtro em DAX retornam tipos de dados específicos, pesquisar valores em tabelas relacionadas e filtrar pelos valores relacionados. As funções de pesquisa funcionam com tabelas e relações, assim como um banco de dados. As funções de filtragem permitem manipular o contexto de dados para criar cálculos dinâmicos. Para obter mais informações, consulte [Funções de filtro (DAX)](http://msdn.microsoft.com/en-us/b036fd40-4d3b-426d-a0d2-80258b53d8e5).  
  
### <a name="information-functions"></a>Funções informativas  
 Uma função informativa verifica a célula ou linha fornecida como um argumento e indica se o valor corresponde ao tipo esperado. Por exemplo, a função ISERROR retorna TRUE quando o valor referenciado contém um erro. Para obter mais informações, consulte [Funções informativas (DAX)](http://msdn.microsoft.com/en-us/6d2bee09-0456-4444-b4d2-c231fd788a2e).  
  
### <a name="logical-functions"></a>Funções lógicas  
 As funções lógicas agem sobre uma expressão para retornar informações sobre os valores da expressão. Por exemplo, a função TRUE permite saber se uma expressão que você está avaliando retorna um valor TRUE. Para obter mais informações, consulte [Funções lógicas (DAX)](http://msdn.microsoft.com/en-us/2eb33add-60b2-44ab-b761-012a473116a2).  
  
### <a name="mathematical-and-trigonometric-functions"></a>Funções matemáticas e trigonométricas  
 As funções matemáticas em DAX são muito semelhantes às funções matemáticas e trigonométricas do Excel. Existem algumas pequenas diferenças nos tipos de dados numéricos usados por funções DAX. Para obter mais informações, consulte [Funções matemáticas e trigonométricas (DAX)](http://msdn.microsoft.com/en-us/1f408ec1-e769-43d6-a68c-567bc30d893f).  
 
### <a name="other-functions"></a>Outras funções  
 Essas funções executam ações exclusivas que não podem ser definidas por qualquer uma das categorias a maioria das outras funções pertencem ao. Para obter mais informações, consulte [outras funções (DAX)](https://msdn.microsoft.com/mt150101).
  
### <a name="statistical-functions"></a>Funções estatísticas  
 O DAX fornece funções estatísticas que executam agregações. Além de criar somas e médias, ou localizar os valores mínimo e máximo, na DAX também é possível filtrar uma coluna antes de agregar ou criar agregações com base em tabelas relacionadas. Para obter mais informações, consulte [Funções estatísticas (DAX)](http://msdn.microsoft.com/en-us/ba4c1298-57a0-40fc-b6f6-00e187ace559).  
  
### <a name="text-functions"></a>Funções de texto  
 As funções de texto na DAX são bem semelhantes às suas correspondentes no Excel. Você pode retornar parte de uma cadeia de caracteres, pesquisar texto em uma cadeia de caracteres ou concatenar valores de cadeia de caracteres. A DAX também fornece funções para controlar os formatos de datas, horas e números. Para obter mais informações, consulte [Funções de texto (DAX)](http://msdn.microsoft.com/en-us/e4821571-ae55-4df7-ae98-c578200bba5f).  
  
### <a name="time-intelligence-functions"></a>Funções de inteligência de tempo  
 As funções de inteligência de tempo fornecidas em DAX permitem criar cálculos que usam o conhecimento interno sobre calendários e datas. Usando intervalos de hora e data em combinação com agregações ou cálculos, você pode criar comparações significativas em períodos de tempo comparáveis para vendas, inventário, e assim por diante. Para obter mais informações, consulte [funções de inteligência de tempo (DAX)](http://msdn.microsoft.com/en-us/91df278d-4b28-40c1-a572-cdb91f081517).  
  
###  <a name="bkmk_TableFunc"></a> Funções com valor de tabela  
 Existem funções DAX que produzem tabelas, aceitam tabelas como entrada ou ambas as opções. Como uma tabela pode ter uma única coluna, as funções com valor de tabela também aceitam colunas únicas como entradas. É importante compreender como usar essas funções com valor de tabela para usar completamente as fórmulas DAX. O DAX inclui os seguintes tipos de funções com valor de tabela:  
  
  **Funções de filtro** -retornam uma coluna, tabela ou valores relacionados à linha atual.  
    
  **Funções de agregação** -agregam qualquer expressão às linhas de uma tabela.  
    
  **Funções de inteligência de tempo** - retornam uma tabela de datas, ou usar uma tabela de datas para calcular uma agregação.  
  
##  <a name="bkmk_context"></a> Contexto em fórmulas DAX  
 *Contexto* é um conceito importante para entender quando criar fórmulas que usam DAX. O contexto é o que permite executar análise dinâmica, como os resultados de uma fórmula são alterados para refletir a seleção atual de linha ou célula, além de qualquer dado relacionado. Entender o que é contexto e seu uso eficiente é vital para compilar análises dinâmicas de alto desempenho e para solucionar problemas em fórmulas.  
  
 As fórmulas em modelos de tabela podem ser avaliadas em um contexto diferente, dependendo de outros elementos de design:  
  
-   Filtros aplicados em uma Tabela Dinâmica ou relatório  
  
-   Filtros definidos dentro de uma fórmula  
  
-   Relações especificadas usando funções especiais dentro de uma fórmula  
  
 Há tipos diferentes de contexto: *contexto de linha*, *contexto de consulta*e *contexto de filtro*.  
  
###  <a name="bkmk_row_context"></a> Contexto de linha  
 O*Contexto de linha* pode considerado como "a linha atual". Se você criar uma fórmula em uma coluna calculada, o contexto de linha dessa fórmula incluirá os valores de todas as colunas na linha atual. Se a tabela estiver relacionada a outra tabela, o conteúdo também incluirá todos os valores dessa outra tabela que estão relacionados à linha atual.  
  
 Por exemplo, suponha que você crie uma coluna calculada, `=[Freight] + [Tax]`, que soma os valores de duas colunas, Freight e Tax, da mesma tabela. Esta fórmula automaticamente obtém somente os valores da linha atual nas colunas especificadas.  
  
 Contexto de linha também segue os relacionamentos que foram definidos entre tabelas, incluindo relacionamentos definidos dentro de uma coluna calculada usando fórmulas DAX, para determinar quais linhas nas tabelas relacionadas estão associadas à linha atual.  
  
 Por exemplo, a fórmula a seguir usa a função RELATED para buscar um valor de imposto de uma tabela relacionada, com base na região para a qual o pedido foi enviado. O valor do imposto é determinado com o uso do valor para a região na tabela atual, pesquisando-se a região na tabela relacionada e obtendo-se o valor do imposto para essa região na tabela relacionada.  
  
```  
= [Freight] + RELATED('Region'[TaxRate])  
```  
  
 Esta fórmula obtém a taxa de imposto para a região atual da tabela de Região e adiciona-a ao valor da coluna Freight. Nas fórmulas DAX, você não precisa saber ou especificar a relação específica que conecta as tabelas.  
  
#### <a name="multiple-row-context"></a>Contexto de várias linhas  
 A DAX inclui várias funções que iteram cálculos em uma tabela. Essas funções podem ter várias linhas atuais, cada uma com seu próprio contexto de linha.  Em essência, estas funções permitem criar fórmulas que executam operações recursivamente em um loop interno e exterior.  
  
 Por exemplo, vamos supor que o modelo contenha uma tabela **Products** e uma tabela **Sales** . Talvez os usuários queiram percorrer toda a tabela de vendas, que contém várias transações que envolvem vários produtos, e encontrar a maior quantidade solicitada de cada produto em qualquer transação.  
  
 Com a DAX você pode criar uma única fórmula que retorna o valor correto e os resultados são atualizados automaticamente a qualquer momento em que um usuário adicionar dados às tabelas.  
  
```  
=MAXX(FILTER(Sales,[ProdKey]=EARLIER([ProdKey])),Sales[OrderQty])  
```  
  
 Para obter um passo a passo detalhado dessa fórmula, consulte a [Função EARLIER (DAX)](http://msdn.microsoft.com/en-us/6d126c4d-2315-49ec-899d-cb396eefbae6).  
  
 Em resumo, a função EARLIER armazena o contexto de linha da operação que precedeu a operação atual. O tempo todo, a função armazena na memória dois conjuntos de contexto: um deles representa a linha atual do loop interno da fórmula, e o outro representa a linha atual do loop externo da fórmula. A DAX alimenta automaticamente valores entre os dois loops para que você possa criar agregações complexas.  
  
####  <a name="bkmk_query_context"></a> Contexto de consulta  
 *Contexto de consulta* se refere ao subconjunto de dados recuperados implicitamente para uma fórmula. Quando um usuário coloca uma medida ou outro campo de valor em uma Tabela Dinâmica ou um relatório baseado em um modelo de tabela, o mecanismo examina os cabeçalhos de linha e coluna, Segmentações de Dados e filtros de relatório para determinar o contexto. Em seguida, as consultas necessárias são executadas em uma fonte de dados para obter o subconjunto correto de dados, fazer os cálculos definidos pela fórmula e popular cada célula na Tabela Dinâmica ou no relatório. O conjunto de dados recuperado é o contexto de consulta para cada célula.  
  
> [!WARNING]  
>  Para um modelo no DirectQuery, o contexto é avaliado e em seguida as operações de conjunto para recuperar o subconjunto correto de dados e calcular os resultados são traduzidas para instruções SQL. Essas instruções são então executadas diretamente no repositório de dados relacional. Portanto, embora o método de obter os dados e calcular os resultados seja diferente, o próprio contexto não é alterado.  
  
 Como o contexto altera dependendo de onde você coloca a fórmula, os resultados da fórmula também podem ser alterados.  
  
 Por exemplo, suponhamos que você crie uma fórmula simples que soma os valores na coluna **Profit** da tabela **Sales** : `=SUM('Sales'[Profit])`.  Se você usar essa fórmula em uma coluna calculada na tabela **Vendas** , os resultados da fórmula serão os mesmos para toda a tabela, porque o contexto da consulta da fórmula sempre será todo o conjunto de dados da tabela **Vendas** . Os resultados terão lucro para todas as regiões, todos os produtos, todos os anos etc.  
  
 No entanto, em geral os usuários não desejam ver o mesmo resultado centenas de vezes, mas desejam obter o lucro de um determinado ano, um país específico, um certo produto ou uma combinação desses itens e depois obter um total geral.  
  
 Em uma Tabela Dinâmica, o contexto pode ser alterado com a adição ou remoção de cabeçalhos de coluna e linha, e adição ou remoção de Segmentações de Dados. Sempre que os usuários adicionam cabeçalhos de coluna ou linha à Tabela Dinâmica, eles alteram o contexto de consulta no qual a medida é avaliada. As operações de divisão e filtragem também afetam o contexto. Portanto, a mesma fórmula, usada em uma medida, é avaliada em um *contexto de consulta* diferente para cada célula.  
  
####  <a name="bkmk_filter_context"></a> Contexto de filtro  
 *Contexto de filtro* é o conjunto de valores permitido em cada coluna, ou nos valores recuperados de uma tabela relacionada. Os filtros podem ser aplicados à coluna no designer ou na camada de apresentação (relatórios e Tabelas Dinâmicas). Filtros também podem ser definidos explicitamente por expressões de filtro dentro da fórmula.  
  
 O contexto de filtro é adicionado quando você especifica restrições de filtro no conjunto de valores permitido em uma coluna ou tabela, usando argumentos de uma fórmula. O contexto de filtro é aplicado sobre outros contextos, como o contexto de linha ou o contexto de consulta.  
  
 Em modelos de tabela, há muitos modos de criar contexto de filtro. Dentro do contexto de clientes que podem consumir o modelo, como relatórios do Power BI, os usuários podem criar filtros dinamicamente adicionando segmentações de dados ou filtros de relatório nos cabeçalhos de linha e coluna. Você também pode especificar expressões de filtro diretamente dentro da fórmula, para especificar valores relacionados, para filtrar tabelas que são usadas como entradas ou para obter contexto dinamicamente para os valores que são usados em cálculos. Você também pode desmarcar completa ou seletivamente os filtros em colunas específicas. Isto é muito útil ao criar fórmulas que calculam totais principais.  
  
 Para obter mais informações sobre como criar filtros dentro de fórmulas, consulte a [Função FILTER (DAX)](http://msdn.microsoft.com/en-us/f1f6bee4-547b-407c-b70b-9216b2f3d3fd).  
  
 Para obter um exemplo de como os filtros são limpos para criar totais gerais, consulte a [Função ALL (DAX)](http://msdn.microsoft.com/en-us/a7e0ab71-d83e-4463-bc77-9eb5dd73c6fc).  
  
 Para obter exemplos de como limpar e aplicar filtros dentro de fórmulas, consulte a [Função ALLEXCEPT (DAX)](http://msdn.microsoft.com/en-us/a6f575a1-9803-4bb2-85b3-c95c060f1fb1).  
  
####  <a name="bkmk_determine_context"></a> Determinando o contexto em fórmulas  
 Quando você cria uma fórmula do DAX, a fórmula é testada primeiro para sintaxe válida e para ter certeza de que os nomes das colunas e tabelas incluídos na fórmula podem ser localizados no contexto atual. Se qualquer coluna ou tabela especificada pela fórmula não puder ser localizada, um erro será retornado.  
  
 O contexto durante a validação (e operações de recálculo) é determinado conforme descrito nas seções anteriores, usando as tabelas disponíveis no modelo, qualquer relacionamento entre tabela e qualquer filtro que tenha sido aplicado.  
  
 Por exemplo, se você tiver importado alguns dados em uma nova tabela e não tiver relacionado a nenhuma outra tabela (e não tiver aplicado filtros), o *contexto atual* será o conjunto inteiro de colunas da tabela. Se a tabela estiver vinculada por relações com outras tabelas, o contexto atual incluirá as tabelas relacionadas. Se você adicionar uma coluna da tabela a um relatório que tem segmentação de dados e talvez algum filtros de relatório, o contexto para a fórmula será o subconjunto de dados em cada célula do relatório.  
  
 O contexto é um conceito avançado que também pode dificultar a solução de erros de fórmulas. Nós recomendamos que você comece com fórmulas simples e relacionamentos para verificar como o contexto funciona. A seção a seguir fornece alguns exemplos de como as fórmulas usam tipos diferentes de contexto para retornar resultados dinamicamente.  
  
##### <a name="examples-of-context-in-formulas"></a>Exemplos de contexto em fórmulas  
  
1.  A [Função RELATED (DAX)](http://msdn.microsoft.com/en-us/0023fd13-c17a-4243-ab77-3779a4b502b6) expande o contexto da linha atual para incluir valores em uma coluna relacionada. Isso permite a execução de pesquisas. O exemplo neste tópico ilustra a interação entre a filtragem e o contexto de linha.  
  
2.  A [Função FILTER (DAX)](http://msdn.microsoft.com/en-us/f1f6bee4-547b-407c-b70b-9216b2f3d3fd) permite especificar as linhas a serem incluídas no contexto atual. Os exemplos neste tópico também ilustram como inserir filtros em outras funções que executam agregações.  
  
3.  A [Função ALL (DAX)](http://msdn.microsoft.com/en-us/a7e0ab71-d83e-4463-bc77-9eb5dd73c6fc) define o contexto dentro de uma fórmula. Você pode usá-la para anular filtros aplicados como resultado do contexto de consulta.  
  
4.  A [Função ALLEXCEPT (DAX)](http://msdn.microsoft.com/en-us/a6f575a1-9803-4bb2-85b3-c95c060f1fb1) permite remover todos os filtros, exceto um especificado por você. Os dois tópicos incluem exemplos que orientam você durante a criação de fórmulas e a compreensão dos contextos complexos.  
  
5.  A [Função EARLIER (DAX)](http://msdn.microsoft.com/en-us/6d126c4d-2315-49ec-899d-cb396eefbae6) e a [Função EARLIEST (DAX)](http://msdn.microsoft.com/en-us/9befa04d-78db-492e-a463-80b8b77206d6) permitem executar loop pelas tabelas que executam cálculos referenciando, simultaneamente, um valor de um loop interno. Se você estiver familiarizado com o conceito de recursão e com loops internos e externos, apreciará o poder proporcionado pelas funções EARLIER e EARLIEST. Se você não for experiente com esses conceitos, siga as etapas no exemplo atentamente para ver como os contextos internos e externos são usados ao fazer cálculos.  
  
##  <a name="bkmk_RelModel"></a> Fórmulas e o modelo de tabela  
 O designer de modelo no SSDT, é uma área onde você pode trabalhar com várias tabelas de dados e conectar as tabelas em um modelo de tabela. Dentro deste modelo, as tabelas são unidas por relações em colunas com valores comuns (chaves). O modelo de tabela permite vincular valores a colunas em outras tabelas e cria mais cálculos interessantes. Da mesma maneira que em um banco de dados relacional, você pode conectar muitos níveis de tabelas relacionadas e usar colunas de qualquer tabela nos resultados.  
  
 Por exemplo, você pode vincular uma tabela de vendas, uma tabela de produtos e uma tabela de categorias de produto e os usuários podem utilizar várias combinações das colunas nas Tabelas Dinâmicas e em relatórios. Os campos relacionados podem ser usados para filtrar tabelas conectadas ou criar cálculos sobre subconjuntos. (Se você não estiver familiarizado com o banco de dados relacional e trabalhar com tabelas e junções, consulte [relações](../../analysis-services/tabular-models/relationships-ssas-tabular.md).)  
  
 Os modelos de tabela dão suporte a várias relações entre tabelas. Para evitar confusão ou resultados errados, somente uma relação é designada de cada vez como a relação ativa, mas você pode alterar a relação ativa como for necessário para atravessar conexões diferentes nos dados nos cálculos. A [Função USERELATIONSHIP (DAX)](http://msdn.microsoft.com/en-us/200484ab-9da1-4570-a100-7f9ed20d33af) pode ser usada para especificar uma ou mais relações a serem usadas em um cálculo específico.  
  
 Em um modelo de tabela, você deve observar estas regras de design de fórmula:  
  
-   Quando as tabelas estão conectadas por uma relação, você deve verificar se essas duas colunas usadas como chaves têm valores correspondentes. No entanto, a integridade referencial não é imposta e, portanto, é possível ter valores não correspondentes em uma coluna de chave e, ainda assim, criar uma relação. Se isso ocorrer, você deve estar ciente de que valores em branco ou não correspondentes pode afetar os resultados das fórmulas.  
  
-   Ao vincular tabelas em seu modelo usando relações, você amplia o escopo, ou *contexto*, no qual as fórmulas são avaliadas. As alterações no contexto resultantes da adição de novas tabelas, novas relações, ou de alterações na relação ativa podem fazer seus resultados serem alterados de maneira imprevista. Para obter mais informações, consulte [Contexto em fórmulas DAX](#bkmk_context) anteriormente neste tópico.  
  
##  <a name="bkmk_tables"></a> Trabalhando com tabelas e colunas  
 As tabelas em modelos de tabela são semelhantes às tabelas do Excel, mas diferentes quanto à forma como funcionam com dados e fórmulas:  
  
-   As fórmulas só funcionam com tabelas e colunas, e não com células individuais, referências de intervalos ou matrizes.  
  
-   As fórmulas podem usar relações para obter valores de tabelas relacionadas. Os valores recuperados sempre são relacionados ao valor da linha atual.  
  
-   Não pode haver dados irregulares, como ocorre em uma planilha do Excel. Cada linha de uma tabela deve conter o mesmo número de colunas. No entanto, pode haver valores vazios em algumas colunas. As tabelas de dados do Excel e as tabelas de dados do modelo tabular não são intercambiáveis.  
  
-   Como um tipo de dados é definido para cada coluna, cada valor nessa coluna deve ser do mesmo tipo.  
  
### <a name="referring-to-tables-and-columns-in-formulas"></a>Referenciando tabelas e colunas em fórmulas  
 É possível referenciar qualquer tabela e coluna usando seu nome. Por exemplo, a seguinte fórmula ilustra como referenciar colunas de duas tabelas usando o nome *totalmente qualificado* :  
  
```  
=SUM('New Sales'[Amount]) + SUM('Past Sales'[Amount])  
```  
  
 Quando uma fórmula é avaliada, o designer do modelo primeiro verifica a sintaxe geral e, em seguida, os nomes das colunas e tabelas que você fornece em relação a possíveis colunas e tabelas no contexto atual. Se o nome for ambíguo ou se a coluna ou tabela não puder ser encontrada, você obterá um erro na fórmula (uma cadeia de caracteres #ERROR em lugar de um valor de dados em células nas quais o erro ocorre). Para obter mais informações sobre requisitos de nomenclatura para tabelas, colunas e outros objetos, consulte "Requisitos de nomenclatura" em [Referência de Sintaxe DAX](http://msdn.microsoft.com/en-us/098630f4-7d1d-467e-976c-99b2279430d5).  
  
### <a name="table-relationships"></a>Relações de tabela  
 Ao criar relações entre tabelas, você ganha a capacidade de procurar dados em outra tabela e usar valores relacionados para executar cálculos complexos. Por exemplo, é possível usar uma coluna calculada para procurar todos os registros de envio relacionados ao revendedor atual e, em seguida, à soma dos custos de envio de cada. Em muitos casos, porém, uma relação talvez não seja necessária. Você pode usar a função LOOKUPVALUE em uma fórmula para retornar o valor no *result_columnName* para a linha que atende aos critérios especificados nos parâmetros *search_column* e *search_value* .  
  
 Muitas funções DAX exigem uma relação existente entre as tabelas, ou entre várias tabelas, para localizar as colunas que você referenciou e retornar resultados que tenham sentido. Outras funções tentarão identificar a relação; no entanto, tendo em vista melhores resultados, você deverá criar sempre uma relação onde for possível. Para obter mais informações, consulte [Fórmulas e o modelo de tabela](#bkmk_RelModel) anteriormente neste tópico.  
  
##  <a name="bkmk_RefreshRecalc"></a> Atualizando os resultados de fórmulas (Processo)  
 *Processamento de dados* e *recálculo* são duas operações separadas, mas relacionadas. Você deve compreender totalmente esses conceitos ao criar um modelo que contenha fórmulas complexas, grandes volumes de dados ou dados obtidos de fontes de dados externas.  
  
 *Processamento de dados* é o processo de atualizar os dados em um modelo com novos dados de uma fonte de dados externa.  
  
 *Recálculo* é o processo de atualizar os resultados das fórmulas para refletir todas as alterações feitas nas próprias fórmulas e nos dados subjacentes. O recálculo pode afetar o desempenho das seguintes formas:  
  
-   O valores em uma coluna calculada são computados e armazenados no modelo. Para atualizar os valores na coluna calculada, você deverá processar o modelo usando um dos três comandos de processamento: Processar Completo, Processar Dados ou Processar Recálculo. O resultado da fórmula sempre deve ser recalculado para a coluna inteira, todas as vezes que você alterar a fórmula.  
  
-   Os valores calculados por medidas são avaliados dinamicamente sempre que um usuário adiciona a medida a uma tabela dinâmica ou abre um relatório; à medida que o usuário modifica o contexto, os valores retornados pela medida são alterados. Os resultados da medida sempre refletem o mais recente no cache na memória.  
  
 O processamento e o recálculo não têm efeito nas fórmulas de filtro de linha, a menos que o resultado de um recálculo retorne um valor diferente, tornando a linha consultável ou não consultável pelos membros da função.  
  
 Para obter mais informações, consulte [processar dados](../../analysis-services/tabular-models/process-data-ssas-tabular.md).  
  
##  <a name="bkmk_troubleshoot"></a> Solucionando problemas de erros em fórmulas  
 Se você receber um erro ao definir uma fórmula, talvez a fórmula contenha um *erro sintático*, um *erro semântico*ou *erro de cálculo*.  
  
 Erros sintáticos são os mais fáceis de resolver. Em geral, eles envolvem a falta de um parêntese ou de uma vírgula. Para obter ajuda com a sintaxe de funções individuais, consulte [Referência de Função DAX](http://msdn.microsoft.com/en-us/4dbb28a1-dd1a-4fca-bcd5-e90f74864a7b).  
  
 O outro tipo de erro ocorre quando a sintaxe está correta, mas o valor ou a coluna referenciada não faz sentido no contexto da fórmula. Esses erros semânticos e de cálculo podem ser causados por um dos seguintes problemas:  
  
-   A fórmula se refere a uma coluna, tabela ou função não existente.  
  
-   A fórmula parece estar correta, mas quando o mecanismo de dados busca os dados, encontra uma incompatibilidade de tipos e gera um erro.  
  
-   A fórmula passa um número incorreto ou um tipo de parâmetros a uma função.  
  
-   A fórmula referencia uma coluna diferente que tem o erro e, por isso, os valores são inválidos.  
  
-   A fórmula refere-se a uma coluna que não foi processada, significando que tem metadados mas nenhum dado real para usar para cálculos.  
  
 Nos quatro primeiros casos, o DAX sinaliza a coluna inteira que contém a fórmula inválida. No último caso, a DAX torna a coluna indisponível para indicar que ela está em um estado não processado.  
  
##  <a name="bkmk_addional_resources"></a> Recursos adicionais  
 A [Modelagem Tabular &#40;Tutorial do Adventure Works&#41;](../../analysis-services/tabular-modeling-adventure-works-tutorial.md) fornece instruções passo a passo sobre como criar um modelo de tabela que inclui muitos cálculos nas colunas calculadas, medidas e filtros de linha. Para a maioria das fórmulas, uma descrição sobre o que a fórmula deve fazer é fornecida.  
  
 O [Blog da equipe do Analysis Services](http://go.microsoft.com/fwlink/?LinkID=220949&clcid=0x409) fornece as últimas informações, dicas, notícias e anúncios. 
  
 O [Central de Recursos do DAX](http://go.microsoft.com/fwlink/?LinkID=220966&clcid=0x409) fornece informações internas e externas sobre o DAX, incluindo várias soluções DAX enviadas por profissionais de Business Intelligence líderes.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de DAX (Data Analysis Expressions)](http://msdn.microsoft.com/en-us/70a82136-0926-4a91-bcb3-e18e82593b0d)   
 [Medidas](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [Colunas calculadas](../../analysis-services/tabular-models/ssas-calculated-columns.md)   
 [Funções](../../analysis-services/tabular-models/roles-ssas-tabular.md)   
 [KPIs](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [Fontes de dados com suporte](../../analysis-services/tabular-models/data-sources-supported-ssas-tabular.md)  
  
  

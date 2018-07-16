---
title: Exemplos de expressões (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- page breaks [Reporting Services], expressions
- green-bar reports [Reporting Services]
- Visual Basic [Reporting Services]
- functions [Reporting Services], examples
- custom code [Reporting Services]
- appearance of reports
- formatting reports [Reporting Services], expressions
- show/hide [Reporting Services]
- parameters [Reporting Services], expressions
- visibility [Reporting Services], expressions
- page headers [Reporting Services]
- page footers [Reporting Services]
- dates [Reporting Services], expressions
- expressions [Reporting Services], examples
ms.assetid: 87ddb651-a1d0-4a42-8ea9-04dea3f6afa4
caps.latest.revision: 97
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 97bfdd80fc183291f21042d11620d0a3e28e0b49
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37205036"
---
# <a name="expression-examples-report-builder-and-ssrs"></a>Exemplos de expressões (Construtor de Relatórios e SSRS)
  Expressões costumam ser usadas em relatórios para controlar o conteúdo e a aparência do relatório. As expressões são escritas no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]e podem usar funções internas, código personalizado, variáveis de relatório/grupo e variáveis definidas pelo usuário. As expressões começam com um sinal de igual (=). Para obter mais informações sobre o editor de expressões e os tipos de referências que podem ser incluídos, consulte [Uso de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md) e [Adicionar uma expressão &#40;Construtor de Relatórios e SSRS&#41;](add-an-expression-report-builder-and-ssrs.md).  
  
> [!IMPORTANT]  
>  Quando o RDL Sandboxing é habilitado, somente certos tipos e membros podem ser usados no texto da expressão durante o tempo de publicação do relatório. Para obter mais informações, consulte [Habilitar e desabilitar o RDL Sandboxing](../enable-and-disable-rdl-sandboxing.md).  
  
 Este tópico fornece exemplos de expressões que podem ser usadas para tarefas comuns em um relatório.  
  
-   [Funções do Visual Basic](#VisualBasicFunctions) Exemplos de funções de data, de cadeia de caracteres, de conversão e condicionais do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] .  
  
-   [Funções de relatórios](#ReportFunctions) Exemplos de funções de agregação e de outras funções internas de relatórios.  
  
-   [Aparência dos dados do relatório](#AppearanceofReportData) Exemplos de alteração da aparência de um relatório.  
  
-   Exemplos de[propriedades](#Properties) para definir propriedades de item de relatório para controlar formato ou visibilidade.  
  
-   [Parâmetros](#Parameters) Exemplos de uso de parâmetros em uma expressão.  
  
-   [Código Personalizado](#CustomCode) Exemplos de código personalizado inserido.  
  
 Para obter exemplos de expressões para usos específicos, consulte os tópicos seguintes:  
  
-   [Exemplos de expressões de grupo &#40;relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)  
  
-   [Exemplos de equações de filtro &#40;relatórios e SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md)  
  
-   [Filtros geralmente usados &#40;relatórios e SSRS&#41;](commonly-used-filters-report-builder-and-ssrs.md)  
  
-   [Referências de coleções de variáveis de grupo e de relatório &#40;relatórios e SSRS&#41;](built-in-collections-report-and-group-variables-references-report-builder.md)  
  
 Para obter mais informações sobre expressões simples e complexas, em que você pode usar expressões e os tipos de referências que pode incluir em uma expressão, consulte tópicos em [Expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md). Para obter mais informações sobre o contexto em que as expressões são avaliadas para calcular agregações, consulte [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Para aprender como gravar expressões que usam muitas das funções e dos operadores também empregados por exemplos de expressões neste tópico, mas no contexto da gravação de um relatório, consulte [Tutorial: introdução às expressões](../tutorial-introducing-expressions.md).  
  
 O editor de expressão inclui uma exibição hierárquica de funções internas. Quando você seleciona a função, um exemplo de código aparece no painel Valores. Para obter mais informações, consulte o [caixa de diálogo expressão](../expression-dialog-box.md) ou [caixa de diálogo expressão &#40;relatórios&#41;](../expression-dialog-box-report-builder.md).  
  
 Se estiver usando o Designer de Consulta do Modelo de Relatório para criar uma consulta do conjunto de dados que usa um modelo de relatório como uma fonte de dados, você usará fórmulas, e não expressões. Essas fórmulas ajudam a especificar os dados de relatório usando cálculos personalizados integrados na consulta que especifica os dados a serem retornados da fonte de dados do modelo de relatório. Para obter mais informações, consulte [Fórmulas em consultas de modelo de relatório &#40;Construtor de Relatórios e SSRS&#41;](formulas-in-report-model-queries-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="functions"></a>Funções  
 Muitas expressões em um relatório contêm funções. É possível formatar dados, aplicar lógica e acessar metadados do relatório usando estas funções. É possível gravar expressões que usam funções da biblioteca em tempo de execução do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] e dos namespaces <xref:System.Convert> e <xref:System.Math> . É possível adicionar referências a funções a partir de outros assemblies ou de código personalizado. Você também pode usar classes do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], incluindo <xref:System.Text.RegularExpressions>.  
  
###  <a name="VisualBasicFunctions"></a> Funções do Visual Basic  
 Você pode usar as funções do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] para manipular os dados exibidos nas caixas de texto ou usados para parâmetros, propriedades ou outras áreas do relatório. Esta seção fornece exemplos que demonstram algumas dessas funções. Para obter mais informações, consulte [Membros da biblioteca em tempo de execução do Visual Basic](http://go.microsoft.com/fwlink/?LinkId=198941) no MSDN.  
  
 O [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] fornece muitas opções de formatos personalizados como, por exemplo, para formatos de data específicos. Para obter mais informações, consulte [Tipos de Formatação](http://go.microsoft.com/fwlink/?LinkId=112024) no MSDN.  
  
#### <a name="math-functions"></a>Funções matemáticas  
  
-   O `Round` função é útil para números arredondados para o inteiro mais próximo. A expressão a seguir arredonda 1,3 para 1:  
  
    ```  
    = Round(1.3)  
    ```  
  
     Você também pode escrever uma expressão para arredondar um valor para um múltiplo especificado, semelhante ao `MRound` função no Excel. Multiplique o valor por um fator que cria um inteiro, arredonde o número e divida pelo mesmo fator. Por exemplo, para arredondar 1,3 para o múltiplo mais próximo de 0,2 (1,4), use a seguinte expressão.  
  
    ```  
    = Round(1.3*5)/5  
    ```  
  
####  <a name="DateFunctions"></a> Funções de data  
  
-   O `Today` função fornece a data atual. Essa expressão pode ser usada em uma caixa de texto para exibir a data no relatório ou em um parâmetro para filtrar dados baseados na data atual.  
  
    ```  
    =Today()  
    ```  
  
-   A função `DateAdd` é útil para fornecer um intervalo de datas baseado em um único parâmetro. A expressão a seguir fornece uma data seis meses posterior à data de um parâmetro denominado *StartDate*.  
  
    ```  
    =DateAdd(DateInterval.Month, 6, Parameters!StartDate.Value)  
    ```  
  
-   O `Year` função exibe o ano de uma data específica. Você pode usar essa função para agrupar datas em conjunto ou para exibir o ano como um rótulo para um conjunto de datas. Essa expressão fornece o ano para um grupo determinado de datas de pedidos de vendas. O `Month` função e outras funções também podem ser usadas para manipular datas. Para obter mais informações, consulte a documentação do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)].  
  
    ```  
    =Year(Fields!OrderDate.Value)  
    ```  
  
-   É possível combinar funções em uma expressão para personalizar o formato. A expressão a seguir altera o formato de uma data na forma mês-dia-ano para mês-semana-número da semana. Por exemplo, 23/12/2009 para a terceira semana de dezembro:  
  
    ```  
    =Format(Fields!MyDate.Value, "MMMM") & " Week " &   
    (Int(DateDiff("d", DateSerial(Year(Fields!MyDate.Value),   
    Month(Fields!MyDate.Value),1), Fields!FullDateAlternateKey.Value)/7)+1).ToString  
    ```  
  
     Quando usado como um campo calculado em um conjunto de dados, é possível usar essa expressão em um gráfico para agregar valores por semana dentro de cada mês.  
  
-   A expressão a seguir formata o valor SellStartDate como MMM-AA. O campo SellStartDate é um tipo de dados de data/hora.  
  
    ```  
    =FORMAT(Fields!SellStartDate.Value, "MMM-yy")  
    ```  
  
-   A expressão a seguir formata o valor SellStartDate como dd/MM/aaaa. O campo SellStartDate é um tipo de dados datetime.  
  
    ```  
    =FORMAT(Fields!SellStartDate.Value, "dd/MM/yyyy")  
    ```  
  
-   A função `CDate` converte o valor em uma data. O `Now` função retorna um valor date contendo a data atual e a hora de acordo com seu sistema. `DateDiff` retorna um valor Longo especificando o número de intervalos de hora entre dois valores de Data.  
  
     O exemplo a seguir exibe a data de início do ano atual  
  
    ```  
    =DateAdd(DateInterval.Year,DateDiff(DateInterval.Year,CDate("01/01/1900"),Now()),CDate("01/01/1900"))  
    ```  
  
-   O exemplo a seguir exibe a data de início do mês anterior com base no mês atual.  
  
    ```  
    =DateAdd(DateInterval.Month,DateDiff(DateInterval.Month,CDate("01/01/1900"),Now())-1,CDate("01/01/1900"))  
    ```  
  
-   A expressão a seguir gera os anos de intervalo entre SellStartDate e LastReceiptDate. Esses campos estão em dois conjuntos de dados diferentes, DataSet1 e DataSet2. A [Função First &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-first-function.md), que é uma função de agregação, retorna o primeiro valor de SellStartDate em DataSet1 e o primeiro valor de LastReceiptDate em DataSet2.  
  
    ```  
    =DATEDIFF(“yyyy”, First(Fields!SellStartDate.Value, "DataSet1"), First(Fields!LastReceiptDate.Value, "DataSet2"))  
    ```  
  
-   O `DatePart` função retorna um valor inteiro que contém o componente especificado de um determinado valor de data. A expressão a seguir retorna o ano para o primeiro valor do SellStartDate em DataSet1. O escopo do conjunto de dados é especificado, pois há vários conjuntos de dados no relatório.  
  
    ```  
    =Datepart("yyyy", First(Fields!SellStartDate.Value, "DataSet1"))  
  
    ```  
  
-   O `DateSerial` função retorna um valor Date representando um ano, mês e dia, com as informações de hora definidas para meia-noite. O exemplo a seguir exibe a data de término do mês anterior com base no mês atual.  
  
    ```  
    =DateSerial(Year(Now()), Month(Now()), "1").AddDays(-1)  
    ```  
  
-   As expressões a seguir exibem várias datas com base em um valor de parâmetro de data selecionado pelo usuário.  
  
|Descrição de exemplo|Exemplo|  
|-------------------------|-------------|  
|Ontem|`=DateSerial(Year(Parameters!TodaysDate.Value),Month(Parameters!TodaysDate.Value),Day(Parameters!TodaysDate.Value)-1)`|  
|Dois Dias Atrás|`=DateSerial(Year(Parameters!TodaysDate.Value),Month(Parameters!TodaysDate.Value),Day(Parameters!TodaysDate.Value)-2)`|  
|Um Mês Atrás|`=DateSerial(Year(Parameters!TodaysDate.Value),Month(Parameters!TodaysDate.Value)-1,Day(Parameters!TodaysDate.Value))`|  
|Dois Meses Atrás|`=DateSerial(Year(Parameters!TodaysDate.Value),Month(Parameters!TodaysDate.Value)-2,Day(Parameters!TodaysDate.Value))`|  
|Um Ano Atrás|`=DateSerial(Year(Parameters!TodaysDate.Value)-1,Month(Parameters!TodaysDate.Value),Day(Parameters!TodaysDate.Value))`|  
|Dois Anos Atrás|`=DateSerial(Year(Parameters!TodaysDate.Value)-2,Month(Parameters!TodaysDate.Value),Day(Parameters!TodaysDate.Value))`|  
  
####  <a name="StringFunctions"></a> Funções de cadeia de caracteres  
  
-   Combine mais de um campo usando operadores de concatenação e constantes do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] . A expressão a seguir retorna dois campos, cada um em uma linha separada na mesma caixa de texto:  
  
    ```  
    =Fields!FirstName.Value & vbCrLf & Fields!LastName.Value   
    ```  
  
-   Formate datas e números em uma cadeia de caracteres com a função `Format`. A expressão a seguir exibe valores dos parâmetros *StartDate* e *EndDate* em formato de data por extenso:  
  
    ```  
    =Format(Parameters!StartDate.Value, "D") & " through " &  Format(Parameters!EndDate.Value, "D")    
    ```  
  
     Se a caixa de texto contiver apenas uma data ou número, você deve usar a propriedade de formato da caixa de texto para aplicar a formatação em vez do `Format` função dentro da caixa de texto.  
  
-   O `Right`, `Len`, e `InStr` funções são úteis para retornar uma subcadeia de caracteres, por exemplo, cortar *domínio*\\*nome de usuário* para apenas o nome de usuário. A expressão a seguir retorna a parte da cadeia de caracteres à direita de um caractere de barra invertida (\\) de um parâmetro denominado *User*:  
  
    ```  
    =Right(Parameters!User.Value, Len(Parameters!User.Value) - InStr(Parameters!User.Value, "\"))  
    ```  
  
     A expressão a seguir resulta no mesmo valor anterior, usando membros da classe [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] <xref:System.String> em vez das funções do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] :  
  
    ```  
    =Parameters!User.Value.Substring(Parameters!User.Value.IndexOf("\")+1, Parameters!User.Value.Length-Parameters!User.Value.IndexOf("\")-1)  
    ```  
  
-   Exiba os valores selecionados de um parâmetro de vários valores. O exemplo a seguir usa o `Join` função para concatenar os valores selecionados do parâmetro *MySelection* em uma única cadeia de caracteres que pode ser definida como uma expressão para o valor de uma caixa de texto em um item de relatório:  
  
    ```  
    = Join(Parameters!MySelection.Value)  
    ```  
  
     O exemplo a seguir faz o mesmo que exemplo acima, além de exibir uma cadeia de texto antes da lista de valores selecionados.  
  
    ```  
    =”Report for “ & JOIN(Parameters!MySelection.Value, “ & “)  
  
    ```  
  
-   O `Regex` funções do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] <xref:System.Text.RegularExpressions> são úteis para alterar o formato de cadeias de caracteres existentes, por exemplo, um número de telefone de formatação. A expressão a seguir usa o `Replace` função para alterar o formato de um número de telefone de dez dígitos em um campo de "*nnn*-*nnn*-*nnnn* "para" (*nnn*) *nnn*-*nnnn*":  
  
    ```  
    =System.Text.RegularExpressions.Regex.Replace(Fields!Phone.Value, "(\d{3})[ -.]*(\d{3})[ -.]*(\d{4})", "($1) $2-$3")  
    ```  
  
    > [!NOTE]  
    >  Verifique se o valor para Fields!Phone.Value não tem espaços adicionais e se é do tipo <xref:System.String>.  
  
#### <a name="lookup"></a>Pesquisar  
  
-   Ao especificar um campo chave, você pode usar a função `Lookup` para recuperar um valor de um conjunto de dados para uma relação um-para-um como, por exemplo, um par de valor-chave. A expressão seguinte exibe o nome de produto de um conjunto de dados (“Produto”), considerando o identificador de produto para correspondência:  
  
    ```  
    =Lookup(Fields!PID.Value, Fields!ProductID.Value, Fields.ProductName.Value, "Product")  
    ```  
  
#### <a name="lookupset"></a>LookupSet  
  
-   Ao especificar um campo de chave, você pode usar o `LookupSet` função para recuperar um conjunto de valores de um conjunto de dados para uma relação um-para-muitos. Por exemplo, uma pessoa pode ter vários números de telefone. No exemplo seguinte, suponha que o conjunto de dados PhoneList contenha um identificador de pessoa e um número de telefone em cada linha. `LookupSet` Retorna uma matriz de valores. A seguinte expressão combina os valores de retorno em uma única cadeia de caracteres e exibe a lista de números de telefone para a pessoa especificada por ContactID:  
  
    ```  
    =Join(LookupSet(Fields!ContactID.Value, Fields!PersonID.Value, Fields!PhoneNumber.Value, "PhoneList"),",")  
    ```  
  
####  <a name="ConversionFunctions"></a> Funções de conversão  
 É possível usar as funções do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] para converter um campo de um tipo de dados em outro tipo de dados. As funções de conversão podem ser usadas para converter um tipo de dados padrão de um campo no tipo de dados necessário para cálculos ou para combinar texto.  
  
-   A expressão a seguir converte a constante 500 para o tipo Decimal a fim de compará-la a um tipo de dados de dinheiro [!INCLUDE[tsql](../../includes/tsql-md.md)] no campo Valor de uma expressão de filtro.  
  
    ```  
    =CDec(500)  
    ```  
  
-   A expressão a seguir exibe o número de valores selecionados para o parâmetro de diversos valores *MySelection*.  
  
    ```  
    =CStr(Parameters!MySelection.Count)  
    ```  
  
####  <a name="DecisionFunctions"></a> Funções de decisão  
  
-   A função `Iif` retorna um de dois valores, dependendo da expressão ser verdadeira ou não. A expressão a seguir usa a função `Iif` para retornar um valor booliano de `True` se o valor de `LineTotal` exceder 100. Caso contrário, ele retornará `False`:  
  
    ```  
    =IIF(Fields!LineTotal.Value > 100, True, False)  
    ```  
  
-   Use várias `IIF` funções (também conhecido como "IIFs aninhadas") para retornar um dos três valores, dependendo do valor de `PctComplete`. A expressão a seguir pode ser colocada na cor de preenchimento de uma caixa de texto para alterar a cor de plano de fundo, dependendo do valor na caixa de texto.  
  
    ```  
    =IIF(Fields!PctComplete.Value >= 10, "Green", IIF(Fields!PctComplete.Value >= 1, "Blue", "Red"))  
    ```  
  
     Valores maiores ou iguais a 10 são exibidos com um plano de fundo verde, entre 1 e 9 são exibidos com um plano de fundo azul e menores do que 1 são exibidos com um plano de fundo vermelho.  
  
-   Uma maneira diferente de obter a mesma funcionalidade usa a `Switch` função. A função `Switch` é útil quando você tem três ou mais condições a serem testadas. A função `Switch` retorna o valor associado à primeira expressão em uma série avaliada como verdadeira:  
  
    ```  
    =Switch(Fields!PctComplete.Value >= 10, "Green", Fields!PctComplete.Value >= 1, "Blue", Fields!PctComplete.Value = 1, "Yellow", Fields!PctComplete.Value <= 0, "Red",)  
    ```  
  
     Valores maiores ou iguais a 10 são exibidos com um plano de fundo verde, entre 1 e 9 são exibidos com um plano de fundo azul, iguais a 1 são exibidos com um plano de fundo amarelo e 0 ou menos são exibidos com um plano de fundo vermelho.  
  
-   Teste o valor do campo `ImportantDate` e retorne "Vermelho", se ele tiver mais de uma semana, caso contrário, "Azul". Esta expressão pode ser usada para controlar a propriedade Cor de uma caixa de texto em um item de relatório:  
  
    ```  
    =IIF(DateDiff("d",Fields!ImportantDate.Value, Now())>7,"Red","Blue")  
    ```  
  
-   Testar o valor da `PhoneNumber` do campo e retorne "Sem valor" se ele estiver `null` (`Nothing` em [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]); caso contrário, retornará o valor do número de telefone. Esta expressão pode ser usada para controlar o valor de uma caixa de texto em um item de relatório.  
  
    ```  
    =IIF(Fields!PhoneNumber.Value Is Nothing,"No Value",Fields!PhoneNumber.Value)  
    ```  
  
-   Testar o valor da `Department` do campo e retornar o nome de um sub-relatório ou um `null` (`Nothing` em [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]). Esta expressão pode ser usada para sub-relatórios detalhados condicional.  
  
    ```  
    =IIF(Fields!Department.Value = "Development", "EmployeeReport", Nothing)  
    ```  
  
-   Teste se o valor de um campo é nulo. Esta expressão pode ser usada para controlar a propriedade `Hidden` de um item de relatório de imagem. No exemplo a seguir, a imagem especificada pelo campo [LargePhoto] será exibida apenas se o valor do campo não for nulo.  
  
    ```  
    =IIF(IsNothing(Fields!LargePhoto.Value),True,False)  
    ```  
  
-   A função `MonthName` retorna um valor de cadeia de caracteres que contém o nome do mês especificado. O exemplo a seguir exibe NA no campo Mês quando o campo contiver o valor de 0.  
  
    ```  
    IIF(Fields!Month.Value=0,"NA",MonthName(IIF(Fields!Month.Value=0,1,Fields!Month.Value)))  
  
    ```  
  
###  <a name="ReportFunctions"></a> Funções de relatórios  
 Em uma expressão, você pode adicionar uma referência a funções de relatório adicionais que manipulam dados em um relatório. Esta seção fornece exemplos de duas dessas funções. Para obter mais informações sobre as funções e exemplos de relatório, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md).  
  
#####  <a name="Sum"></a> Sum  
  
-   O `Sum` função pode somar os valores em um grupo ou região de dados. Essa função pode ser útil no cabeçalho ou no rodapé de um grupo. A expressão a seguir exibe a soma de dados no grupo Ordem ou na região de dados:  
  
    ```  
    =Sum(Fields!LineTotal.Value, "Order")  
    ```  
  
-   Você também pode usar o `Sum` função para cálculos de agregação condicionais. Por exemplo, se um conjunto de dados tiver um campo denominado Estado com valores possíveis Não Iniciado, Iniciado, Concluído, a seguinte expressão, quando colocada em um cabeçalho do grupo, calculará a soma de agregação apenas para o valor Concluído:  
  
    ```  
    =Sum(IIF(Fields!State.Value = "Finished", 1, 0))  
    ```  
  
#####  <a name="RowNumber"></a> RowNumber  
  
-   A função `RowNumber`, quando usada em uma caixa de texto dentro de uma região de dados, exibe o número da linha de cada instância da caixa de texto na qual a expressão é exibida. Essa função pode ser útil para numerar linhas em uma tabela. Ela também pode ser útil para tarefas mais complexas, como fornecer quebras de página baseadas no número de linhas. Para obter mais informações, consulte [Quebras de página](#PageBreaks) neste tópico.  
  
     O escopo especificado para `RowNumber` controla quando a renumeração é iniciada. O `Nothing` palavra-chave indica que a função iniciará a contagem na primeira linha na região de dados externa. Para iniciar a contagem dentro de regiões de dados aninhadas, use o nome da região de dados. Para iniciar a contagem dentro de um grupo, use o nome do grupo.  
  
    ```  
    =RowNumber(Nothing)  
    ```  
  
##  <a name="AppearanceofReportData"></a> Aparência dos dados do relatório  
 É possível usar expressões para manipular como os dados são exibidos em um relatório. Por exemplo, é possível exibir os valores de dois campos em uma única caixa de texto, exibir informações sobre o relatório ou afetar o modo como as quebras de página são inseridas no relatório.  
  
###  <a name="PageHeadersandFooters"></a> Cabeçalhos e rodapés de página  
 Ao criar um relatório, você pode exibir o nome do relatório e o número da página no rodapé. Para fazer isso, você pode usar as expressões a seguir:  
  
-   A seguinte expressão fornece o nome do relatório e a hora em que foi executado. Ela pode ser colocada em uma caixa de texto no rodapé ou no corpo do relatório. A hora é formatada com a cadeia de caracteres de formatação do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] para data abreviada:  
  
    ```  
    =Globals.ReportName & ", dated " & Format(Globals.ExecutionTime, "d")  
    ```  
  
-   A seguinte expressão, colocada em uma caixa de texto no rodapé de um relatório, fornece o número da página e o total de páginas no relatório:  
  
    ```  
    =Globals.PageNumber & " of " & Globals.TotalPages  
    ```  
  
 Os exemplos a seguir descrevem como exibir os primeiros e os últimos valores de uma página no cabeçalho da página, semelhante ao que você pode encontrar em uma listagem de diretório. O exemplo pressupõe uma região de dados que contém uma caixa de texto denominada `LastName`.  
  
-   A expressão a seguir, colocada em uma caixa de texto no lado esquerdo do cabeçalho da página, fornece o primeiro valor da caixa de texto `LastName` na página:  
  
    ```  
    =First(ReportItems("LastName").Value)  
    ```  
  
-   A expressão a seguir, colocada em uma caixa de texto no lado direito do cabeçalho da página, fornece o último valor da caixa de texto `LastName` na página:  
  
    ```  
    =Last(ReportItems("LastName").Value)  
    ```  
  
 O exemplo a seguir descreve como exibir um total de páginas. O exemplo pressupõe uma região de dados que contém uma caixa de texto denominada `Cost`.  
  
-   A expressão a seguir, colocada no cabeçalho ou no rodapé de página, fornece a soma dos valores na caixa de texto `Cost` da página:  
  
    ```  
    =Sum(ReportItems("Cost").Value)  
    ```  
  
> [!NOTE]  
>  Você pode fazer referência a apenas um item de relatório por expressão em um cabeçalho ou rodapé de página. Além disso, é possível fazer referência ao nome da caixa de texto, mas não à expressão de dados reais dentro da caixa de texto, nas expressões de cabeçalho e rodapé de página.  
  
###  <a name="PageBreaks"></a> Quebras de página  
 Em alguns relatórios, você pode desejar colocar uma quebra de página no final de um número de linhas especificado ou, além disso, em grupos ou itens de relatório. Para fazer isso, crie um grupo que contenha os grupos ou registros de detalhes desejados, adicione uma quebra de página ao grupo e adicione uma expressão de grupo ao grupo por um número de linhas especificado.  
  
-   A expressão a seguir, quando colocada na expressão de grupo, atribui um número para cada conjunto de 25 linhas. Quando uma quebra de página é definida para o grupo, essa expressão resulta em uma quebra de página a cada 25 linhas.  
  
    ```  
    =Ceiling(RowNumber(Nothing)/25)  
    ```  
  
     Para permitir que o usuário defina um valor para o número de linhas por página, crie um parâmetro denominado `RowsPerPage` e baseie a expressão de grupo no parâmetro, conforme mostrado na expressão a seguir:  
  
    ```  
    =Ceiling(RowNumber(Nothing)/Parameters!RowsPerPage.Value)  
    ```  
  
     Para obter mais informações sobre como configurar quebras de página para um grupo, consulte [Adicionar uma quebra de página &#40;Construtor de Relatórios e SSRS&#41;](add-a-page-break-report-builder-and-ssrs.md).  
  
##  <a name="Properties"></a> propriedades  
 As expressões não são usadas apenas para exibir dados nas caixas de texto. Elas também podem ser usadas para alterar o modo como as propriedades são aplicadas aos itens do relatório. É possível alterar informações de estilo para um item de relatório ou alterar sua visibilidade.  
  
###  <a name="Formatting"></a> Formatação  
  
-   A expressão a seguir, quando usada na propriedade Color de uma caixa de texto, altera a cor do texto dependendo do valor do campo `Profit` :  
  
    ```  
    =Iif(Fields!Profit.Value < 0, "Red", "Black")  
    ```  
  
     Você também pode usar a variável de objeto [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] do `Me`. Essa variável é outra maneira de fazer referência ao valor de uma caixa de texto.  
  
     `=Iif(Me.Value < 0, "Red", "Black")`  
  
-   A expressão a seguir, quando usada na propriedade BackgroundColor de um item de relatório em uma região de dados, alterna a cor da tela de fundo de cada linha entre verde claro e branco:  
  
    ```  
    =Iif(RowNumber(Nothing) Mod 2, "PaleGreen", "White")  
    ```  
  
     Se você estiver usando uma expressão para um escopo especificado, poderá precisar indicar o conjunto de dados para a função de agregação:  
  
    ```  
    =Iif(RowNumber("Employees") Mod 2, "PaleGreen", "White")  
    ```  
  
> [!NOTE]  
>  As cores disponíveis são provenientes da enumeração de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] KnownColor.  
  
### <a name="chart-colors"></a>Cores dos gráficos  
 Para especificar cores para um gráfico de Forma, você pode usar código personalizado para controlar a ordem em que as cores são mapeadas para valores de pontos de dados. Isso ajuda a usar cores consistentes para vários gráficos que têm os mesmos grupos de categorias. Para obter mais informações, consulte [Especificar cores consistentes em gráficos com várias formas &#40;Construtor de Relatórios e SSRS&#41;](charts-report-builder-and-ssrs.md).  
  
###  <a name="Visibility"></a> Visibilidade  
 Você pode mostrar e ocultar itens em um relatório usando as propriedades de visibilidade para o item de relatório. Em uma região de dados, como uma tabela, é possível ocultar inicialmente as linhas de detalhes com base no valor de uma expressão.  
  
-   A expressão a seguir, quando usada para visibilidade inicial de linhas de detalhes em um grupo, mostra as linhas de detalhes de todas as vendas que excedem 90 por cento no campo `PctQuota` :  
  
    ```  
    =Iif(Fields!PctQuota.Value>.9, False, True)  
    ```  
  
-   A expressão a seguir, quando definida na propriedade Hidden de uma tabela, mostrará a tabela apenas se ela tiver mais de 12 linhas:  
  
    ```  
    =IIF(CountRows()>12,false,true)  
    ```  
  
-   A expressão a seguir, quando definida no `Hidden` propriedade de uma coluna, mostrará a coluna apenas se o campo existir no conjunto de dados do relatório depois que os dados são recuperados da fonte de dados:  
  
    ```  
    =IIF(Fields!Column_1.IsMissing, true, false)  
    ```  
  
###  <a name="Hyperlinks"></a> URLs  
 É possível personalizar URLs usando dados do relatório e também controlar condicionalmente se as URLs são adicionadas como uma ação para uma caixa de texto.  
  
-   A expressão a seguir, quando usada como uma ação em uma caixa de texto, gera uma URL personalizada que especifica o campo do conjunto de dados `EmployeeID` como um parâmetro da URL.  
  
    ```  
    ="http://adventure-works/MyInfo?ID=" & Fields!EmployeeID.Value  
    ```  
  
     Para obter mais informações, consulte [Adicionar um hiperlink a uma URL &#40;Construtor de Relatórios e SSRS&#41;](add-a-hyperlink-to-a-url-report-builder-and-ssrs.md).  
  
-   A expressão a seguir controla condicionalmente se uma URL deve ser adicionada em uma caixa de texto. Essa expressão depende de um parâmetro denominado `IncludeURLs` que permite que um usuário decida se deve incluir URLs ativas em um relatório. Essa expressão é definida como uma ação em uma caixa de texto. Configurando o parâmetro como Falso e exibindo o relatório, você pode exportar o relatório Microsoft Excel sem hiperlinks.  
  
    ```  
    =IIF(Parameters!IncludeURLs.Value,"http://adventure-works.com/productcatalog",Nothing)  
    ```  
  
##  <a name="ReportData"></a> Dados do Relatório  
 As expressões podem ser usadas para manipular os dados usados no relatório. Você pode fazer referência a parâmetros e a outras informações do relatório. É possível até mesmo alterar a consulta usada para recuperar dados para o relatório.  
  
###  <a name="Parameters"></a> Parâmetros  
 É possível usar expressões em um parâmetro para variar o valor padrão do parâmetro. Por exemplo, você pode usar um parâmetro para filtrar dados para um usuário específico baseado na ID do usuário usada para executar o relatório.  
  
-   A expressão a seguir, quando usada com o valor padrão para um parâmetro, coleta a ID do usuário da pessoa que executa o relatório:  
  
    ```  
    =User!UserID  
    ```  
  
-   Para consultar um parâmetro em um parâmetro de consulta, expressão de filtro, caixa de texto ou outra área do relatório, use a coleção global de `Parameters`. Este exemplo supõe que o parâmetro é denominado *Department*:  
  
    ```  
    =Parameters!Department.Value  
    ```  
  
-   Parâmetros podem ser criados em um relatório, mas definidos como ocultos. Quando o relatório é executado no servidor de relatório, o parâmetro não é exibido na barra de ferramentas e o leitor de relatório não pode alterar o valor padrão. É possível usar um parâmetro oculto, definido como um valor padrão, como uma constante personalizada. É possível usar esse valor em qualquer expressão, incluindo uma expressão de campo. A expressão a seguir identifica o campo especificado pelo valor do parâmetro padrão para o parâmetro denominado *ParameterField*:  
  
    ```  
    =Fields(Parameters!ParameterField.Value).Value  
    ```  
  
##  <a name="CustomCode"></a> Código Personalizado  
 É possível usar código personalizado em um relatório. O código personalizado é inserido em um relatório ou armazenado em um assembly personalizado que é usado no relatório. Para obter mais informações sobre o código personalizado, consulte [Referências a código personalizado e assemblies em expressões no Designer de Relatórios &#40;SSRS&#41;](custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
### <a name="using-group-variables-for-custom-aggregation"></a>Usando variáveis de grupo para agregação personalizada  
 Você pode inicializar o valor para uma variável de grupo que é local para um escopo de grupo específico e depois incluir uma referência a essa variável nas expressões. Um dos modos pelos quais é possível usar uma variável de grupo com código personalizado é implementar uma agregação personalizada. Para obter mais informações, consulte [Usando variáveis de grupo no Reporting Services 2008 para agregação personalizada](http://go.microsoft.com/fwlink/?LinkId=128714).  
  
 Para obter mais informações sobre variáveis, consulte [relatório e referências de coleções de variáveis de grupo &#40;construtor de relatórios e SSRS&#41;](built-in-collections-report-and-group-variables-references-report-builder.md).  
  
## <a name="suppressing-null-or-zero-values-at-run-time"></a>Suprimindo valores nulos ou zero em tempo de execução  
 Alguns valores em uma expressão podem ser avaliados como nulos ou indefinidos na hora do processamento do relatório. Isso pode criar erros de tempo de execução que resultam em **#Erro** exibidos na caixa de texto em vez da expressão avaliada. A função `IIF` é particularmente sensível a esse comportamento porque, ao contrário de uma instrução If-Then-Else, cada parte da instrução `IIF` é avaliada (incluindo chamadas de função) antes de ser passada para a rotina que é testada como `true` ou `false`. A instrução `=IIF(Fields!Sales.Value is NOTHING, 0, Fields!Sales.Value)` gerará **#Erro** no relatório renderizado se `Fields!Sales.Value` for NOTHING.  
  
 Para evitar essa condição, use uma das seguintes estratégias:  
  
-   Defina o numerador como 0 e o denominador como 1, se o valor do campo B for 0 ou indefinido. Caso contrário defina o numerador como o valor do campo A e o denominador como o valor do campo B.  
  
    ```  
    =IIF(Field!B.Value=0, 0, Field!A.Value / IIF(Field!B.Value =0, 1, Field!B.Value))  
    ```  
  
-   Use uma função de código personalizado para retornar o valor da expressão. O exemplo a seguir retorna a diferença da porcentagem entre um valor atual e um valor anterior. Isso pode ser usado para calcular a diferença entre quaisquer dois valores sucessivos e trata o caso de borda da primeira comparação (quando não há valor anterior) e casos em que o valor anterior ou o valor atual é `null` (`Nothing` no [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]).  
  
    ```  
    Public Function GetDeltaPercentage(ByVal PreviousValue, ByVal CurrentValue) As Object  
        If IsNothing(PreviousValue) OR IsNothing(CurrentValue) Then  
            Return Nothing  
        Else if PreviousValue = 0 OR CurrentValue = 0 Then  
            Return Nothing  
        Else   
            Return (CurrentValue - PreviousValue) / CurrentValue  
        End If  
    End Function  
    ```  
  
     A expressão a seguir mostra como chamar esse código personalizado de uma caixa de texto, para o contêiner “ColumnGroupByYear” (grupo ou região de dados).  
  
    ```  
    =Code.GetDeltaPercentage(Previous(Sum(Fields!Sales.Value),"ColumnGroupByYear"), Sum(Fields!Sales.Value))  
    ```  
  
     Isso ajuda a evitar exceções em tempo de execução. Agora você pode usar uma expressão como `=IIF(Me.Value < 0, "red", "black")` na propriedade `Color` da caixa de texto para exibição condicional do texto, dependendo se os valores são maiores que ou menores que 0.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplos de equações de filtro &#40;relatórios e SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md)   
 [Exemplos de expressões de grupo &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Usos de expressões em relatórios &#40;relatórios e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Filtros geralmente usados &#40;relatórios e SSRS&#41;](commonly-used-filters-report-builder-and-ssrs.md)  
  
  

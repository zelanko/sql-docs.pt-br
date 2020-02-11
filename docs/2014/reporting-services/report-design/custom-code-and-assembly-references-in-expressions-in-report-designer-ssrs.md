---
title: Referências de código personalizado e assemblies em expressões no Designer de Relatórios (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- items [Reporting Services], expressions
- data [Reporting Services], expressions
- expressions [Reporting Services], about expressions
- expressions [Reporting Services]
- SSRS, expressions
- formulas [Reporting Services]
- data manipulation [Reporting Services]
- SQL Server Reporting Services, expressions
ms.assetid: ae8a0166-2ccc-45f4-8d28-c150da7b73de
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: df09ab032929de0eca51c9640f5c5cb23d1cde21
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66106104"
---
# <a name="custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs"></a>Referências a código personalizado e assemblies em expressões no Designer de Relatórios (SSRS)
  É possível adicionar referências ao código personalizado inserido em um relatório ou aos assemblies personalizados criados e salvos em seu computador e implantá-los no servidor de relatório. Use o código inserido para constantes personalizadas, funções complexas ou funções usadas várias vezes em um mesmo relatório. Use assemblies de código personalizado para manter o código em um único local e compartilhá-lo para uso em vários relatórios. O código personalizado pode incluir novas constantes, variáveis, funções ou sub-rotinas personalizadas. É possível incluir referências somente leitura em coleções internas, como a coleção de Parâmetros. No entanto, não é possível passar conjuntos de valores de dados do relatório para funções personalizadas. Especificamente, não há suporte para agregações personalizadas.  
  
> [!IMPORTANT]  
>  Para cálculos de detecção de hora avaliados uma vez em tempo de execução que você deseja manter com o mesmo valor ao longo do processamento do relatório, considere se uma variável de relatório ou uma variável de grupo deve ser usada. Para obter mais informações, consulte [Referências de coleções de variáveis de grupo e de relatório &#40;Construtor de Relatórios e SSRS&#41;](built-in-collections-report-and-group-variables-references-report-builder.md).  
  
 O Designer de Relatórios é o ambiente de criação preferido a ser usado para adicionar código personalizado a um relatório. O Construtor de Relatórios dá suporte ao processamento de relatórios que têm expressões válidas ou que incluem referências a assemblies personalizados em um servidor de relatório. O Construtor de Relatórios não fornece uma maneira de adicionar uma referência a um assembly personalizado.  
  
> [!NOTE]  
>  Lembre-se de que, durante uma atualização de um servidor de relatório, os relatórios que dependem de assemblies personalizados podem exigir etapas adicionais para concluir a atualização. Para obter mais informações, consulte [Use Upgrade Advisor to Prepare for Upgrades](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="RB3"></a>Trabalhando com código personalizado no Construtor de Relatórios  
 No Construtor de Relatórios, você pode abrir um relatório em um servidor de relatório que inclua referências a assemblies personalizados. Por exemplo, você pode editar relatórios que são criados e implantados no Designer de Relatórios no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Os assemblies personalizados devem ser implantados no servidor de relatório.  
  
 Não é possível fazer o seguinte:  
  
1.  Adicionar referências ou instâncias de membro de classe a um relatório.  
  
2.  Visualizar um relatório com referências a assemblies personalizados no modo local.  
  
##  <a name="Common"></a>Incluindo referências a funções comumente usadas  
 Use a caixa de diálogo **Expressão** para exibir uma lista categorizada de funções comuns internas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Quando você expande **Funções Comuns** e clica em uma categoria, o painel **Item** exibe a lista de funções incluídas em uma expressão. As funções comuns incluem classes dos [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] <xref:System.Math> <xref:System.Convert> namespaces e das funções [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] de biblioteca de tempo de execução. Por conveniência, é possível exibir as funções usadas mais frequentemente na caixa de diálogo **Expressão** , onde elas são listadas por categoria: Texto, Data e Hora, Matemática, Inspeção, Fluxo do Programa, Agregação, Financeira, Conversão e Diversas. As funções usadas com menor frequência não são exibidas na lista, mas ainda podem ser usadas em uma expressão.  
  
 Para usar uma função interna, clique duas vezes no nome da função no painel Item. Uma descrição da função é exibida no painel Descrição e um exemplo de chamada da função é exibido no painel Exemplo. No painel de código, quando você digita o nome da função seguido por um parêntese esquerdo **(**, a ajuda do IntelliSense exibe cada sintaxe válida para a chamada de função. Por exemplo, para calcular o valor máximo de um campo denominado `Quantity` em uma tabela, adicione a expressão simples `=Max(` ao painel Código e use as marcas inteligentes para exibir todas as sintaxes válidas possíveis para a chamada da função. Para concluir este exemplo, digite `=Max(Fields!Quantity.Value)`.  
  
 Para obter mais informações sobre cada função, consulte <xref:System.Math>, <xref:System.Convert>e [Membros da Biblioteca de Runtime do Visual Basic](https://go.microsoft.com/fwlink/?LinkId=198941) no MSDN.  
  
##  <a name="NotCommon"></a>Incluindo referências a funções usadas com menos frequência  
 Para incluir uma referência em outros namespaces de CLR usados com menor frequência, você deve usar uma referência totalmente qualificada, por exemplo, <xref:System.Text.StringBuilder>. O IntelliSense não tem suporte no painel de código da caixa de diálogo **Expressão** para essas funções usadas com menor frequência.  
  
 Para obter mais informações, confira [Membros da Biblioteca de Runtime do Visual Basic](https://go.microsoft.com/fwlink/?LinkId=198941) no MSDN.  
  
##  <a name="External"></a>Incluindo referências a assemblies externos  
 Para incluir uma referência em uma classe em um assembly externo, você deve identificar o assembly para o processador de relatório. Use a página **Referências** da caixa de diálogo **Propriedades do Relatório** para especificar o nome totalmente qualificado do assembly a ser adicionado ao relatório. Na expressão, você deve usar o nome totalmente qualificado para a classe no assembly. As classes em um assembly externo não são exibidas na caixa de diálogo **Expressão** . Você deve fornecer o nome correto para a classe. Um nome totalmente qualificado inclui o namespace, o nome da classe e o nome do membro.  
  
##  <a name="Embedded"></a>Incluindo código inserido  
 Para adicionar código inserido a um relatório, use a guia Código da caixa de diálogo **Propriedades do Relatório** . O bloco de código criado pode conter vários métodos. Os métodos no código inserido devem ser gravados [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] e devem ser baseados em instância. O processador de relatório adiciona referências automaticamente para os namespaces System.Convert e System.Math. Use a página **Referências** da caixa de diálogo **Propriedades do Relatório** para adicionar referências adicionais do assembly. Para obter mais informações, consulte [Adicionar uma referência de assembly a um relatório &#40;SSRS&#41;](add-an-assembly-reference-to-a-report-ssrs.md).  
  
 Os métodos no código inserido são disponibilizados por meio de um membro do `Code` definido globalmente. Você os acessa consultando o membro do `Code` e o nome do método. O exemplo a seguir chama o método `ToUSD` que converte o valor no campo `StandardCost` para um valor em dólar:  
  
```  
=Code.ToUSD(Fields!StandardCost.Value)  
```  
  
 Para fazer referência às coleções internas no código personalizado, inclua uma referência no objeto `Report` interno:  
  
```  
=Report.Parameters!Param1.Value  
```  
  
 Os exemplos a seguir mostram como definir algumas constantes e variáveis personalizadas.  
  
```  
Public Const MyNote = "Authored by Bob"  
Public Const NCopies As Int32 = 2  
Public Dim  MyVersion As String = "123.456"  
Public Dim MyDoubleVersion As Double = 123.456  
```  
  
 Embora as constantes personalizadas não apareçam na categoria de **Constantes** na caixa de diálogo **Expressão** (que exibe apenas constantes internas), é possível adicionar referências a elas por meio de qualquer expressão, conforme mostrado nos exemplos a seguir. Em uma expressão, uma constante personalizada é tratada como uma `Variant`.  
  
```  
=Code.MyNote  
=Code.NCopies  
=Code.MyVersion  
=Code.MyDoubleVersion  
```  
  
 O exemplo a seguir inclui a referência e a implementação de código da função `FixSpelling` que substitui o texto `"Bicycle"` para todas as ocorrências do texto "Bike" no campo `SubCategory`.  
  
 `=Code.FixSpelling(Fields!SubCategory.Value)`  
  
 O código a seguir, quando inserido em um bloco de código de definição de relatório, mostra uma implementação do método `FixSpelling`. Este exemplo mostra como usar uma referência totalmente qualificada para a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] `StringBuilder` classe.  
  
```vb  
Public Function FixSpelling(ByVal s As String) As String  
   Dim strBuilder As New System.Text.StringBuilder(s)  
   If s.Contains("Bike") Then  
      strBuilder.Replace("Bike", "Bicycle")  
      Return strBuilder.ToString()  
      Else : Return s  
   End If  
End Function  
```  
  
 Para obter mais informações sobre coleções de objetos internos e inicialização, consulte [Referências globais internas e referências de usuários &#40;Construtor de Relatórios e SSRS&#41;](built-in-collections-built-in-globals-and-users-references-report-builder.md) e [Inicializando objetos Assembly personalizados](../custom-assemblies/initializing-custom-assembly-objects.md).  
  
##  <a name="Parameters"></a>Incluindo referências a parâmetros do código  
 É possível fazer referência à coleção de parâmetros globais por meio de código personalizado em um bloco de código da definição do relatório ou em um assembly personalizado fornecido. A coleção de parâmetros é somente leitura e não possui iteradores públicos. Você não pode usar [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] `For Each` uma construção para percorrer a coleção. É preciso saber o nome do parâmetro definido na definição de relatório antes de referenciá-lo no código. No entanto, é possível iterar através de todos os valores de um parâmetro de vários valores.  
  
 A tabela a seguir inclui exemplos de como fazer referência à coleção interna de `Parameters` no código personalizado:  
  
|DESCRIÇÃO|Referência em expressão|Definição de código personalizado|  
|-----------------|-----------------------------|----------------------------|  
|Passando uma coleção de parâmetros globais inteira para código personalizado.<br /><br /> Esta função retorna o valor de um parâmetro de relatório específico *MyParameter*.|`=Code.DisplayAParameterValue(Parameters)`|`Public Function DisplayAParameterValue(`<br /><br /> `ByVal parameters as Parameters) as Object`<br /><br /> `Return parameters("MyParameter").Value`<br /><br /> `End Function`|  
|Passando um parâmetro individual para código personalizado.<br /><br /> Este exemplo retorna o valor do parâmetro passado. Se o parâmetro for um parâmetro de vários valores, a cadeia de caracteres de retorno será uma concatenação de todos os valores.|`=Code.ShowParametersValues(Parameters!DayOfTheWeek)`|`Public Function ShowParameterValues(ByVal parameter as Parameter)` <br />  `as String` <br /> `Dim s as String`  <br />  `If parameter.IsMultiValue then` <br />  `s = "Multivalue: "`  <br /> `For i as integer = 0 to parameter.Count-1` <br />  `s = s + CStr(parameter.Value(i)) + " "`  <br />  `Next` <br /> `Else` <br /> `s = "Single value: " + CStr(parameter.Value)` <br /> `End If` <br />  `Return s` <br /> `End Function`|  
  
##  <a name="Custom"></a>Incluindo referências a código de assemblies personalizados  
 Para usar assemblies personalizados em um relatório, você deve primeiro criar o assembly, torná-lo disponível para o Designer de Relatórios, adicionar uma referência ao assembly no relatório e usar uma expressão no relatório para fazer referência aos métodos contidos nesse assembly. Quando o relatório é implantado no servidor de relatório, você deve também implantar o assembly personalizado no servidor de relatório.  
  
 Para obter informações sobre como criar um assembly personalizado e torná-lo disponível para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], consulte [Usando assemblies personalizados com relatórios](../custom-assemblies/using-custom-assemblies-with-reports.md).  
  
 Para consultar o código personalizado em uma expressão, você deve chamar o membro de uma classe dentro do assembly. A maneira de fazer isso depende do método ser estático ou baseado em instância. Os métodos estáticos dentro de um assembly personalizado estão disponíveis globalmente dentro do relatório. É possível acessar métodos estáticos em expressões especificando o namespace, a classe e o nome do método. O exemplo a seguir chama o `ToGBP`método, que converte o valor do valor **StandardCost** de dólar para libras esterlinas:  
  
```  
=CurrencyConversion.DollarCurrencyConversion.ToGBP(Fields!StandardCost.Value)  
```  
  
 Os métodos baseados em instância estão disponíveis por meio de um membro do `Code` definido globalmente. Você os acessa fazendo referência ao membro do `Code`, seguido pelo nome da instância e do método. O exemplo a seguir chama o método `ToEUR`de instância, que converte o valor de **StandardCost** de dólar em euro:  
  
```  
=Code.m_myDollarCoversion.ToEUR(Fields!StandardCost.Value)  
```  
  
> [!NOTE]  
>  No Designer de Relatório, um assembly personalizado é carregado uma vez e não é descarregado até que o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]seja fechado. Se você visualizar um relatório, fizer alterações em um assembly personalizado usado no relatório e visualizar o relatório novamente, as alterações não serão exibidas na segunda visualização. Para recarregar o assembly, feche e abra o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] novamente e visualize o relatório.  
  
 Para obter mais informações sobre como acessar o código, consulte [Accessing Custom Assemblies Through Expressions](../custom-assemblies/accessing-custom-assemblies-through-expressions.md).  
  
##  <a name="collections"></a>Passando coleções internas para assemblies personalizados  
 Se você deseja passar coleções internas, como *Globals* ou *Parameters* , em um assembly personalizado para processamento, você deve adicionar uma referência de assembly no projeto de código ao assembly que define as coleções internas e acessar o namespace correto. O assembly que você precisará referenciar será diferente dependendo da finalidade para a qual você está desenvolvendo o assembly personalizado: para um relatório executado em um servidor de relatórios (relatório do servidor) ou um relatório executado localmente em um aplicativo .NET (relatório local). Confira os detalhes abaixo.  
  
-   **Namespace:** Microsoft. ReportingServices. ReportProcessing. ReportObjectModel  
  
-   **Assembly (relatório local):** Microsoft. ReportingServices. ProcessingObjectModel. dll  
  
-   **Assembly (relatório do servidor):** Microsoft. ReportViewer. ProcessingObjectModel. dll  
  
 Como o conteúdo das coleções *Fields* e *ReportItems* pode ser alterado dinamicamente em runtime, você não deverá retê-las durante as chamadas no assembly personalizado (por exemplo, em uma variável de membro). A mesma recomendação geralmente se aplica a todas as coleções internas.  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar código a um relatório &#40;SSRS&#41;](add-code-to-a-report-ssrs.md)   
 [Usando assemblies personalizados com relatórios](../custom-assemblies/using-custom-assemblies-with-reports.md)   
 [Adicionar uma referência de assembly a um relatório &#40;SSRS&#41;](add-an-assembly-reference-to-a-report-ssrs.md)   
 [Reporting Services tutoriais &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Exemplos de relatório (Construtor de Relatórios e SSRS)](https://go.microsoft.com/fwlink/?LinkId=198283)  
  
  

---
title: Tipos de dados em expressões (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 94fdf921-270c-4c12-87b3-46b1cc98fae5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 86aa646865ecfe3da6ed1ad4bacb75907ab39472
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/09/2019
ms.locfileid: "68891862"
---
# <a name="data-types-in-expressions-report-builder-and-ssrs"></a>Tipos de dados em expressões (Construtor de Relatórios e SSRS)
  Os tipos de dados representam tipos diferentes de dados de forma que eles possam ser armazenados e processados com eficiência. Tipos de dados comuns incluem texto (também conhecido como cadeias de caracteres) com e sem casas decimais, datas e horas e imagens. Os valores em um relatório devem ser um tipo de dados RDL. Você pode formatar um valor de acordo com sua preferência ao exibi-lo em um relatório. Por exemplo, um campo que representa moeda pode ser armazenado na definição de relatório como um número de ponto flutuante, mas pode ser exibido em uma variedade de formatos, dependendo da propriedade de formato escolhida.  
  
 Para obter mais informações sobre formatos de exibição, consulte [Formatando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](formatting-report-items-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-definition-language-rdl-data-types-and-common-language-runtime-clr-data-types"></a>Tipos de dados RDL e CLR  
 Valores que são especificados em um arquivo RDL devem ser um tipo de dados RDL. Quando o relatório é compilado e processado, os tipos de dados RDL são convertidos em tipos de dados CLR. A seguinte tabela exibe a conversão, que é marcada como Padrão:  
  
|Tipo RDL|Tipos CLR|  
|--------------|---------------|  
|Cadeia de caracteres|Padrão: Cadeia de caracteres<br /><br /> Chart, GUID, Timespan|  
|Boolean|Padrão: Boolean|  
|Inteiro|Padrão: Int64<br /><br /> Int16, Int32, Uint16, Uint64, Byte, Sbyte|  
|DateTime|Padrão: DateTime<br /><br /> DateTimeOffset|  
|Float|Padrão: Double<br /><br /> Single, Decimal|  
|Binary|Padrão: Byte[]|  
|Variante|Qualquer um dos itens acima, exceto Byte[]|  
|VariantArray|Matriz de Variant|  
|Serializável|Variação ou tipos marcados com Serializable ou que implementam ISerializable.|  
  
## <a name="understanding-data-types-and-writing-expressions"></a>Entendendo tipos de dados e escrevendo expressões  
 É importante entender os tipos de dados quando você grava expressões para comparar ou combinar valores; por exemplo, quando você define expressões de grupo ou filtro ou calcular agregações. As comparações e os cálculos são válidos somente entre itens do mesmo tipo de dados. Se os tipos de dados não coincidirem, você deverá converter explicitamente o tipo de dados no item de relatório usando uma expressão.  
  
 A lista a seguir descreve os casos quando você precisa converter os dados em um tipo de dados diferente:  
  
-   Comparando o valor de um parâmetro de relatório de um tipo de dados a um campo de conjunto de dados de um tipo de dados diferente.  
  
-   Escrevendo expressões de filtro que compõem valores de tipos de dados diferentes.  
  
-   Escrevendo expressões de classificação que combinam campos de tipos de dados diferentes.  
  
-   Escrevendo expressões de grupo que combinam campos de tipos de dados diferentes.  
  
-   Convertendo um valor recuperado da fonte de dados de um tipo de dados para um tipo de dados diferente.  
  
## <a name="determining-the-data-type-of-report-data"></a>Determinando o tipo de dados dos dados do relatório  
 Para determinar o tipo de dados de um item de relatório, você pode gravar uma expressão que retorne seu tipo de dados. Por exemplo, para mostrar o tipo de dados para o campo `MyField`, adicione a seguinte expressão a uma célula de tabela: `=Fields!MyField.Value.GetType().ToString()`. O resultado exibe o tipo de dados CLR usado para representar `MyField`, por exemplo, `System.String` ou `System.DateTime`.  
  
## <a name="converting-dataset-fields-to-a-different-data-type"></a>Convertendo campos de conjunto de dados em um tipo de dados diferente  
 Você também pode converter os campos de conjunto de dados antes de usá-los em um relatório. A lista a seguir descreve as maneiras que você pode converter um campo de conjunto de dados existente:  
  
-   Modifique a consulta do conjunto de dados para adicionar um novo campo de consulta com os dados convertidos. Para as fontes de dados relacionais ou multidimensionais, isso usa os recursos de origem de dados para executar a conversão.  
  
-   Crie um campo calculado com base em um campo de conjunto de dados de relatório existente, escrevendo uma expressão que converta todos os dados em uma coluna de conjunto de resultados em uma nova coluna com um tipo de dados diferente. Por exemplo, a expressão seguir converte o campo Ano de um valor inteiro para um valor de cadeia: `=CStr(Fields!Year.Value)`. Para saber mais, confira [Adicionar, editar e atualizar campos no painel de dados do relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).  
  
-   Verifique se a extensão de processamento de dados que você está usando inclui metadados para recuperar dados pré-formatados. Por exemplo, uma consulta MDX [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] inclui a propriedade estendida FORMATTED_VALUE para valores de cubo que já foram formatados ao processar o cubo. Para obter mais informações, consulte [Propriedades de campos estendidos para um banco de dados do Analysis Services &#40;SSRS&#41;](../report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md).  
  
## <a name="understanding-parameter-data-types"></a>Entendendo os tipos de dados de parâmetro  
 Os parâmetros de relatório devem ser um dos cinco tipos de dados: Booliano, DateTime, Inteiro, Float ou Texto (também chamado de Cadeia de caracteres). Quando sua consulta de conjunto de dados inclui parâmetros de consulta, os parâmetros de relatório são criados automaticamente e vinculados a parâmetros de consulta. O tipo de dados padrão para um parâmetro de relatório é String. Para alterar o tipo de dados padrão de um parâmetro de relatório, selecione o valor correto da lista suspensa **Tipo de dados** na página **Geral** da caixa de diálogo **Propriedades do Parâmetro de Relatórios** .  
  
> [!NOTE]  
>  Os parâmetros de relatório que são tipos de dados DateTime não oferecem suporte a milissegundos. Embora você possa criar um parâmetro com base em valores que incluem milissegundos, você não pode selecionar um valor a partir de uma lista suspensa de valores disponíveis que inclui valores de Data e Hora que incluem milissegundos.  
  
## <a name="writing-expressions-that-convert-data-types-or-extract-parts-of-data"></a>Escrevendo expressões que convertem tipos de dados ou extraem partes de dados  
 Quando você combina campos de texto e conjunto de dados usando o operador de concatenação (&), o CLR (Common Language Runtime) geralmente fornece os formatos padrão. Quando você precisa converter explicitamente um parâmetro ou campo de conjunto de dados em um tipo de dados específico, você deve usar um método CLR ou uma função de biblioteca em tempo de execução do Visual Basic para converter os dados.  
  
 A tabela a seguir mostra exemplos de conversão de tipos de dados.  
  
|Tipo de conversão|Exemplo|  
|------------------------|-------------|  
|DateTime para String|`=CStr(Fields!Date.Value)`|  
|String para DateTime|`=DateTime.Parse(Fields!DateTimeinStringFormat.Value)`|  
|String para DateTimeOffset|`=DateTimeOffset.Parse(Fields!DateTimeOffsetinStringFormat.Value)`|  
|Extraindo o ano|`=Year(Fields!TimeinStringFormat.Value)`<br /><br /> `-- or --`<br /><br /> `=Year(Fields!TimeinDateTimeFormat.Value)`|  
|Booleano para Integer|`=CInt(Parameters!BooleanField.Value)`<br /><br /> \- 1 é verdadeiro e 0 é falso.|  
|Booleano para Integer|`=System.Convert.ToInt32(Fields!BooleanFormat.Value)`<br /><br /> 1 é verdadeiro e 0 é falso.|  
|Apenas a parte DateTime do valor DateTimeOffset|`=Fields!MyDatetimeOffset.Value.DateTime`|  
|Apenas a parte Offset do valor DateTimeOffset|`=Fields!MyDatetimeOffset.Value.Offset`|  
  
 Você também pode usar a função Formatar para controlar o formato de exibição do valor. Para obter mais informações, consulte [Funções (Visual Basic)](https://go.microsoft.com/fwlink/?linkid=111483).  
  
## <a name="advanced-examples"></a>Exemplos avançados  
 Quando você se conecta a uma fonte de dados com um provedor de dados que não fornece suporte à conversão para todos os tipos de dados dessa fonte de dados, o tipo de dados padrão para tipos de dados não suportados é String. Os exemplos a seguir fornecem soluções para tipos de dados específicos retornados como uma cadeia.  
  
### <a name="concatenating-a-string-and-a-clr-datetimeoffset-data-type"></a>Concatenando um tipo de dados String e um DateTimeOffset CLR  
 Para a maioria dos tipos de dados, o CLR fornece conversões padrão para que você possa concatenar valores que são de tipos de dados diferentes em uma cadeia, usando o operador &. Por exemplo, a expressão a seguir concatena o texto "A data e hora são:" com um campo de conjunto de dados StartDate, que é um valor <xref:System.DateTime> : `="The date and time are: " & Fields!StartDate.Value`.  
  
 Para alguns tipos de dados, talvez você precise incluir a função ToString. Por exemplo, a expressão a seguir mostra o mesmo exemplo usando o tipo de dados CLR <xref:System.DateTimeOffset>, que inclui a data, a hora e o deslocamento de fuso horário relativo ao fuso horário UTC: `="The time is: " & Fields!StartDate.Value.ToString()`.  
  
### <a name="converting-a-string-data-type-to-a-clr-datetime-data-type"></a>Convertendo um tipo de dados String em um tipo de dados DateTime CLR  
 Se uma extensão de processamento de dados não oferecer suporte a todos os tipos de dados definidos em uma fonte de dados, os dados poderão ser recuperados como texto. Por exemplo, um valor de tipo de dados `datetimeoffset(7)` pode ser recuperado como um tipo de dados String. Em Perth, Austrália, o valor da cadeia para 1º de julho de 2008, às 6:05:07,9999999 AM. seria semelhante a:  
  
 `2008-07-01 06:05:07.9999999 +08:00`  
  
 Este exemplo mostra a data (1º de julho de 2008), seguida pela hora com uma precisão de 7 dígitos (6:05:07.9999999 AM), seguida pelo deslocamento de fuso horário UTC em horas e minutos (mais 8 horas, 0 minutos). Para os exemplos a seguir, este valor foi colocado em um campo `String` chamado `MyDateTime.Value`.  
  
 Você pode usar uma das seguintes estratégias para converter esses dados para um ou mais valores CLR:  
  
-   Em uma caixa de texto, use uma expressão para extrair partes da cadeia. Por exemplo:  
  
    -   A expressão a seguir extrai apenas a parte da hora do deslocamento de fuso horário UTC e converte-a em minutos: `=CInt(Fields!MyDateTime.Value.Substring(Fields!MyDateTime.Value.Length-5,2)) * 60`  
  
         O resultado é `480`.  
  
    -   A expressão a seguir converte a cadeia em um valor de data e hora: `=DateTime.Parse(Fields!MyDateTime.Value)`  
  
         Se a cadeia `MyDateTime.Value` tiver um deslocamento UTC, a função `DateTime.Parse` primeiro se ajustará para o deslocamento UTC (7 AM - [`+08:00`] para a hora UTC de 11 PM. da noite anterior). A função `DateTime.Parse` então aplicará o deslocamento UTC do servidor de relatórios local e, se necessário, ajustará a hora novamente para o Horário de Verão. Por exemplo, em Redmond, Washington, o deslocamento de horário local ajustado para o Horário de Verão é `[-07:00]`ou 7 horas antes de 11 PM. O resultado é o seguinte `DateTime` valor: `2007-07-06 04:07:07 PM` (6 de julho de 2007 às 16:07).  
  
 Para obter mais informações sobre como converter `DateTime` cadeias de caracteres em tipos de dados, consulte Analisando cadeias de [caracteres de data e hora](https://go.microsoft.com/fwlink/?LinkId=89703), [Formatando data e hora para uma cultura específica](https://go.microsoft.com/fwlink/?LinkId=89704)e [escolhendo entre DateTime, DateTimeOffset e TimeZoneInfo](https://go.microsoft.com/fwlink/?linkid=110652) em Inglês.  
  
-   Adicione um novo campo calculado ao conjunto de dados de relatório que use uma expressão para extrair partes da cadeia. Para saber mais, confira [Adicionar, editar e atualizar campos no painel de dados do relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-data/add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs.md).  
  
-   Altere a consulta do conjunto de dados do relatório para usar as funções [!INCLUDE[tsql](../../includes/tsql-md.md)] para extrair os valores de data e hora independentemente para criar colunas separadas. O exemplo a seguir mostra como usar a função `DatePart` para adicionar uma coluna para o ano e um coluna para o fuso horário UTC convertido em minutos:  
  
     `SELECT`  
  
     `MyDateTime,`  
  
     `DATEPART(year, MyDateTime) AS Year,`  
  
     `DATEPART(tz, MyDateTime) AS OffsetinMinutes`  
  
     `FROM MyDates`  
  
     O conjunto de resultados tem três colunas. A primeira coluna é a data e hora, a segunda coluna é o ano e a terceira é o deslocamento UTC em minutos. A linha a seguir mostra os dados de exemplo:  
  
     `2008-07-01 06:05:07             2008                   480`  
  
 Para obter mais informações sobre tipos de dados do banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql) e [Tipos e funções de dados de data e hora &#40;Transact-SQL&#41;](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql) em [Manuais Online do SQL Server](https://go.microsoft.com/fwlink/?linkid=120955).  
  
 Para obter mais emformações sobre tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , consulte [Tipos de dados no Analysis Services](https://docs.microsoft.com/analysis-services/multidimensional-models/olap-physical/data-types-in-analysis-services) em [SQL Server Books Onleme](https://go.microsoft.com/fwlink/?linkid=120955).  
  
## <a name="see-also"></a>Consulte também  
 [Formatando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](formatting-report-items-report-builder-and-ssrs.md)  
  
  

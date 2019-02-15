---
title: Referências de coleções de campos de conjuntos de dados (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 006c6bd3-d776-4c20-9092-32e40688ac49
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: d4717b1f8a905576d2f59657fd8ae8ad00396e3b
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56297424"
---
# <a name="dataset-fields-collection-references-report-builder-and-ssrs"></a>Referências de coleções de campos de conjuntos de dados (Construtor de Relatórios e SSRS)
  Cada conjunto de dados de um relatório contém uma coleção Fields. A coleção Fields é o conjunto de campos especificado pela consulta do conjunto de dados, além de qualquer campo calculado adicional que você criar. Assim que você criar um conjunto de dados, a coleção de campos aparecerá no painel **Dados do Relatório** .  
  
 Uma referência de campo simples em uma expressão é exibida na superfície de design como uma expressão simples. Por exemplo, quando você arrasta o campo `Sales` do painel de dados do relatório para uma célula de tabela na superfície de design, o `[Sales]` é exibido. Isso representa a expressão subjacente `=Fields!Sales.Value` definida na propriedade Value da caixa de texto. Quando o relatório for executado, o processador de relatório avaliará essa expressão e exibirá os dados reais a partir da fonte de dados na caixa de texto da célula de tabela. Para obter mais informações, consulte [Expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md) e [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](../report-data/dataset-fields-collection-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="displaying-the-field-collection-for-a-dataset"></a>Exibindo a coleção de campos de um conjunto de dados  
 Para exibir os valores individuais de uma coleção de dados, arraste cada campo para uma linha de detalhes da tabela e execute o relatório. Referências provenientes da linha de detalhes de uma tabela ou da região de dados da lista exibem um valor para cada linha do conjunto de dados.  
  
 Para exibir valores resumidos para o campo, arraste cada campo numérico para a área de dados de uma matriz. A função de agregação padrão de total da linha é Sum, por exemplo, `=Sum(Fields!Sales.Value)`. Você também pode alterar a função padrão para calcular outros totais. Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md).  
  
 Para exibir valores resumidos de uma coleção de campos em uma caixa de texto diretamente na superfície de design (não parte de uma região de dados), especifique o nome do conjunto de dados como um escopo da função de agregação. Por exemplo, para um conjunto de dados chamado `SalesData`, a expressão a seguir especifica o total de todos os valores do campo `Sales`: `=Sum(Fields!Sales,"SalesData")`.  
  
 Quando você usa a caixa de diálogo **Expressão** para definir uma referência de campo simples, é possível selecionar a coleção Fields no painel Categoria e ver a lista de campos disponíveis no painel **Campo** . Cada campo tem várias propriedades, incluindo o Value e IsMissing. As demais propriedades são propriedades de campo estendidas predefinidas que podem estar disponíveis para o conjunto de dados, dependendo do tipo de fonte de dados.  
  
### <a name="detecting-nulls-for-a-dataset-field"></a>Detectando nulos para um campo do conjunto de dados  
 Para detectar se o valor de um campo é nulo (`Nothing` em [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]), use a função `IsNothing`. Se ela for incluída em uma caixa de texto de uma linha de detalhes de tabela, a expressão a seguir testará o campo `MiddleName` e substituirá o texto "No Middle Name" quando o valor for nulo e o próprio valor do campo quando esse valor não for nulo:  
  
 `=IIF(IsNothing(Fields!MiddleName.Value),"No Middle Name",Fields!MiddleName.Value)`  
  
### <a name="detecting-missing-fields-for-dynamic-queries-at-run-time"></a>Detectando campos ausentes em consultas dinâmicas em tempo de execução  
 Por padrão, os itens na coleção Fields têm duas propriedades: Value e IsMissing. A propriedade IsMissing indica se um campo que foi definido para um conjunto de dados em tempo de design estará contido em um dos campos recuperados em tempo de execução. Por exemplo, a consulta pode chamar um procedimento armazenado cujo conjunto de resultados varia de acordo com um parâmetro de entrada ou a consulta pode ser `SELECT * FROM` *\<table>*, em que a definição da tabela foi alterada.  
  
> [!NOTE]  
>  IsMissing detecta alterações no esquema do conjunto de dados entre o tempo de design e o tempo de execução de qualquer tipo de fonte de dados. IsMissing não pode ser usado para detectar membros vazios em um cubo multidimensional e não está relacionado aos conceitos da linguagem MDX consulta de `EMPTY` e `NON EMPTY`.  
  
 É possível testar a propriedade IsMissing em código personalizado para determinar a existência de um campo em um conjunto de resultados. Não é possível testar sua presença usando uma expressão com uma chamada de função [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], como `IIF` ou `SWITCH`, pois [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] avalia todos os parâmetros da chamada de função, resultando em um erro quando a referência ao campo ausente for avaliada.  
  
#### <a name="example-for-controlling-the-visibility-of-a-dynamic-column-for-a-missing-field"></a>Exemplo de controle da visibilidade de uma coluna dinâmica de um campo ausente  
 Para definir uma expressão que controla a visibilidade de uma coluna que exibe um campo em um conjunto de dados, primeiro defina uma função de código personalizado que retorne um valor booliano com base na existência ou ausência do campo. Por exemplo, a função de código personalizado a seguir retornará verdadeiro se o campo estiver ausente e falso se ele existir.  
  
```  
Public Function IsFieldMissing(field as Field) as Boolean  
 If (field.IsMissing) Then  
 Return True  
  Else   
  Return False  
 End If  
End Function  
```  
  
 Para usar essa função para controlar a visibilidade de uma coluna, defina a propriedade Hidden da coluna como a seguinte expressão:  
  
 `=Code.IsFieldMissing(Fields!FieldName)`  
  
 A coluna ficará oculta se o campo não existir.  
  
#### <a name="example-for-controlling-the-text-box-value-for-a-missing-field"></a>Exemplo de controle da visibilidade de um valor de caixa de texto de um campo ausente  
 Para usar o texto que você escrever em substituição do valor de um campo ausente, escreva um código personalizado que retorne o texto que você possa usar no lugar do valor do campo quando o campo estiver ausente. Por exemplo, a função de código personalizado a seguir retornará o valor do campo se o campo existir e a mensagem indicando que você deve especificar o segundo parâmetro se o campo não existir:  
  
```  
Public Function IsFieldMissingThenString(field as Field, strMessage as String) as String  
 If (field.IsMissing) Then  
  Return strMessage  
 Else   
  Return field.Value  
  End If  
End Function  
```  
  
 Para usar essa função em uma caixa de texto, adicione a seguinte expressão à propriedade Value:  
  
 `=Code.IsFieldMissingThenString(Fields!FieldName,"Missing")`  
  
 A caixa de texto exibe o valor do campo ou o texto que você especificou.  
  
### <a name="using-extended-field-properties"></a>Usando propriedades de campo estendidas  
 As propriedades de campo estendidas são propriedades adicionais definidas em um campo pela extensão de processamento de dados, que é determinada pelo tipo de fonte de dados do conjunto de dados. As propriedades de campo estendidas são predefinidas ou específicas para um tipo de fonte de dados. Para obter mais informações, consulte [Propriedades de campos estendidos para um banco de dados do Analysis Services &#40;SSRS&#41;](../report-data/extended-field-properties-for-an-analysis-services-database-ssrs.md).  
  
 Se você especificar uma propriedade que não é suportada pelo campo, a avaliação da expressão será `null` (`Nothing` em [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]). Se um provedor de dados não oferecer suporte a propriedades de campo estendidas, ou se o campo não for encontrado quando a consulta for executada, o valor da propriedade será \`null` (`Nothing` em [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]) para propriedades do tipo `String` e `Object` e zero (0) para propriedades do tipo `Integer`. Uma extensão de processamento de dados pode fazer bom uso das propriedades predefinidas ao otimizar consultas que incluem essa sintaxe.  
  
## <a name="see-also"></a>Consulte também  
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Adicionar dados a um relatório &#40;relatórios e SSRS&#41;](../report-data/report-datasets-ssrs.md)  
  
  

---
title: Recuperando dados usando o AdomdDataReader | Microsoft Docs
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
helpviewer_keywords:
- retrieving data
- AdomdDataReader object
- data retrieval [ADOMD.NET], AdomdDataReader object
ms.assetid: 8ed7ea26-b5f8-4852-80fc-75dd62df5b3a
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a04a25d6bf72a8bacd5af46313982e8ff0197170
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="retrieving-data-using-the-adomddatareader"></a>Recuperando dados usando o AdomdDataReader
  Na recuperação de dados analíticos, o objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> oferece um bom equilíbrio entre sobrecarga e interatividade. O objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> recupera um fluxo dados somente leitura, somente encaminhamento, bidimensional a partir de uma fonte de dados analíticos. Esse fluxo de dados não armazenado permite que a lógica procedural processe com eficiência os resultados de uma fonte de dados analíticos de forma sequencial. Isso faz do <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> uma boa opção para a recuperação de grandes quantidades de dados para fins de exibição, uma vez que os dados não são armazenados em cache em memória.  
  
 O <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> também pode melhorar o desempenho do aplicativo ao recuperar dados assim que estiverem disponíveis, em vez de aguardar os resultados completos da consulta a ser retornada. O <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> também reduz a sobrecarga do sistema porque, por padrão, este leitor só armazena uma linha de cada vez em memória.  
  
 A desvantagem do desempenho otimizado é que o objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> oferece menos informações sobre os dados recuperados do que outros métodos de recuperação de dados. O objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> não dá suporte a um modelo de objeto grande para a representação de dados ou de metadados e esse modelo de objeto também não permite recursos analíticos mais complexos, como o write-back de célula. No entanto, o objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> oferece um conjunto de métodos com rigidez de tipo para a recuperação de dados de conjuntos de células e um método para a recuperação de metadados de conjuntos de células em formato tabular. Além disso, <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> implementa o **IDbDataReader** interface para o suporte da associação de dados e para recuperar dados usando o **SelectCommand** método, do **System. Data**  namespace da biblioteca de classe do Microsoft .NET Framework.  
  
## <a name="retrieving-data-from-the-adomddatareader"></a>Recuperando dados do AdomdDataReader  
 Para usar o objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> para recuperar dados, siga estas etapas:  
  
1.  **Crie uma nova instância do objeto.**  
  
     Para criar uma nova instância da classe <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>, chame o método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.Execute%2A> ou <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand.ExecuteReader%2A> do objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdCommand>.  
  
2.  **Recupere dados.**  
  
     Quando o comando executa a consulta, o ADOMD.NET retorna os resultados no **Resultset** Formatar, um formato tabular como descrito na especificação XML for Analysis, para mesclar os dados para o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> objeto. Um formato tabelar é incomum na consulta de dados analíticos que consideram a dimensionalidade variável em tais dados.  
  
     O ADOMD.NET armazena esses resultados tabulares no buffer de rede no cliente até que você solicite-os usando um dos métodos a seguir:  
  
    -   Chame o método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.Read%2A> do objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>.  
  
         O método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.Read%2A> obtém uma linha dos resultados da consulta. Você pode passar o nome ou a referência ordinal, da coluna para o [Item](https://msdn.microsoft.com/en-us/library/ms131793(v=sql.130).aspx) propriedade para acessar cada coluna da linha retornada. Por exemplo, a primeira coluna da linha atual é nomeada, ColumnName. Em seguida, `reader[0].ToString()` ou `reader["ColumnName"].ToString()` retornarão o conteúdo da primeira coluna da linha atual.  
  
    -   Chame um dos métodos de acessador de tipo.  
  
         O <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> oferece uma série de métodos de acessador de tipo – métodos que permitem o acesso a valores de coluna em seus tipos de dados nativos. Quando você conhece o tipo de dados subjacente de um valor de coluna, um método de acessador de tipo reduz a quantidade de conversão de tipo exigida na recuperação do valor da coluna e oferece o melhor desempenho.  
  
         Alguns dos métodos de acessador de tipo disponíveis incluem <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.GetDateTime%2A>, <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.GetDouble%2A> e <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.GetInt32%2A>. Para obter uma lista completa de métodos de acessador de tipo, consulte <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>.  
  
3.  **Feche o leitor.**  
  
     Você deve sempre chamar o método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.Close%2A> ao terminar de usar o objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>. Embora uma instância de um objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> esteja aberta, o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> é usado exclusivamente pelo <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>. Você não poderá executar qualquer comando na instância do <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>, incluindo a criação de outro <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> ou **System.XML. XmlReader**, até que você feche o original <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>.  
  
### <a name="example-of-retrieving-data-from-the-adomddatareader"></a>Exemplo de recuperação de dados do AdomdDataReader  
 O exemplo de código a seguir itera por meio de um objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> e retorna os dois primeiros valores, como cadeias de caracteres, de cada linha.  
  
```vb  
If Reader.HasRows Then  
    Do While objReader.Read()  
        Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _  
            objReader.GetString(0), objReader.GetString(1))  
    Loop  
Else  
  Console.WriteLine("No rows returned.")  
End If  
  
objReader.Close()  
```  
  
```csharp  
if (objReader.HasRows)  
  while (objReader.Read())  
    Console.WriteLine("\t{0}\t{1}", _  
        objReader.GetString(0), objReader.GetString(1));  
else  
  Console.WriteLine("No rows returned.");  
  
objReader.Close();  
```  
  
## <a name="retrieving-metadata-from-the-adomddatareader"></a>Recuperando metadados do AdomdDataReader  
 Embora uma instância de um objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader> esteja aberta, você poderá recuperar informações de esquema, ou metadados, sobre o conjunto de registros atual por meio do método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.GetSchemaTable%2A>. <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.GetSchemaTable%2A>Retorna um **DataTable** objeto que é preenchido com as informações de esquema para o conjunto de registros atual. O **DataTable** conterá uma linha para cada coluna do conjunto de registros. Cada coluna da linha da tabela do esquema é mapeada para uma propriedade da coluna retornada no conjunto de células, em que **ColumnName** é o nome da propriedade e o valor da coluna é o valor da propriedade.  
  
### <a name="example-of-retrieving-metadata-from-the-adomddatareader"></a>Exemplo de recuperação de metadados do AdomdDataReader  
 O exemplo de código a seguir grava as informações de esquema para um objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader>.  
  
```vb  
Dim schemaTable As DataTable = objReader.GetSchemaTable()  
  
Dim objRow As DataRow  
Dim objColumn As DataColumn  
  
For Each objRow In schemaTable.Rows  
  For Each objColumn In schemaTable.Columns  
    Console.WriteLine(objColumn.ColumnName & " = " & objRow(objColumn).ToString())  
  Next  
  Console.WriteLine()  
Next  
DataTable schemaTable = objReader.GetSchemaTable();  
```  
  
```csharp  
foreach (DataRow objRow in schemaTable.Rows)  
{  
  foreach (DataColumn objColumn in schemaTable.Columns)  
    Console.WriteLine(objColumn.ColumnName + " = " + objRow[objColumn]);  
  Console.WriteLine();  
}  
```  
  
## <a name="retrieving-multiple-result-sets"></a>Recuperando vários conjuntos de resultados  
 A mineração de dados dá suporte ao conceito de tabelas aninhadas, exibidas pelo ADOMD.NET como conjuntos de linhas aninhados. Para recuperar o conjunto de linhas aninhado associado a cada linha, você deve chamar o <xref:Microsoft.AnalysisServices.AdomdClient.AdomdDataReader.GetDataReader%2A> método.  
  
## <a name="see-also"></a>Consulte também  
 [Recuperando dados de uma fonte de dados analíticos](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-from-an-analytical-data-source.md)   
 [Recuperando dados usando o conjunto de células](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-cellset.md)   
 [Recuperando dados usando o XmlReader](../../analysis-services/multidimensional-models-adomd-net-client/retrieving-data-using-the-xmlreader.md)  
  
  


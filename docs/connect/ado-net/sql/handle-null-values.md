---
title: Manipulando valores nulos
description: Demonstra como trabalhar com valores de GUID e uniqueidentifier em SQL Server e .NET.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: f18b288f-b265-4bbe-957f-c6833c0645ef
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 6ae2bc8d816dd2bc32572447483dacd76dd967f0
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452189"
---
# <a name="handling-null-values"></a>Manipulando valores nulos

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Um valor nulo em um banco de dados relacional é usado quando o valor em uma coluna é desconhecido ou está ausente. Um NULL não é uma cadeia de caracteres vazia (para tipos de dados character ou DateTime) nem um valor zero (para tipos de dados numéricos). A especificação ANSI SQL-92 declara que um NULL deve ser o mesmo para todos os tipos de dados, para que todos os nulos sejam manipulados consistentemente. O namespace <xref:System.Data.SqlTypes> fornece semântica nula implementando a interface <xref:System.Data.SqlTypes.INullable>. Cada um dos tipos de dados no <xref:System.Data.SqlTypes> tem sua própria propriedade `IsNull` e um valor `Null` que pode ser atribuído a uma instância desse tipo de dados.  
  
> [!NOTE]
>  O .NET Framework versão 2,0 e o .NET Core versão 1,0 introduziram suporte para tipos anuláveis, que permitem aos programadores estender um tipo de valor para representar todos os valores do tipo subjacente. Esses tipos anuláveis CLR representam uma instância da estrutura <xref:System.Nullable>. Esse recurso é especialmente útil quando os tipos de valor são Boxed e unboxed, fornecendo compatibilidade aprimorada com tipos de objeto. Os tipos anuláveis CLR não se destinam ao armazenamento de nulos de banco de dados porque um nulo SQL ANSI não se comporta da mesma maneira que uma referência de `null` (ou `Nothing` em Visual Basic). Para trabalhar com valores nulos do SQL de banco de dados ANSI, use <xref:System.Data.SqlTypes> nulos em vez de <xref:System.Nullable>. Para obter mais informações sobre como trabalhar com tipos anuláveis C# CLR no, consulte [tipos anuláveis](https://docs.microsoft.com/dotnet/csharp/programming-guide/nullable-types/)e para ver como C# [usar tipos anuláveis](https://docs.microsoft.com/dotnet/csharp/programming-guide/nullable-types/using-nullable-types/).  
  
## <a name="nulls-and-three-valued-logic"></a>Lógica nula e de três valores  
Permitir valores nulos em definições de coluna apresenta uma lógica de três valores em seu aplicativo. Uma comparação pode ser avaliada como uma das três condições:  
  
- True  
  
- Falso  
  
- Unknown (desconhecido)  
  
Como NULL é considerado desconhecido, dois valores nulos comparados entre si não são considerados iguais. Em expressões que usam operadores aritméticos, se qualquer um dos operandos for nulo, o resultado será nulo também.  
  
## <a name="nulls-and-sqlboolean"></a>Nulos e SqlBoolean  
A comparação entre qualquer <xref:System.Data.SqlTypes> retornará um <xref:System.Data.SqlTypes.SqlBoolean>. A função `IsNull` para cada `SqlType` retorna uma <xref:System.Data.SqlTypes.SqlBoolean> e pode ser usada para verificar se há valores nulos. As tabelas a seguir mostram como os operadores e, ou, e não funcionam na presença de um valor nulo. (T = true, F = false e U = Unknown, ou NULL.)  
  
![Tabela da verdade](../media/truthtable-bpuedev11.gif "|::ref1::|")  
  
### <a name="understanding-the-ansi_nulls-option"></a>Compreendendo a opção ANSI_NULLS  
<xref:System.Data.SqlTypes> fornece a mesma semântica que quando a opção ANSI_NULLS é definida em SQL Server. Todos os operadores aritméticos (+, -, *, /, %), operadores bit a bit (~, &, &#124;) e a maioria das funções retornarão nulo se algum operando ou argumento for nulo, exceto na propriedade `IsNull`.  
  
O padrão ANSI SQL-92 não oferece suporte a *columnName* = NULL em uma cláusula WHERE. Em SQL Server, a opção ANSI_NULLS controla a nulabilidade padrão no banco de dados e a avaliação de comparações com valores nulos. Se a ANSI_NULLS estiver ativada (o padrão), o operador IS NULL deverá ser usado em expressões ao testar valores nulos. Por exemplo, a comparação seguinte sempre retorna unknown quando ANSI_NULLS for on:  
  
```console
colname > NULL  
```  
  
A comparação com uma variável que contém um valor nulo também produz desconhecido:  
  
```console
colname > @MyVariable  
```  
  
Use o predicado IS NULL ou IS NOT NULL para testar um valor nulo. Isso pode adicionar complexidade à cláusula WHERE. Por exemplo, a coluna Territórioid na tabela cliente AdventureWorks permite valores nulos. Se uma instrução SELECT for testada para obter valores nulos além de outros, ela deverá incluir um predicado IS NULL:  
  
```sql
SELECT CustomerID, AccountNumber, TerritoryID  
FROM AdventureWorks.Sales.Customer  
WHERE TerritoryID IN (1, 2, 3)  
   OR TerritoryID IS NULL  
```  
  
Se você definir ANSI_NULLS off no SQL Server, poderá criar expressões que usem o operador de igualdade para comparar com NULL. No entanto, você não pode impedir que diferentes conexões definam opções nulas para essa conexão. Usar IS NULL para testar valores nulos sempre funciona, independentemente das configurações de ANSI_NULLS para uma conexão.  
  
Não há suporte para a configuração de ANSI_NULLS off em um `DataSet`, que sempre segue o padrão ANSI SQL-92 para manipular valores nulos no <xref:System.Data.SqlTypes>.  
  
## <a name="assigning-null-values"></a>Atribuindo valores nulos  
Os valores nulos são especiais, e suas semânticas de armazenamento e atribuição diferem em sistemas de tipos e sistemas de armazenamento diferentes. Uma `Dataset` foi projetada para ser usada com diferentes sistemas de tipo e armazenamento.  
  
Esta seção descreve a semântica nula para atribuir valores nulos a um <xref:System.Data.DataColumn> em um <xref:System.Data.DataRow> entre os diferentes sistemas de tipos.  
  
`DBNull.Value`  
Essa atribuição é válida para um `DataColumn` de qualquer tipo. Se o tipo implementa `INullable`, `DBNull.Value` é forçado para o valor NULL com rigidez de tipos apropriado.  
  
`SqlType.Null`  
Todos os tipos de dados <xref:System.Data.SqlTypes> implementam `INullable`. Se o valor NULL com rigidez de tipos puder ser convertido no tipo de dados da coluna usando operadores de conversão implícito, a atribuição deverá passar. Caso contrário, uma exceção de conversão inválida será lançada.  
  
`null`  
Se ' NULL ' for um valor válido para o tipo de dados especificado `DataColumn`, ele será forçado no `DbNull.Value` apropriado ou `Null` associado ao tipo `INullable` (`SqlType.Null`)  
  
`derivedUdt.Null`  
Para colunas UDT, os nulos são sempre armazenados com base no tipo associado à `DataColumn`. Considere o caso de um UDT associado a um `DataColumn` que não implementa `INullable` enquanto sua subclasse faz. Nesse caso, se um valor NULL com rigidez de tipos associado à classe derivada for atribuído, ele será armazenado como um `DbNull.Value` não tipado, porque o armazenamento nulo é sempre consistente com o tipo de dados de DataColumn.  
  
> [!NOTE]
>  No momento, não há suporte para a estrutura `Nullable<T>` ou <xref:System.Nullable> no `DataSet`.  
  
### <a name="multiple-column-row-assignment"></a>Atribuição de várias colunas (linha)  
`DataTable.Add`, `DataTable.LoadDataRow` ou outras APIs que aceitam uma <xref:System.Data.DataRow.ItemArray%2A> que são mapeadas para uma linha, mapeiam ' NULL ' para o valor padrão de DataColumn. Se um objeto na matriz contiver `DbNull.Value` ou sua contraparte com rigidez de tipos, as mesmas regras descritas acima serão aplicadas.  
  
Além disso, as regras a seguir se aplicam a uma instância de `DataRow.["columnName"]` atribuições nulas:  
  
- O valor *default* padrão é `DbNull.Value` para todos, a não ser para as colunas nulas fortemente tipadas em que ele é o valor nulo fortemente tipado apropriado.  
  
- Os valores nulos nunca são gravados durante a serialização para arquivos XML (como em "xsi: nil").  
  
- Todos os valores não nulos, incluindo os padrões, sempre são gravados durante a serialização para XML. Isso é diferente da semântica XSD/XML em que um valor nulo (xsi: nil) é explícito e o valor padrão é implícito (se não estiver presente em XML, um analisador de validação pode obtê-lo de um esquema XSD associado). O oposto é verdadeiro para um `DataTable`: um valor nulo é implícito e o valor padrão é explícito.  
  
- Todos os valores de coluna ausentes para linhas lidas da entrada XML são atribuídos nulos. Linhas criadas usando <xref:System.Data.DataTable.NewRow%2A> ou métodos semelhantes recebem o valor padrão de DataColumn.  
  
- O método <xref:System.Data.DataRow.IsNull%2A> retorna `true` para `DbNull.Value` e `INullable.Null`.  
  
## <a name="assigning-null-values"></a>Atribuindo valores nulos  
O valor padrão para qualquer instância de <xref:System.Data.SqlTypes> é NULL.  
  
Os valores nulos em <xref:System.Data.SqlTypes> são específicos do tipo e não podem ser representados por um único valor, como `DbNull`. Use a propriedade `IsNull` para verificar se há nulos.  
  
Valores nulos podem ser atribuídos a um <xref:System.Data.DataColumn>, conforme mostrado no exemplo de código a seguir. Você pode atribuir diretamente valores nulos a `SqlTypes` variáveis sem disparar uma exceção.  
  
### <a name="example"></a>Exemplo  
O exemplo de código a seguir cria um <xref:System.Data.DataTable> com duas colunas definidas como <xref:System.Data.SqlTypes.SqlInt32> e <xref:System.Data.SqlTypes.SqlString>. O código adiciona uma linha de valores conhecidos, uma linha de valores nulos e, em seguida, itera através da <xref:System.Data.DataTable>, atribuindo os valores a variáveis e exibindo a saída na janela do console.  
  
[!code-csharp[DataWorks SqlInt32_IsNull#1](~/../sqlclient/doc/samples/SqlInt32_IsNull.cs#1)]
  
Este exemplo exibe os seguintes resultados:  
  
```console
isColumnNull=False, ID=123, Description=Side Mirror  
isColumnNull=True, ID=Null, Description=Null  
```  
  
## <a name="comparing-null-values-with-sqltypes-and-clr-types"></a>Comparando valores nulos com hipertipos e tipos CLR  
Ao comparar valores nulos, é importante entender a diferença entre a maneira como o método `Equals` avalia valores nulos em <xref:System.Data.SqlTypes> em comparação com o modo como ele funciona com tipos CLR. Todos os métodos de `Equals` de <xref:System.Data.SqlTypes> usam semânticas de banco de dados para avaliar valores nulos: se um ou ambos os valores forem nulos, a comparação produzirá NULL. Por outro lado, usar o método CLR `Equals` em dois <xref:System.Data.SqlTypes> produzirá true se ambos forem nulos. Isso reflete a diferença entre usar um método de instância, como o método CLR `String.Equals`, e usar o método estático/compartilhado, `SqlString.Equals`.  
  
O exemplo a seguir demonstra a diferença nos resultados entre o método `SqlString.Equals` e o método `String.Equals` quando cada um é passado por um par de valores nulos e, em seguida, um par de cadeias de caracteres vazias.  
  
[!code-csharp[DataWorks SqlString_Equals#1](~/../sqlclient/doc/samples/SqlString_Equals.cs#1)]
  
O código produz a seguinte saída:  
  
```console
SqlString.Equals shared/static method:  
  Two nulls=Null  
  
String.Equals instance method:  
  Two nulls=True  
  
SqlString.Equals shared/static method:  
  Two empty strings=True  
  
String.Equals instance method:  
  Two empty strings=True   
```  
  
## <a name="next-steps"></a>Próximas etapas
- [Tipos de dados do SQL Server e do ADO.NET](sql-server-data-types.md)

---
title: Manipulando valores nulos
description: Demonstra como trabalhar com valores de GUID e uniqueidentifier no SQL Server e .NET.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: f18b288f-b265-4bbe-957f-c6833c0645ef
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 861ed4395e6cf8f5e8df3a5cc41a0f6da597e5ad
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247748"
---
# <a name="handling-null-values"></a>Manipulando valores nulos

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Um valor nulo em um banco de dados relacional é usado quando o valor em uma coluna é desconhecido ou está ausente. Um valor nulo não é uma cadeia de caracteres vazia (para tipos de dados character ou datetime) nem um valor zero (para tipos de dados numéricos). A especificação ANSI SQL-92 declara que um valor nulo deve ser o mesmo para todos os tipos de dados, para que todos os nulos sejam manipulados consistentemente. O namespace <xref:System.Data.SqlTypes> fornece semântica nula ao implementar a interface <xref:System.Data.SqlTypes.INullable>. Cada um dos tipos de dados no <xref:System.Data.SqlTypes> tem uma propriedade própria `IsNull` e um valor `Null` que pode ser atribuído a uma instância desse tipo de dados.  
  
> [!NOTE]
>  O .NET Framework versão 2.0 e o .NET Core versão 1.0 introduziram suporte para tipos que permitem valor nulo, o que possibilita aos programadores estender um tipo de valor para representar todos os valores do tipo subjacente. Esses tipos CLR que permitem valor nulo representam uma instância da estrutura <xref:System.Nullable>. Essa funcionalidade é especialmente útil quando os tipos de valor são boxed e unboxed, fornecendo compatibilidade aprimorada com tipos de objeto. Os tipos CLR que permitem valor nulo não se destinam ao armazenamento de nulos de banco de dados porque um nulo ANSI SQL não se comporta da mesma maneira que uma referência de `null` (ou `Nothing` no Visual Basic). Para trabalhar com valores nulos ANSI SQL de banco de dados, use nulos <xref:System.Data.SqlTypes> em vez de <xref:System.Nullable>. Para obter mais informações sobre como trabalhar com tipos CLR que permitem valores nulos no C#, confira [Tipos que permitem valor nulo](https://docs.microsoft.com/dotnet/csharp/programming-guide/nullable-types/) e, para C#, confira [Como usar tipos que permitem valor nulo](https://docs.microsoft.com/dotnet/csharp/programming-guide/nullable-types/using-nullable-types/).  
  
## <a name="nulls-and-three-valued-logic"></a>Lógica nula e de três valores  
Permitir valores nulos em definições de coluna apresenta uma lógica de três valores em seu aplicativo. Uma comparação pode ser avaliada como uma das três condições:  
  
- True  
  
- Falso  
  
- Unknown (desconhecido)  
  
Como um nulo é considerado desconhecido, dois valores nulos comparados entre si não são considerados iguais. Em expressões que usam operadores aritméticos, se um dos operandos for nulo, o resultado será nulo também.  
  
## <a name="nulls-and-sqlboolean"></a>Nulos e SqlBoolean  
A comparação entre um <xref:System.Data.SqlTypes> retornará um <xref:System.Data.SqlTypes.SqlBoolean>. A função `IsNull` para cada `SqlType` retorna um <xref:System.Data.SqlTypes.SqlBoolean> e pode ser usada para verificar se há valores nulos. As tabelas da verdade a seguir mostram como os operadores AND, OR e NOT funcionam na presença de um valor nulo. (T = verdadeiro, F = falso e U = desconhecido ou nulo.)  
  
![Tabela da verdade](../media/truthtable-bpuedev11.gif "TruthTable_bpuedev11")  
  
### <a name="understanding-the-ansi_nulls-option"></a>Noções básicas sobre a opção ANSI_NULLS  
O <xref:System.Data.SqlTypes> fornece a mesma semântica que quando a opção ANSI_NULLS é definida no SQL Server. Todos os operadores aritméticos (+, -, *, /, %), operadores bit a bit (~, &, &#124;) e a maioria das funções retornarão nulo se algum operando ou argumento for nulo, exceto na propriedade `IsNull`.  
  
O padrão ANSI SQL-92 não oferece suporte a *columnName* = NULL em uma cláusula WHERE. No SQL Server, a opção ANSI_NULLS controla a nulabilidade padrão no banco de dados e a avaliação de comparações com valores nulos. Se ANSI_NULLS estiver ativado (o padrão), o operador IS NULL deverá ser usado em expressões ao testar valores nulos. Por exemplo, a comparação seguinte sempre retorna unknown quando ANSI_NULLS for on:  
  
```console
colname > NULL  
```  
  
A comparação com uma variável que contém um valor nulo também produz valores desconhecidos:  
  
```console
colname > @MyVariable  
```  
  
Use o predicado IS NULL ou IS NOT NULL para testar um valor nulo. Isso pode adicionar complexidade à cláusula WHERE. Por exemplo, a coluna TerritoryID na tabela Cliente AdventureWorks permite valores nulos. Se uma instrução SELECT for testada para obter valores nulos além de outros, ela deverá incluir um predicado IS NULL:  
  
```sql
SELECT CustomerID, AccountNumber, TerritoryID  
FROM AdventureWorks.Sales.Customer  
WHERE TerritoryID IN (1, 2, 3)  
   OR TerritoryID IS NULL  
```  
  
Se você desativar ANSI_NULLS no SQL Server, poderá criar expressões que usam o operador de igualdade para comparar com o valor nulo. No entanto, você não pode impedir que diferentes conexões configurem opções nulas para essa conexão. Usar IS NULL para testar valores nulos sempre funciona, independentemente das configurações de ANSI_NULLS para uma conexão.  
  
A desativação de ANSI_NULLS não é compatível em um `DataSet`, que sempre segue o padrão ANSI SQL-92 para manipular valores nulos no <xref:System.Data.SqlTypes>.  
  
## <a name="assigning-null-values"></a>Como atribuir valores nulos  
Os valores nulos são especiais e suas semânticas de armazenamento e atribuição diferem em sistemas de tipos e sistemas de armazenamento diferentes. Um `Dataset` foi projetado para ser usado com diferentes sistemas de tipo e armazenamento.  
  
Esta seção descreve a semântica nula para atribuir valores nulos a um <xref:System.Data.DataColumn> em um <xref:System.Data.DataRow> entre os diferentes sistemas de tipos.  
  
`DBNull.Value`  
Essa atribuição é válida para um `DataColumn` de qualquer tipo. Se o tipo implementa `INullable`, o `DBNull.Value` é forçado no valor nulo fortemente tipado apropriado.  
  
`SqlType.Null`  
Todos os tipos de dados <xref:System.Data.SqlTypes> implementam `INullable`. Se o valor nulo fortemente tipado puder ser convertido no tipo de dados da coluna usando operadores de conversão implícitos, a atribuição deverá passar. Caso contrário, uma exceção de conversão inválida será lançada.  
  
`null`  
Se nulo for um valor válido para o tipo de dados `DataColumn` especificado, ele será forçado no `DbNull.Value` ou no `Null` apropriado associado ao tipo `INullable` (`SqlType.Null`)  
  
`derivedUdt.Null`  
Para colunas UDT, os nulos são sempre armazenados com base no tipo associado à `DataColumn`. Considere o caso de um UDT associado a um `DataColumn` que não implementa `INullable`, enquanto sua subclasse faz a implementação. Nesse caso, se um valor nulo fortemente tipado associado à classe derivada for atribuído, ele será armazenado como um `DbNull.Value` não tipado, porque o armazenamento nulo é sempre consistente com o tipo de dados de DataColumn.  
  
> [!NOTE]
>  No momento, a estrutura `Nullable<T>` ou <xref:System.Nullable> não é compatível no `DataSet`.  
  
### <a name="multiple-column-row-assignment"></a>Atribuição de várias colunas (linhas)  
`DataTable.Add`, `DataTable.LoadDataRow` ou outras APIs que aceitam um <xref:System.Data.DataRow.ItemArray%2A> que é mapeado para uma linha, mapeiam "nulo" para o valor padrão da DataColumn. Se um objeto na matriz contiver `DbNull.Value` ou sua contraparte fortemente tipada, as mesmas regras descritas acima serão aplicadas.  
  
Além disso, as seguintes regras se aplicam a uma instância de atribuições nulas de `DataRow.["columnName"]`:  
  
- O valor *default* padrão é `DbNull.Value` para todos, a não ser para as colunas nulas fortemente tipadas em que ele é o valor nulo fortemente tipado apropriado.  
  
- Os valores nulos nunca são gravados durante a serialização para arquivos XML (como em "xsi:nil").  
  
- Todos os valores não nulos, incluindo os padrões, sempre são gravados durante a serialização para XML. Isso é diferente da semântica XSD/XML em que um valor nulo (xsi:nil) é explícito e o valor padrão é implícito (se não estiver presente em XML, um analisador de validação poderá obtê-lo de um esquema XSD associado). O oposto é verdadeiro para um `DataTable`: um valor nulo é implícito e o valor padrão é explícito.  
  
- Todos os valores de coluna ausentes para linhas lidas da entrada XML são atribuídos como NULL. As linhas criadas usando <xref:System.Data.DataTable.NewRow%2A> ou métodos semelhantes recebem o valor padrão de DataColumn.  
  
- O método <xref:System.Data.DataRow.IsNull%2A> retorna `true` para `DbNull.Value` e `INullable.Null`.  
  
## <a name="assigning-null-values"></a>Como atribuir valores nulos  
O valor padrão para uma instância <xref:System.Data.SqlTypes> é nulo.  
  
Os valores nulos em <xref:System.Data.SqlTypes> são específicos do tipo e não podem ser representados por um valor, como `DbNull`. Use a propriedade `IsNull` para verificar valores nulos.  
  
Os valores nulos podem ser atribuídos a um <xref:System.Data.DataColumn>, conforme mostrado no exemplo de código a seguir. Você pode atribuir diretamente valores nulos a variáveis `SqlTypes` sem disparar uma exceção.  
  
### <a name="example"></a>Exemplo  
O exemplo de código a seguir cria um <xref:System.Data.DataTable> com duas colunas definidas como <xref:System.Data.SqlTypes.SqlInt32> e <xref:System.Data.SqlTypes.SqlString>. O código adiciona uma linha de valores conhecidos, uma linha de valores nulos e, em seguida, itera por <xref:System.Data.DataTable>, atribuindo os valores a variáveis e exibindo a saída na janela do console.  
  
[!code-csharp[DataWorks SqlInt32_IsNull#1](~/../sqlclient/doc/samples/SqlInt32_IsNull.cs#1)]
  
Esse exemplo mostra os seguintes resultados:  
  
```console
isColumnNull=False, ID=123, Description=Side Mirror  
isColumnNull=True, ID=Null, Description=Null  
```  
  
## <a name="comparing-null-values-with-sqltypes-and-clr-types"></a>Como comparar valores nulos com SqlTypes e tipos CLR  
Ao comparar valores nulos, é importante entender a diferença entre a maneira como o método `Equals` avalia valores nulos em <xref:System.Data.SqlTypes> em comparação com o modo como ele funciona com tipos CLR. Todos os métodos <xref:System.Data.SqlTypes>`Equals` usam semânticas de banco de dados para avaliar valores nulos: se um ou ambos os valores forem nulos, a comparação produzirá um valor nulo. Por outro lado, usar o método CLR `Equals` em dois <xref:System.Data.SqlTypes> produzirá true se ambos forem valores nulos. Isso reflete a diferença entre usar um método de instância, como o método CLR `String.Equals`, e usar o método estático/compartilhado, `SqlString.Equals`.  
  
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

---
title: Configurar parâmetros
description: Os objetos de comando usam parâmetros para passar valores a instruções SQL ou procedimentos armazenados, fornecendo verificação de tipo e validação no ADO.NET.
ms.date: 11/25/2020
dev_langs:
- csharp
ms.assetid: 537d8a2c-d40b-4000-83eb-bc1fcc93f707
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: a24241d3ef66739a85422397426278738987bf15
ms.sourcegitcommit: debaff72dbfae91b303f0acd42dd6d99e03135a2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96428180"
---
# <a name="configuring-parameters"></a>Configurar parâmetros

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Objetos de comando usam parâmetros para passar valores para instruções SQL ou procedimentos armazenados, fornecendo verificação de tipo e validação. Diferentemente do texto de comando, o parâmetro de entrada é tratado como um valor literal, não como código executável. Isso ajuda a proteger contra ataques de "Injeção de SQL", em que um invasor insere um comando que compromete a segurança no servidor em uma instrução SQL.

Os comandos parametrizados também podem melhorar o desempenho de execução da consulta, porque ajudam o servidor de banco de dados a corresponder exatamente ao comando de entrada com um plano de consulta em cache apropriado. Para obter mais informações, confira [Reutilização e armazenamento em cache do plano de execução](/sql/relational-databases/query-processing-architecture-guide#execution-plan-caching-and-reuse) e [Parâmetros e reutilização de plano de execução](/sql/relational-databases/query-processing-architecture-guide#PlanReuse). Além dos benefícios de segurança e desempenho, os comandos parametrizados fornecem um método conveniente para organizar os valores passados para uma fonte de dados.

Um objeto <xref:System.Data.Common.DbParameter> pode ser criado usando o construtor ou adicionando-o ao <xref:System.Data.Common.DbCommand.DbParameterCollection%2A> chamando o método `Add` da coleção <xref:System.Data.Common.DbParameterCollection>. O método `Add` utilizará como entrada argumentos de construtor ou um objeto de parâmetro existente, dependendo do provedor de dados.

## <a name="supplying-the-parameterdirection-property"></a>Fornecer a propriedade ParameterDirection

Ao adicionar parâmetros, você deverá fornecer uma propriedade <xref:System.Data.ParameterDirection> para parâmetros diferentes dos parâmetros de entrada. A tabela a seguir mostra os valores `ParameterDirection` que você pode usar com a enumeração <xref:System.Data.ParameterDirection>.

|Nome do membro|Descrição|
|-----------------|-----------------|
|<xref:System.Data.ParameterDirection.Input>|O parâmetro é um parâmetro de entrada. Este é o padrão.|
|<xref:System.Data.ParameterDirection.InputOutput>|O parâmetro pode executar entrada e saída.|
|<xref:System.Data.ParameterDirection.Output>|O parâmetro é um parâmetro de saída.|
|<xref:System.Data.ParameterDirection.ReturnValue>|O parâmetro representa um valor de retorno de uma operação como um procedimento armazenado, uma função interna ou uma função definida pelo usuário.|

## <a name="working-with-parameter-placeholders"></a>Trabalhar com espaços reservados de parâmetro

A sintaxe para espaços reservados de parâmetro depende da fonte de dados. O Provedor de Dados do Microsoft SqlClient para SQL Server lida com a nomenclatura e a especificação de parâmetros e espaços reservados de parâmetros de maneira diferente. O provedor de dados do SqlClient usa parâmetros nomeados no formato `@`*nomedoparâmetro*.

## <a name="specifying-parameter-data-types"></a>Especificar tipos de dados de parâmetros

O tipo de dados de um parâmetro é específico para o Provedor de Dados do Microsoft SqlClient para SQL Server. Especificar o tipo converte o valor de `Parameter` para o tipo de Provedor de Dados Microsoft SqlClient para SQL Server antes de transmitir o valor à fonte de dados. Você também pode especificar o tipo de um `Parameter` genericamente definindo a propriedade `DbType` de um objeto `Parameter` para um <xref:System.Data.DbType> específico.

O tipo de objeto `Parameter` do Provedor de Dados do Microsoft SqlClient para SQL Server é inferido do tipo .NET Framework de `Value` do objeto `Parameter` ou de `DbType` do objeto `Parameter`. A tabela a seguir mostra o tipo inferido de `Parameter` baseado no objeto passado como o valor do `Parameter` ou `DbType` especificado.

|Tipo .NET|DbType|SqlDbType|
|-------------------------|------------|---------------|
|<xref:System.Boolean>|Booliano|bit|
|<xref:System.Byte>|Byte|TinyInt|
|byte[]|Binário|VarBinary. Essa conversão implícita falhará se a matriz de bytes for maior que o tamanho máximo de um VarBinary, que é de 8000 bytes. Para matrizes de bytes maiores que 8000 bytes, defina <xref:System.Data.SqlDbType> explicitamente.|
|<xref:System.Char>| |Inferir um <xref:System.Data.SqlDbType> do char não tem suporte.|
|<xref:System.DateTime>|Datetime|DateTime|
|<xref:System.DateTimeOffset>|DateTimeOffset|DateTimeOffset no SQL Server 2008. Inferir um <xref:System.Data.SqlDbType> de DateTimeOffset não tem suporte em versões do SQL Server anteriores ao SQL Server 2008.|
|<xref:System.Decimal>|Decimal|Decimal|
|<xref:System.Double>|Double|Float|
|<xref:System.Single>|Single|Real|
|<xref:System.Guid>|Guid|UniqueIdentifier|
|<xref:System.Int16>|Int16|SmallInt|
|<xref:System.Int32>|Int32|int|
|<xref:System.Int64>|Int64|BigInt|
|<xref:System.Object>|Objeto|Variante|
|<xref:System.String>|String|NVarChar. Essa conversão implícita falhará se a cadeia de caracteres for maior do que o tamanho máximo de um NVarChar, que é 4000 caracteres. Para cadeias de caracteres maiores que 4000 caracteres, defina explicitamente o <xref:System.Data.SqlDbType>.|
|<xref:System.TimeSpan>|Hora|Hora no SQL Server 2008. Inferir um <xref:System.Data.SqlDbType> de TimeSpan não tem suporte em versões do SQL Server anteriores ao SQL Server 2008.|
|<xref:System.UInt16>|UInt16|Inferir um <xref:System.Data.SqlDbType> do UInt16 não tem suporte.|
|<xref:System.UInt32>|UInt32|Inferir um <xref:System.Data.SqlDbType> do UInt32 não tem suporte.|
|<xref:System.UInt64>|UInt64|Inferir um <xref:System.Data.SqlDbType> do UInt64 não tem suporte.|
||AnsiString|VarChar|
||AnsiStringFixedLength|Char|
||Moeda|Money|
||Data|Data no SQL Server 2008. Inferir um <xref:System.Data.SqlDbType> de Date não tem suporte em versões do SQL Server anteriores ao SQL Server 2008.|
||SByte|Inferir um <xref:System.Data.SqlDbType> do SByte não tem suporte.|
||StringFixedLength|NChar|
||Hora|Hora no SQL Server 2008. Inferir um <xref:System.Data.SqlDbType> de Time não tem suporte em versões do SQL Server anteriores ao SQL Server 2008.|
||VarNumeric|Inferir um <xref:System.Data.SqlDbType> do VarNumeric não tem suporte.|
|tipo definido pelo usuário (um objeto com <xref:Microsoft.SqlServer.Server.SqlUserDefinedAggregateAttribute>|O SqlClient sempre retorna um Objeto|`SqlDbType.Udt` se <xref:Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute> estiver presente; caso contrário `Variant`|

> [!NOTE]
> Conversões de decimal para outros tipos são conversões de limitação que arredondam o valor decimal para o valor inteiro mais próximo de zero. Se o resultado da conversão não for representável no tipo de destino, um <xref:System.OverflowException> será gerado.

> [!NOTE]
> Quando você envia um valor de parâmetro nulo para o servidor, deve especificar <xref:System.DBNull>, não `null` (`Nothing` no Visual Basic). O valor nulo no sistema é um objeto vazio que não tem nenhum valor. <xref:System.DBNull> é usado para representar valores nulos.

## <a name="deriving-parameter-information"></a>Derivar informações de parâmetro

Os parâmetros também podem ser derivados de um procedimento armazenado usando a classe `DbCommandBuilder`. A classe `SqlCommandBuilder` fornece um método estático, `DeriveParameters`, que preenche automaticamente a coleção de parâmetros de um objeto de comando que usa informações de parâmetro de um procedimento armazenado. Observe que `DeriveParameters` substitui qualquer informação de parâmetro existente para o comando.

> [!NOTE]
> Derivar informações de parâmetro provoca uma penalidade de desempenho porque exige ida e volta adicional à fonte de dados para recuperar as informações. Se as informações de parâmetro forem conhecidas em tempo de design, você poderá melhorar o desempenho do seu aplicativo definindo os parâmetros explicitamente.

Para obter mais informações, confira [Gerar comandos com CommandBuilders](generate-commands-with-commandbuilders.md).

## <a name="using-parameters-with-a-sqlcommand-and-a-stored-procedure"></a>Usar parâmetros com um SqlCommand e um procedimento armazenado

Os procedimentos armazenados oferecem várias vantagens em aplicativos orientados a dados. Ao usar procedimentos armazenados, as operações de banco de dados podem ser encapsuladas em um único comando, otimizadas para melhor desempenho e aprimoradas com segurança adicional. Embora um procedimento armazenado possa ser chamado passando o nome do procedimento armazenado seguido por argumentos de parâmetros como uma instrução SQL, usar a coleção de <xref:System.Data.Common.DbCommand.Parameters%2A> do objeto <xref:System.Data.Common.DbCommand> do ADO.NET permite definir mais explicitamente os parâmetros de procedimento armazenados e acessar parâmetros de saída e valores de retorno.

> [!NOTE]
> As instruções parametrizadas são executadas no servidor usando `sp_executesql,` que permite a reutilização do plano de consulta. Os cursores locais ou variáveis no lote `sp_executesql` não são visíveis para os lotes que chamam `sp_executesql`. As alterações no contexto de banco de dados duram somente até o final da instrução `sp_executesql`. Para saber mais, confira [sp_executesql (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-executesql-transact-sql).

Ao usar parâmetros com um <xref:Microsoft.Data.SqlClient.SqlCommand> para executar um procedimento armazenado do SQL Server, os nomes dos parâmetros adicionados à coleção de <xref:Microsoft.Data.SqlClient.SqlCommand.Parameters%2A> devem coincidir com os nomes dos marcadores de parâmetros no procedimento armazenado. O Provedor de Dados do Microsoft SqlClient para SQL Server não oferece suporte ao espaço reservado de ponto de interrogação (?) para transmitir parâmetros a uma instrução SQL ou a um procedimento armazenado. Ele trata parâmetros no procedimento armazenado como parâmetros nomeados e procura marcadores de parâmetro compatíveis. Por exemplo, o procedimento armazenado `CustOrderHist` é definido usando um parâmetro chamado `@CustomerID`. Quando o código executar o procedimento armazenado, também deverá usar um parâmetro chamado `@CustomerID`.

```sql
CREATE PROCEDURE dbo.CustOrderHist @CustomerID varchar(5)
```

### <a name="example"></a>Exemplo

Este exemplo demonstra como chamar um procedimento armazenado do SQL Server no banco de dados de exemplo `Northwind`. O nome do procedimento armazenado é `dbo.SalesByCategory` e tem um parâmetro de entrada chamado `@CategoryName` com um tipo de dados de `nvarchar(15)`. O código cria um novo <xref:Microsoft.Data.SqlClient.SqlConnection> dentro de um bloco using para que a conexão seja descartada quando o procedimento terminar. Os objetos <xref:Microsoft.Data.SqlClient.SqlCommand> e <xref:Microsoft.Data.SqlClient.SqlParameter> são criados e suas propriedades são definidas. Um <xref:Microsoft.Data.SqlClient.SqlDataReader> executa o `SqlCommand` e retorna o conjunto de resultados do procedimento armazenado, exibindo a saída na janela do console.

> [!NOTE]
> Em vez de criar objetos `SqlCommand` e `SqlParameter` e depois definir as propriedades em instruções separadas, você poderá eleger usar um dos construtores sobrecarregados para definir várias propriedades em uma única instrução.

[!code-csharp[DataWorks SqlClient.StoredProcedure#1](~/../sqlclient/doc/samples/SqlCommand_StoredProcedure.cs#1)]

## <a name="see-also"></a>Confira também

- [Comandos e parâmetros](commands-parameters.md)
- [Mapeamentos de tipo de dados no ADO.NET](data-type-mappings-ado-net.md)

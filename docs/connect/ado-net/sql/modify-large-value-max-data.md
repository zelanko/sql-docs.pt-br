---
title: Modificando dados de valor grande (máx) no ADO.NET
description: Descreve como trabalhar com tipos de dados de valores grandes.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 8aca5f00-d80e-4320-81b3-016d0466f7ee
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 9acbd8fb795fe1a14e77e5d746f729d37c11cc8d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896683"
---
# <a name="modifying-large-value-max-data-in-adonet"></a>Modificando dados de valor grande (máx) no ADO.NET

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Os tipos de dados de objetos grandes (LOB) são os que excedem o tamanho de linha máximo de 8 KB. O SQL Server apresenta um especificador `max` para tipos de dados `varchar`, `nvarchar` e `varbinary` para permitir o armazenamento de valores tão grandes quanto 2^32 bytes. Colunas de tabela e variáveis Transact-SQL podem especificar tipos de dados `varchar(max)`, `nvarchar(max)` ou `varbinary(max)`. No .NET, os tipos de dados `max` podem ser buscados por um `DataReader` e também podem ser especificados como valores de parâmetro de entrada e saída sem qualquer administração especial. Para tipos de dados `varchar` grandes, os dados podem ser recuperados e atualizados incrementalmente.  
  
Os tipos de dados `max` podem ser usados para comparações, como variáveis Transact-SQL, e para concatenação. Eles também podem ser usados nas cláusulas DISTINCT, ORDER BY, GROUP BY de uma instrução SELECT e também em agregações, ingressos e subconsultas.

Confira [Usar tipos de dados de valores grandes](https://go.microsoft.com/fwlink/?LinkId=120498) nos Manuais Online do SQL Server para obter mais detalhes sobre os tipos de valores grandes.
  
## <a name="large-value-type-restrictions"></a>Restrições de tipos de valores grandes  
As seguintes restrições se aplicam aos tipos de dados `max` que não existem para tipos de dados menores:  
  
- Um `sql_variant` não pode conter um tipo de dados `varchar` grande.  
  
- As colunas `varchar` grandes não podem ser especificadas como uma coluna de chave em um índice. Elas são permitidas em uma coluna incluída em um índice não clusterizado.  
  
- As colunas `varchar` grandes não podem ser usadas como colunas de chave de particionamento.  
  
## <a name="working-with-large-value-types-in-transact-sql"></a>Trabalhar com tipos de valores grandes em Transact-SQL  
A função `OPENROWSET` do Transact-SQL é um método único de conectar e acessar dados remotos. `OPENROWSET` pode ser referenciada na cláusula FROM de uma consulta como se fosse um nome de tabela. Também pode ser referenciada como a tabela de destino de uma instrução INSERT, UPDATE ou DELETE.  
  
A função `OPENROWSET` inclui o provedor de conjunto de linhas `BULK` que permite ler dados diretamente de um arquivo sem carregar os dados em uma tabela de destino. Isso o habilita a usar `OPENROWSET` com uma instrução INSERT SELECT simples.  
  
Os argumentos de opção `OPENROWSET BULK` fornecem o controle significativo sobre os pontos de início e término da leitura de dados, como tratar erros e como os dados são interpretados. Por exemplo, você pode especificar que o arquivo de dados seja lido como uma única linha, um conjunto de linhas de coluna única do tipo `varbinary`, `varchar` ou `nvarchar`. Para obter a sintaxe e as opções completas, confira Manuais Online do SQL Server.  
  
O exemplo a seguir insere uma foto na tabela ProductPhoto do banco de dados de amostra do AdventureWorks. Ao usar o provedor `BULK OPENROWSET`, você deverá fornecer a lista de colunas nomeada mesmo se não estiver inserindo valores em cada coluna. A chave primária nesse caso é definida como uma coluna de identidade e pode ser omitida da lista de colunas. Observe que você também deve fornecer um nome de correlação no final da instrução `OPENROWSET` que, nesse caso, é ThumbnailPhoto. Isso se correlaciona com a coluna na tabela `ProductPhoto` na qual o arquivo está sendo carregado.  
  
```sql
INSERT Production.ProductPhoto (  
    ThumbnailPhoto,   
    ThumbnailPhotoFilePath,   
    LargePhoto,   
    LargePhotoFilePath)  
SELECT ThumbnailPhoto.*, null, null, N'tricycle_pink.gif'  
FROM OPENROWSET   
    (BULK 'c:\images\tricycle.jpg', SINGLE_BLOB) ThumbnailPhoto  
```  
  
## <a name="updating-data-using-update-write"></a>Atualização de dados que usam UPDATE .WRITE  
A instrução Transact-SQL UPDATE tem uma nova sintaxe WRITE para modificar o conteúdo das colunas `varchar(max)`, `nvarchar(max)` ou `varbinary(max)`. Isso permite que você execute atualizações parciais dos dados. A sintaxe UPDATE .WRITE é mostrada aqui na forma abreviada:  
  
UPDATE  
  
{ *\<object>* }  
  
SET  
  
{ *column_name* = { .WRITE ( *expression* , @Offset , @Length ) }  
  
O método WRITE especifica que uma seção do valor do *column_name* será modificada. A expressão é o valor que será copiado para o *column_name*, o `@Offset` é o ponto inicial no qual a expressão será escrita e o argumento `@Length` é o comprimento da seção na coluna.  
  
|Se|Então|  
|--------|----------|  
|A expressão é definida como NULL|`@Length` é ignorado, e o valor em *column_name* é truncado no `@Offset` especificado.|  
|`@Offset` é NULL|A operação de atualização acrescentará a expressão ao final do valor de *column_name* existente e `@Length` será ignorado.|  
|Se `@Offset` for maior que o comprimento do valor de column_name, o|SQL Server retornará um erro.|  
|`@Length` é NULL|A operação de atualização removerá todos os dados de `@Offset` até o final do valor de `column_name`.|  
  
> [!NOTE]
>  `@Offset` nem `@Length` poderá ser um número negativo.  
  
## <a name="example"></a>Exemplo  
Este exemplo de Transact-SQL atualiza um valor parcial em DocumentSummary, uma coluna `nvarchar(max)` na tabela de documentos no banco de dados AdventureWorks. A palavra "components" é substituída pela palavra "features" especificando a palavra de substituição, o local de início (deslocamento) da palavra a ser substituída nos dados existentes e o número de caracteres a serem substituídos (comprimento). Esse exemplo inclui instruções SELECT antes e depois da instrução UPDATE para comparar resultados.  
  
```sql
USE AdventureWorks;  
GO  
--View the existing value.  
SELECT DocumentSummary  
FROM Production.Document  
WHERE DocumentID = 3;  
GO  
-- The first sentence of the results will be:  
-- Reflectors are vital safety components of your bicycle.  
  
--Modify a single word in the DocumentSummary column  
UPDATE Production.Document  
SET DocumentSummary .WRITE (N'features',28,10)  
WHERE DocumentID = 3 ;  
GO   
--View the modified value.  
SELECT DocumentSummary  
FROM Production.Document  
WHERE DocumentID = 3;  
GO  
-- The first sentence of the results will be:  
-- Reflectors are vital safety features of your bicycle.  
```  
  
## <a name="working-with-large-value-types-in-adonet"></a>Trabalhar com tipos de valores grandes no ADO.NET  
Você pode trabalhar com tipos de valores grandes no ADO.NET especificando tipos de valores grandes como objetos <xref:Microsoft.Data.SqlClient.SqlParameter> em um <xref:Microsoft.Data.SqlClient.SqlDataReader> para retornar um conjunto de resultados ou usando <xref:Microsoft.Data.SqlClient.SqlDataAdapter> para preencher um `DataSet`/`DataTable`. Não há nenhuma diferença entre a maneira como você trabalha com um tipo de valor grande e seu tipo de dado de valor menor relacionado.  
  
### <a name="using-getsqlbytes-to-retrieve-data"></a>Como usar GetSqlBytes para recuperar dados  
O método `GetSqlBytes` de <xref:Microsoft.Data.SqlClient.SqlDataReader> pode ser usado para recuperar o conteúdo de uma coluna `varbinary(max)`. O fragmento de código a seguir aceita um objeto <xref:Microsoft.Data.SqlClient.SqlCommand> chamado `cmd` que seleciona dados `varbinary(max)` de uma tabela e um objeto <xref:Microsoft.Data.SqlClient.SqlDataReader> chamado `reader` que recupera os dados como <xref:System.Data.SqlTypes.SqlBytes>.  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBytes bytes = reader.GetSqlBytes(0);  
    }  
```  
  
### <a name="using-getsqlchars-to-retrieve-data"></a>Como usar GetSqlChars para recuperar dados  
O método `GetSqlChars` do <xref:Microsoft.Data.SqlClient.SqlDataReader> pode ser usado para recuperar o conteúdo de uma coluna `varchar(max)` ou `nvarchar(max)`. O fragmento de código a seguir aceita um objeto <xref:Microsoft.Data.SqlClient.SqlCommand> chamado `cmd`,que seleciona dados `nvarchar(max)` de uma tabela e um objeto <xref:Microsoft.Data.SqlClient.SqlDataReader> chamado `reader` que recupera os dados.   
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
{  
    SqlChars buffer = reader.GetSqlChars(0);  
}  
```  
  
### <a name="using-getsqlbinary-to-retrieve-data"></a>Como usar GetSqlBinary para recuperar dados  
O método `GetSqlBinary` de um <xref:Microsoft.Data.SqlClient.SqlDataReader> pode ser usado para recuperar o conteúdo de uma coluna `varbinary(max)`. O fragmento de código a seguir aceita um objeto <xref:Microsoft.Data.SqlClient.SqlCommand> chamado `cmd` que seleciona dados `varbinary(max)` de uma tabela e um objeto <xref:Microsoft.Data.SqlClient.SqlDataReader> chamado `reader` que recupera os dados como um fluxo <xref:System.Data.SqlTypes.SqlBinary>.  
  
```csharp  
reader = cmd.ExecuteReader(CommandBehavior.CloseConnection);  
while (reader.Read())  
    {  
        SqlBinary binaryStream = reader.GetSqlBinary(0);  
    }  
```  
  
### <a name="using-getbytes-to-retrieve-data"></a>Como usar GetBytes para recuperar dados  
O método `GetBytes` de um <xref:Microsoft.Data.SqlClient.SqlDataReader> lê um fluxo de bytes do deslocamento de coluna especificado na matriz de bytes começando com o deslocamento de matriz especificado. O fragmento de código a seguir aceita um objeto <xref:Microsoft.Data.SqlClient.SqlDataReader> chamado `reader` que recupera bytes em uma matriz de bytes. Observe que, ao contrário de `GetSqlBytes`, `GetBytes` requer um tamanho para o buffer da matriz.  
  
```csharp  
while (reader.Read())  
{  
    byte[] buffer = new byte[4000];  
    long byteCount = reader.GetBytes(1, 0, buffer, 0, 4000);  
}  
```  
  
### <a name="using-getvalue-to-retrieve-data"></a>Como usar GetValue para recuperar dados  
O método `GetValue` de um <xref:Microsoft.Data.SqlClient.SqlDataReader> lê o valor do deslocamento de coluna especificado em uma matriz. O fragmento de código a seguir aceita um objeto <xref:Microsoft.Data.SqlClient.SqlDataReader> chamado `reader` que recupera dados binários do deslocamento da primeira coluna e, em seguida, dados da cadeia de caracteres do deslocamento da segunda coluna.  
  
```csharp  
while (reader.Read())  
{  
    // Read the data from varbinary(max) column  
    byte[] binaryData = (byte[])reader.GetValue(0);  
  
    // Read the data from varchar(max) or nvarchar(max) column  
    String stringData = (String)reader.GetValue(1);  
}  
```  
  
## <a name="converting-from-large-value-types-to-clr-types"></a>Conversão de tipos de valores grandes para tipos CLR  
Você pode converter o conteúdo de uma coluna `varchar(max)` ou `nvarchar(max)` usando qualquer um dos métodos de conversão de cadeia de caracteres, como `ToString`. O fragmento de código a seguir aceita um objeto <xref:Microsoft.Data.SqlClient.SqlDataReader> chamado `reader` que recupera os dados.  
  
```csharp  
while (reader.Read())  
{  
     string str = reader[0].ToString();  
     Console.WriteLine(str);  
}  
```  
  
### <a name="example"></a>Exemplo  
O código a seguir recupera o nome e o objeto `LargePhoto` da tabela `ProductPhoto` no banco de dados `AdventureWorks` e salva-os em um arquivo. O assembly precisa ser compilado com uma referência ao namespace <xref:System.Drawing>.  O método <xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlBytes%2A> do <xref:Microsoft.Data.SqlClient.SqlDataReader> retorna um objeto <xref:System.Data.SqlTypes.SqlBytes> que expõe uma propriedade `Stream`. O código usa isso para criar um novo objeto `Bitmap` e o salva no Gif `ImageFormat`.  
  
[!code-csharp[DataWorks SqlBytes_Stream#1](~/../sqlclient/doc/samples/SqlBytes_Stream.cs#1)]
  
## <a name="using-large-value-type-parameters"></a>Como usar parâmetros de tipos de valores grandes  
Os tipos de valores grandes podem ser usados em objetos <xref:Microsoft.Data.SqlClient.SqlParameter> da mesma maneira que você usa tipos de valores menores em objetos <xref:Microsoft.Data.SqlClient.SqlParameter>. Você pode recuperar tipos de valores grandes como valores <xref:Microsoft.Data.SqlClient.SqlParameter>, conforme mostrado no exemplo a seguir. O código pressupõe que o seguinte procedimento GetDocumentSummary armazenado exista no banco de dados de exemplo AdventureWorks. O procedimento armazenado tem um parâmetro de entrada denominado @DocumentID e retorna o conteúdo da coluna DocumentSummary no parâmetro de saída @DocumentSummary.  
  
```sql
CREATE PROCEDURE GetDocumentSummary   
(  
    @DocumentID int,  
    @DocumentSummary nvarchar(MAX) OUTPUT  
)  
AS  
SET NOCOUNT ON  
SELECT  @DocumentSummary=Convert(nvarchar(MAX), DocumentSummary)  
FROM    Production.Document  
WHERE   DocumentID=@DocumentID  
```  
  
### <a name="example"></a>Exemplo  
O código ADO.NET cria objetos <xref:Microsoft.Data.SqlClient.SqlConnection> e <xref:Microsoft.Data.SqlClient.SqlCommand> para executar o procedimento armazenado GetDocumentSummary e recuperar o resumo do documento, que é armazenado como um tipo de valor grande. O código a seguir transmite um valor para o parâmetro de entrada @DocumentID e exibe os resultados repassados no parâmetro de saída @DocumentSummary na janela do console.  
  
[!code-csharp[DataWorks SqlParameter_Value#1](~/../sqlclient/doc/samples/SqlParameter_Value.cs#1)]
  
## <a name="next-steps"></a>Próximas etapas
- [Dados binários e de valor grande do SQL Server](sql-server-binary-large-value-data.md)
- [Operações de dados do SQL Server no ADO.NET](sql-server-data-operations.md)

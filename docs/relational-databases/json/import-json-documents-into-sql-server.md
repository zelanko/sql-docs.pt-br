---
title: Importar documentos JSON para o SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0e908ec0-7173-4cd2-8f48-2700757b53a5
caps.latest.revision: 5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 9045ebe77cf2f60fecad22672f3f055d8c5fdff2
ms.openlocfilehash: 95489b4e72f1321f7e1139f06040eb81a5956b15
ms.contentlocale: pt-br
ms.lasthandoff: 07/31/2017

---
# <a name="import-json-documents-into-sql-server"></a>Importar documentos JSON para o SQL Server
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Este tópico descreve como importar arquivos JSON para o SQL Server. No momento, há muitos documentos JSON armazenados em arquivos. Informações de log de aplicativos em arquivos JSON, sensores que geram informações armazenadas em arquivos JSON e assim por diante. É importante ser capaz de ler os dados JSON armazenados em arquivos, carregar os dados no SQL Server e analisá-los.

## <a name="import-a-json-document-into-a-single-column"></a>Importar um documento JSON em uma única coluna
**OPENROWSET(BULK)** é uma função com valor de tabela que pode ler dados de qualquer arquivo na unidade local ou rede, se o SQL Server tiver acesso de leitura para esse local. Ela retorna uma tabela com uma única coluna com o conteúdo do arquivo. Há várias opções que podem ser usadas com a função OPENROWSET(BULK), como separadores. Mas, no caso mais simples, você pode simplesmente carregar todo o conteúdo de um arquivo como um valor de texto. (Esse valor grande único é conhecido como um objeto grande de caractere único ou SINGLE_CLOB.) 

Aqui está um exemplo da função **OPENROWSET(BULK)** que lê o conteúdo de um arquivo JSON e retorna para o usuário como um único valor:

```sql
SELECT BulkColumn
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j
```

OPENJSON(BULK) lê o conteúdo do arquivo e o retorna em `BulkColumn`.

Também é possível carregar o conteúdo do arquivo em uma variável local ou uma tabela, conforme mostrado no exemplo a seguir:

```sql
-- Load file contents into a variable
SELECT @json = BulkColumn
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j

-- Load file contents into a table 
SELECT BulkColumn
 INTO #temp 
 FROM OPENROWSET (BULK 'C:\JSON\Books\book.json', SINGLE_CLOB) as j
```

Depois de carregar o conteúdo do arquivo JSON, você pode salvar o texto JSON em uma tabela.

## <a name="import-multiple-json-documents"></a>Importar vários documentos JSON
Use a mesma abordagem para carregar um conjunto por vez de arquivos JSON do sistema de arquivos em uma variável local. Suponha que os arquivos são nomeados como `book<index>.json`.
  
```sql
DECLARE @i INT = 1
DECLARE @json AS NVARCHAR(MAX)

WHILE(@i < 10)
BEGIN
    SET @file = 'C:\JSON\Books\book' + cast(@i AS VARCHAR(5)) + '.json';
    SELECT @json = BulkColumn FROM OPENROWSET (BULK (@file), SINGLE_CLOB) AS j
    SELECT * FROM OPENJSON(@json) AS json
    -- Optionally, save the JSON text in a table.
    SET @i = @i + 1 ;
END
```

## <a name="import-json-documents-from-azure-file-storage"></a>Importar documentos JSON do Azure File Storage
Também é possível usar OPENROWSET(BULK) conforme descrito acima para ler os arquivos JSON de outros locais de arquivos que o SQL Server pode acessar. Por exemplo, o Azure File Storage dá suporte ao protocolo SMB. Como resultado, você pode mapear uma unidade virtual local para o compartilhamento de armazenamento do Azure File usando o seguinte procedimento:
1.  Crie uma conta de armazenamento do arquivo (por exemplo, `mystorage`), um compartilhamento de arquivo (por exemplo, `sharejson`) e uma pasta no Azure File Storage usando o portal do Azure ou o Azure PowerShell.
2.  Carregar alguns arquivos JSON no compartilhamento de armazenamento de arquivos.
3.  Crie uma regra de firewall de saída no Firewall do Windows no computador que permite a porta 445. Observe que o seu provedor de serviços de Internet pode bloquear essa porta. Se você receber um erro DNS (erro 53) na etapa seguinte,então você não abriu a porta 445 ou seu ISP está bloqueando a porta.
4. Monte o compartilhamento do Armazenamento de Arquivos do Azure como uma unidade local (por exemplo, `T:`).

    Esta é a sintaxe do comando:

    ```dos
    net use [drive letter] \\[storage name].file.core.windows.net\[share name] /u:[storage account name] [storage account access key]
    ```

    Veja este exemplo que atribui a letra da unidade local `T:` ao compartilhamento de Armazenamento de Arquivos do Azure:

    ```dos
    net use t: \\mystorage.file.core.windows.net\sharejson /u:myaccount hb5qy6eXLqIdBj0LvGMHdrTiygkjhHDvWjUZg3Gu7bubKLg==
    ```

    Você pode encontrar a chave de conta de armazenamento e a chave de acesso da conta de armazenamento primária ou secundária na seção Chaves em Configurações no portal do Azure.

5.  Agora você pode acessar os arquivos JSON do compartilhamento de Armazenamento de Arquivos do Azure usando a unidade mapeada, conforme mostrado no exemplo a seguir:

    ```sql
    SELECT book.* FROM
     OPENROWSET(BULK N't:\books\books.json', SINGLE_CLOB) AS json
     CROSS APPLY OPENJSON(BulkColumn)
     WITH( id nvarchar(100), name nvarchar(100), price float,
        pages_i int, author nvarchar(100)) AS book
    ```

Para mais informações sobre o Azure File Storage, consulte [Armazenamento de arquivo](https://azure.microsoft.com/en-us/services/storage/files/).

## <a name="import-json-documents-from-azure-blob-storage"></a>Importar documentos JSON do Armazenamento de Blobs do Azure

Você pode carregar arquivos diretamente no Banco de Dados SQL do Azure do Armazenamento de Blobs do Azure com o comando T-SQL BULK INSERT ou a função OPENROWSET.

Primeiro, crie uma fonte de dados externa, como mostrado no exemplo a seguir.

```sql
CREATE EXTERNAL DATA SOURCE MyAzureBlobStorage
 WITH ( TYPE = BLOB_STORAGE,
        LOCATION = 'https://myazureblobstorage.blob.core.windows.net',
        CREDENTIAL= MyAzureBlobStorageCredential);
```

Em seguida, execute um comando BULK INSERT com a opção DATA_SOURCE.

```sql
BULK INSERT Product
FROM 'data/product.dat'
WITH ( DATA_SOURCE = 'MyAzureBlobStorage');
```

Para obter mais informações e um exemplo OPENROWSET, consulte [Carregar arquivos do Armazenamento de Blobs do Azure no Banco de Dados SQL do Azure](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/02/23/loading-files-from-azure-blob-storage-into-azure-sql-database/).

## <a name="parse-json-documents-into-rows-and-columns"></a>Analisar documentos JSON em linhas e colunas
Em vez de ler um arquivo JSON inteiro como um único valor, pode ser útil analisá-lo e retornar os livros no arquivo e suas propriedades em linhas e colunas. Este exemplo usa um arquivo JSON [deste site](https://github.com/tamingtext/book/blob/master/apache-solr/example/exampledocs/books.json) que contém uma lista de livros.

### <a name="example-1"></a>Exemplo 1
No exemplo mais simples, você pode carregar apenas a lista inteira do arquivo. 

```sql
SELECT value
 FROM OPENROWSET (BULK 'C:\JSON\Books\books.json', SINGLE_CLOB) as j
 CROSS APPLY OPENJSON(BulkColumn)
```

### <a name="example-2"></a>Exemplo 2
OPENROWSET lê um valor de texto simples do arquivo, retorna-o como uma BulkColumn e passa para a função OPENJSON. O OPENJSON percorre a matriz de objetos JSON da matriz BulkColumn e retorna um livro em cada linha formatado como JSON:

```json
{"id":"978-0641723445″, "cat":["book","hardcover"], "name":"The Lightning Thief", … 
{"id":"978-1423103349″, "cat":["book","paperback"], "name":"The Sea of Monsters", … 
{"id":"978-1857995879″, "cat":["book","paperback"], "name":"Sophie’s World : The Greek … 
{"id":"978-1933988177″, "cat":["book","paperback"], "name":"Lucene in Action, Second … 
```

### <a name="example-3"></a>Exemplo 3
A função OPENJSON pode analisar o conteúdo do JSON e transformá-lo em uma tabela ou em um conjunto de resultados. O exemplo a seguir carrega o conteúdo, analisa o JSON carregado e retorna os cinco campos como colunas:

```sql
SELECT book.*
 FROM OPENROWSET (BULK 'C:\JSON\Books\books.json', SINGLE_CLOB) as j
 CROSS APPLY OPENJSON(BulkColumn)
 WITH( id nvarchar(100), name nvarchar(100), price float,
 pages_i int, author nvarchar(100)) AS book
```

Neste exemplo, OPENROWSET(BULK) lê o conteúdo do arquivo e passa esse conteúdo para a função OPENJSON com um esquema definido para a saída. O OPENJSON corresponde a propriedades em objetos JSON usando nomes de coluna. Por exemplo, a propriedade `price` é retornada como uma coluna `price` e convertida para o tipo de dados float. Estes são os resultados:

|ID|Nome|price|pages_i|Autor
|---|---|---|---|---|
978-0641723445|O ladrão de raios|12,5|384|Rick Riordan| 
978-1423103349|O mar de monstros|6,49|304|Rick Riordan| 
978-1857995879|O mundo de Sofia|3.07|64|Jostein Gaarder| 
978-1933988177|Lucene em ação, Second Edition|30,5|475|Michael McCandless|
||||||

Agora você pode retornar esta tabela ao usuário ou carregar os dados em outra tabela.

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>Saiba mais sobre o suporte interno a JSON no SQL Server  
Para ver várias soluções específicas, casos de uso e recomendações, consulte as [postagens no blog sobre o suporte interno a JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) no SQL Server e no Banco de Dados SQL do Azure, publicadas por Jovan Popovic, gerente de programas da Microsoft.
  
## <a name="see-also"></a>Consulte também
[Converter dados JSON em linhas e colunas com OPENJSON](../../relational-databases/json/convert-json-data-to-rows-and-columns-with-openjson-sql-server.md)



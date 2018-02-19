---
title: "Atualizado — Documentos de bancos de dados relacionais | Microsoft Docs"
description: "Exibir trechos de conteúdo atualizado para documentação de Bancos de Dados Relacionais alterada recentemente."
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: relational-databases
ms.date: 02/03/2018
ms.openlocfilehash: 38f9ee55137c54adddb07fbe9f3b74dd43d51a3a
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-relational-databases-docs"></a>Novos e recém-atualizados: documentos de Bancos de Dados Relacionais



Quase todos os dias a Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/). Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **03-12-2017** &nbsp; até &nbsp; **03-02-2018**
- *Área de assunto:* &nbsp; **Bancos de dados relacionais**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Armazenar documentos JSON no SQL Server ou no Banco de Dados SQL](json/store-json-documents-in-sql-tables.md)
2. [Avaliação de Vulnerabilidades SQL](security/sql-vulnerability-assessment.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Inicialização de arquivo de bancos de dados](#TitleNum_1)
2. [Banco de dados tempdb](#TitleNum_2)
3. [Dados JSON no SQL Server](#TitleNum_3)
4. [Lição 1: conectando-se ao Mecanismo de Banco de Dados](#TitleNum_4)
5. [Gerenciar o tamanho do arquivo de log de transações](#TitleNum_5)
6. [bcp_bind](#TitleNum_6)
7. [Guia de criação de índice do SQL Server](#TitleNum_7)
8. [sp_execute_external_script (Transact-SQL)](#TitleNum_8)
9. [Criar chaves primárias](#TitleNum_9)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-database-file-initializationdatabasesdatabase-instant-file-initializationmd"></a>1. &nbsp; [Inicialização de arquivo de bancos de dados](databases/database-instant-file-initialization.md)

*Atualizado: 23-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Próximo](#TitleNum_2))

<!-- Source markdown line 81.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c5f2aa53a8b43d4c43e0602cf945cb7c7028a27d 04c261c6588af1f53cda2fce3e9a86167c50b686  (PR=4702  ,  Filename=database-instant-file-initialization.md  ,  Dirpath=docs\relational-databases\databases\  ,  MergeCommitSha40=3206a31870f8febab7d1718fa59fe0590d4d45db) -->



```
Database Instant File Initialization: disabled. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.
```

**Aplica-se a:** SQL Server (começando com o SQL Server 2012 SP4, SQL Server 2014 SP2 e SQL Server 2016 até o SQL Server de 2017)

**Considerações sobre segurança**

Ao usar a IFI (Inicialização Instantânea de Arquivo), como o conteúdo excluído do disco é substituído somente à medida que novos dados são gravados nos arquivos, o conteúdo excluído poderá ser acessado por uma entidade de segurança não autorizada, até que outros dados sejam gravados nessa área específica do arquivo de dados. Embora o arquivo de banco de dados esteja associado à instância do SQL Server, esse risco de divulgação de informações é reduzido pela DACL (lista de controle de acesso discricionário) no arquivo. Essa DACL permite acesso de arquivo somente à conta de serviço do SQL Server e ao administrador local. Porém, quando o arquivo é desassociado, ele pode ser acessado por um usuário ou serviço que não tenha SE\_MANAGE\_NOME_DO_VOLUME. Existe uma consideração similar quando é feito o backup do banco de dados: se o arquivo de backup não estiver protegido com uma DACL adequada, o conteúdo excluído poderá ficar disponível para um usuário ou um serviço não autorizado.

Outra consideração é que, quando um arquivo é aumentado usando IFI, um administrador do SQL Server pode, potencialmente, acessar o conteúdo da página bruta e ver o conteúdo excluído anteriormente.

Se os arquivos de banco de dados estão hospedados em uma rede de área de armazenamento, também é possível que a rede de área de armazenamento apresente sempre novas páginas como pré-inicializadas e, fazer com que o sistema operacional reinicialize as páginas, poderá gerar uma sobrecarga desnecessária.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-tempdb-databasedatabasestempdb-databasemd"></a>2. &nbsp; [Banco de dados tempdb](databases/tempdb-database.md)

*Atualizado: 17-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_1) | [Próximo](#TitleNum_3))

<!-- Source markdown line 100.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 337555ea28f4c3fdd6b78f1bfb4d62607a6bf92d 3257c92d6e2a88968fc44e5f6262c02cd0624635  (PR=0  ,  Filename=tempdb-database.md  ,  Dirpath=docs\relational-databases\databases\  ,  MergeCommitSha40=45e6082acc29ba306525e7c08d2c22cc2b86eec3) -->



 Para obter uma descrição dessas opções de banco de dados, consulte [Opções ALTER DATABASE SET (Transact-SQL)](databases/../../t-sql/statements/alter-database-transact-sql-set-options.md).

**Banco de dados tempdb no Banco de Dados SQL**


|SLO|Tamanho máximo do arquivo de dados do tempdb (MBs)|Nº de arquivos de dados do tempdb|Tamanho máximo de dados do tempdb (MB)|
|---|---:|---:|---:|
|Basic|14.225|1|14.225|
|S0|14.225|1|14.225|
|S1|14.225|1|14.225|
|S2|14.225| 1|14.225|
|S3|32.768|1|32.768|
|S4|32.768|2|65.536|
|S6|32.768|3|98.304|
|S7|32.768|6|196.608|
|S9|32.768|12|393.216|
|S12|32.768|12|393.216|
|P1|32.768|12|393.216|
|P2|32.768|12|393.216|
|P4|32.768|12|393.216|
|P6|32.768|12|393.216|
|P11|32.768|12|393.216|
|P15|32.768|12|393.216|
|Pools Elásticos Premium (todas as configurações de DTU)|14.225|12|170.700|
|Pools Elásticos Standard (todas as configurações de DTU)|14.225|12|170.700|
|Pools Elásticos Básicos (todas as configurações de DTU)|14.225|12|170.700|
||||




&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-json-data-in-sql-serverjsonjson-data-sql-servermd"></a>3. &nbsp; [Dados JSON no SQL Server](json/json-data-sql-server.md)

*Atualizado: 01-02-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_2) | [Próximo](#TitleNum_4))

<!-- Source markdown line 233.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 62dd9c68d8cb72d6bf51b941a0731224514f0a7f 19e276637a463b412f2c29a84f9fb7d0b0f5fcc5  (PR=4783  ,  Filename=json-data-sql-server.md  ,  Dirpath=docs\relational-databases\json\  ,  MergeCommitSha40=73f18ae24a9a48234bf997ee9a2ef441bc4918b9) -->



-   [Loading GeoJSON data into SQL Server 2016](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/01/05/loading-geojson-data-into-sql-server/) (Carregando dados GeoJSON no SQL Server 2016)

**Analisar dados JSON com consultas SQL**

Se precisar filtrar ou agregar dados JSON para fins de relatório, você poderá usar **OPENJSON** para transformar o JSON em um formato relacional. Você pode usar o Transact-SQL padrão e funções internas para preparar os relatórios.

```
SELECT Tab.Id, SalesOrderJsonData.Customer, SalesOrderJsonData.Date
FROM   SalesOrderRecord AS Tab
          CROSS APPLY
     OPENJSON (Tab.json, N'$.Orders.OrdersArray')
           WITH (
              Number   varchar(200) N'$.Order.Number',
              Date     datetime     N'$.Order.Date',
              Customer varchar(200) N'$.AccountNumber',
              Quantity int          N'$.Item.Quantity'
           )
  AS SalesOrderJsonData
WHERE JSON_VALUE(Tab.json, '$.Status') = N'Closed'
ORDER BY JSON_VALUE(Tab.json, '$.Group'), Tab.DateModified
```



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-lesson-1-connecting-to-the-database-enginelesson-1-connecting-to-the-database-enginemd"></a>4. &nbsp; [Lição 1: conectando-se ao mecanismo de banco de dados](lesson-1-connecting-to-the-database-engine.md)

*Atualizado: 13-12-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_3) | [Próximo](#TitleNum_5))

<!-- Source markdown line 79.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3c070935895450fd2ea054e2be9e1c48f7dc2b6c 0c386e3d47fb7f8f1e63b9301f0cafec2bc88ab0  (PR=4282  ,  Filename=lesson-1-connecting-to-the-database-engine.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=6e016a4ffd28b09456008f40ff88aef3d911c7ba) -->



2.  Selecione **Mecanismo de Banco de Dados**.

    ![object-explorer](../relational-databases/media/object-explorer.png)

3.  Na caixa **Nome do servidor**, digite o nome da instância do mecanismo de banco de dados. Para a instância padrão do SQL Server, o nome do servidor é o nome do computador. Para uma instância nomeada do SQL Server, o nome do servidor é *<nome_do_computador>***\\***<nome_da_instância>,* por exemplo, **ACCTG_SRVR\SQLEXPRESS**. A captura de tela a seguir mostra a conexão à instância padrão (sem nome) do SQL Server em um computador chamado 'PracticeComputer'. O usuário conectado no Windows é Marina do domínio Contoso. Ao usar a Autenticação do Windows, não é possível alterar o nome de usuário.

    ![connect-to-server](../relational-databases/media/connect-to-server.png)

4.  Clique em **Conectar**.

> [!NOTE]
> Este tutorial presume que você não esteja familiarizado com o SQL Server e que não tenha problemas específicos em estabelecer a conexão. Isso deve ser suficiente para a maioria das pessoas e mantém este tutorial simples. Para obter as etapas de solução de problemas, consulte [Solucionando problemas de conexão com o Mecanismo de Banco de Dados do SQL Server](../database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine.md).

**<a name="additional"></a>Autorizando conexões adicionais**

Agora que você se conectou ao SQL Server como um administrador, uma de suas primeiras tarefas é autorizar que outros usuários se conectem. Você faz isso criando um logon e autorizando esse logon para acessar um banco de dados como um usuário. Logons podem ser de autenticação do Windows, que usam credenciais do Windows ou logons de autenticação do SQL Server, que armazenam informações de autenticação no SQL Server e são independentes de suas credenciais do Windows. Use a autenticação do Windows sempre que possível.



&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-manage-the-size-of-the-transaction-log-filelogsmanage-the-size-of-the-transaction-log-filemd"></a>5. &nbsp; [Gerenciar o tamanho do arquivo de log de transações](logs/manage-the-size-of-the-transaction-log-file.md)

*Atualizado: 17-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_4) | [Próximo](#TitleNum_6))

<!-- Source markdown line 105.  ms.author= "jhubbard".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5847b31cf8f6003a380f0c8aaa289efdc55be678 84e45320d81db218cde17fbf8b9668a9ac3805a7  (PR=0  ,  Filename=manage-the-size-of-the-transaction-log-file.md  ,  Dirpath=docs\relational-databases\logs\  ,  MergeCommitSha40=45e6082acc29ba306525e7c08d2c22cc2b86eec3) -->



-   Um pequeno incremento de aumento pode gerar um número excessivo de [VLFs](logs/../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) pequenos e pode reduzir o desempenho. Para determinar a distribuição ideal de VLF para o tamanho atual do log de transações de todos os bancos de dados em uma instância determinada e os incrementos de crescimento necessários para alcançar o tamanho necessário, consulte este [script](http://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs).

-   Um grande incremento de aumento pode gerar um número pequeno de [VLFs](logs/../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md#physical_arch) grandes e também pode afetar o desempenho. Para determinar a distribuição ideal de VLF para o tamanho atual do log de transações de todos os bancos de dados em uma instância determinada e os incrementos de crescimento necessários para alcançar o tamanho necessário, consulte este [script](http://github.com/Microsoft/tigertoolbox/tree/master/Fixing-VLFs).

-   Mesmo com o aumento automático habilitado, você pode receber uma mensagem informando que o log de transações está cheio, caso ele não possa aumentar rápido o suficiente para atender às necessidades da consulta. Para obter mais informações sobre como alterar o incremento de aumento, consulte [Opções de arquivo e grupo de arquivos de ALTER DATABASE &#40;Transact-SQL&#41;](logs/../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md)

-   Ter vários arquivos de log em um banco de dados não melhora o desempenho de forma alguma, porque os arquivos de log de transações não usam o [preenchimento proporcional](logs/../../relational-databases/pages-and-extents-architecture-guide.md#ProportionalFill) como arquivos de dados no mesmo grupo de arquivos.

-   Os arquivos de log podem ser definidos para serem reduzidos automaticamente. No entanto, isso **não é recomendável** e a propriedade de banco de dados **auto_shrink** é definida como FALSE por padrão. Se **auto_shrink** for definido como TRUE, a redução automática reduzirá o tamanho de um arquivo apenas quando mais de 25% de seu espaço estiver inutilizado.



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-bcpbindnative-client-odbc-extensions-bulk-copy-functionsbcp-bindmd"></a>6. &nbsp; [bcp_bind](native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)

*Atualizado: 30-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_5) | [Próximo](#TitleNum_7))

<!-- Source markdown line 127.  ms.author= "genemi".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 d50791cef948ce8b3066438e317ab4d34d535258 e6f70559e7237cfc86dfc5746d218c08bec52af6  (PR=4762  ,  Filename=bcp-bind.md  ,  Dirpath=docs\relational-databases\native-client-odbc-extensions-bulk-copy-functions\  ,  MergeCommitSha40=60006e90d03fdb75b282bbc0dad3d40571bacacc) -->



 A tabela a seguir lista os tipos de dados enumerados válidos e os tipos de dados ODBC C correspondentes.

|eDataType|Tipo de C|
|-----------------------|------------|
|SQLTEXT|char *|
|SQLNTEXT|wchar_t *|
|SQLCHARACTER|char *|
|SQLBIGCHAR|char *|
|SQLVARCHAR|char *|
|SQLBIGVARCHAR|char *|
|SQLNCHAR|wchar_t *|
|SQLNVARCHAR|wchar_t *|
|SQLBINARY|unsigned char *|
|SQLBIGBINARY|unsigned char *|
|SQLVARBINARY|unsigned char *|
|SQLBIGVARBINARY|unsigned char *|
|SQLBIT|char|
|SQLBITN|char|
|SQLINT1|char|
|SQLINT2|short int|
|SQLINT4|INT|
|SQLINT8|_int64|
|SQLINTN|*cbIndicator*<br /> 1: SQLINT1<br /> 2: SQLINT2<br /> 4: SQLINT4<br /> 8: SQLINT8|
|SQLFLT4|FLOAT|
|SQLFLT8|FLOAT|
|SQLFLTN|*cbIndicator*<br /> 4: SQLFLT4<br /> 8: SQLFLT8|
|SQLDECIMALN|SQL_NUMERIC_STRUCT|
|SQLNUMERICN|SQL_NUMERIC_STRUCT|
|SQLMONEY|DBMONEY|
|SQLMONEY4|DBMONEY4|
|SQLMONEYN|*cbIndicator*<br /> 4: SQLMONEY4<br /> 8: SQLMONEY|
|SQLTIMEN|SQL_SS_TIME2_STRUCT|
|SQLDATEN|SQL_DATE_STRUCT|
|SQLDATETIM4|DBDATETIM4|
|SQLDATETIME|DBDATETIME|
|SQLDATETIMN|*cbIndicator*<br /> 4: SQLDATETIM4<br /> 8: SQLDATETIME|
|SQLDATETIME2N|SQL_TIMESTAMP_STRUCT|
|SQLDATETIMEOFFSETN|SQL_SS_TIMESTAMPOFFSET_STRUCT|
|SQLIMAGE|unsigned char *|
|SQLUDT|unsigned char *|
|SQLUNIQUEID|SQLGUID|
|SQLVARIANT|*Qualquer tipo de dados, exceto:*<br />–   text<br />–   ntext<br />–   image<br />–   varchar(max)<br />–   varbinary(max)<br />–   nvarchar(max)<br />–   xml<br />–   timestamp|
|SQLXML|*Tipos de dados C compatíveis:*<br />–   char*<br />–   wchar_t *<br />–   unsigned char *|



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-sql-server-index-design-guidesql-server-index-design-guidemd"></a>7. &nbsp; [Guia de criação de índice do SQL Server](sql-server-index-design-guide.md)

*Atualizado: 02-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_6) | [Próximo](#TitleNum_8))

<!-- Source markdown line 700.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 bd09c9e66cd3cf5f3ebebe7ffa6e937978353169 8e5cbbf0063971676a8bafefba75aa5c7c28be61  (PR=0  ,  Filename=sql-server-index-design-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=74daee358fef75a25d75c69d971d08536c5bd2be) -->



Do SQL Server 2016 em diante, é possível criar um **índice columnstore não clusterizado atualizável em uma tabela rowstore**. O índice columnstore armazena uma cópia dos dados, portanto, você precisa de armazenamento extra. No entanto, os dados no índice columnstore serão compactados em um tamanho menor do que a tabela rowstore precisa.  Com isso, você pode executar análises no índice columnstore e transações no índice rowstore ao mesmo tempo. O repositório de colunas é atualizado quando dados são alterados na tabela rowstore, assim, ambos os índices trabalham com os mesmos dados.

Do SQL Server 2016 em diante, é possível ter **um ou mais índices rowstore não clusterizados em um índice columnstore**. Fazendo isso, você pode executar buscas de tabela eficientes no columnstore subjacente. Outras opções também são disponibilizadas. Por exemplo, você pode impor uma restrição de chave primária usando uma restrição UNIQUE na tabela rowstore. Como um valor não exclusivo não poderá ser inserido na tabela rowstore, o SQL Server não pode inserir o valor no columnstore.

**Considerações sobre desempenho**


-   A definição do índice columnstore não clusterizado oferece suporte ao uso de uma condição filtrada. Para minimizar o impacto no desempenho da adição de um índice columnstore em uma tabela OLTP, use uma condição filtrada para criar um índice columnstore não clusterizado apenas nos dados inativos da sua carga de trabalho operacional.

-   Uma tabela na memória pode ter um índice columnstore. Você pode criá-lo quando a tabela for criada ou adicioná-lo mais tarde com [ALTER TABLE &#40;Transact-SQL&#41;](../t-sql/statements/alter-table-transact-sql.md). Antes do SQL Server 2016, somente uma tabela baseada em disco podia ter um índice columnstore.

Para obter mais informações, consulte [Índices columnstore – desempenho de consultas](../relational-databases/indexes/columnstore-indexes-query-performance.md).

**Diretrizes de design**


-   Uma tabela rowstore pode ter um índice columnstore não clusterizado atualizável. Antes do SQL Server 2014, o índice columnstore não clusterizado era somente leitura.



&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-spexecuteexternalscript-transact-sqlsystem-stored-proceduressp-execute-external-script-transact-sqlmd"></a>8. &nbsp; [sp_execute_external_script (Transact-SQL)](system-stored-procedures/sp-execute-external-script-transact-sql.md)

*Atualizado: 23-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_7) | [Próximo](#TitleNum_9))

<!-- Source markdown line 207.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0ee4d591ae9d9a5c015eec98aad9ccbb86268761 ac9b439c23ffae5fcc77639de6ff955763cf5844  (PR=4696  ,  Filename=sp-execute-external-script-transact-sql.md  ,  Dirpath=docs\relational-databases\system-stored-procedures\  ,  MergeCommitSha40=d7dcbcebbf416298f838a39dd5de6a46ca9f77aa) -->



Para gerar um modelo semelhante usando Python, altere o identificador de idioma de `@language=N'R'` para `@language = N'Python'`e faça as modificações necessárias para o argumento `@script`. Caso contrário, todos os parâmetros funcionam do mesmo modo que para o R.

**C. Criar um modelo de Python e gerar pontuações com base nele**


Este exemplo ilustra como usar sp\_execute\_external\_script para gerar pontuações em um modelo simples de Python.

```
CREATE PROCEDURE [dbo].[py_generate_customer_scores]
AS
BEGIN

**Input query to generate the customer data**

DECLARE @input_query NVARCHAR(MAX) = N'SELECT customer, orders, items, cost FROM dbo.Sales.Orders`

EXEC sp_execute_external_script @language = N'Python', @script = N'
import pandas as pd
from sklearn.cluster import KMeans

**Get data from input query**

customer_data = my_input_data

**Define the model**

n_clusters = 4
est = KMeans(n_clusters=n_clusters, random_state=111).fit(customer_data[["orders","items","cost"]])
clusters = est.labels_
customer_data["cluster"] = clusters

OutputDataSet = customer_data
'
, @input_data_1 = @input_query
, @input_data_1_name = N'my_input_data'
WITH RESULT SETS (("CustomerID" int, "Orders" float,"Items" float,"Cost" float,"ClusterResult" float));
END;
GO
```

Títulos de coluna usados no código Python não são enviados como saída para o SQL Server. Portanto, use a instrução WITH RESULTS para especificar os nomes de coluna e tipos de dados a serem usados pelo SQL.

Para pontuação, você também pode usar a função nativa [PREDICT](system-stored-procedures/../../t-sql/queries/predict-transact-sql.md), que é normalmente mais rápida porque evita que o tempo de execução do Python ou do R seja chamado.




&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-create-primary-keystablescreate-primary-keysmd"></a>9. &nbsp; [Criar Chaves Primárias](tables/create-primary-keys.md)

*Atualizado: 18-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_8))

<!-- Source markdown line 102.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 d18b485f314cc005d624cab8a51650d3b8f55f89 9bd2e9453206e8940d30b0a01c43f9d8e1aed606  (PR=4652  ,  Filename=create-primary-keys.md  ,  Dirpath=docs\relational-databases\tables\  ,  MergeCommitSha40=6b4aae3706247ce9b311682774b13ac067f60a79) -->



**Para criar uma chave primária com um índice não clusterizado em uma nova tabela**


1.  No **Pesquisador de Objetos**, conecte-se a uma instância do Mecanismo de Banco de Dados.

2.  Na barra Padrão, clique em **Nova Consulta**.

3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo cria uma tabela e define uma chave primária na coluna `CustomerID` e um índice clusterizado em `TransactionID`.

```
    USE AdventureWorks2012;
    GO
    CREATE TABLE Production.TransactionHistoryArchive1
    (
       CustomerID uniqueidentifier DEFAULT NEWSEQUENTIALID(),
       TransactionID int IDENTITY (1,1) NOT NULL,
       CONSTRAINT PK_TransactionHistoryArchive_TransactionID PRIMARY KEY NONCLUSTERED (uniqueidentifier)
    );
    GO

    -- Now add the clustered index
    CREATE CLUSTERED INDEX CIX_TransactionID ON Production.TransactionHistoryArchive1 (TransactionID);
    GO
```







## <a name="similar-articles-about-new-or-updated-articles"></a>Artigos semelhantes sobre artigos novos ou atualizados

Esta seção lista artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que *têm* artigos novos ou atualizados recentemente


- [Novo + Atualizado (1 + 3):&nbsp; documentos sobre a **Análise Avançada para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + Atualizado (0 + 1):&nbsp; documentos sobre o **Sistema de Plataforma Analítica para SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Novo + Atualizado (0 + 1):&nbsp; documentos sobre a **Conexão ao SQL**](../connect/new-updated-connect.md)
- [Novo + Atualizado (0 + 1):&nbsp; documentos sobre o **Mecanismo de Banco de Dados para SQL**](../database-engine/new-updated-database-engine.md)
- [Novo + Atualizado (12 + 1): **documentos sobre o** Integration Services para SQL](../integration-services/new-updated-integration-services.md)
- [Novo + Atualizado (6 + 2):&nbsp; documentos sobre o **Linux para SQL**](../linux/new-updated-linux.md)
- [Novo + atualizado (15 + 0): **documentos sobre o** PowerShell para SQL](../powershell/new-updated-powershell.md)
- [Novo + Atualizado (2 + 9):&nbsp; documentos sobre **Bancos de Dados Relacionais para SQL**](../relational-databases/new-updated-relational-databases.md)
- [Novo + Atualizado (1 + 0):&nbsp; documentos sobre o **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Novo + Atualizado (1 + 1):&nbsp; documentos sobre o **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Novo + Atualizado (1 + 1):&nbsp; documentos sobre o **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Novo + Atualizado (0+1):&nbsp; documentos sobre o **SSDT (SQL Server Data Tools)**](../ssdt/new-updated-ssdt.md)
- [Novo + Atualizado (1+2):&nbsp; documentos sobre o **SSMS (SQL Server Management Studio)**](../ssms/new-updated-ssms.md)
- [Novo + Atualizado (0 + 2):&nbsp; documentos sobre o **Transact-SQL**](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Áreas de assunto que *não* têm nenhum artigo novo ou atualizado recentemente


- [Novo + Atualizado (0 + 0): documentos sobre **DMA (Assistente de Migração de Dados) para o SQL**](../dma/new-updated-dma.md)
- [Novo + atualizado (0 + 0): documentos do **ADO (ActiveX Data Objects) para SQL**](../ado/new-updated-ado.md)
- [Novo + Atualizado (0+0): documentos sobre o **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Novo + atualizado (0 + 0): documentos do **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): documentos de **Extensões DMX (Data Mining) para SQL**](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0+0): documentos sobre o **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): documentos de **Expressão MDX para SQL**](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): documentos do **ODBC (Open Database Connectivity) para SQL**](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): documentos de **Exemplos para SQL**](../sample/new-updated-sample.md)
- [Novo + atualizado (0 + 0): documentos do **SSMA (SQL Server Migration Assistant)**](../ssma/new-updated-ssma.md)
- [Novo + Atualizado (0 + 0): documentos de **Ferramentas para SQL**](../tools/new-updated-tools.md)
- [Novo + atualizado (0 + 0): documentos do **XQuery para SQL**](../xquery/new-updated-xquery.md)



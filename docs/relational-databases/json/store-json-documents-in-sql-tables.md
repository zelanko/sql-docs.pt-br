---
title: Armazenar documentos JSON no SQL Server ou no Banco de Dados SQL | Microsoft Docs
ms.description: This article describes why and how to store and index JSON documents in SQL Server or SQL Database, and how to optimize queries over the JSON documents.
ms.custom: ''
ms.date: 01/04/2018
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.openlocfilehash: 385ae3aafb58d012e6473abc0fe4b8f8f5d40eb6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62705974"
---
# <a name="store-json-documents-in-sql-server-or-sql-database"></a>Armazenar documentos JSON no SQL Server ou no Banco de Dados SQL
O SQL Server e o Banco de Dados SQL do Azure têm funções nativas do JSON que permitem analisar documentos JSON usando a linguagem SQL padrão. Agora você pode armazenar documentos JSON no SQL Server ou no Banco de Dados SQL e consultar dados JSON em um banco de dados NoSQL. Este artigo descreve as opções para armazenar documentos JSON no SQL Server ou no Banco de Dados SQL.

## <a name="classic-tables"></a>Tabelas clássicas

A maneira mais simples de armazenar documentos JSON no SQL Server ou no Banco de Dados SQL é criar uma tabela de duas colunas que contenha a ID e o conteúdo do documento. Por exemplo:

```sql
create table WebSite.Logs (
    _id bigint primary key identity,
    log nvarchar(max)
);
```

Essa estrutura é equivalente às coleções que você pode encontrar em bancos de dados de documentos clássicos. A chave primária `_id` é um valor de incremento automático que fornece um identificador exclusivo para cada documento e possibilita pesquisas rápidas. Essa estrutura é uma boa escolha para os cenários clássicos de NoSQL em que você deseja recuperar um documento pela ID ou atualizar um documento armazenado pela ID.

O tipo de dados nvarchar(max) permite armazenar documentos JSON com até 2 GB. No entanto, caso tenha certeza de que seus documentos JSON não são maiores que 8 KB, é recomendável usar NVARCHAR(4000) em vez de NVARCHAR(max) por questões de desempenho.

A tabela de exemplo criada no exemplo anterior pressupõe que os documentos JSON válidos sejam armazenados na coluna `log`. Caso deseje ter certeza de que o JSON válido é salvo na coluna `log`, adicione uma restrição CHECK à coluna. Por exemplo:

```sql
ALTER TABLE WebSite.Logs
    ADD CONSTRAINT [Log record should be formatted as JSON]
                   CHECK (ISJSON(log)=1)
```

Sempre que alguém insere ou atualiza um documento na tabela, essa restrição verifica se o documento JSON está formatado corretamente. Sem a restrição, a tabela é otimizada para inserções, porque qualquer documento JSON é adicionado diretamente à coluna sem nenhum processamento.

Ao armazenar seus documentos JSON na tabela, use a linguagem Transact-SQL padrão para consultar os documentos. Por exemplo:

```sql
SELECT TOP 100 JSON_VALUE(log, '$.severity'), AVG( CAST( JSON_VALUE(log,'$.duration') as float))
 FROM WebSite.Logs
 WHERE CAST( JSON_VALUE(log,'$.date') as datetime) > @datetime
 GROUP BY JSON_VALUE(log, '$.severity')
 HAVING AVG( CAST( JSON_VALUE(log,'$.duration') as float) ) > 100
 ORDER BY AVG( CAST( JSON_VALUE(log,'$.duration') as float) ) DESC
```

É uma grande vantagem poder usar *qualquer* função T-SQL e cláusula de consulta para consultar documentos JSON. O SQL Server e o Banco de Dados SQL não introduzem nenhuma restrição nas consultas que podem ser usadas para analisar documentos JSON. Você pode extrair valores de um documento JSON com a função `JSON_VALUE` e usá-la na consulta como qualquer outro valor.

Essa capacidade de usar a sintaxe de consulta T-SQL avançada é a principal diferença entre o SQL Server e o Banco de Dados SQL e os bancos de dados NoSQL clássicos – no Transact-SQL, provavelmente, você terá qualquer função necessária para processar dados JSON.

## <a name="indexes"></a>Índices

Se você descobrir que as consultas frequentemente pesquisam documentos por alguma propriedade (por exemplo, uma propriedade `severity` em um documento JSON), adicione um índice NONCLUSTERED clássico à propriedade para acelerar as consultas.

Crie uma coluna computada que expõe valores JSON das colunas JSON no caminho especificado (ou seja, no caminho `$.severity`) e crie um índice padrão nessa coluna computada. Por exemplo:

```sql
create table WebSite.Logs (
    _id bigint primary key identity,
    log nvarchar(max),

    severity AS JSON_VALUE(log, '$.severity'),
    index ix_severity (severity)
);
```

A coluna computada usada neste exemplo é uma coluna não persistente ou virtual que não adiciona espaço extra à tabela. Ela é usada pelo índice `ix_severity` para melhorar o desempenho das consultas com o seguinte exemplo:

```sql
SELECT log
FROM Website.Logs
WHERE JSON_VALUE(log, '$.severity') = 'P4'
```

Uma característica importante desse índice é o reconhecimento de ordenação. Se a coluna NVARCHAR original tiver uma propriedade COLLATION (por exemplo, diferenciação de maiúsculas e minúsculas ou idioma japonês), o índice será organizado de acordo com as regras do idioma ou as regras de diferenciação de maiúsculas e minúsculas associadas com a coluna NVARCHAR. Esse reconhecimento de ordenação poderá ser um recurso importante caso você esteja desenvolvendo aplicativos para mercados globais que precisam usar regras de idioma personalizadas durante o processamento de documentos JSON.

## <a name="large-tables--columnstore-format"></a>Tabelas grandes e formato columnstore

Se você espera ter um grande número de documentos JSON em sua coleção, recomendamos adicionar um índice CLUSTERED COLUMNSTORE à coleção, conforme mostrado no seguinte exemplo:

```sql
create sequence WebSite.LogID as bigint;
go
create table WebSite.Logs (
    _id bigint default(next value for WebSite.LogID),
    log nvarchar(max),

    INDEX cci CLUSTERED COLUMNSTORE
);
```

Um índice CLUSTERED COLUMNSTORE fornece alta compactação de dados (até 25x) que pode reduzir consideravelmente os requisitos de espaço de armazenamento, reduzir o custo de armazenamento e aumentar o desempenho de E/S da carga de trabalho. Além disso, os índices CLUSTERED COLUMNSTORE são otimizados para análise e verificações de tabela em documentos JSON e, portanto, podem ser a melhor opção para análise de log.

O exemplo anterior usa um objeto de sequência para atribuir valores à coluna `_id`. As sequências e as identidades são opções válidas para a coluna de ID.

## <a name="frequently-changing-documents--memory-optimized-tables"></a>Documentos com alterações frequentes e tabelas com otimização de memória

Se você espera uma grande quantidade de operações de atualização, inserção e exclusão em suas coleções, armazene os documentos JSON em tabelas com otimização de memória. As coleções de JSON com otimização de memória sempre mantêm os dados na memória e, portanto, não há nenhuma sobrecarga de E/S de armazenamento. Além disso, as coleções de JSON otimizado para memória são completamente livres de bloqueio – ou seja, as ações em documentos não bloqueiam nenhuma outra operação.

A única coisa que você precisa fazer para converter uma coleção clássica em uma coleção com otimização de memória é especificar a opção **with (memory_optimized=on)** após a definição de tabela, conforme mostrado no exemplo a seguir. Em seguida, você terá uma versão com otimização de memória da coleção de JSON.

```sql
create table WebSite.Logs (
  _id bigint identity primary key nonclustered,
  log nvarchar(4000)
) with (memory_optimized=on)
```

Uma tabela com otimização de memória é a melhor opção para documentos com alterações frequentes. Quando estiver considerando o uso de tabelas com otimização de memória, considere também o desempenho. Use NVARCHAR(4000) em vez de NVARCHAR(max) para os documentos JSON nas coleções com otimização de memória, se possível, porque ele pode melhorar drasticamente o desempenho.

Assim como ocorre com as tabelas clássicas, é possível adicionar índices aos campos que estão sendo expostos em tabelas com otimização de memória usando colunas computadas. Por exemplo:

```sql
create table WebSite.Logs (

  _id bigint identity primary key nonclustered,
  log nvarchar(4000),

  severity AS cast(JSON_VALUE(log, '$.severity') as tinyint) persisted,
  index ix_severity (severity)

) with (memory_optimized=on)
```

Para maximizar o desempenho, converta o valor JSON no menor tipo possível que pode ser usado para armazenar o valor da propriedade. No exemplo anterior, **tinyint** é usado.

Também coloque consultas SQL que atualizam documentos JSON em procedimentos armazenados para obter o benefício da compilação nativa. Por exemplo:

```sql
CREATE PROCEDURE WebSite.UpdateData(@Id int, @Property nvarchar(100), @Value nvarchar(100))
WITH SCHEMABINDING, NATIVE_COMPILATION

AS BEGIN
    ATOMIC WITH (transaction isolation level = snapshot,  language = N'English')

    UPDATE WebSite.Logs
    SET log = JSON_MODIFY(log, @Property, @Value)
    WHERE _id = @Id;

END
```

Esse procedimento compilado nativamente usa a consulta e cria um código .DLL que a executa. Um procedimento compilado nativamente é a abordagem mais rápida para consultar e atualizar dados.

## <a name="conclusion"></a>Conclusão

As funções nativas do JSON no SQL Server e no Banco de Dados SQL possibilitam processar documentos JSON da mesma forma como em bancos de dados NoSQL. Todo banco de dados – relacional ou NoSQL – tem alguns prós e contras em relação ao processamento de dados JSON. O principal benefício de armazenar documentos JSON no SQL Server ou no Banco de Dados SQL é o suporte completo à linguagem SQL. Use a linguagem Transact-SQL avançada para processar dados e configurar uma variedade de opções de armazenamento (de índices columnstore para alta compactação e análise rápida a tabelas com otimização de memória para processamento livre de bloqueios). Ao mesmo tempo, você obtém o benefício dos recursos de internacionalização e segurança maduros que podem ser facilmente reutilizados no cenário de NoSQL. Os motivos descritos nesse artigo são excelentes para considerar o armazenamento de documentos JSON no SQL Server ou no Banco de Dados SQL.

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Saiba mais sobre JSON no SQL Server e no Banco de Dados SQL do Azure  
  
### <a name="microsoft-videos"></a>Vídeos da Microsoft

Para obter uma introdução visual ao suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure, consulte os seguintes vídeos:

-   [SQL Server 2016 e suporte para JSON](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Usando JSON no SQL Server 2016 e no Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON é uma ponte entre o NoSQL e mundos relacionais](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)

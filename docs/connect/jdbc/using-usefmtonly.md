---
title: Recuperar o ParameterMetaData por meio de useFmtOnly | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: ''
author: rene-ye
ms.author: v-reye
manager: kenvh
ms.openlocfilehash: 6877a6421622ab52a92b89502c68f47c4c315d93
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69025500"
---
# <a name="retrieving-parametermetadata-via-usefmtonly"></a>Recuperar o ParameterMetaData por meio de useFmtOnly
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O Microsoft JDBC Driver para SQL Server inclui uma maneira alternativa de consultar os Metadados de Parâmetros do servidor, **useFmtOnly**. Esse recurso foi introduzido na versão 7.4 do driver e é necessário como solução alternativa para problemas conhecidos no `sp_describe_undeclared_parameters`.
  
  O driver usa principalmente o procedimento armazenado `sp_describe_undeclared_parameters` para consultar os Metadados de Parâmetros, pois essa é a abordagem recomendada para a recuperação de Metadados de Parâmetros na maioria das circunstâncias. No entanto, a execução do procedimento armazenado atualmente falha nos seguintes casos de uso:
  
-   Em relação às colunas Always Encrypted
  
-   Em relação a tabelas temporárias e variáveis de tabela
  
-   Em relação às exibições 
  
  A solução proposta para esses casos de uso é analisar a consulta SQL do usuário para parâmetros e destinos de tabela e, em seguida, executar uma consulta `SELECT` com `FMTONLY` habilitado. O trecho a seguir ajudará a visualizar o recurso.
  
```sql
--create a normal table 'Foo' and a temporary table 'Bar'
CREATE TABLE Foo(c1 int);
CREATE TABLE #Bar(c1 int);

EXEC sp_describe_undeclared_parameters N'SELECT * FROM Foo WHERE c1 = @p0' --works fine
EXEC sp_describe_undeclared_parameters N'SELECT * FROM #Bar WHERE c1 = @p0' --fails with "Invalid object name '#Bar'"

SET FMTONLY ON;
SELECT c1 FROM Foo; --works
SET FMTONLY OFF;
SET FMTONLY ON;
SELECT c1 FROM #Bar; --works
SET FMTONLY OFF;
```
 
## <a name="turning-the-feature-onoff"></a>Habilitar/desabilitar o recurso 
 O recurso **useFmtOnly** está desabilitado por padrão. Os usuários podem habilitar esse recurso por meio da cadeia de conexão ao especificar `useFmtOnly=true`. Por exemplo: `jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;useFmtOnly=true;`.
 
 Como alternativa, o recurso está disponível por meio de `SQLServerDataSource`.
 ```java
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName(<server>);
ds.setPortNumber(<port>);
ds.setDatabaseName("<databaseName>");
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setUseFmtOnly(true);
try (Connection c = ds.getConnection()) {
    // do work with connection
}
 ```
 
 O recurso também está disponível no nível da Instrução. Os usuários podem habilitar/desabilitar o recurso por meio de `PreparedStatement.setUseFmtOnly(boolean)`.
> [!NOTE]  
>  O driver priorizará a propriedade de nível da Instrução sobre a propriedade de nível da Conexão.

## <a name="using-the-feature"></a>Usar o recurso
  Uma vez habilitado, o driver começará a usar internamente o novo recurso em vez de `sp_describe_undeclared_parameters` ao consultar os Metadados de Parâmetros. Não há mais nenhuma ação adicional necessária do usuário final.
```java
final String sql = "INSERT INTO #Bar VALUES (?)";
try (Connection c = DriverManager.getConnection(URL, USERNAME, PASSWORD)) {
    try (Statement s = c.createStatement()) {
        s.execute("CREATE TABLE #Bar(c1 int)");
    }
    try (PreparedStatement p1 = c.prepareStatement(sql); PreparedStatement p2 = c.prepareStatement(sql)) {
        ((SQLServerPreparedStatement) p1).setUseFmtOnly(true);
        ParameterMetaData pmd1 = p1.getParameterMetaData();
        System.out.println(pmd1.getParameterTypeName(1)); // prints int
        ParameterMetaData pmd2 = p2.getParameterMetaData(); // throws exception, Invalid object name '#Bar'
    }
}
```
> [!NOTE]  
>  O recurso apenas dá suporte a consultas `SELECT/INSERT/UPDATE/DELETE`. As consultas devem começar com uma das quatro palavras-chave com suporte ou uma [Expressão de Tabela Comum](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql?view=sql-server-2017) seguida por uma das consultas com suporte. Não há suporte para parâmetros dentro de Expressão de Tabela Comum.

## <a name="known-issues"></a>Problemas conhecidos
  Atualmente, há alguns problemas com o recurso, causados por deficiências na lógica de análise do SQL. Esses problemas podem ser abordados em uma atualização futura do recurso e estão documentados abaixo, juntamente com as sugestões de solução alternativa.
  
a. Usar um alias "encaminhar declarado"
```sql
CREATE TABLE Foo(c1 int)

DELETE fooAlias FROM Foo fooAlias WHERE c1 > ?; --Invalid object name 'fooAlias'

--Workaround #1: Specify AS keyword
DELETE fooAlias FROM Foo AS fooAlias WHERE c1 > ?;
--Workaround #2: Use the table name
DELETE Foo FROM Foo fooAlias WHERE c1 > ?;
```

B. Nome de coluna ambíguo quando as tabelas têm nomes de colunas compartilhados
```sql
CREATE TABLE Foo(c1 int, c2 int, c3 int)
CREATE TABLE Bar(c1 int, c2 int, c3 int)

SELECT c1,c2 FROM Foo WHERE c3 IN (SELECT c3 FROM Bar WHERE c1 > ? and c2 < ? and c3 = ?); --Ambiguous Column Name

--Workaround: Use aliases
SELECT c1,c2 FROM Foo WHERE c3 IN (SELECT c3 FROM Bar b WHERE b.c1 = ? and b.c2 = ? and b.c3 = ?);
```

C. SELECT de uma subconsulta com parâmetros
```sql

CREATE TABLE Foo(c1 int)

SELECT * FROM (SELECT * FROM Foo WHERE c1 = ?) WHERE c1 = ?; --Incorrect syntax near '?'

--Workaround: N/A
```

D. Subconsultas em uma cláusula SET
```sql
CREATE TABLE Foo(c1 int)

UPDATE Foo SET c1 = (SELECT c1 FROM Foo) WHERE c1 = ?; --Incorrect syntax near ')'

--Workaround: Add a 'delimiting' condition
UPDATE Foo SET c1 = (SELECT c1 FROM Foo HAVING (HASH JOIN)) WHERE c1 = ?;
```

## <a name="see-also"></a>Confira também  
 [Configuração das propriedades de conexão](../../connect/jdbc/setting-the-connection-properties.md)  
  
  

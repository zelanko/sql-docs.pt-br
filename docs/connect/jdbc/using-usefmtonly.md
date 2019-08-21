---
title: Recuperando ParameterMetaData por meio de useFmtOnly | Microsoft Docs
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
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69025500"
---
# <a name="retrieving-parametermetadata-via-usefmtonly"></a>Recuperando ParameterMetaData via useFmtOnly
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O Microsoft JDBC Driver para SQL Server inclui uma maneira alternativa de consultar metadados de parâmetro do servidor, **useFmtOnly**. Esse recurso foi introduzido pela primeira vez na versão 7,4 do driver e é necessário como solução alternativa para problemas conhecidos no `sp_describe_undeclared_parameters`.
  
  O driver usa principalmente o procedimento `sp_describe_undeclared_parameters` armazenado para consultar metadados de parâmetro, pois essa é a abordagem recomendada para a recuperação de metadados de parâmetro na maioria das circunstâncias. No entanto, a execução do procedimento armazenado atualmente falha nos seguintes casos de uso:
  
-   Em relação às colunas Always Encrypted
  
-   Em relação a tabelas temporárias e variáveis de tabela
  
-   Contra exibições 
  
  A solução proposta para esses casos de uso é analisar a consulta SQL do usuário para parâmetros e destinos de tabela e, em `SELECT` seguida, `FMTONLY` executar uma consulta com habilitado. O trecho a seguir ajudará a visualizar o recurso.
  
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
 
## <a name="turning-the-feature-onoff"></a>Ativar/desativar o recurso 
 O recurso **useFmtOnly** está desativado por padrão. Os usuários podem habilitar esse recurso por meio da cadeia de `useFmtOnly=true`conexão especificando. Por exemplo: `jdbc:sqlserver://<server>:<port>;databaseName=<databaseName>;user=<user>;password=<password>;useFmtOnly=true;`.
 
 Como alternativa, o recurso está disponível por `SQLServerDataSource`meio do.
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
 
 O recurso também está disponível no nível de instrução. Os usuários podem ativar/desativar o recurso por `PreparedStatement.setUseFmtOnly(boolean)`meio do.
> [!NOTE]  
>  O driver priorizará a propriedade de nível de instrução sobre a propriedade de nível de conexão.

## <a name="using-the-feature"></a>Como usar o recurso
  Uma vez habilitado, o driver começará internamente a usar o novo recurso `sp_describe_undeclared_parameters` em vez de ao consultar os metadados do parâmetro. Não há nenhuma ação adicional necessária do usuário final.
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
>  O recurso só dá `SELECT/INSERT/UPDATE/DELETE` suporte a consultas. As consultas devem começar com uma das 4 palavras-chave com suporte ou uma [expressão de tabela comum](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql?view=sql-server-2017) seguida por uma das consultas com suporte. Não há suporte para parâmetros em expressões de tabela comuns.

## <a name="known-issues"></a>Problemas conhecidos
  Atualmente, há alguns problemas com o recurso, causados por deficiências na lógica de análise do SQL. Esses problemas podem ser abordados em uma atualização futura do recurso e documentados abaixo, juntamente com sugestões de solução alternativa.
  
A. Como usar um alias ' encaminhar declarado '
```sql
CREATE TABLE Foo(c1 int)

DELETE fooAlias FROM Foo fooAlias WHERE c1 > ?; --Invalid object name 'fooAlias'

--Workaround #1: Specify AS keyword
DELETE fooAlias FROM Foo AS fooAlias WHERE c1 > ?;
--Workaround #2: Use the table name
DELETE Foo FROM Foo fooAlias WHERE c1 > ?;
```

B. Nome de coluna ambíguo quando as tabelas têm nomes de coluna compartilhados
```sql
CREATE TABLE Foo(c1 int, c2 int, c3 int)
CREATE TABLE Bar(c1 int, c2 int, c3 int)

SELECT c1,c2 FROM Foo WHERE c3 IN (SELECT c3 FROM Bar WHERE c1 > ? and c2 < ? and c3 = ?); --Ambiguous Column Name

--Workaround: Use aliases
SELECT c1,c2 FROM Foo WHERE c3 IN (SELECT c3 FROM Bar b WHERE b.c1 = ? and b.c2 = ? and b.c3 = ?);
```

C. SELECIONAR de uma subconsulta com parâmetros
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
  
  

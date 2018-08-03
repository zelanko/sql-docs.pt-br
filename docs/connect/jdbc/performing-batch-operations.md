---
title: Executando operações em lote | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1a576d95-7da6-4b7b-8b32-59e5b4d354c4
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c668dabd9b9a1957ffb69d034a59cc8df1cc4025
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/27/2018
ms.locfileid: "39279010"
---
# <a name="performing-batch-operations"></a>Executando operações em lote
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para melhorar o desempenho quando várias atualizações de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] estão ocorrendo, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] oferece a capacidade de enviar várias atualizações como uma única unidade de trabalho, também conhecido como lote.  
  
 As classes [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) podem ser usadas para enviar atualizações em lote. O método [addBatch](../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md) é usado para adicionar um comando. O método [clearBatch](../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md) é usado para limpar a lista de comandos. O método [executeBatch](../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md) é usado para enviar todos os comandos para processamento. Apenas as instruções DDL (linguagem de definição de dados) e DML (linguagem de manipulação de dados) que retornam uma contagem de atualização simples podem ser executadas como parte de um lote.  
  
 O método executeBatch retorna uma matriz de valores **int** que correspondem à contagem de atualizações de cada comando. Se um dos comandos falhar, um BatchUpdateException é lançada e você deve usar o método getUpdateCounts da classe BatchUpdateException para recuperar a matriz de contagem de atualização. Se um comando falhar, o driver continuará processando os comandos restantes. No entanto, se um comando tiver um erro de sintaxe, as instruções do lote falharão.  
  
> [!NOTE]  
>  Caso não precise usar contagens de atualizações, emita primeiro uma instrução SET NOCOUNT ON para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Isso reduzirá o tráfego de rede, além de melhorar o desempenho do aplicativo.  
  
 Como exemplo, crie a seguinte tabela no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]:  
  
```sql
CREATE TABLE TestTable   
   (Col1 int IDENTITY,   
    Col2 varchar(50),   
    Col3 int);  
```  
  
 No exemplo a seguir, uma conexão aberta com o banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] é passada para a função, o método addBatch é usado para criar as instruções a serem executadas e o método executeBatch é chamado para enviar o lote ao banco de dados.  
  
```java
public static void executeBatchUpdate(Connection con) {  
   try {  
      Statement stmt = con.createStatement();  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('X', 100)");  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('Y', 200)");  
      stmt.addBatch("INSERT INTO TestTable (Col2, Col3) VALUES ('Z', 300)");  
      int[] updateCounts = stmt.executeBatch();  
      stmt.close();  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usando instruções com o JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  

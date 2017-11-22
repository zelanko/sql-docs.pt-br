---
title: "Executando operações em lote | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1a576d95-7da6-4b7b-8b32-59e5b4d354c4
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 44acde56f2ddc25c66b7e896089499c5597ae779
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="performing-batch-operations"></a>Executando operações em lote
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para melhorar o desempenho quando várias atualizações para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados estão ocorrendo, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece a capacidade de submeter várias atualizações como uma única unidade de trabalho, também conhecido como um lote.  
  
 O [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), e [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) classes podem ser usadas para enviar atualizações em lotes. O [addBatch](../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md) método é usado para adicionar um comando. O [clearBatch](../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md) método é usado para limpar a lista de comandos. O [executeBatch](../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md) método é usado para enviar todos os comandos para processamento. Apenas as instruções DDL (linguagem de definição de dados) e DML (linguagem de manipulação de dados) que retornam uma contagem de atualização simples podem ser executadas como parte de um lote.  
  
 O método executeBatch retorna uma matriz de **int** valores que correspondem à contagem de atualização de cada comando. Se um dos comandos falhar, um BatchUpdateException será lançada e você deve usar o método getUpdateCounts da classe BatchUpdateException para recuperar a matriz de contagem de atualização. Se um comando falhar, o driver continuará processando os comandos restantes. No entanto, se um comando tiver um erro de sintaxe, as instruções do lote falharão.  
  
> [!NOTE]  
>  Se você não precisa usar contagens de atualização, você poderá emitir primeiro uma instrução SET NOCOUNT ON para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Isso reduzirá o tráfego de rede, além de melhorar o desempenho do aplicativo.  
  
 Por exemplo, crie a seguinte tabela no [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo:  
  
```  
CREATE TABLE TestTable   
   (Col1 int IDENTITY,   
    Col2 varchar(50),   
    Col3 int);  
```  
  
 No exemplo a seguir, uma conexão aberta para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passado para a função, o método addBatch é usado para criar as instruções a serem executadas e o método executeBatch é chamado para enviar o lote ao banco de dados.  
  
```  
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
  
## <a name="see-also"></a>Consulte também  
 [Usando instruções com o JDBC Driver](../../connect/jdbc/using-statements-with-the-jdbc-driver.md)  
  
  

---
title: "Usando um procedimento armazenado com uma contagem de atualização | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 64cf4877-5995-4bfc-8865-b7618a5c8d01
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fb038eeb3b3b0f14ef0ace1076244bd64949ed81
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="using-a-stored-procedure-with-an-update-count"></a>Usando um procedimento armazenado com uma contagem de atualização
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para modificar dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados usando um procedimento armazenado, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) classe. Usando a classe SQLServerCallableStatement, você pode chamar procedimentos armazenados que modificam dados contidos no banco de dados e retornar uma contagem do número de linhas afetadas, também conhecido como a contagem de atualização.  
  
 Depois que você configurou a chamada ao procedimento armazenado usando a classe SQLServerCallableStatement, em seguida, você pode chamar o procedimento armazenado usando o [executar](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) ou [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) método. O método executeUpdate retornará um **int** valor que contém o número de linhas afetadas pelo procedimento armazenado, mas o método execute não. Se você usar o método execute e deseja obter a contagem do número de linhas afetadas, você pode chamar o [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) método depois de executar o procedimento armazenado.  
  
> [!NOTE]  
>  Se você quiser que o driver JDBC retorne todas as contagens de atualização, inclusive contagens de atualização retornadas por gatilhos que possam ter sido acionados, defina a propriedade da cadeia de conexão lastUpdateCount como "false". Para obter mais informações sobre a propriedade lastUpdateCount, consulte [definindo as propriedades de Conexão](../../connect/jdbc/setting-the-connection-properties.md).  
  
 Por exemplo, criar a tabela a seguir e o procedimento armazenado e também inserir dados de exemplo no [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo:  
  
```  
CREATE TABLE TestTable   
   (Col1 int IDENTITY,   
    Col2 varchar(50),   
    Col3 int);  
  
CREATE PROCEDURE UpdateTestTable  
   @Col2 varchar(50),  
   @Col3 int  
AS  
BEGIN  
   UPDATE TestTable  
   SET Col2 = @Col2, Col3 = @Col3  
END;  
INSERT INTO dbo.TestTable (Col2, Col3) VALUES ('b', 10);  
```  
  
 No exemplo a seguir, uma conexão aberta para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passado para a função, o método execute é usado para chamar o procedimento armazenado UpdateTestTable e, em seguida, o método getUpdateCount é usado para retornar uma contagem das linhas que são afetadas pelo procedimento armazenado.  
  
 [!code[JDBC#UsingSprocWithUpdateCount1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_0_1.java)]  
  
## <a name="see-also"></a>Consulte também  
 [Usando instruções com procedimentos armazenados](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  


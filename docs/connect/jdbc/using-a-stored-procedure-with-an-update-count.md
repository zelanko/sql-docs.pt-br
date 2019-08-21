---
title: Como usar um procedimento armazenado com uma contagem de atualização | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 64cf4877-5995-4bfc-8865-b7618a5c8d01
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 851974955b9311efc149ecdff310bfbb1d8869fc
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026934"
---
# <a name="using-a-stored-procedure-with-an-update-count"></a>Como usar um procedimento armazenado com uma contagem de atualização

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para modificar dados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um procedimento armazenado, o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece a classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md). Usando a classe SQLServerCallableStatement, você pode chamar procedimentos armazenados que modificam dados que estão no banco de dados e retornam uma contagem do número de linhas afetadas, também chamada de contagem de atualização.

Depois de definir a chamada para o procedimento armazenado usando a classe SQLServerCallableStatement, chame o procedimento armazenado usando o método [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) ou o método [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md). O método executeUpdate retornará um valor **int** que contém o número de linhas afetadas pelo procedimento armazenado, mas o método execute não o retornará. Se você usa o método execute e quer obter a contagem do número de linhas afetadas, chame o método [getUpdateCount](../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md) depois de executar o procedimento armazenado.

> [!NOTE]  
> Se você quiser que o driver JDBC retorne todas as contagens de atualização, inclusive contagens de atualização retornadas por gatilhos que possam ter sido acionados, defina a propriedade da cadeia de conexão lastUpdateCount como "false". Para obter mais informações sobre a propriedade lastUpdateCount, consulte [definindo as propriedades de conexão](../../connect/jdbc/setting-the-connection-properties.md).

Como um exemplo, crie a tabela seguinte e o procedimento armazenado e insira dados de exemplo no banco de dados de exemplo do [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]:

```sql
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

No exemplo seguinte, uma conexão aberta ao banco de dados de amostra do [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] é passada para a função, o método execute é usado para chamar o procedimento armazenado UpdateTestTable e, em seguida, o método getUpdateCount é usado para retornar uma contagem das linhas que são afetadas pelo procedimento armazenado.

[!code[JDBC#UsingSprocWithUpdateCount1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_0_1.java)]

## <a name="see-also"></a>Confira também

[Como usar instruções com procedimentos armazenados](../../connect/jdbc/using-statements-with-stored-procedures.md)

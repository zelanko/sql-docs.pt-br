---
title: Como usar um procedimento armazenado com parâmetros de saída | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 1c006f27-7e99-43d5-974c-7b782659290c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: efafaa709666620e7237f2481c392aba25dfd5f8
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2019
ms.locfileid: "69026828"
---
# <a name="using-a-stored-procedure-with-output-parameters"></a>Como usar um procedimento armazenado com parâmetros de saída

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Um procedimento armazenado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que pode ser chamado é aquele que retorna um ou mais parâmetros OUT, que são parâmetros usados pelo procedimento armazenado para retornar os dados ao aplicativo de chamada. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece a classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), que pode ser usada para chamar esse tipo de procedimento armazenado e processar os dados retornados.

Ao chamar esse tipo de procedimento armazenado usando o driver JDBC, você precisa usar a sequência de escape `call` do SQL junto com o método [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) da classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). A sintaxe da sequência de escape `call` com parâmetros OUT é a seguinte:

`{call procedure-name[([parameter][,[parameter]]...)]}`

> [!NOTE]  
> Para obter mais informações sobre as sequências de escape do SQL, consulte [usando sequências de escape do SQL](../../connect/jdbc/using-sql-escape-sequences.md).

Ao construir a sequência de escape `call`, especifique os parâmetros OUT usando o caractere ? (ponto de interrogação). Esse caractere age como um espaço reservado para os valores de parâmetros que retornarão do procedimento armazenado. Para especificar um valor para um parâmetro OUT, especifique o tipo de dados de cada parâmetro usando o método [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) da classe SQLServerCallableStatement antes de executar o procedimento armazenado.

O valor especificado para o parâmetro OUT no método registerOutParameter precisa ser um dos tipos de dados do JDBC contidos em java.sql.Types que, por sua vez, é mapeado para um dos tipos de dados nativos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre o JDBC [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os tipos de dados, consulte [noções básicas sobre os tipos de dados do driver JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md).

Ao passar para o método registerOutParameter um valor para um parâmetro OUT, especifique não só o tipo de dados a ser usado para o parâmetro, mas também o posicionamento ordinal do parâmetro ou o nome do parâmetro no procedimento armazenado. Por exemplo, se o procedimento armazenado contiver um único parâmetro OUT, seu valor ordinal será 1; se o procedimento armazenado contiver dois parâmetros, o primeiro valor ordinal será 1 e o segundo valor ordinal será 2.

> [!NOTE]  
> O driver JDBC não dá suporte ao uso dos tipos de dados CURSOR, SQLVARIANT, TABLE e TIMESTAMP do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como parâmetros OUT.

Como exemplo, crie o seguinte procedimento armazenado no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]:

```sql
CREATE PROCEDURE GetImmediateManager  
   @employeeID INT,  
   @managerID INT OUTPUT  
AS  
BEGIN  
   SELECT @managerID = ManagerID
   FROM HumanResources.Employee
   WHERE EmployeeID = @employeeID  
END
```

Esse procedimento armazenado retorna um único parâmetro OUT (managerID), que é um inteiro, com base no parâmetro IN especificado (employeeID), que também é um inteiro. O valor retornado no parâmetro OUT é o ManagerID baseado no EmployeeID contido na tabela HumanResources.Employee.

No seguinte exemplo, uma conexão aberta com o banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] é passada para a função, e o método [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) é usado para chamar o procedimento armazenado GetImmediateManager:

```java
public static void executeStoredProcedure(Connection con) throws SQLException {  
    try(CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}");) {  
        cstmt.setInt(1, 5);  
        cstmt.registerOutParameter(2, java.sql.Types.INTEGER);  
        cstmt.execute();  
        System.out.println("MANAGER ID: " + cstmt.getInt(2));  
    }  
}
```

Esse exemplo usa as posições ordinais para identificar os parâmetros. Como alternativa, você pode identificar um parâmetro usando seu nome em vez da sua posição ordinal. O exemplo de código a seguir modifica o exemplo anterior para demonstrar como usar os parâmetros nomeados em um aplicativo Java. Observe que os nomes de parâmetro correspondem aos nomes de parâmetro na definição do procedimento armazenado:

```java
public static void executeStoredProcedure(Connection con) throws SQLException {  
    try(CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}"); ) {  
        cstmt.setInt("employeeID", 5);  
        cstmt.registerOutParameter("managerID", java.sql.Types.INTEGER);  
        cstmt.execute();  
        System.out.println("MANAGER ID: " + cstmt.getInt("managerID"));  
    }  
}
```

> [!NOTE]  
> Esses exemplos usam o método Execute da classe SQLServerCallableStatement para executar o procedimento armazenado. Ele é usado porque o procedimento armazenado também não retornou um conjunto de resultados. Se ele tivesse retornado, o método [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) teria sido usado.

Os procedimentos armazenados podem retornar contagens de atualização e vários conjuntos de resultados. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] segue a especificação do JDBC 3.0, a qual declara que vários conjuntos de resultados e contagens de atualizações devem ser recuperados antes da recuperação dos parâmetros OUT. Ou seja, o aplicativo deve recuperar todos os objetos ResultSet e as contagens de atualização antes de recuperar os parâmetros OUT usando os métodos CallableStatement. getter. Caso contrário, os objetos ResultSet e as contagens de atualizações que ainda não foram recuperados serão perdidos quando os parâmetros OUT forem recuperados. Para obter mais informações sobre contagens de atualização e vários conjuntos de resultados, consulte [usando um procedimento armazenado com uma contagem de atualizações](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md) e [usando vários conjuntos de resultados](../../connect/jdbc/using-multiple-result-sets.md).

## <a name="see-also"></a>Confira também

[Como usar instruções com procedimentos armazenados](../../connect/jdbc/using-statements-with-stored-procedures.md)

---
title: "Usando um procedimento armazenado com parâmetros de saída | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1c006f27-7e99-43d5-974c-7b782659290c
caps.latest.revision: 29
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8e5c3b945652c04cbbe75563d853703b5676b43f
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="using-a-stored-procedure-with-output-parameters"></a>Usando um procedimento armazenado com parâmetros de saída
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] procedimento armazenado que você pode chamar é aquele que retorna um ou mais parâmetros OUT, que são parâmetros que usa o procedimento armazenado para retornar dados de volta para o aplicativo de chamada. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) classe, que você pode usar para chamar esse tipo de procedimento armazenado e processar os dados que ele retorna.  
  
 Quando você chama esse tipo de procedimento armazenado usando o driver JDBC, você deve usar o `call` sequência de escape SQL junto com o [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) método o [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) classe. A sintaxe para a `call` sequência de escape com parâmetros OUT é o seguinte:  
  
 `{call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  Para obter mais informações sobre sequências de escape SQL, consulte [usando sequências de Escape SQL](../../connect/jdbc/using-sql-escape-sequences.md).  
  
 Quando você cria o `call` sequência de escape, especifique os parâmetros OUT usando o? (ponto de interrogação). Esse caractere age como um espaço reservado para os valores de parâmetros que retornarão do procedimento armazenado. Para especificar um valor para um parâmetro OUT, você deve especificar o tipo de dados de cada parâmetro usando o [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) método da classe SQLServerCallableStatement antes de executar o procedimento armazenado.  
  
 O valor que você especificar para o parâmetro OUT no método registerOutParameter deve ser um dos tipos de dados do JDBC contidos em Types, que por sua vez é mapeado para um nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de dados. Para obter mais informações sobre o JDBC e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de dados, consulte [Noções básicas sobre os tipos de dados do Driver JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md).  
  
 Quando você passar um valor para o método registerOutParameter para um parâmetro OUT, você deve especificar não só o tipo de dados a ser usado para o parâmetro, mas também o posicionamento ordinal do parâmetro ou o nome do parâmetro no procedimento armazenado. Por exemplo, se o procedimento armazenado contiver um único parâmetro OUT, seu valor ordinal será 1; se o procedimento armazenado contiver dois parâmetros, o primeiro valor ordinal será 1 e o segundo valor ordinal será 2.  
  
> [!NOTE]  
>  O driver JDBC não suporta o uso de CURSOR, SQLVARIANT, tabela e TIMESTAMP [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de dados como parâmetros de saída.  
  
 Por exemplo, crie o seguinte procedimento armazenado no [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo:  
  
```  
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
  
 No exemplo a seguir, uma conexão aberta para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passado para a função e o [executar](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) método é usado para chamar o procedimento armazenado GetImmediateManager:  
  
```  
public static void executeStoredProcedure(Connection con) {  
   try {  
      CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}");  
      cstmt.setInt(1, 5);  
      cstmt.registerOutParameter(2, java.sql.Types.INTEGER);  
      cstmt.execute();  
      System.out.println("MANAGER ID: " + cstmt.getInt(2));  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
 Esse exemplo usa as posições ordinais para identificar os parâmetros. Como alternativa, você pode identificar um parâmetro usando seu nome em vez da sua posição ordinal. O exemplo de código a seguir modifica o exemplo anterior para demonstrar como usar os parâmetros nomeados em um aplicativo Java. Observe que os nomes de parâmetro correspondem aos nomes de parâmetro na definição do procedimento armazenado:  
  
```  
public static void executeStoredProcedure(Connection con) {  
   try {  
      CallableStatement cstmt = con.prepareCall("{call dbo.GetImmediateManager(?, ?)}");  
      cstmt.setInt("employeeID", 5);  
      cstmt.registerOutParameter("managerID", java.sql.Types.INTEGER);  
      cstmt.execute();  
      System.out.println("MANAGER ID: " + cstmt.getInt("managerID"));  
      cstmt.close();  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
```  
  
 }  
  
> [!NOTE]  
>  Esses exemplos usam o método execute da classe SQLServerCallableStatement para executar o procedimento armazenado. Ele é usado porque o procedimento armazenado também não retornou um conjunto de resultados. Se usasse, o [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) método seria usado.  
  
 Os procedimentos armazenados podem retornar contagens de atualização e vários conjuntos de resultados. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] segue a especificação do JDBC 3.0, que declara que vários conjuntos de resultados e contagens de atualização devem ser recuperadas antes que os parâmetros OUT forem recuperados. Ou seja, o aplicativo deve recuperar todos os objetos do conjunto de resultados e contagens de atualização antes de recuperar os parâmetros OUT usando os métodos CallableStatement.getter. Caso contrário, os objetos de conjunto de resultados e contagens de atualização já não foram recuperadas serão perdidas quando os parâmetros OUT forem recuperados. Para obter mais informações sobre contagens de atualização e vários conjuntos de resultados, consulte [usando um procedimento armazenado com uma contagem de atualização](../../connect/jdbc/using-a-stored-procedure-with-an-update-count.md) e [usando vários conjuntos de resultados](../../connect/jdbc/using-multiple-result-sets.md).  
  
## <a name="see-also"></a>Consulte também  
 [Usando instruções com procedimentos armazenados](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  


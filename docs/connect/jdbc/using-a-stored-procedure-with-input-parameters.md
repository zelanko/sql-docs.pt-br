---
title: Usando um procedimento armazenado com parâmetros de entrada | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8f491b70-7d1b-42bd-964f-9a8b86af5eaa
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 611e1eef9d87fd0fc1838e2e40ed8626786c62d2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="using-a-stored-procedure-with-input-parameters"></a>Usando um procedimento armazenado com parâmetros de entrada
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] procedimento armazenado que você pode chamar é aquele que contém um ou mais parâmetros IN, que são parâmetros que podem ser usados para passar dados para o procedimento armazenado. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece o [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) classe, que você pode usar para chamar esse tipo de procedimento armazenado e processar os dados que ele retorna.  
  
 Quando você usa o driver JDBC para chamar um procedimento armazenado com parâmetros, você deve usar o `call` sequência de escape SQL junto com o [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) método o [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) classe. A sintaxe para a `call` sequência de escape com parâmetros é da seguinte maneira:  
  
 `{call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  Para obter mais informações sobre sequências de escape SQL, consulte [usando sequências de Escape SQL](../../connect/jdbc/using-sql-escape-sequences.md).  
  
 Quando você cria o `call` sequência de escape, especifique os parâmetros IN usando a? (ponto de interrogação). Esse caractere age como um espaço reservado para os valores de parâmetros que serão passados para o procedimento armazenado. Para especificar um valor para um parâmetro, você pode usar um dos métodos setter da classe SQLServerPreparedStatement. O método setter que você pode usar é determinado pelo tipo de dados do parâmetro IN.  
  
 Ao passar um valor para o método setter, você deve especificar não somente o valor real que será usado no parâmetro, mas também o posicionamento ordinal do parâmetro no procedimento armazenado. Por exemplo, se seu procedimento armazenado contiver um único parâmetro IN, seu valor ordinal será 1. Se o procedimento armazenado contiver dois parâmetros, o primeiro valor ordinal será 1 e o segundo valor ordinal será 2.  
  
 Como um exemplo de como chamar um procedimento armazenado que contém um parâmetro IN, use o procedimento armazenado uspGetEmployeeManagers o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo. Este procedimento armazenado aceita um único parâmetro de entrada denominado EmployeeID que é um valor inteiro e retorna uma lista recursiva de funcionários e seus gerentes com base no EmployeeID especificado. O código Java para chamar este procedimento armazenado é o seguinte:  
  
```  
public static void executeSprocInParams(Connection con) {  
   try {  
      PreparedStatement pstmt = con.prepareStatement("{call dbo.uspGetEmployeeManagers(?)}");  
      pstmt.setInt(1, 50);  
      ResultSet rs = pstmt.executeQuery();  
  
      while (rs.next()) {  
         System.out.println("EMPLOYEE:");  
         System.out.println(rs.getString("LastName") + ", " + rs.getString("FirstName"));  
         System.out.println("MANAGER:");  
         System.out.println(rs.getString("ManagerLastName") + ", " + rs.getString("ManagerFirstName"));  
         System.out.println();  
      }  
      rs.close();  
      pstmt.close();  
   }  
  
   catch (Exception e) {  
      e.printStackTrace();  
    }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Usando instruções com procedimentos armazenados](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  

---
title: Como usar um procedimento armazenado com parâmetros de entrada | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 8f491b70-7d1b-42bd-964f-9a8b86af5eaa
caps.latest.revision: 21
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c408fc703a3f6d9831cae226ce858b1a20a80c7
ms.sourcegitcommit: 6fa72c52c6d2256c5539cc16c407e1ea2eee9c95
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/27/2018
ms.locfileid: "39278767"
---
# <a name="using-a-stored-procedure-with-input-parameters"></a>Usando um procedimento armazenado com parâmetros de entrada
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Um procedimento armazenado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] que pode ser chamado é aquele que contém um ou mais parâmetros IN, que são parâmetros que podem ser usados para passar dados para o procedimento armazenado. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece a classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), que pode ser usada para chamar esse tipo de procedimento armazenado e processar os dados retornados.  
  
 Ao usar o driver JDBC para chamar um procedimento armazenado com parâmetros IN, você deve usar a sequência de escape do SQL `call` junto com o método [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) da classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). A sintaxe da sequência de escape `call` com parâmetros IN é a seguinte:  
  
 `{call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  Para obter mais informações sobre as sequências de escape SQL, consulte [usando sequências de Escape SQL](../../connect/jdbc/using-sql-escape-sequences.md).  
  
 Ao construir a sequência de escape `call`, especifique os parâmetros IN usando ? (ponto de interrogação). Esse caractere age como um espaço reservado para os valores de parâmetros que serão passados para o procedimento armazenado. Para especificar um valor para um parâmetro, você pode usar um dos métodos setter da classe SQLServerPreparedStatement. O método setter que você pode usar é determinado pelo tipo de dados do parâmetro IN.  
  
 Ao passar um valor para o método setter, você deve especificar não somente o valor real que será usado no parâmetro, mas também o posicionamento ordinal do parâmetro no procedimento armazenado. Por exemplo, se seu procedimento armazenado contiver um único parâmetro IN, seu valor ordinal será 1. Se o procedimento armazenado contiver dois parâmetros, o primeiro valor ordinal será 1 e o segundo valor ordinal será 2.  
  
 Como um exemplo de como chamar um procedimento armazenado que contém um parâmetro IN, use o procedimento armazenado uspGetEmployeeManagers no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]. Este procedimento armazenado aceita um único parâmetro de entrada denominado EmployeeID que é um valor inteiro e retorna uma lista recursiva de funcionários e seus gerentes com base no EmployeeID especificado. O código Java para chamar este procedimento armazenado é o seguinte:  
  
```java
public static void executeSprocInParams(Connection con) throws SQLException {  
    try(PreparedStatement pstmt = con.prepareStatement("{call dbo.uspGetEmployeeManagers(?)}"); ) {  

        pstmt.setInt(1, 50);  
        ResultSet rs = pstmt.executeQuery();  

        while (rs.next()) {  
            System.out.println("EMPLOYEE:");  
            System.out.println(rs.getString("LastName") + ", " + rs.getString("FirstName"));  
            System.out.println("MANAGER:");  
            System.out.println(rs.getString("ManagerLastName") + ", " + rs.getString("ManagerFirstName"));  
            System.out.println();  
        }  
    }
}
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usando instruções com procedimentos armazenados](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  

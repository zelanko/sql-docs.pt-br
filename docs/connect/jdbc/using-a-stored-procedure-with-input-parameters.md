---
title: Como usar um procedimento armazenado com parâmetros de entrada | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8f491b70-7d1b-42bd-964f-9a8b86af5eaa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6c84e4081b9369d504d173387c6944b06d927c9c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "69026901"
---
# <a name="using-a-stored-procedure-with-input-parameters"></a>Como usar um procedimento armazenado com parâmetros de entrada

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Um procedimento armazenado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que pode ser chamado é aquele que contém um ou mais parâmetros IN, que são parâmetros que podem ser usados para passar dados para o procedimento armazenado. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece a classe [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md), que pode ser usada para chamar esse tipo de procedimento armazenado e processar os dados retornados.

Ao usar o driver JDBC para chamar um procedimento armazenado com parâmetros IN, você deve usar a sequência de escape do SQL `call` junto com o método [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) da classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). A sintaxe da sequência de escape `call` com parâmetros IN é a seguinte:

`{call procedure-name[([parameter][,[parameter]]...)]}`

> [!NOTE]  
> Para obter mais informações sobre as sequências de escape do SQL, confira [Como usar sequências de escape do SQL](../../connect/jdbc/using-sql-escape-sequences.md).

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

## <a name="see-also"></a>Confira também

[Como usar instruções com procedimentos armazenados](../../connect/jdbc/using-statements-with-stored-procedures.md)

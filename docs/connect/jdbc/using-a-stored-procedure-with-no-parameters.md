---
title: "Usando um procedimento armazenado sem parâmetros | Microsoft Docs"
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
ms.assetid: e9470a6d-a758-4c56-96ec-7b37139e36a7
caps.latest.revision: "18"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 19e9377f7ac42f7999ecc507a3a8aae7cbda8fc4
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2017
---
# <a name="using-a-stored-procedure-with-no-parameters"></a>Usando um procedimento armazenado sem parâmetros
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  O tipo mais simples de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] procedimento armazenado que você pode chamar é aquele que não contém parâmetros e retorna um único conjunto de resultados. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece o [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) classe, que você pode usar para chamar esse tipo de procedimento armazenado e processar os dados que ele retorna.  
  
 Quando você usa o driver JDBC para chamar um procedimento armazenado sem parâmetros, você deve usar o `call` sequência de escape do SQL. A sintaxe para a `call` sequência de escape sem parâmetros é da seguinte maneira:  
  
 `{call procedure-name}`  
  
> [!NOTE]  
>  Para obter mais informações sobre sequências de escape SQL, consulte [usando sequências de Escape SQL](../../connect/jdbc/using-sql-escape-sequences.md).  
  
 Por exemplo, crie o seguinte procedimento armazenado no [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo:  
  
```  
CREATE PROCEDURE GetContactFormalNames   
AS  
BEGIN  
   SELECT TOP 10 Title + ' ' + FirstName + ' ' + LastName AS FormalName   
   FROM Person.Contact  
END  
```  
  
 Esse procedimento armazenado retorna um único conjunto de resultados que contém uma coluna de dados, uma combinação do título, do nome e do sobrenome dos dez primeiros contatos presentes na tabela Person.Contact.  
  
 No exemplo a seguir, uma conexão aberta para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passado para a função e o [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) método é usado para chamar o procedimento armazenado GetContactFormalNames.  
  
```  
public static void executeSprocNoParams(Connection con) {  
   try {  
      Statement stmt = con.createStatement();  
      ResultSet rs = stmt.executeQuery("{call dbo.GetContactFormalNames}");  
  
      while (rs.next()) {  
         System.out.println(rs.getString("FormalName"));  
      }  
      rs.close();  
      stmt.close();  
   }  
   catch (Exception e) {  
      e.printStackTrace();  
   }  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Usando instruções com procedimentos armazenados](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  

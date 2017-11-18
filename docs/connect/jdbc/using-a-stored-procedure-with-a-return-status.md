---
title: Usando um procedimento armazenado com um Status de retorno | Microsoft Docs
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
ms.assetid: 4b126e95-8458-41d6-af37-fc6662859f19
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8247f7f81e70aafac8d109abe7f8303c8e13f487
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="using-a-stored-procedure-with-a-return-status"></a>Usando um procedimento armazenado com um status de retorno
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] procedimento armazenado que você pode chamar é aquele que retorna um status ou um parâmetro de resultado. Em geral, isso é usado para indicar o êxito ou a falha do procedimento armazenado. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece o [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) classe, que você pode usar para chamar esse tipo de procedimento armazenado e processar os dados que ele retorna.  
  
 Quando você chama esse tipo de procedimento armazenado usando o driver JDBC, você deve usar o `call` sequência de escape SQL em conjunto com o [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) método o [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) classe . A sintaxe para a `call` sequência de escape com um parâmetro de status de retorno é o seguinte:  
  
 `{[?=]call procedure-name[([parameter][,[parameter]]...)]}`  
  
> [!NOTE]  
>  Para obter mais informações sobre sequências de escape SQL, consulte [usando sequências de Escape SQL](../../connect/jdbc/using-sql-escape-sequences.md).  
  
 Quando você cria o `call` sequência de escape, especifique o parâmetro de status de retorno usando o? (ponto de interrogação). Esse caractere age como um espaço reservado para o valor de parâmetro que retornará do procedimento armazenado. Para especificar um valor para um parâmetro de status de retorno, você deve especificar o tipo de dados do parâmetro usando o [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) método da classe SQLServerCallableStatement, antes de executar o procedimento armazenado.  
  
> [!NOTE]  
>  Ao usar o driver JDBC com um banco de dados do SQL Server, o valor especificado para o parâmetro de status de retorno no método registerOutParameter sempre será um inteiro, que pode ser especificada usando o tipo de dados Java.SQL.  
  
 Além disso, quando você passar um valor para o método registerOutParameter para um parâmetro de status de retorno, você deve especificar não só o tipo de dados a ser usado para o parâmetro, mas o posicionamento ordinal do parâmetro na chamada de procedimento armazenado. No caso do parâmetro de status de retorno, a posição ordinal será sempre 1 porque ele é sempre o primeiro parâmetro na chamada para o procedimento armazenado. Embora a classe SQLServerCallableStatement oferece suporte para usar o nome do parâmetro para indicar o parâmetro específico, você pode usar somente o número de posição ordinal do parâmetro para parâmetros de status de retorno.  
  
 Por exemplo, crie o seguinte procedimento armazenado no [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo:  
  
```  
CREATE PROCEDURE CheckContactCity  
   (@cityName CHAR(50))  
AS  
BEGIN  
   IF ((SELECT COUNT(*)  
   FROM Person.Address  
   WHERE City = @cityName) > 1)  
   RETURN 1  
ELSE  
   RETURN 0  
END  
```  
  
 Esse procedimento armazenado retorna o valor de status 1 ou 0, dependendo se a cidade especificada no parâmetro cityName se encontra ou não na tabela Person.Address.  
  
 No exemplo a seguir, uma conexão aberta para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passado para a função e o [executar](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) método é usado para chamar o procedimento armazenado CheckContactCity:  
  
 [!code[JDBC#UsingSprocWithReturnStatus1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_1_1.java)]  
  
## <a name="see-also"></a>Consulte também  
 [Usando instruções com procedimentos armazenados](../../connect/jdbc/using-statements-with-stored-procedures.md)  
  
  


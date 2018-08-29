---
title: Uso de um procedimento armazenado com um status de retorno | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4b126e95-8458-41d6-af37-fc6662859f19
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2fd75507ca7c1615b0282a9f56a1e8f4b33bc22b
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42785878"
---
# <a name="using-a-stored-procedure-with-a-return-status"></a>Usando um procedimento armazenado com um status de retorno

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Um procedimento armazenado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você pode chamar é um que retorna um parâmetro de status ou resultado. Em geral, isso é usado para indicar o êxito ou a falha do procedimento armazenado. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece a classe [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md), que pode ser usada para chamar esse tipo de procedimento armazenado e para processar os dados retornados.

Ao chamar esse tipo de procedimento armazenado usando o driver JDBC, você deve usar a sequência de escape `call` do SQL em conjunto com o método [prepareCall](../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md) da classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md). A sintaxe da sequência de escape `call` com um parâmetro de status de retorno é a seguinte:

`{[?=]call procedure-name[([parameter][,[parameter]]...)]}`

> [!NOTE]  
> Para obter mais informações sobre as sequências de escape SQL, consulte [usando sequências de Escape SQL](../../connect/jdbc/using-sql-escape-sequences.md).

Ao construir a sequência de escape `call`, especifique o parâmetro de status de retorno usando o ? (ponto de interrogação). Esse caractere age como um espaço reservado para o valor de parâmetro que retornará do procedimento armazenado. Para especificar um valor para um parâmetro de status de retorno, é necessário especificar o tipo de dados do parâmetro usando o método [registerOutParameter](../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) da classe SQLServerCallableStatement antes de executar o procedimento armazenado.

> [!NOTE]  
> Ao usar o driver JDBC com um banco de dados do SQL Server, o valor que você especificar para o parâmetro de status de retorno no método registerOutParameter será sempre um inteiro, condição que você pode especificar usando o tipo de dados java.sql.Types.INTEGER.

Além disso, ao passar para o método registerOutParameter um valor para um parâmetro de status de retorno, você deve especificar não só o tipo de dados a ser usado para o parâmetro, mas também o posicionamento ordinal do parâmetro na chamada de procedimento armazenado. No caso do parâmetro de status de retorno, a posição ordinal será sempre 1 porque ele é sempre o primeiro parâmetro na chamada para o procedimento armazenado. Embora a classe SQLServerCallableStatement dê suporte ao uso do nome do parâmetro para indicar o parâmetro específico, você só pode usar o número de posição ordinal para parâmetros de status de retorno.

Como exemplo, crie o seguinte procedimento armazenado no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]:

```sql
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

No exemplo a seguir, uma conexão aberta com o banco de dados de amostra [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] é passada para a função, e o método [execute](../../connect/jdbc/reference/execute-method-sqlserverstatement.md) é usado para chamar o procedimento armazenado CheckContactCity:

[!code[JDBC#UsingSprocWithReturnStatus1](../../connect/jdbc/codesnippet/Java/using-a-stored-procedure_1_1.java)]

## <a name="see-also"></a>Consulte Também

[Usando instruções com procedimentos armazenados](../../connect/jdbc/using-statements-with-stored-procedures.md)

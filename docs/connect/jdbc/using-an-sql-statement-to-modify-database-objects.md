---
title: Usando uma instrução SQL para modificar objetos de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f49ea499-df3c-4e85-9fc7-450fb99622a6
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b126fb0b5a72688c1801cf8854d8035763c8245f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32851491"
---
# <a name="using-an-sql-statement-to-modify-database-objects"></a>Usando uma instrução SQL para modificar objetos de banco de dados
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Para modificar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos de banco de dados usando uma instrução SQL, você pode usar o [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) método o [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) classe. O método executeUpdate passar a instrução SQL para o banco de dados para processamento e, em seguida, retorna um valor de 0 porque nenhuma linha foi afetada.  
  
 Para fazer isso, você deve primeiro criar um objeto SQLServerStatement usando o [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) método o [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) classe.  
  
> [!NOTE]  
>  As instruções SQL que modificam objetos dentro de um banco de dados são chamadas de instruções DDL (linguagem de definição de dados). Entre elas estão instruções como CREATE TABLE, DROP TABLE, CREATE INDEX e DROP INDEX. Para obter mais informações sobre os tipos de instruções DDL que são suportados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
 No exemplo a seguir, uma conexão aberta para o [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] banco de dados de exemplo é passado para a função, é construída uma instrução SQL que criará TestTable simples no banco de dados e, em seguida, a instrução é executada e o valor de retorno é exibido.  
  
 [!code[JDBC#UsingSQLToModifyDBObjects1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_0_1.java)]  
  
## <a name="see-also"></a>Consulte também  
 [Usando instruções com SQL](../../connect/jdbc/using-statements-with-sql.md)  
  
  

---
title: Como usar uma instrução SQL para modificar objetos de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f49ea499-df3c-4e85-9fc7-450fb99622a6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 257dba1d93b2a22838cf7c3c631f65a29d517157
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66790244"
---
# <a name="using-an-sql-statement-to-modify-database-objects"></a>Usando uma instrução SQL para modificar objetos de banco de dados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para modificar os objetos de banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando uma instrução SQL, é possível usar o método [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) da classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md). O método executeUpdate passará a instrução SQL para o banco de dados para processamento e, em seguida, retornará um valor 0 porque nenhuma linha foi afetada.

Para isso, você deve primeiro criar um objeto SQLServerStatement usando o método [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) da classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md).

> [!NOTE]  
> As instruções SQL que modificam objetos dentro de um banco de dados são chamadas de instruções DDL (linguagem de definição de dados). Isso inclui instruções como `CREATE TABLE`, `DROP TABLE`, `CREATE INDEX`, e `DROP INDEX`. Para obter mais informações sobre os tipos de instruções DDL compatíveis com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja "Tipos de dados (Transact-SQL)" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

No exemplo a seguir, uma conexão aberta com o banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] é passada para a função; é construída uma instrução SQL que criará TestTable simples no banco de dados; em seguida, a instrução é executada e o valor retornado da coluna de IDENTITY é exibido.

[!code[JDBC#UsingSQLToModifyDBObjects1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_0_1.java)]

## <a name="see-also"></a>Consulte Também

[Usando instruções com SQL](../../connect/jdbc/using-statements-with-sql.md)

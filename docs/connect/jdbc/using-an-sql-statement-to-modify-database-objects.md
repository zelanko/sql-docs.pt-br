---
title: Como usar uma instrução SQL para modificar objetos de banco de dados | Microsoft Docs
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
ms.openlocfilehash: a3386121432f918ef447f5d3ad1f4ff79a64c681
ms.sourcegitcommit: 2f9cafc1d7a3773a121bdb78a095018c8b7c149f
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/08/2018
ms.locfileid: "39662438"
---
# <a name="using-an-sql-statement-to-modify-database-objects"></a>Usando uma instrução SQL para modificar objetos de banco de dados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Para modificar os objetos de banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] usando uma instrução SQL, é possível usar o método [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) da classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md). O método executeUpdate passará a instrução SQL para o banco de dados para processamento e, em seguida, retornará um valor 0 porque nenhuma linha foi afetada.

Para isso, você deve primeiro criar um objeto SQLServerStatement usando o método [createStatement](../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md) da classe [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md).

> [!NOTE]  
> As instruções SQL que modificam objetos dentro de um banco de dados são chamadas de instruções DDL (linguagem de definição de dados). Isso inclui instruções como `CREATE TABLE`, `DROP TABLE`, `CREATE INDEX`, e `DROP INDEX`. Para obter mais informações sobre os tipos de instruções DDL compatíveis com [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], veja "Tipos de dados (Transact-SQL)" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].

No exemplo a seguir, uma conexão aberta com o banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] é passada para a função; é construída uma instrução SQL que criará TestTable simples no banco de dados; em seguida, a instrução é executada e o valor retornado da coluna de IDENTITY é exibido.

[!code[JDBC#UsingSQLToModifyDBObjects1](../../connect/jdbc/codesnippet/Java/using-an-sql-statement-t_0_1.java)]

## <a name="see-also"></a>Consulte Também

[Usando instruções com SQL](../../connect/jdbc/using-statements-with-sql.md)

---
title: Estruturas e bibliotecas de conectividade | Microsoft Docs
description: "Lista os drivers de conectividade que os aplicativos cliente podem usar de vários idiomas para se conectar ao Microsoft SQL Server em execução no local ou na nuvem, no Linux, o Windows ou o Docker e também para o banco de dados do SQL Azure e o Azure SQL Data Warehouse."
author: sanagama
ms.author: sanagama
manager: jhubbard
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 80efe5ff-09ba-48a0-ac93-a91d62cff47c
ms.workload: Inactive
ms.openlocfilehash: 91327a1f067f6a8ef11481b489e6d296870c6c86
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2017
---
# <a name="connectivity-libraries-and-frameworks-for-microsoft-sql-server"></a>Bibliotecas de conectividade e estruturas para o Microsoft SQL Server

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Confira nosso [obter tutoriais de Introdução](http://aka.ms/sqldev) começar com linguagens de programação como c#, Java, Node.js, PHP e Python e compilar um aplicativo usando o SQL Server no Linux ou Windows ou o Docker no macOS rapidamente.

A tabela a seguir lista as bibliotecas de conectividade ou *drivers* que aplicativos cliente podem usar de uma variedade de idiomas para conectar e usar o Microsoft SQL Server em execução no local ou na nuvem, no Linux, o Windows ou o Docker e também para o banco de dados do SQL Azure e o Azure SQL Data Warehouse. 

| Idioma | Plataforma | Recursos adicionais | Download | Introdução |
| :-- | :-- | :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Microsoft ADO.NET for SQL Server](http://msdn.microsoft.com/library/mt657768.aspx) | [Download](https://msdn.microsoft.com/vstudio/aa496123.aspx) | [Introdução](https://www.microsoft.com/en-us/sql-server/developer-get-started/csharp/ubuntu)
| Java | Windows, Linux, macOS | [Microsoft JDBC Driver para SQL Server](http://msdn.microsoft.com/library/mt484311.aspx) | [Download](http://go.microsoft.com/fwlink/?LinkId=245496) |  [Introdução](https://www.microsoft.com/en-us/sql-server/developer-get-started/java/ubuntu)
| PHP | Windows, Linux, macOS| [Driver SQL do PHP para SQL Server](http://msdn.microsoft.com/library/dn865013.aspx) | Sistema Operacional: <br/> \*[Windows](https://www.microsoft.com/download/details.aspx?id=20098) <br/> \*[Linux](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) <br/> \*[macOS](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) |  [Introdução](https://www.microsoft.com/en-us/sql-server/developer-get-started/php/ubuntu)
| Node.js | Windows, Linux, macOS | [Driver Node.js para SQL Server](../connect/node-js/node-js-driver-for-sql-server.md) |  [Introdução](https://www.microsoft.com/en-us/sql-server/developer-get-started/node/ubuntu)
| Python | Windows, Linux, macOS | [Driver do SQL Python](../connect/python/python-driver-for-sql-server.md) <br/> \*[pyodbc](http://msdn.microsoft.com/library/mt763257.aspx) |  [Introdução](https://www.microsoft.com/en-us/sql-server/developer-get-started/python/ubuntu)
| Ruby | Windows, Linux, macOS | [Ruby Driver para SQL Server](../connect/ruby/ruby-driver-for-sql-server.md) | [Introdução](https://www.microsoft.com/en-us/sql-server/developer-get-started/ruby/ubuntu)
| C++ | Windows, Linux, macOS | [Microsoft ODBC Driver for SQL Server](https://msdn.microsoft.com/en-us/library/mt654048(v=sql.1).aspx) | [Download](https://msdn.microsoft.com/en-us/library/mt654048(v=sql.1).aspx) |  

A tabela a seguir lista alguns exemplos de estruturas de mapeamento relacional objeto (ORM) e frameworks da web que aplicativos cliente podem usar com o Microsoft SQL Server em execução no local ou na nuvem, no Linux, o Windows ou o Docker e também para o banco de dados do SQL Azure e o Azure SQL Data Warehouse. 

| Idioma | Plataforma | ORM(s) |
| :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Entity Framework](https://docs.microsoft.com/en-us/ef)<br>[Entity Framework Core](https://docs.microsoft.com/en-us/ef/core/index) |
| Java | Windows, Linux, macOS |[No modo de hibernação ORM](http://hibernate.org/orm)|
| PHP | Windows, Linux | [Laravel (eloquente)](https://laravel.com/docs/5.0/eloquent) |
| Node.js | Windows, Linux, macOS | [Sequelize ORM](http://docs.sequelizejs.com) |
| Python | Windows, Linux, macOS |[Django](https://www.djangoproject.com/) |
| Ruby | Windows, Linux, macOS | [Ruby nos trilhos](http://rubyonrails.org/) |

## <a name="related-links"></a>Links relacionados
- [Drivers do SQL Server](http://msdn.microsoft.com/library/mt654049.aspx) para conectar-se de aplicativos cliente

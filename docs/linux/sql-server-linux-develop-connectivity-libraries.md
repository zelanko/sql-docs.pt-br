---
title: Bibliotecas e estruturas de conectividade
description: Lista os drivers de conectividade de várias linguagens que os aplicativos cliente podem usar para se conectar ao Microsoft SQL Server em execução local ou na nuvem, no Linux, Windows ou Docker e também no Banco de Dados SQL do Azure e no Azure Synapse Analytics.
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 80efe5ff-09ba-48a0-ac93-a91d62cff47c
ms.openlocfilehash: c626df1042ed3b3d9ecb5e25bbd219ceb468bfee
ms.sourcegitcommit: 22102f25db5ccca39aebf96bc861c92f2367c77a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2020
ms.locfileid: "92115489"
---
# <a name="connectivity-libraries-and-frameworks-for-microsoft-sql-server"></a>Bibliotecas e estruturas de conectividade para o Microsoft SQL Server

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Confira os [Tutoriais de Introdução](https://aka.ms/sqldev) para começar rapidamente a usar linguagens de programação, como C#, Java, Node.js, PHP e Python e compilar um aplicativo usando o SQL Server em Linux ou Windows ou Docker em macOS.

A tabela a seguir lista os *drivers* ou as bibliotecas de conectividade de várias linguagens que os aplicativos cliente podem usar para se conectar e executar o Microsoft SQL Server no local ou na nuvem, no Linux, Windows ou Docker e também no Banco de Dados SQL do Azure e no Azure Synapse Analytics. 

| Linguagem | Plataforma | Recursos adicionais | Baixar | Introdução |
| :-- | :-- | :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Microsoft ADO.NET for SQL Server](../connect/ado-net/microsoft-ado-net-sql-server.md) | [Download](https://msdn.microsoft.com/vstudio/aa496123.aspx) | [Introdução](https://www.microsoft.com/sql-server/developer-get-started/csharp/ubuntu)
| Java | Windows, Linux, macOS | [Microsoft JDBC Driver para SQL Server](../connect/jdbc/microsoft-jdbc-driver-for-sql-server.md) | [Download](https://go.microsoft.com/fwlink/?LinkId=245496) |  [Introdução](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu)
| PHP | Windows, Linux, macOS| [Driver do SQL PHP para SQL Server](../connect/php/microsoft-php-driver-for-sql-server.md) | Sistema Operacional: <br/> \* [Windows](https://www.microsoft.com/download/details.aspx?id=20098) <br/> \* [Linux](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) <br/> \* [macOS](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) |  [Introdução](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu)
| Node.js | Windows, Linux, macOS | [Driver Node.js para SQL Server](../connect/node-js/node-js-driver-for-sql-server.md) |  [Introdução](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu)
| Python | Windows, Linux, macOS | [Python SQL Driver](../connect/python/python-driver-for-sql-server.md) <br/> \* [pyodbc](../connect/python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md) |  [Introdução](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu)
| Ruby | Windows, Linux, macOS | [Ruby Driver para SQL Server](../connect/ruby/ruby-driver-for-sql-server.md) | [Introdução](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu)
| C++ | Windows, Linux, macOS | [Microsoft ODBC Driver for SQL Server](../connect/odbc/microsoft-odbc-driver-for-sql-server.md) | [Download](../connect/odbc/microsoft-odbc-driver-for-sql-server.md) |  

A tabela a seguir lista alguns exemplos de estruturas de ORM (Mapeamento Relacional de Objeto) e estruturas da Web que os aplicativos cliente podem usar com o Microsoft SQL Server em execução local ou na nuvem, no Linux, Windows ou Docker e também no Banco de Dados SQL do Azure e no Azure Synapse Analytics. 

| Linguagem | Plataforma | ORM(s) |
| :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Entity Framework](/ef)<br>[Entity Framework Core](/ef/core/index) |
| Java | Windows, Linux, macOS |[Colocar o ORM em hibernação](https://hibernate.org/orm)|
| PHP | Windows, Linux | [Laravel (Eloquent)](https://laravel.com/docs/5.0/eloquent) |
| Node.js | Windows, Linux, macOS | [Sequelize ORM](http://sequelize.org/) |
| Python | Windows, Linux, macOS |[Django](https://www.djangoproject.com/) |
| Ruby | Windows, Linux, macOS | [Ruby on Rails](https://rubyonrails.org/) |

## <a name="related-links"></a>Links relacionados
- [Drivers do SQL Server](../connect/sql-connection-libraries.md) para conectar-se de aplicativos cliente
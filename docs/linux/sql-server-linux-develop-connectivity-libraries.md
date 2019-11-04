---
title: Bibliotecas e estruturas de conectividade
description: Lista os drivers de conectividade que os aplicativos cliente podem usar de várias linguagens para conectarem-se ao Microsoft SQL Server em execução local ou na nuvem, no Linux, no Windows ou no Docker e também no Banco de Dados SQL do Azure e no SQL Data Warehouse do Azure.
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 80efe5ff-09ba-48a0-ac93-a91d62cff47c
ms.openlocfilehash: a4ed76cde2cd8ff8b9d862b981dcbed2361c6ae8
ms.sourcegitcommit: 4fb6bc7c81a692a2df706df063d36afad42816af
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/29/2019
ms.locfileid: "73049736"
---
# <a name="connectivity-libraries-and-frameworks-for-microsoft-sql-server"></a>Bibliotecas e estruturas de conectividade para o Microsoft SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Confira os [Tutoriais de Introdução](https://aka.ms/sqldev) para começar rapidamente a usar linguagens de programação, como C#, Java, Node.js, PHP e Python e compilar um aplicativo usando o SQL Server em Linux ou Windows ou Docker em macOS.

A tabela a seguir lista os *drivers* ou as bibliotecas de conectividade que os aplicativos cliente podem usar de uma variedade de idiomas para conectarem-se e usarem o Microsoft SQL Server em execução local ou na nuvem, em Linux, Windows ou Docker e também para o Banco de Dados SQL do Azure e o SQL Data Warehouse do Azure. 

| Linguagem | Plataforma | Recursos adicionais | Download | Introdução |
| :-- | :-- | :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Microsoft ADO.NET for SQL Server](/sql/connect/ado-net/microsoft-ado-net-sql-server) | [Download](https://msdn.microsoft.com/vstudio/aa496123.aspx) | [Introdução](https://www.microsoft.com/sql-server/developer-get-started/csharp/ubuntu)
| Java | Windows, Linux, macOS | [Microsoft JDBC Driver para SQL Server](https://msdn.microsoft.com/library/mt484311.aspx) | [Download](https://go.microsoft.com/fwlink/?LinkId=245496) |  [Introdução](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu)
| PHP | Windows, Linux, macOS| [Driver do SQL PHP para SQL Server](../connect/php/microsoft-php-driver-for-sql-server.md) | Sistema Operacional: <br/> \* [Windows](https://www.microsoft.com/download/details.aspx?id=20098) <br/> \* [Linux](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) <br/> \* [macOS](https://github.com/Microsoft/msphpsql/tree/dev#install-unix) |  [Introdução](https://www.microsoft.com/sql-server/developer-get-started/php/ubuntu)
| Node.js | Windows, Linux, macOS | [Driver Node.js para SQL Server](../connect/node-js/node-js-driver-for-sql-server.md) |  [Introdução](https://www.microsoft.com/sql-server/developer-get-started/node/ubuntu)
| Python | Windows, Linux, macOS | [Python SQL Driver](../connect/python/python-driver-for-sql-server.md) <br/> \* [pyodbc](https://msdn.microsoft.com/library/mt763257.aspx) |  [Introdução](https://www.microsoft.com/sql-server/developer-get-started/python/ubuntu)
| Ruby | Windows, Linux, macOS | [Ruby Driver para SQL Server](../connect/ruby/ruby-driver-for-sql-server.md) | [Introdução](https://www.microsoft.com/sql-server/developer-get-started/ruby/ubuntu)
| C++ | Windows, Linux, macOS | [Microsoft ODBC Driver for SQL Server](https://msdn.microsoft.com/library/mt654048(v=sql.1).aspx) | [Download](https://msdn.microsoft.com/library/mt654048(v=sql.1).aspx) |  

A tabela a seguir lista alguns exemplos de estruturas de ORM (Mapeamento Relacional de Objeto) e estruturas da Web que os aplicativos cliente podem usar com o Microsoft SQL Server em execução local ou na nuvem, em Linux, Windows ou Docker e também no Banco de Dados SQL do Azure e no SQL Data Warehouse do Azure. 

| Linguagem | Plataforma | ORM(s) |
| :-- | :-- | :-- |
| C# | Windows, Linux, macOS | [Entity Framework](https://docs.microsoft.com/ef)<br>[Entity Framework Core](https://docs.microsoft.com/ef/core/index) |
| Java | Windows, Linux, macOS |[Colocar o ORM em hibernação](https://hibernate.org/orm)|
| PHP | Windows, Linux | [Laravel (Eloquent)](https://laravel.com/docs/5.0/eloquent) |
| Node.js | Windows, Linux, macOS | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | Windows, Linux, macOS |[Django](https://www.djangoproject.com/) |
| Ruby | Windows, Linux, macOS | [Ruby on Rails](https://rubyonrails.org/) |

## <a name="related-links"></a>Links relacionados
- [Drivers do SQL Server](https://msdn.microsoft.com/library/mt654049.aspx) para conectar-se de aplicativos cliente

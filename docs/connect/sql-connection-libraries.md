---
title: Bibliotecas de conexão para Bancos de Dados do Microsoft SQL | Microsoft Docs
description: Fornece links para download de módulos que permitem a conexão ao Microsoft SQL Server e ao Banco de Dados SQL do Azure de uma ampla variedade de linguagens de programação do cliente.
author: MightyPen
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: article
ms.date: 06/18/2018
ms.author: genemi
ms.openlocfilehash: 71254b937c4c0173af9e1549efb98a0b42f65e02
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78338607"
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>Módulos de conexão para bancos de dados do Microsoft SQL

Este artigo fornece links de download para módulos de conexão ou *drivers* que seus programas cliente podem usar para interagir com o [Microsoft SQL Server](../relational-databases/database-features.md) e com o gêmeo dele na nuvem, o [Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/). Os drivers estão disponíveis para uma variedade de linguagens de programação, em execução nos seguintes sistemas operacionais:

- Linux
- MacOS
- Windows

#### <a name="oop-to-relational-mismatch"></a>Incompatibilidade de OOP para relacional

*Relacional*: Os programas cliente escritos em uma linguagem OOP (programação orientada a objeto) geralmente usam drivers SQL que retornam dados consultados em um formato mais relacional do que orientado a objetos. O C# usando ADO.NET é um exemplo. Às vezes, a incompatibilidade entre os formatos OOP e relacional torna o código OOP mais difícil de escrever e entender.

*ORM*: outros drivers ou estruturas retornam dados consultados no formato OOP, evitando a incompatibilidade. Esses drivers funcionam esperando que as classes tenham sido definidas para corresponder às colunas de dados de tabelas do SQL específicas. Em seguida, o driver executa o *ORM* (mapeamento relacional de objeto) para retornar dados consultados como uma instância de uma classe. O EF (Entity Framework) da Microsoft para C# e o Hibernate para Java são dois exemplos.

Este artigo destina seções separadas para esses dois tipos de drivers de conexão.

<a name="anchor-20-drivers-relational-access" />

## <a name="drivers-for-relational-access"></a>Drivers para acesso relacional


<!--
Each given Microsoft Download Center page should be enhanced
with a link to the next NEWER version page, on the day that the
original page is no longer the latest because the newer page is being added.
But this policy is not agreed on or observed,
putting the links in the following table at risk for being outdated.

PHP driver in Github.com also uses this FWLink:  https://go.microsoft.com/fwlink/?LinkID=518036 ,
although the FWLink is less precise than is https://github.com/Microsoft/msphpsql/tree/dev#install-unix .
-->

| Linguagem | Baixar o driver do SQL |
| :------- | :---------------------- |
| C# | [ADO.NET](https://www.microsoft.com/net/download/)<br />[Microsoft.Data.SqlClient](https://www.nuget.org/packages/Microsoft.Data.SqlClient/)<br /><br />[.NET Core para Linux-Ubuntu](https://www.microsoft.com/net/core#Ubuntu)<br />[.NET Core para macOS](https://www.microsoft.com/net/core#macos)<br />[.NET Core para Windows](https://www.microsoft.com/net/core) |
| C++ | [ODBC](./odbc/download-odbc-driver-for-sql-server.md)<br /><br />[OLE DB](./oledb/download-oledb-driver-for-sql-server.md) |
| Java | [JDBC](./jdbc/download-microsoft-jdbc-driver-for-sql-server.md) |
| Node.js | [Driver do Node.js, instruções de instalação](./node-js/step-1-configure-development-environment-for-node-js-development.md) |
| PHP | [PHP](./php/download-drivers-php-sql-server.md) |
| Python | [pyodbc, instruções de instalação](./python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md)<br />[Baixar o ODBC](./odbc/download-odbc-driver-for-sql-server.md) |
| Ruby | [Driver do Ruby, instruções de instalação](./ruby/step-1-configure-development-environment-for-ruby-development.md)<br />[Página de download do Ruby](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br /> |

<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>Drivers para acesso de ORM


A tabela a seguir lista exemplos de estruturas de ORM (mapeamento relacional de objeto) que os aplicativos cliente usam para se conectar aos bancos de dados do Microsoft SQL.


| Linguagem | Download do driver de ORM |
| :------- | :------------------ |
| C# | [Entity Framework Core](https://docs.microsoft.com/ef/core/)<br />[Entity Framework (6.x ou posterior)](https://docs.microsoft.com/ef/) |
| Java | [Colocar o ORM em hibernação](https://hibernate.org/orm)|
| PHP | [ORM Eloquent, incluído na instalação do Laravel](https://laravel.com/docs/) |
| Node.js | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | [Django](https://www.djangoproject.com/) |
| Ruby | [Ruby on Rails](https://rubyonrails.org/) |


<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>Páginas da Web sobre criação de aplicativos
[https://aka.ms/sqldev](https://aka.ms/sqldev) leva você a um conjunto de páginas da Web sobre *criação de aplicativos*. As páginas da Web fornecem informações sobre várias combinações de linguagem de programação, sistema operacional e driver de conexão SQL. Entre as informações fornecidas pelas páginas da Web sobre criação de aplicativos estão os seguintes itens:

- Detalhes sobre como começar do zero, para cada combinação de linguagem de programação + sistema operacional + driver.
    - Instruções para instalar os drivers de conexão SQL mais recentes.
- Exemplos de código para cada um dos seguintes itens:
    - Exemplos de código relacional de objeto.
    - Exemplos de código ORM.
    - Demonstrações de índice Columnstore para um desempenho muito mais rápido.

#### <a name="first-page-of-build-an-app-webpages"></a>Primeira página das páginas da Web sobre criação de aplicativos
![Páginas da Web sobre criação de aplicativos, captura de tela da primeira página][image-ref-163-buildanapp-webpages-first-page]

#### <a name="menu-for-java---ubuntu-of-build-an-app-webpages"></a>Menu para Java – Ubuntu das páginas da Web sobre criação de aplicativos
![Páginas da Web sobre criação de aplicativos, menu Java Ubuntu][image-ref-167-buildanapp-webpages-menu-java-ubuntu]

&nbsp;

## <a name="related-links"></a>Links relacionados
- [Exemplos de código para se conectar ao Banco de Dados SQL do Azure na nuvem, com Java e outras linguagens](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java).

<!-- Image references -->

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png

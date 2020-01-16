---
title: Desenvolver aplicativos usando o Always Encrypted | Microsoft Docs
ms.custom: ''
ms.date: 10/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0dbf983f044118a5d59812f1183d0733b20cb449
ms.sourcegitcommit: a26cb217adfbbfb3636dff43fb19a46462e2e994
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2019
ms.locfileid: "74492013"
---
# <a name="develop-applications-using-always-encrypted"></a>Desenvolver aplicativos usando o Always Encrypted
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

O[Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) é uma tecnologia de criptografia do lado do cliente que garante que os dados confidenciais (e as chaves de criptografia relacionadas) nunca são revelados para o SQL Server nem para o Banco de Dados SQL do Azure. Com o Always Encrypted, um driver de cliente criptografa de forma transparente os dados confidenciais antes de passá-los para o Mecanismo de Banco de Dados e descriptografa de forma transparente os dados recuperados de colunas de banco de dados criptografadas.

Para obter detalhes sobre como desenvolver aplicativos que usam bancos de dados protegidos pelo Always Encrypted e quais drivers de cliente e versões de driver dão suporte ao Always Encrypted, veja:

- [Usando o Always Encrypted com o Provedor de Dados .NET Framework para SQL Server](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [Use Always Encrypted com o Driver JDBC](../../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)
- [Uso do Always Encrypted com o Driver ODBC](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
- [Como usar o Always Encrypted com drivers PHP](../../../connect/php/using-always-encrypted-php-drivers.md)
- [Como usar Always Encrypted, o Provedor de Dados do Microsoft .NET para SQL Server em aplicativos .NET Core e .NET Framework](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md)
- [Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)

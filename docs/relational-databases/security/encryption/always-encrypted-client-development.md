---
title: Always Encrypted (desenvolvimento do cliente) | Microsoft Docs
ms.custom: SQL2016_New_Updated
ms.date: 07/29/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
caps.latest.revision: "33"
author: stevestein
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 103b3d51f8d9e1a5d809b9202a9808e8a5978bfe
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="always-encrypted-client-development"></a>Always Encrypted (desenvolvimento de cliente)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

O[Always Encrypted](../../../relational-databases/security/encryption/always-encrypted-database-engine.md) é uma tecnologia de criptografia do lado do cliente que garante que os dados confidenciais (e as chaves de criptografia relacionadas) nunca são revelados para o SQL Server nem para o Banco de Dados SQL do Azure. Com o Always Encrypted, um driver de cliente criptografa de forma transparente os dados confidenciais antes de passá-los para o Mecanismo de Banco de Dados e descriptografa de forma transparente os dados recuperados de colunas de banco de dados criptografadas.

Para obter detalhes sobre como desenvolver aplicativos que usam bancos de dados protegidos pelo Always Encrypted e quais drivers de cliente e versões de driver dão suporte ao Always Encrypted, veja:

- [Usando o Always Encrypted com o Provedor de Dados .NET Framework para SQL Server](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [Use Always Encrypted com o Driver JDBC](../../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)
- [Como usar Always Encrypted com o driver ODBC do Windows](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)



## <a name="see-also"></a>Consulte também

[Always Encrypted (mecanismo de banco de dados)](../../../relational-databases/security/encryption/always-encrypted-database-engine.md)


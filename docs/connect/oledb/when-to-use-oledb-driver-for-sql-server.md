---
title: Quando usar o Driver do OLE DB
description: Saiba quando usar o Driver do OLE DB para SQL Server e conheça os conceitos de acesso a dados de alto nível que o diferencia dos outros drivers.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 114a0e65f6d813bb2d43ca8641e3260e9b88f668
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86011898"
---
# <a name="when-to-use-ole-db-driver-for-sql-server"></a>Quando usar o OLE DB Driver for SQL Server
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  O OLE DB para SQL Server é uma tecnologia que você pode usar para acessar dados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Para obter uma discussão sobre as diferentes tecnologias de acesso a dados, confira [Roteiro das tecnologias de acesso a dados](https://go.microsoft.com/fwlink/?LinkID=179186)  
  
 Ao decidir se você usará o OLE DB Driver for SQL Server como a tecnologia de acesso a dados de seu aplicativo, você deverá considerar vários fatores.  
  
 No caso de novos aplicativos, se você estiver usando uma linguagem de programação gerenciada, como o Microsoft Visual C# ou o Visual Basic, e precisar acessar os novos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use o provedor de dados .NET Framework para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que faz parte do .NET Framework.  
  
 Caso esteja desenvolvendo um aplicativo baseado no COM e precise acessar os novos recursos introduzidos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use o OLE DB Driver for SQL Server. Caso não precise do acesso aos novos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você poderá continuar a usar o WDAC (Windows Data Access Components).  
  
 Para os aplicativos OLE DB existentes, o principal problema é se você precisa acessar os novos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Caso tenha um aplicativo consolidado que não precise dos novos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você poderá continuar usando o WDAC. No entanto, caso precise acessar esses novos recursos, como o [tipo de dados xml](../../t-sql/xml/xml-transact-sql.md), use o OLE DB Driver for SQL Server.  
  
 Tanto o Driver do OLE DB para SQL Server quanto o MDAC oferecem suporte ao isolamento de transação de leitura confirmada usando controle de versão de linha, mas apenas o Driver do OLE DB para SQL Server dá suporte ao isolamento da transação de instantâneo. (Em termos de programação, o isolamento de transação de leitura confirmada por meio do controle de versão de linha é igual à transação de leitura confirmada.)  
  
 Confira mais informações sobre as diferenças entre o Driver do OLE DB para SQL Server e o MDAC em [Atualizar um aplicativo do MDAC para o Driver do OLE DB para SQL Server](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Driver do OLE DB para SQL Server](oledb-driver-for-sql-server.md)  
 [Tópicos de instruções do OLE DB](ole-db-how-to/ole-db-how-to-topics.md)  
  
  

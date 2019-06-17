---
title: Quando usar o OLE DB Driver for SQL Server | Microsoft Docs
description: Quando usar o OLE DB Driver for SQL Server
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
manager: jroth
ms.openlocfilehash: 210a15d827cb8f0a828c11c1c8fe87586cd79028
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66795883"
---
# <a name="when-to-use-ole-db-driver-for-sql-server"></a>Quando usar o OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  Driver do OLE DB para SQL Server é uma tecnologia que você pode usar para acessar dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados.  Para obter uma discussão sobre as diferentes tecnologias de acesso a dados, confira [Roteiro das tecnologias de acesso a dados](https://go.microsoft.com/fwlink/?LinkID=179186)  
  
 Ao decidir se você usará o OLE DB Driver for SQL Server como a tecnologia de acesso a dados de seu aplicativo, você deverá considerar vários fatores.  
  
 No caso de novos aplicativos, se você estiver usando uma linguagem de programação gerenciada, como o Microsoft Visual C# ou o Visual Basic, e precisar acessar os novos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use o provedor de dados .NET Framework para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que faz parte do .NET Framework.  
  
 Caso esteja desenvolvendo um aplicativo baseado no COM e precise acessar os novos recursos introduzidos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use o OLE DB Driver for SQL Server. Caso não precise do acesso aos novos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você poderá continuar a usar o WDAC (Windows Data Access Components).  
  
 Para os aplicativos OLE DB existentes, o principal problema é se você precisa acessar os novos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Caso tenha um aplicativo consolidado que não precise dos novos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você poderá continuar usando o WDAC. No entanto, caso precise acessar esses novos recursos, como o [tipo de dados xml](../../t-sql/xml/xml-transact-sql.md), use o OLE DB Driver for SQL Server.  
  
 Ambos os Driver OLE DB para o suporte do SQL Server e o MDAC isolamento de transação confirmada usando controle de versão de linha, mas apenas Driver do OLE DB do SQL Server dá suporte a transações para isolamento de instantâneo de leitura. (Em termos de programação, o isolamento de transação de leitura confirmada por meio do controle de versão de linha é igual à transação de leitura confirmada.)  
  
 Para obter informações sobre as diferenças entre o Driver do OLE DB para SQL Server e o MDAC, consulte [atualizando um aplicativo para o Driver do OLE DB para SQL Server no MDAC](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  
  
## <a name="see-also"></a>Consulte Também  
 [OLE DB Driver for SQL Server](../oledb/oledb-driver-for-sql-server.md)     
 [Tópicos de instruções do OLE DB](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  

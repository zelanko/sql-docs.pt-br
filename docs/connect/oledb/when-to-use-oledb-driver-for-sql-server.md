---
title: Quando usar o Driver do OLE DB para SQL Server | Microsoft Docs
description: Quando usar o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: b3fa8f071055f33bb256d3b28ed4aaa807f093a8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32856231"
---
# <a name="when-to-use-ole-db-driver-for-sql-server"></a>Quando usar o Driver do OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  OLE DB Driver para SQL Server é uma tecnologia que você pode usar para acessar dados em um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados.  Para uma discussão sobre as tecnologias de acesso a dados diferentes, consulte [roteiro de tecnologias de acesso de dados](http://go.microsoft.com/fwlink/?LinkID=179186)  
  
 Ao decidir se deseja usar o Driver OLE DB para SQL Server como a tecnologia de acesso a dados do seu aplicativo, você deve considerar vários fatores.  
  
 No caso de novos aplicativos, se você estiver usando uma linguagem de programação gerenciada, como o Microsoft Visual C# ou o Visual Basic, e precisar acessar os novos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use o provedor de dados .NET Framework para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que faz parte do .NET Framework.  
  
 Se você estiver desenvolvendo um aplicativo baseado em COM e precisar acessar os novos recursos introduzidos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você deve usar o Driver do OLE DB para SQL Server. Caso não precise do acesso aos novos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você poderá continuar a usar o WDAC (Windows Data Access Components).  
  
 Para aplicativos OLE DB existentes, o principal problema é se você precisar acessar os novos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Caso tenha um aplicativo consolidado que não precise dos novos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você poderá continuar usando o WDAC. Mas se você precisar acessar esses novos recursos, como o [tipo de dados xml](../../t-sql/xml/xml-transact-sql.md), você deve usar o Driver do OLE DB para SQL Server.  
  
 Ambos os Driver OLE DB para o suporte do SQL Server e o MDAC isolamento de transação confirmada usando controle de versão de linha, mas somente OLE DB Driver para isolamento de transação do SQL Server dá suporte a instantâneo de leitura. (Em termos de programação, o isolamento de transação de leitura confirmada por meio do controle de versão de linha é igual à transação de leitura confirmada.)  
  
 Para obter informações sobre as diferenças entre o OLE DB Driver para SQL Server e o MDAC, consulte [atualizando um aplicativo para o Driver do OLE DB para SQL Server do MDAC](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  
  
## <a name="see-also"></a>Consulte também  
 [Driver do OLE DB para SQL Server](../oledb/oledb-driver-for-sql-server.md)     
 [Tópicos de instruções do OLE DB](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  

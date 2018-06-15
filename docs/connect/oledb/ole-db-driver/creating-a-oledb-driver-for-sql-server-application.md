---
title: Criando um Driver do OLE DB para o aplicativo do SQL Server | Microsoft Docs
description: Criando um Driver OLE DB para o aplicativo do SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|oledb-driver-for-sql-server
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, application creation
- applications [OLE DB Driver for SQL Server]
- OLE DB, creating applications
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 09cd1243859ef11dccf4a86084aa919a3cc5624a
ms.sourcegitcommit: e1bc8c486680e6d6929c0f5885d97d013a537149
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2018
ms.locfileid: "35665306"
---
# <a name="creating-an-ole-db-driver-for-sql-server-application"></a>Criando um Driver do OLE DB para o aplicativo do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  A criação de um Driver OLE DB para o aplicativo do SQL Server envolve estas etapas:  
  
1.  Estabelecimento de uma conexão a uma fonte de dados.  
  
2.  Execução de um comando.  
  
3.  Processamento dos resultados.  
  
> [!NOTE]  
>  Quando possível, use a Autenticação do Windows. Se a Autenticação do Windows não estiver disponível, solicite aos usuários que digitem suas credenciais em tempo de execução. Evite armazenar as credenciais em um arquivo. Se você deve manter as credenciais, criptografe-as com [cryptoAPI Win32](http://go.microsoft.com/fwlink/?LinkId=9504).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Estabelecendo uma conexão com uma fonte de dados](../../oledb/ole-db-driver/establishing-a-connection-to-a-data-source.md)  
  
-   [Executando um comando](../../oledb/ole-db-driver/executing-a-command.md)  
  
-   [Processando resultados](../../oledb/ole-db-driver/processing-results.md)  
  
-   [Sobre propriedades OLE DB](../../oledb/ole-db-driver/about-ole-db-properties.md)  
  
-   [Uso da cláusula OUTPUT com OLE DB no Driver do OLE DB para SQL Server](../../oledb/ole-db-driver/using-the-output-clause-with-ole-db-in-oledb-driver-for-sql-server.md)  
  
## <a name="see-also"></a>Consulte também  
 [Programação no Driver do OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  

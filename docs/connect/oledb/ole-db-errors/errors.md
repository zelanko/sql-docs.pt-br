---
title: Erros | Microsoft Docs
description: Erros
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 84c20e744dc69c18d3c46a26f49ed78bf63ce40c
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43021985"
---
# <a name="errors"></a>Erros
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Os objetos OLE/COM informam erros através do código de retorno de HRESULT das funções de membro de objeto. Um HRESULT de OLE/COM é uma estrutura de bits compactados. A OLE fornece macros que eliminam a referência de membros de estrutura.  
  
 O OLE/COM especifica a interface **IErrorInfo**. A interface expõe métodos como **GetDescription**. Isso permite que clientes extraiam detalhes de erros dos servidores OLE/COM. O OLE DB estende **IErrorInfo** para dar suporte ao retorno de vários pacotes de informações de erros em uma execução de função de único membro.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode retornar vários erros. Um aplicativo pode recuperar erros do servidor um de cada vez chamando [IMultipleResults::GetResult](http://go.microsoft.com/fwlink/?LinkId=129630) combinado com ISQLErrorInfo e IErrorRecords.  
  
 O OLE DB Driver for SQL Server expõe as interfaces de objetos de erro **IErrorInfo** aprimorada por registro do OLE DB, **ISQLErrorInfo** personalizada e [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1) específica do provedor.  
  
 Para obter informações sobre como rastrear erros, confira [Rastreamento do acesso a dados](http://go.microsoft.com/fwlink/?LinkId=125805). Para obter informações sobre os aprimoramentos para rastreamento de erro adicionado ao [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], consulte [acessando informações de diagnóstico no Log de eventos estendidos](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Códigos de retorno](../../oledb/ole-db-errors/return-codes.md)  
  
-   [Informações em interfaces de erro](../../oledb/ole-db-errors/information-in-error-interfaces.md)  
  
-   [Detalhes de erros do SQL Server](../../oledb/ole-db-errors/sql-server-error-detail.md)  
  
-   [Recuperando informações de erro](../../oledb/ole-db-errors/retrieving-error-information.md)  
  
-   [Resultados da mensagem do SQL Server](../../oledb/ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Programação no Driver do OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  

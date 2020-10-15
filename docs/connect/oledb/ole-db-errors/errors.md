---
title: OLE DB Errors
description: Saiba mais sobre como os erros são retornados no Driver do OLE DB para SQL Server e como você pode obter informações sobre eles.
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- OLE/COM errors
- errors [OLE DB]
- OLE DB error handling, about error handling
- OLE DB error handling
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f806ff605b8f35f112de4c16216e0da24d2df31c
ms.sourcegitcommit: 7eb80038c86acfef1d8e7bfd5f4e30e94aed3a75
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92081995"
---
# <a name="errors"></a>Errors
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Os objetos OLE/COM informam erros através do código de retorno de HRESULT das funções de membro de objeto. Um HRESULT de OLE/COM é uma estrutura de bits compactados. A OLE fornece macros que eliminam a referência de membros de estrutura.  
  
 O OLE/COM especifica a interface **IErrorInfo**. A interface expõe métodos como **GetDescription**. Isso permite que clientes extraiam detalhes de erros dos servidores OLE/COM. O OLE DB estende **IErrorInfo** para dar suporte ao retorno de vários pacotes de informações de erros em uma execução de função de único membro.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode retornar vários erros. Um aplicativo pode recuperar erros do servidor um de cada vez chamando [IMultipleResults::GetResult](/previous-versions/windows/desktop/ms721289(v=vs.85)) combinado com ISQLErrorInfo e IErrorRecords.  
  
 O OLE DB Driver for SQL Server expõe as interfaces de objetos de erro **IErrorInfo** aprimorada por registro do OLE DB, **ISQLErrorInfo** personalizada e [ISQLServerErrorInfo](../ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md) específica do provedor.  
  
 Para obter informações sobre como rastrear erros, confira [Rastreamento do acesso a dados](/previous-versions/sql/sql-server-2008/cc765421(v=sql.100)). Para obter informações sobre aprimoramentos no rastreamento de erros adicionados em [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], confira [Acessar informações de diagnóstico nos logs de eventos estendidos](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Códigos de retorno](../../oledb/ole-db-errors/return-codes.md)  
  
-   [Informações em interfaces de erro](../../oledb/ole-db-errors/information-in-error-interfaces.md)  
  
-   [Detalhes de erros do SQL Server](../../oledb/ole-db-errors/sql-server-error-detail.md)  
  
-   [Recuperando informações de erro](../../oledb/ole-db-errors/retrieving-error-information.md)  
  
-   [Resultados da mensagem do SQL Server](../../oledb/ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Programação no Driver do OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  

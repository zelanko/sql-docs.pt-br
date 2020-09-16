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
ms.openlocfilehash: ddd8fd4e6280e49d924a0bf60f4d8a4900c114e4
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862006"
---
# <a name="errors"></a>Errors
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Os objetos OLE/COM informam erros através do código de retorno de HRESULT das funções de membro de objeto. Um HRESULT de OLE/COM é uma estrutura de bits compactados. A OLE fornece macros que eliminam a referência de membros de estrutura.  
  
 O OLE/COM especifica a interface **IErrorInfo**. A interface expõe métodos como **GetDescription**. Isso permite que clientes extraiam detalhes de erros dos servidores OLE/COM. O OLE DB estende **IErrorInfo** para dar suporte ao retorno de vários pacotes de informações de erros em uma execução de função de único membro.  
  
 O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] pode retornar vários erros. Um aplicativo pode recuperar erros do servidor um de cada vez chamando [IMultipleResults::GetResult](https://go.microsoft.com/fwlink/?LinkId=129630) combinado com ISQLErrorInfo e IErrorRecords.  
  
 O OLE DB Driver for SQL Server expõe as interfaces de objetos de erro **IErrorInfo** aprimorada por registro do OLE DB, **ISQLErrorInfo** personalizada e [ISQLServerErrorInfo](https://docs.microsoft.com/sql/connect/oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db?view=sql-server-ver15) específica do provedor.  
  
 Para obter informações sobre como rastrear erros, confira [Rastreamento do acesso a dados](https://go.microsoft.com/fwlink/?LinkId=125805). Para obter informações sobre aprimoramentos no rastreamento de erros adicionados em [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], confira [Acessar informações de diagnóstico nos logs de eventos estendidos](../../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Códigos de retorno](../../oledb/ole-db-errors/return-codes.md)  
  
-   [Informações em interfaces de erro](../../oledb/ole-db-errors/information-in-error-interfaces.md)  
  
-   [Detalhes de erros do SQL Server](../../oledb/ole-db-errors/sql-server-error-detail.md)  
  
-   [Recuperando informações de erro](../../oledb/ole-db-errors/retrieving-error-information.md)  
  
-   [Resultados da mensagem do SQL Server](../../oledb/ole-db-errors/sql-server-message-results.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Programação no Driver do OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
  
  

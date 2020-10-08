---
title: Informações em interfaces de erro
description: O Driver do OLE DB para SQL Server relata algumas informações sobre erros e status nas interfaces de erro definidas por OLE DB IErrorInfo, IErrorRecords e ISQLErrorInfo.
ms.custom: ''
ms.date: 05/06/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error interfaces
- ISQLErrorInfo interface
- errors [OLE DB], error interfaces
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25115cc1e5d34624b13c6218cef256e686d39e3d
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727182"
---
# <a name="information-in-error-interfaces"></a>Informações em interfaces de erro
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O OLE DB Driver for SQL Server relata algumas informações sobre erros e status nas interfaces de erro definidas por OLE DB **IErrorInfo**, **IErrorRecords** e **ISQLErrorInfo**.  
  
 O Driver do OLE DB para SQL Server dá suporte a funções de membro **IErrorInfo** como a seguir.  
  
|Função de membro|Descrição|  
|---------------------|-----------------|  
|**GetDescription**|Cadeia de caracteres de mensagem de erro descritiva.|  
|**GetGUID**|GUID da interface que definiu o erro.|  
|**GetHelpContext**|Sem suporte. Sempre retorna zero.|  
|**GetHelpFile**|Sem suporte. Sempre retorna NULL.|  
|**GetSource**|Cadeia de caracteres "Microsoft OLE DB Driver for SQL Server".|  
  
 O Driver do OLE DB para SQL Server dá suporte a funções de membro **IErrorInfo** disponíveis para consumidor como a seguir.  
  
|Função de membro|Descrição|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|Preenche uma estrutura ERRORINFO com informações básica sobre um erro. Uma estrutura ERRORINFO contém membros que identificam o valor de retorno HRESULT para o erro e o provedor e interface aos quais o erro se aplica.|  
|**GetCustomErrorObject**|Retorna uma referência em interfaces **ISQLErrorInfo** e [ISQLServerErrorInfo](../ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md?view=sql-server-ver15).|  
|**GetErrorInfo**|Retorna uma referência em uma interface **IErrorInfo**.|  
|**GetErrorParameters**|O Driver do OLE DB para SQL Server não retorna parâmetros para o consumidor por meio de **GetErrorParameters**.|  
|**GetRecordCount**|Contagem de registros de erro disponível.|  
  
 O Driver do OLE DB para SQL Server dá suporte para os parâmetros **ISQLErrorInfo::GetSQLInfo** como a seguir.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*pbstrSQLState*|Retorna um valor SQLSTATE para o erro. São definidos valores SQLSTATE nas especificações SQL-92, ODBC ISO SQL e de API. Nem o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nem o Driver do OLE DB para SQL Server definiram valores SQLSTATE específicos de implementação.|  
|*plNativeError*|Retorna o número do erro do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de **master.dbo.sysmessages** quando disponível. Os erros nativos estão disponíveis após uma tentativa bem-sucedida de inicializar uma fonte de dados do Driver do OLE DB para SQL Server. Antes da tentativa, o Driver do OLE DB para SQL Server sempre retorna zero.|  
  
## <a name="see-also"></a>Consulte Também  
 [Erros](../../oledb/ole-db-errors/errors.md)  
  

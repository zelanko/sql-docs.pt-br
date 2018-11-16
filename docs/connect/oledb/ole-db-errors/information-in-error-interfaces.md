---
title: Informações em Interfaces de erro | Microsoft Docs
description: Informações em interfaces de erro
ms.custom: ''
ms.date: 06/14/2018
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
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: c80013249af94a2ad94c221bc6155dca7c7d2664
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606756"
---
# <a name="information-in-error-interfaces"></a>Informações em interfaces de erro
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O OLE DB Driver for SQL Server relata algumas informações sobre erros e status nas interfaces de erro definidas por OLE DB **IErrorInfo**, **IErrorRecords** e **ISQLErrorInfo**.  
  
 O Driver do OLE DB para SQL Server dá suporte a **IErrorInfo** funções de membro da seguinte maneira.  
  
|Função de membro|Descrição|  
|---------------------|-----------------|  
|**GetDescription**|Cadeia de caracteres de mensagem de erro descritiva.|  
|**GetGUID**|GUID da interface que definiu o erro.|  
|**GetHelpContext**|Sem suporte. Sempre retorna zero.|  
|**GetHelpFile**|Sem suporte. Sempre retorna NULL.|  
|**GetSource**|Cadeia de caracteres "Microsoft OLE DB Driver for SQL Server".|  
  
 O Driver do OLE DB para SQL Server dá suporte ao consumidor disponíveis **IErrorRecords** funções de membro da seguinte maneira.  
  
|Função de membro|Descrição|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|Preenche uma estrutura ERRORINFO com informações básica sobre um erro. Uma estrutura ERRORINFO contém membros que identificam o valor de retorno HRESULT para o erro e o provedor e interface aos quais o erro se aplica.|  
|**GetCustomErrorObject**|Retorna uma referência em interfaces **ISQLErrorInfo** e [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1).|  
|**GetErrorInfo**|Retorna uma referência em uma interface **IErrorInfo**.|  
|**GetErrorParameters**|O Driver do OLE DB para SQL Server não retorna parâmetros para o consumidor por meio **GetErrorParameters**.|  
|**GetRecordCount**|Contagem de registros de erro disponível.|  
  
 O Driver do OLE DB para SQL Server dá suporte a **isqlerrorinfo:: Getsqlinfo** parâmetros da seguinte maneira.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*pbstrSQLState*|Retorna um valor SQLSTATE para o erro. São definidos valores SQLSTATE nas especificações SQL-92, ODBC ISO SQL e de API. Nem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nem o Driver OLE DB para SQL Server definidos valores SQLSTATE específicos de implementação.|  
|*plNativeError*|Retorna o número do erro do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de **master.dbo.sysmessages** quando disponível. Erros nativos estão disponíveis após uma tentativa bem-sucedida de inicializar um Driver OLE DB para fonte de dados do SQL Server. Antes da tentativa, o Driver do OLE DB para SQL Server sempre retorna zero.|  
  
## <a name="see-also"></a>Consulte Também  
 [Erros](../../oledb/ole-db-errors/errors.md)  
  
  

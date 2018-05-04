---
title: Informações em Interfaces de erro | Microsoft Docs
description: Informações em interfaces de erro
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-errors
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error interfaces
- ISQLErrorInfo interface
- errors [OLE DB], error interfaces
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 4f79c469f40c778342e1093df0386acee80890de
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="information-in-error-interfaces"></a>Informações em interfaces de erro
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O Driver OLE DB para SQL Server reporta algumas informações de erro e de status nas interfaces de erro definidas pelo OLE DB **IErrorInfo**, **IErrorRecords**, e **ISQLErrorInfo**.  
  
 O Driver OLE DB para SQL Server dá suporte a **IErrorInfo** funções de membro da seguinte maneira.  
  
|Função de membro|Description|  
|---------------------|-----------------|  
|**GetDescription**|Cadeia de caracteres de mensagem de erro descritiva.|  
|**GetGUID**|GUID da interface que definiu o erro.|  
|**GetHelpContext**|Sem suporte. Sempre retorna zero.|  
|**GetHelpFile**|Sem suporte. Sempre retorna NULL.|  
|**GetSource**|Cadeia de caracteres "Microsoft OLE DB Driver para SQL Server".|  
  
 O Driver OLE DB para SQL Server dá suporte ao consumidor disponíveis **IErrorRecords** funções de membro da seguinte maneira.  
  
|Função de membro|Description|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|Preenche uma estrutura ERRORINFO com informações básica sobre um erro. Uma estrutura ERRORINFO contém membros que identificam o valor de retorno HRESULT para o erro e o provedor e interface aos quais o erro se aplica.|  
|**GetCustomErrorObject**|Retorna uma referência em interfaces **ISQLErrorInfo** e [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1).|  
|**GetErrorInfo**|Retorna uma referência em uma **IErrorInfo** interface.|  
|**GetErrorParameters**|O Driver OLE DB para SQL Server não retorna parâmetros para o consumidor por meio de **GetErrorParameters**.|  
|**GetRecordCount**|Contagem de registros de erro disponível.|  
  
 O Driver OLE DB para SQL Server dá suporte a **isqlerrorinfo:: Getsqlinfo** parâmetros da seguinte maneira.  
  
|Parâmetro|Description|  
|---------------|-----------------|  
|*pbstrSQLState*|Retorna um valor SQLSTATE para o erro. São definidos valores SQLSTATE nas especificações SQL-92, ODBC ISO SQL e de API. Nem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nem o Driver OLE DB para SQL Server definidos valores SQLSTATE específicos de implementação.|  
|*plNativeError*|Retorna o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] número do erro **Master.dbo** quando disponível. Erros nativos estão disponíveis após uma tentativa bem-sucedida de inicializar um Driver OLE DB para fonte de dados do SQL Server. Antes da tentativa, o Driver OLE DB para SQL Server sempre retorna zero.|  
  
## <a name="see-also"></a>Consulte também  
 [Erros](../../oledb/ole-db-errors/errors.md)  
  
  

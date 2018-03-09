---
title: "Informações em Interfaces de erro | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-errors
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error interfaces
- ISQLErrorInfo interface
- errors [OLE DB], error interfaces
ms.assetid: 4620f03f-1193-43e7-ba19-ad022737d300
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e62543ca064b30efcbac57433dc024ca198ebb77
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="information-in-error-interfaces"></a>Informações em interfaces de erro
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client reporta algumas informações de erro e de status nas interfaces de erro definidas pelo OLE DB **IErrorInfo**, **IErrorRecords**, e **ISQLErrorInfo** .  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client oferece suporte a **IErrorInfo** funções de membro da seguinte maneira.  
  
|Função de membro|Description|  
|---------------------|-----------------|  
|**GetDescription**|Cadeia de caracteres de mensagem de erro descritiva.|  
|**GetGUID**|GUID da interface que definiu o erro.|  
|**GetHelpContext**|Sem suporte. Sempre retorna zero.|  
|**GetHelpFile**|Sem suporte. Sempre retorna NULL.|  
|**GetSource**|Cadeia de caracteres "Microsoft SQL Server Native Client".|  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB Native Client oferece suporte ao consumidor disponíveis **IErrorRecords** funções de membro da seguinte maneira.  
  
|Função de membro|Description|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|Preenche uma estrutura ERRORINFO com informações básica sobre um erro. Uma estrutura ERRORINFO contém membros que identificam o valor de retorno HRESULT para o erro e o provedor e interface aos quais o erro se aplica.|  
|**GetCustomErrorObject**|Retorna uma referência em interfaces **ISQLErrorInfo** e [ISQLServerErrorInfo](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1).|  
|**GetErrorInfo**|Retorna uma referência em uma **IErrorInfo** interface.|  
|**GetErrorParameters**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client não retorna parâmetros para o consumidor por meio de **GetErrorParameters**.|  
|**GetRecordCount**|Contagem de registros de erro disponível.|  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client oferece suporte a **isqlerrorinfo:: Getsqlinfo** parâmetros da seguinte maneira.  
  
|Parâmetro|Description|  
|---------------|-----------------|  
|*pbstrSQLState*|Retorna um valor SQLSTATE para o erro. São definidos valores SQLSTATE nas especificações SQL-92, ODBC ISO SQL e de API. Nem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nem o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor Native Client OLE DB definidos valores SQLSTATE específicos de implementação.|  
|*plNativeError*|Retorna o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] número do erro **Master.dbo** quando disponível. Erros nativos estão disponíveis após uma tentativa bem-sucedida de inicializar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fonte de dados do provedor OLE DB Native Client. Antes da tentativa de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client sempre retorna zero.|  
  
## <a name="see-also"></a>Consulte também  
 [Erros](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  

---
title: Informações em interfaces de erro | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error interfaces
- ISQLErrorInfo interface
- errors [OLE DB], error interfaces
ms.assetid: 4620f03f-1193-43e7-ba19-ad022737d300
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 256c11c46d24998808821002d3a63bbc17c40931
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73769457"
---
# <a name="information-in-error-interfaces"></a>Informações em interfaces de erro
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB relata algumas informações de erro e status nas interfaces de erro definidas pelo OLE DB **IErrorInfo**, **IErrorRecords**e **ISQLErrorInfo**.  
  
 O provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client oferece suporte às funções membro **IErrorInfo** da seguinte maneira.  
  
|Função de membro|Descrição|  
|---------------------|-----------------|  
|**GetDescription**|Cadeia de caracteres de mensagem de erro descritiva.|  
|**GetGUID**|GUID da interface que definiu o erro.|  
|**GetHelpContext**|Sem suporte. Sempre retorna zero.|  
|**GetHelpFile**|Sem suporte. Sempre retorna NULL.|  
|**GetSource**|Cadeia de caracteres "Microsoft SQL Server Native Client".|  
  
 O provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client oferece suporte a funções de membro **IErrorRecords** disponíveis para o consumidor da seguinte maneira.  
  
|Função de membro|Descrição|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|Preenche uma estrutura ERRORINFO com informações básica sobre um erro. Uma estrutura ERRORINFO contém membros que identificam o valor de retorno HRESULT para o erro e o provedor e interface aos quais o erro se aplica.|  
|**GetCustomErrorObject**|Retorna uma referência em interfaces **ISQLErrorInfo** e [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1).|  
|**GetErrorInfo**|Retorna uma referência em uma interface **IErrorInfo**.|  
|**GetErrorParameters**|O provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client não retorna parâmetros para o consumidor por meio de **Geterroparameters**.|  
|**GetRecordCount**|Contagem de registros de erro disponível.|  
  
 O provedor de OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client oferece suporte aos parâmetros **ISQLErrorInfo:: GetSQLInfo** da seguinte maneira.  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*pbstrSQLState*|Retorna um valor SQLSTATE para o erro. São definidos valores SQLSTATE nas especificações SQL-92, ODBC ISO SQL e de API. Nem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nem o provedor de OLE DB cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativo definiu valores SQLSTATE específicos de implementação.|  
|*plNativeError*|Retorna o número do erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de **master.dbo.sysmessages** quando disponível. Os erros nativos estão disponíveis após uma tentativa bem-sucedida de inicializar uma fonte de dados de provedor de OLE DB de cliente nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Antes da tentativa, o provedor de OLE DB do cliente nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre retorna zero.|  
  
## <a name="see-also"></a>Consulte também  
 [Erros](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  

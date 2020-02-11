---
title: Informações em interfaces de erro | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 60b6b0387aea5475d74c314a10e4fa437fadc005
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62657656"
---
# <a name="information-in-error-interfaces"></a>Informações em interfaces de erro
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo relata algumas informações de erro e status nas interfaces de erro definidas pelo OLE DB **IErrorInfo**, **IErrorRecords**e **ISQLErrorInfo**.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo dá suporte às funções membro **IErrorInfo** da seguinte maneira.  
  
|Função de membro|DESCRIÇÃO|  
|---------------------|-----------------|  
|**GetDescription**|Cadeia de caracteres de mensagem de erro descritiva.|  
|**GetGuid**|GUID da interface que definiu o erro.|  
|**GetHelpContext**|Sem suporte. Sempre retorna zero.|  
|**GetHelpFile**|Sem suporte. Sempre retorna NULL.|  
|**GetSource**|Cadeia de caracteres "Microsoft SQL Server Native Client".|  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo oferece suporte a funções de membro **IErrorRecords** disponíveis para o consumidor da seguinte maneira.  
  
|Função de membro|DESCRIÇÃO|  
|---------------------|-----------------|  
|**GetBasicErrorInfo**|Preenche uma estrutura ERRORINFO com informações básica sobre um erro. Uma estrutura ERRORINFO contém membros que identificam o valor de retorno HRESULT para o erro e o provedor e interface aos quais o erro se aplica.|  
|**GetCustomErrorObject**|Retorna uma referência em interfaces **ISQLErrorInfo** e [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md).|  
|**GetErrorInfo**|Retorna uma referência em uma interface **IErrorInfo**.|  
|**Geterroparameters**|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo não retorna parâmetros para o consumidor por meio de **geterroparameters**.|  
|**GetRecordCount**|Contagem de registros de erro disponível.|  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo oferece suporte aos parâmetros **ISQLErrorInfo:: GetSQLInfo** da seguinte maneira.  
  
|Parâmetro|DESCRIÇÃO|  
|---------------|-----------------|  
|*pbstrSQLState*|Retorna um valor SQLSTATE para o erro. São definidos valores SQLSTATE nas especificações SQL-92, ODBC ISO SQL e de API. Nem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de OLE DB nativo não definiu valores SQLSTATE específicos de implementação.|  
|*plNativeError*|Retorna o número do erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de **master.dbo.sysmessages** quando disponível. Os erros nativos estão disponíveis após uma tentativa bem-sucedida de inicializar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] uma fonte de dados de provedor de OLE DB de cliente nativo. Antes da tentativa, o provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de OLE DB de cliente nativo sempre retorna zero.|  
  
## <a name="see-also"></a>Consulte Também  
 [Errors](errors.md)  
  
  

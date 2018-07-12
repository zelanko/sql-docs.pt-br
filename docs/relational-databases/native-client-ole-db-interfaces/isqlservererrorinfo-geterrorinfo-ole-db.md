---
title: ISQLServerErrorInfo::GetErrorInfo (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISQLServerErrorInfo::GetErrorInfo (OLE DB)
apitype: COM
helpviewer_keywords:
- GetErrorInfo method
ms.assetid: 83265c9c-eaf9-41f0-9f73-b0ae0972f0d5
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 0a157d42f4bb464cef821f344d0218ecd150e76f
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37410597"
---
# <a name="isqlservererrorinfogeterrorinfo-ole-db"></a>ISQLServerErrorInfo::GetErrorInfo (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Retorna um ponteiro para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estrutura de SSERRORINFO do provedor OLE DB do Native Client que contém o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detalhes do erro.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client define as **ISQLServerErrorInfo** interface de erro. Essa interface retorna detalhes de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] erro, incluindo sua severidade e estado.  

  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT GetErrorInfo(  
   SSERRORINFO**ppSSErrorInfo,  
   OLECHAR**ppErrorStrings);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ppSSErrorInfo*[out]  
 Um ponteiro para uma estrutura SSERRORINFO. Se o método falhar ou não há nenhuma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informações associadas com o erro, o provedor não alocará nenhuma memória e garante que o *ppSSErrorInfo* argumento for um ponteiro nulo na saída.  
  
 *ppErrorStrings*[out]  
 Um ponteiro para um ponteiro de cadeia de caracteres Unicode. Se o método falhar ou não há nenhuma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] informações associadas a um erro, o provedor não alocará nenhuma memória e garante que o *ppErrorStrings* argumento for um ponteiro nulo na saída. Liberando a *ppErrorStrings* argumento com o **IMalloc:: Free** método libera os três membros de cadeia de caracteres individuais da estrutura SSERRORINFO retornada, como a memória é alocada em um bloco.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 O método foi bem-sucedido.  
  
 E_INVALIDARG  
 Ambos os *ppSSErrorInfo* ou o *ppErrorStrings* argumento era nulo.  
  
 E_OUTOFMEMORY  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client não foi possível alocar memória suficiente para concluir a solicitação.  
  
## <a name="remarks"></a>Remarks  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client aloca memória para as cadeias de caracteres SSERRORINFO e OLECHAR retornadas por meio dos ponteiros passados pelo consumidor. O consumidor deverá desalocar essa memória usando o **IMalloc:: Free** método quando ele não requer mais acesso aos dados de erro.  
  
 A estrutura SSERRORINFO é definida da seguintes maneira:  
  
```  
typedef struct tagSSErrorInfo  
   {  
   LPOLESTR pwszMessage;  
   LPOLESTR pwszServer;  
   LPOLESTR pwszProcedure;  
   LONG lNative;  
   BYTE bState;  
   BYTE bClass;  
   WORD wLineNumber;  
   }  
SSERRORINFO;  
```  
  
|Membro|Description|  
|------------|-----------------|  
|*pwszMessage*|A mensagem de erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A mensagem é retornada por meio de **IErrorInfo:: GetDescription** método.|  
|*pwszServer*|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na qual o erro ocorreu.|  
|*pwszProcedure*|O nome do procedimento armazenado que gera o erro, se o erro ocorreu em um procedimento armazenado; caso contrário, uma cadeia de caracteres vazia.|  
|*lNative*|O número de erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O número do erro é idêntico àquele retornado na *plNativeError* parâmetro do **isqlerrorinfo:: Getsqlinfo** método.|  
|*bState*|O estado do erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*bClass*|A severidade do erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*wLineNumber*|Quando aplicável, a linha de um procedimento armazenado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que gerou a mensagem de erro. Se nenhum procedimento estiver envolvido, o valor padrão será 1.|  
  
 Os ponteiros na estrutura de fazer referência a endereços na cadeia de caracteres retornada na *ppErrorStrings* argumento.  
  
## <a name="see-also"></a>Consulte também  
 [ISQLServerErrorInfo &#40;OLE DB&#41;](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  

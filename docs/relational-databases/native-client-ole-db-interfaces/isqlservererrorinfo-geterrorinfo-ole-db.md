---
title: ISQLServerErrorInfo::GetErrorInfo (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISQLServerErrorInfo::GetErrorInfo (OLE DB)
apitype: COM
helpviewer_keywords:
- GetErrorInfo method
ms.assetid: 83265c9c-eaf9-41f0-9f73-b0ae0972f0d5
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e9ba54dd905127dc87cb3c14f74036c78daae1a1
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73789364"
---
# <a name="isqlservererrorinfogeterrorinfo-ole-db"></a>ISQLServerErrorInfo::GetErrorInfo (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Retorna um ponteiro para uma estrutura SSERRORINFO do provedor de OLE DB do cliente nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém os detalhes do erro [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O provedor do OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client define a interface de erro **ISQLServerErrorInfo** . Essa interface retorna detalhes de um erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , incluindo sua severidade e estado.  

  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT GetErrorInfo(  
   SSERRORINFO**ppSSErrorInfo,  
   OLECHAR**ppErrorStrings);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ppSSErrorInfo*[out]  
 Um ponteiro para uma estrutura SSERRORINFO. Se o método falhar ou se não houver informações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associadas ao erro, o provedor não alocará nenhuma memória e garantirá que o argumento *ppSSErrorInfo* seja um ponteiro nulo na saída.  
  
 *ppErrorStrings*[out]  
 Um ponteiro para um ponteiro de cadeia de caracteres Unicode. Se o método falhar ou se não houver informações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associadas a um erro, o provedor não alocará nenhuma memória e garantirá que o argumento *ppErrorStrings* seja um ponteiro nulo na saída. A liberação do argumento *ppErrorStrings* com o método **IMalloc::Free** libera os três membros de cadeia de caracteres individuais da estrutura SSERRORINFO retornada, pois a memória é alocada em um bloco.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 O método foi bem-sucedido.  
  
 E_INVALIDARG  
 O argumento *ppSSErrorInfo* ou *ppErrorStrings* era nulo.  
  
 E_OUTOFMEMORY  
 O provedor de OLE DB de cliente nativo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pôde alocar memória suficiente para concluir a solicitação.  
  
## <a name="remarks"></a>Remarks  
 O provedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB aloca memória para as cadeias de caracteres SSERRORINFO e OLECHAR retornadas por meio dos ponteiros passados pelo consumidor. O consumidor precisará desalocar essa memória usando o método **IMalloc::Free** quando não for mais necessário acessar os dados de erro.  
  
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
  
|Membro|Descrição|  
|------------|-----------------|  
|*pwszMessage*|A mensagem de erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A mensagem é retornada por meio do método **IErrorInfo::GetDescription**.|  
|*pwszServer*|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na qual o erro ocorreu.|  
|*pwszProcedure*|O nome do procedimento armazenado que gera o erro, se o erro ocorreu em um procedimento armazenado; caso contrário, uma cadeia de caracteres vazia.|  
|*lNative*|O número de erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O número do erro é idêntico àquele retornado no parâmetro *plNativeError* do método **ISQLErrorInfo::GetSQLInfo**.|  
|*bState*|O estado do erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*bClass*|A severidade do erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*wLineNumber*|Quando aplicável, a linha de um procedimento armazenado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que gerou a mensagem de erro. Se nenhum procedimento estiver envolvido, o valor padrão será 1.|  
  
 Os ponteiros nos endereços de referência da estrutura na cadeia de caracteres retornada no argumento *ppErrorStrings*.  
  
## <a name="see-also"></a>Consulte também  
 [ISQLServerErrorInfo &#40;OLE DB&#41;](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  

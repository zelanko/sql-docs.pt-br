---
title: ISQLServerErrorInfo::GetErrorInfo (OLE DB) | Microsoft Docs
description: ISQLServerErrorInfo::GetErrorInfo (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISQLServerErrorInfo::GetErrorInfo (OLE DB)
apitype: COM
helpviewer_keywords:
- GetErrorInfo method
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b20bd33afde1d05c74b58839c9662b9713139ef5
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2018
---
# <a name="isqlservererrorinfogeterrorinfo-ole-db"></a>ISQLServerErrorInfo::GetErrorInfo (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Retorna um ponteiro para um Driver OLE DB para SQL Server SSERRORINFO estrutura contendo o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] detalhes do erro.  
  
 O Driver OLE DB para SQL Server define o **ISQLServerErrorInfo** interface de erro. Essa interface retorna detalhes de um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] erro, incluindo sua severidade e estado.  

  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT GetErrorInfo(  
   SSERRORINFO**ppSSErrorInfo,  
   OLECHAR**ppErrorStrings);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ppSSErrorInfo*[out]  
 Um ponteiro para uma estrutura SSERRORINFO. Se o método falhar ou não há nenhum [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] informações associadas com o erro, o provedor não alocará nenhuma memória e garante que o *ppSSErrorInfo* argumento é um ponteiro nulo na saída.  
  
 *ppErrorStrings*[out]  
 Um ponteiro para um ponteiro de cadeia de caracteres Unicode. Se o método falhar ou não há nenhum [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] informações associadas a um erro, o provedor não alocará nenhuma memória e garante que o *ppErrorStrings* argumento é um ponteiro nulo na saída. Liberando o *ppErrorStrings* argumento com o **IMalloc:: Free** método libera os três membros de cadeia de caracteres individuais da estrutura SSERRORINFO retornada, como a memória é alocada em um bloco.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 O método foi bem-sucedido.  
  
 E_INVALIDARG  
 Ambos os *ppSSErrorInfo* ou *ppErrorStrings* argumento era nulo.  
  
 E_OUTOFMEMORY  
 O Driver OLE DB para SQL Server não pôde alocar memória suficiente para concluir a solicitação.  
  
## <a name="remarks"></a>Remarks  
 O Driver OLE DB para SQL Server aloca memória para as cadeias de caracteres SSERRORINFO e OLECHAR retornadas por meio dos ponteiros passados pelo consumidor. O consumidor deverá desalocar essa memória usando o **IMalloc:: Free** método quando ele não exige acesso aos dados de erro.  
  
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
|*pwszMessage*|A mensagem de erro do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A mensagem é retornada por meio de **IErrorInfo:: GetDescription** método.|  
|*pwszServer*|O nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na qual o erro ocorreu.|  
|*pwszProcedure*|O nome do procedimento armazenado que gera o erro, se o erro ocorreu em um procedimento armazenado; caso contrário, uma cadeia de caracteres vazia.|  
|*lNative*|O número de erro do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O número do erro é idêntico àquele retornado no *plNativeError* parâmetro o **isqlerrorinfo:: Getsqlinfo** método.|  
|*bState*|O estado do erro do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|*bClass*|A severidade do erro do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|*wLineNumber*|Quando aplicável, a linha de um procedimento armazenado do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que gerou a mensagem de erro. Se nenhum procedimento estiver envolvido, o valor padrão será 1.|  
  
 Referenciam de ponteiros na estrutura de endereços na cadeia de caracteres retornada no *ppErrorStrings* argumento.  
  
## <a name="see-also"></a>Consulte também  
 [ISQLServerErrorInfo &#40; OLE DB &#41;](http://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1)   
 [RAISERROR &#40; Transact-SQL &#41;](../../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  

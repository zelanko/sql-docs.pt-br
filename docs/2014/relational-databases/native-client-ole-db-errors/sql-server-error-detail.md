---
title: Detalhes de erros do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], error details
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error details
- ISQLServerErrorInfo interface
ms.assetid: 51500ee3-3d78-47ec-b90f-ebfc55642e06
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b937fda454ae08549917cdf3682ef20c76373a6
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37408985"
---
# <a name="sql-server-error-detail"></a>Detalhes de erros do SQL Server
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client define a interface de erro específico do provedor [ISQLServerErrorInfo](../../database-engine/dev-guide/isqlservererrorinfo-ole-db.md). A interface retorna mais detalhes sobre um erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e é valiosa em caso de falha na execução de comandos ou em operações do conjunto de linhas.  
  
 Há duas maneiras de obter acesso aos **ISQLServerErrorInfo** interface.  
  
 O consumidor pode chamar **ierrorrecords:: Getcustomererrorobject** para obter uma **ISQLServerErrorInfo** ponteiro, conforme mostrado no exemplo de código a seguir. (Não é necessário obter **ISQLErrorInfo.**) Ambos **ISQLErrorInfo** e **ISQLServerErrorInfo** são objetos de erro OLE DB personalizados, com **ISQLServerErrorInfo** sendo a interface a ser usada para obter informações de erros de servidor, incluindo detalhes como números de linha e de nome de procedimento.  
  
```  
// Get the SQL Server custom error object.  
if(FAILED(hr=pIErrorRecords->GetCustomErrorObject(  
   nRec, IID_ISQLServerErrorInfo,  
   (IUnknown**)&pISQLServerErrorErrorInfo)))  
```  
  
 Outra maneira de obter um **ISQLServerErrorInfo** ponteiro é chamar o **QueryInterface** método em uma já obtido **ISQLErrorInfo** ponteiro. Observe que, como **ISQLServerErrorInfo** contém um superconjunto das informações disponíveis de **ISQLErrorInfo**, faz sentido para ir diretamente para **ISQLServerErrorInfo**por meio **GetCustomerErrorObject**.  
  
 O **ISQLServerErrorInfo** interface expõe uma função de membro [isqlservererrorinfo:: Geterrorinfo](../native-client-ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md). A função retorna um ponteiro para uma estrutura SSERRORINFO e um ponteiro para um buffer de cadeia de caracteres. Ambos os ponteiros fazer referência a memória que o consumidor deverá desalocar usando o **IMalloc:: Free** método.  
  
 Os membros da estrutura SSERRORINFO são interpretados pelo consumidor como a seguir.  
  
|Membro|Description|  
|------------|-----------------|  
|*pwszMessage*|Mensagem de erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Idêntica à cadeia de caracteres retornada em **IErrorInfo:: GetDescription**.|  
|*pwszServer*|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a sessão.|  
|*pwszProcedure*|Se apropriado, o nome do procedimento no qual o erro foi originado. Uma cadeia de caracteres vazia caso contrário.|  
|*lNative*|O número do erro nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Idêntico ao valor retornado na *plNativeError* parâmetro do **isqlerrorinfo:: Getsqlinfo**.|  
|*bState*|O estado de uma mensagem de erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*bClass*|A severidade de uma mensagem de erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*wLineNumber*|Quando aplicável, o número da linha de um procedimento armazenado no qual o erro ocorreu.|  
  
## <a name="see-also"></a>Consulte também  
 [Erros](errors.md)   
 [RAISERROR &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/raiserror-transact-sql)  
  
  

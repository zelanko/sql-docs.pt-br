---
title: Detalhes do erro do SQL Server | Microsoft Docs
description: Detalhes de erros do SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, errors
- errors [OLE DB], error details
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error details
- ISQLServerErrorInfo interface
author: pmasl
ms.author: pelopes
ms.openlocfilehash: ddc9a1b1a242f9a92b1e854520d16abeb7baf809
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015653"
---
# <a name="sql-server-error-detail"></a>Detalhes de erros do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O Driver do OLE DB para SQL Server define a interface de erro específica do provedor [ISQLServerErrorInfo](https://msdn.microsoft.com/library/a8323b5c-686a-4235-a8d2-bda43617b3a1). A interface retorna mais detalhes sobre um erro do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e é valiosa em caso de falha na execução de comandos ou em operações do conjunto de linhas.  
  
 Há dois modos de obter acesso à interface **ISQLServerErrorInfo**.  
  
 O consumidor pode chamar **IErrorRecords::GetCustomerErrorObject** para obter um ponteiro **ISQLServerErrorInfo**, conforme mostrado no exemplo de código a seguir. (Não há necessidade de obter **ISQLErrorInfo**). **ISQLErrorInfo** e **ISQLServerErrorInfo** são objetos de erro personalizados do OLE DB, com **ISQLServerErrorInfo** sendo a interface a ser usada para obter informações de erros do servidor, incluindo detalhes como nome de procedimento e números de linha.  
  
```  
// Get the SQL Server custom error object.  
if(FAILED(hr=pIErrorRecords->GetCustomErrorObject(  
   nRec, IID_ISQLServerErrorInfo,  
   (IUnknown**)&pISQLServerErrorErrorInfo)))  
```  
  
 Outro modo de obter um ponteiro **ISQLServerErrorInfo** é chamar o método **QueryInterface** em um ponteiro **ISQLErrorInfo** já obtido. Observe que pelo fato de **ISQLServerErrorInfo** conter um superconjunto das informações disponíveis de **ISQLErrorInfo**, faz sentido passar diretamente para **ISQLServerErrorInfo** por meio de **GetCustomerErrorObject**.  
  
 A interface **ISQLServerErrorInfo** expõe uma função de membro, [ISQLServerErrorInfo::GetErrorInfo](../../oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md). A função retorna um ponteiro para uma estrutura SSERRORINFO e um ponteiro para um buffer de cadeia de caracteres. Ambos os ponteiros referenciam a memória que precisa ser desalocada pelo consumidor usando o método **IMalloc::Free**.  
  
 Os membros da estrutura SSERRORINFO são interpretados pelo consumidor como a seguir.  
  
|Membro|Descrição|  
|------------|-----------------|  
|*pwszMessage*|Mensagem de erro do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Idêntico à cadeia de caracteres retornada em **IErrorInfo::GetDescription**.|  
|*pwszServer*|O nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para a sessão.|  
|*pwszProcedure*|Se apropriado, o nome do procedimento no qual o erro foi originado. Uma cadeia de caracteres vazia caso contrário.|  
|*lNative*|O número do erro nativo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Idêntico ao valor retornado no parâmetro *plNativeError* de **ISQLErrorInfo::GetSQLInfo**.|  
|*bState*|O estado de uma mensagem de erro do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|*bClass*|A severidade de uma mensagem de erro do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|*wLineNumber*|Quando aplicável, o número da linha de um procedimento armazenado no qual o erro ocorreu.|  
  
## <a name="see-also"></a>Consulte Também  
 [Erros](../../oledb/ole-db-errors/errors.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  

---
description: Detalhes do erro de SQL Server Native Client
title: SQL Server detalhes do erro (provedor de OLE DB de cliente nativo)
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], error details
- IErrorRecords interface
- IErrorInfo interface
- OLE DB error handling, error details
- ISQLServerErrorInfo interface
ms.assetid: 51500ee3-3d78-47ec-b90f-ebfc55642e06
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 47c865556d78fabd84d7a3dea05231d0b60505f3
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91867174"
---
# <a name="sql-server-native-client-error-detail"></a>Detalhes do erro de SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo define a interface de erro específica do provedor [ISQLServerErrorInfo](../../connect/oledb/ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md?view=sql-server-ver15). A interface retorna mais detalhes sobre um erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e é valiosa em caso de falha na execução de comandos ou em operações do conjunto de linhas.  
  
 Há dois modos de obter acesso à interface **ISQLServerErrorInfo**.  
  
 O consumidor pode chamar **IErrorRecords::GetCustomerErrorObject** para obter um ponteiro **ISQLServerErrorInfo**, conforme mostrado no exemplo de código a seguir. (Não há necessidade de obter **ISQLErrorInfo**). **ISQLErrorInfo** e **ISQLServerErrorInfo** são objetos de erro personalizados do OLE DB, com **ISQLServerErrorInfo** sendo a interface a ser usada para obter informações de erros do servidor, incluindo detalhes como nome de procedimento e números de linha.  
  
```  
// Get the SQL Server custom error object.  
if(FAILED(hr=pIErrorRecords->GetCustomErrorObject(  
   nRec, IID_ISQLServerErrorInfo,  
   (IUnknown**)&pISQLServerErrorErrorInfo)))  
```  
  
 Outro modo de obter um ponteiro **ISQLServerErrorInfo** é chamar o método **QueryInterface** em um ponteiro **ISQLErrorInfo** já obtido. Observe que pelo fato de **ISQLServerErrorInfo** conter um superconjunto das informações disponíveis de **ISQLErrorInfo**, faz sentido passar diretamente para **ISQLServerErrorInfo** por meio de **GetCustomerErrorObject**.  
  
 A interface **ISQLServerErrorInfo** expõe uma função de membro, [ISQLServerErrorInfo::GetErrorInfo](../../relational-databases/native-client-ole-db-interfaces/isqlservererrorinfo-geterrorinfo-ole-db.md). A função retorna um ponteiro para uma estrutura SSERRORINFO e um ponteiro para um buffer de cadeia de caracteres. Ambos os ponteiros referenciam a memória que precisa ser desalocada pelo consumidor usando o método **IMalloc::Free**.  
  
 Os membros da estrutura SSERRORINFO são interpretados pelo consumidor como a seguir.  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|*pwszMessage*|Mensagem de erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Idêntico à cadeia de caracteres retornada em **IErrorInfo::GetDescription**.|  
|*pwszServer*|O nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a sessão.|  
|*pwszProcedure*|Se apropriado, o nome do procedimento no qual o erro foi originado. Uma cadeia de caracteres vazia caso contrário.|  
|*lNative*|O número do erro nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Idêntico ao valor retornado no parâmetro *plNativeError* de **ISQLErrorInfo::GetSQLInfo**.|  
|*bState*|O estado de uma mensagem de erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*bClass*|A severidade de uma mensagem de erro do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|*wLineNumber*|Quando aplicável, o número da linha de um procedimento armazenado no qual o erro ocorreu.|  
  
## <a name="see-also"></a>Consulte Também  
 [Erros](../../relational-databases/native-client-ole-db-errors/errors.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  

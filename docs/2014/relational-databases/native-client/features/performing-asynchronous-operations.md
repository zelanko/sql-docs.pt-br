---
title: Executando operações assíncronas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- initialization [SQL Server Native Client]
- database connections [SQL Server Native Client]
- data access [SQL Server Native Client], asynchronous operations
- connections [SQL Server Native Client]
- asynchronous operations [SQL Server Native Client]
- rowsets [SQL Server], initializing
- SQLNCLI, asynchronous operations
- SQL Server Native Client, asynchronous operations
ms.assetid: 8fbd84b4-69cb-4708-9f0f-bbdf69029bcc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 87d961e9613aa390b3001219f88808c8d4ac6ed7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63246144"
---
# <a name="performing-asynchronous-operations"></a>Executando operações assíncronas
  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite que os aplicativos executem operações de banco de dados assíncronas. O processamento assíncrono permite que os métodos retornem imediatamente sem serem bloqueados no thread de chamada. Isto permite muito do poder e flexibilidade de multithreading, sem exigir que o desenvolvedor crie threads explicitamente ou controle a sincronização. Os aplicativos solicitam processamento assíncrono ao inicializar uma conexão de banco de dados ou ao inicializar o resultado da execução de um comando.  
  
## <a name="opening-and-closing-a-database-connection"></a>Abrindo e fechando uma conexão de banco de dados  
 Ao usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client, os aplicativos projetados para inicializar um objeto de fonte de dados de forma assíncrona podem definir o bit DBPROPVAL_ASYNCH_INITIALIZE na propriedade DBPROP_INIT_ASYNCH antes de chamar  **IDBInitialize:: Initialize**. Quando essa propriedade estiver definida, o provedor será retornado imediatamente da chamada a **Initialize** com S_OK, caso a operação seja concluída imediatamente, ou com DB_S_ASYNCHRONOUS, caso a inicialização continue de forma assíncrona. Aplicativos podem consultar o **IDBAsynchStatus** ou [ISSAsynchStatus](../../native-client-ole-db-interfaces/issasynchstatus-ole-db.md)interface no objeto de fonte de dados e, em seguida, chame **idbasynchstatus:: getStatus** ou[ Issasynchstatus:: Waitforasynchcompletion](../../native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md) para obter o status da inicialização.  
  
 Além disso, a propriedade SSPROP_ISSAsynchStatus foi adicionada ao conjunto de propriedades DBPROPSET_SQLSERVERROWSET. Os provedores que dão suporte à interface **ISSAsynchStatus** precisam implementar essa propriedade com um valor de VARIANT_TRUE.  
  
 **IDBAsynchStatus::Abort** ou [ISSAsynchStatus::Abort](../../native-client-ole-db-interfaces/issasynchstatus-abort-ole-db.md) pode ser chamado para cancelar a chamada assíncrona a **Initialize**. O consumidor deve solicitar explicitamente a Inicialização Assíncrona da Fonte de Dados. Caso contrário, **IDBInitialize::Initialize** não será retornado enquanto o objeto de fonte de dados não for completamente inicializado.  
  
> [!NOTE]  
>  Objetos de fonte de dados usados para o pool de conexão não é possível chamar o **ISSAsynchStatus** interface no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client. A interface **ISSAsynchStatus** não é exposta para objetos da fonte de dados em pool.  
>   
>  Se um aplicativo forçar explicitamente o uso do mecanismo de cursor, **IOpenRowset::OpenRowset** e **IMultipleResults::GetResult** não darão suporte ao processamento assíncrono.  
>   
>  Além disso, a dll de proxy/stub de comunicação remota (no MDAC 2.8) não é possível chamar o **ISSAsynchStatus** interface no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. A interface **ISSAsynchStatus** não é exposta por comunicação remota.  
>   
>  Os Componentes de Serviço não dão suporte a **ISSAsynchStatus**.  
  
## <a name="execution-and-rowset-initialization"></a>Execução e inicialização de conjunto de linhas  
 Os aplicativos projetados para abrir assincronamente o resultado da execução de um comando podem definir o bit DBPROPVAL_ASYNCH_INITIALIZE na propriedade DBPROP_ROWSET_ASYNCH. Ao definir esse bit antes de chamar **IDBInitialize::Initialize**, **ICommand::Execute**, **IOpenRowset::OpenRowset** ou **IMultipleResults::GetResult**, o argumento *riid* precisa ser definido como IID_IDBAsynchStatus, IID_ISSAsynchStatus ou IID_IUnknown.  
  
 O método será retornado imediatamente com S_OK se a inicialização do conjunto de linhas for concluída imediatamente, ou com DB_S_ASYNCHRONOUS se o conjunto de linhas continuar sendo inicializado de forma assíncrona, com *ppRowset* definido como a interface solicitada no conjunto de linhas. Para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client, essa interface só pode ser **IDBAsynchStatus** ou **ISSAsynchStatus**. Até o conjunto de linhas ser completamente inicializado, essa interface se comportará como se estivesse em um estado suspenso, e a chamada a **QueryInterface** para interfaces diferentes de **IID_IDBAsynchStatus** ou **IID_ISSAsynchStatus** poderá retornar E_NOINTERFACE. A menos que o consumidor solicite processamento assíncrono explicitamente, o conjunto de linhas é inicializado sincronamente. Todas as interfaces solicitadas estão disponíveis quando **IDBAsynchStaus::GetStatus** ou **ISSAsynchStatus::WaitForAsynchCompletion** é retornado com a indicação de que a operação assíncrona foi concluída. Isto não significa necessariamente que todo o conjunto de linhas esteja preenchido, mas que está completo e totalmente funcional.  
  
 Se o comando executado não retornar um conjunto de linhas, ele ainda será retornado imediatamente com um objeto que dá suporte a **IDBAsynchStatus**.  
  
 Se você precisar obter vários resultados da execução de comando assíncrona, deverá:  
  
-   Definir o bit DBPROPVAL_ASYNCH_INITIALIZE da propriedade DBPROP_ROWSET_ASYNCH antes de executar o comando.  
  
-   Chamar **ICommand::Execute** e solicitar **IMultipleResults**.  
  
 Em seguida, as interfaces **IDBAsynchStatus** e **ISSAsynchStatus** podem ser obtidas consultando a interface de vários resultados usando **QueryInterface**.  
  
 Quando o comando tiver concluído a execução, **IMultipleResults** pode ser usada como normal, com uma exceção do caso síncrono: DB_S_ASYNCHRONOUS pode ser retornado, caso em que **IDBAsynchStatus** ou **ISSAsynchStatus** pode ser usado para determinar quando a operação é concluída.  
  
## <a name="examples"></a>Exemplos  
 No exemplo a seguir, o aplicativo chama um método sem-bloqueio, executa algum outro processamento e retorna para processar os resultados. **ISSAsynchStatus::WaitForAsynchCompletion** aguarda no objeto de evento interno até que a operação de execução assíncrona seja concluída ou que o tempo especificado por *dwMilisecTimeOut* tenha decorrido.  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
  
DBPROPSET CmdPropset[1];  
DBPROP CmdProperties[1];  
  
CmdPropset[0].rgProperties = CmdProperties;  
CmdPropset[0].cProperties = 1;  
CmdPropset[0].guidPropertySet = DBPROPSET_ROWSET;  
  
// Set asynch mode for command.  
CmdProperties[0].dwPropertyID = DBPROP_ROWSET_ASYNCH;  
CmdProperties[0].vValue.vt = VT_I4;  
CmdProperties[0].vValue.lVal = DBPROPVAL_ASYNCH_INITIALIZE;  
CmdProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
  
hr = pICommandProps->SetProperties(1, CmdPropset);  
  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work here...  
  
   hr = pISSAsynchStatus->WaitForAsynchCompletion(dwMilisecTimeOut);  
   if ( hr == S_OK)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
      pISSAsynchStatus->Release();  
   }  
}  
```  
  
 **ISSAsynchStatus::WaitForAsynchCompletion** aguarda no objeto de evento interno até que a operação de execução assíncrona seja concluída ou o valor de *dwMilisecTimeOut* seja passado.  
  
 O exemplo a seguir mostra processamento assíncrono com vários conjuntos de resultados:  
  
```  
DBPROP CmdProperties[1];  
  
// Set asynch mode for command.  
CmdProperties[0].dwPropertyID = DBPROP_ROWSET_ASYNCH;  
CmdProperties[0].vValue.vt = VT_I4;  
CmdProperties[0].vValue.lVal = DBPROPVAL_ASYNCH_INITIALIZE;  
  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_IMultipleResults,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pIMultipleResults);  
  
// Use GetResults for ISSAsynchStatus.  
hr = pIMultipleResults->GetResult(IID_ISSAsynchStatus, (void **) &pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work here...  
  
   hr = pISSAsynchStatus->WaitForAsynchCompletion(dwMilisecTimeOut);  
   if (hr == S_OK)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
      pISSAsynchStatus->Release();  
   }  
}  
```  
  
 Para impedir o bloqueio, o cliente pode verificar o status de uma operação assíncrona em execução, como no exemplo a seguir:  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);   
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   do{  
      // Do some work...  
      hr = pISSAsynchStatus->GetStatus(DB_NULL_HCHAPTER, DBASYNCHOP_OPEN, NULL, NULL, &ulAsynchPhase, NULL);  
   }while (DBASYNCHPHASE_COMPLETE != ulAsynchPhase)  
   if SUCCEEDED(hr)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
   }  
   pIDBAsynchStatus->Release();  
}  
```  
  
 O exemplo a seguir demonstra como você pode cancelar a operação assíncrona atualmente em execução:  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work...  
   hr = pISSAsynchStatus->Abort(DB_NULL_HCHAPTER, DBASYNCHOP_OPEN);  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do SQL Server Native Client](sql-server-native-client-features.md)   
 [Propriedades e comportamentos do conjunto de linhas](../../native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](../../native-client-ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  

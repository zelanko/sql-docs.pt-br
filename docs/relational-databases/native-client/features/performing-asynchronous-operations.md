---
title: "Executando operações assíncronas | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|features
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
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
caps.latest.revision: "45"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6fb5743b009b9f53575a012cf1348820278ca6b0
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="performing-asynchronous-operations"></a>Executando operações assíncronas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite que os aplicativos executem operações de banco de dados assíncronas. O processamento assíncrono permite que os métodos retornem imediatamente sem serem bloqueados no thread de chamada. Isto permite muito do poder e flexibilidade de multithreading, sem exigir que o desenvolvedor crie threads explicitamente ou controle a sincronização. Os aplicativos solicitam processamento assíncrono ao inicializar uma conexão de banco de dados ou ao inicializar o resultado da execução de um comando.  
  
## <a name="opening-and-closing-a-database-connection"></a>Abrindo e fechando uma conexão de banco de dados  
 Ao usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client, os aplicativos projetados para inicializar um objeto de fonte de dados de forma assíncrona podem definir o bit DBPROPVAL_ASYNCH_INITIALIZE na propriedade DBPROP_INIT_ASYNCH antes de chamar  **IDBInitialize:: Initialize**. Quando essa propriedade for definida, o provedor retorna imediatamente da chamada para **inicializar** com S_OK, se a operação foi concluída imediatamente, ou com DB_S_ASYNCHRONOUS, se a inicialização estiver continuando assincronamente. Aplicativos podem consultar o **IDBAsynchStatus** ou [ISSAsynchStatus](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)de interface no objeto de fonte de dados e, em seguida, chamar **idbasynchstatus:: getStatus** ou[ Issasynchstatus:: Waitforasynchcompletion](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md) para obter o status da inicialização.  
  
 Além disso, a propriedade SSPROP_ISSAsynchStatus foi adicionada ao conjunto de propriedades DBPROPSET_SQLSERVERROWSET. Provedores que dão suporte a **ISSAsynchStatus** interface deve implementar essa propriedade com um valor de VARIANT_TRUE.  
  
 **Idbasynchstatus:: Abort** ou [issasynchstatus:: Abort](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-abort-ole-db.md) pode ser chamado para cancelar o assíncrona **inicializar** chamar. O consumidor deve solicitar explicitamente a Inicialização Assíncrona da Fonte de Dados. Caso contrário, **IDBInitialize:: Initialize** não retorna até que o objeto de fonte de dados está completamente inicializado.  
  
> [!NOTE]  
>  Objetos de fonte de dados usados para o pool de conexão não é possível chamar o **ISSAsynchStatus** interface o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor OLE DB Native Client. O **ISSAsynchStatus** interface não é exposta para objetos de fonte de dados em pool.  
>   
>  Se um aplicativo forçar explicitamente o uso do mecanismo de cursor, **IOpenRowset:: OPENROWSET** e **imultipleresults:: GetResult** não dará suporte a processamento assíncrono.  
>   
>  Além disso, a dll de proxy/stub de comunicação remota (no MDAC 2.8) não é possível chamar o **ISSAsynchStatus** interface [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. O **ISSAsynchStatus** interface não é exposta por meio de comunicação remota.  
>   
>  Componentes de serviço não oferecem suporte a **ISSAsynchStatus**.  
  
## <a name="execution-and-rowset-initialization"></a>Execução e inicialização de conjunto de linhas  
 Os aplicativos projetados para abrir assincronamente o resultado da execução de um comando podem definir o bit DBPROPVAL_ASYNCH_INITIALIZE na propriedade DBPROP_ROWSET_ASYNCH. Ao definir esse bit antes de chamar **IDBInitialize:: Initialize**, **ICommand:: execute**, **IOpenRowset:: OPENROWSET** ou **IMultipleResults:: GetResult**, o *riid* argumento deve ser definido como IID_IDBAsynchStatus, IID_ISSAsynchStatus ou IID_IUnknown.  
  
 O método retornará imediatamente com S_OK se a inicialização de conjunto de linhas for concluída imediatamente, ou com DB_S_ASYNCHRONOUS se o conjunto de linhas continuar Inicializando assincronamente, com *ppRowset* definido como a interface solicitada do conjunto de linhas. Para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client, esta interface só pode ser **IDBAsynchStatus** ou **ISSAsynchStatus**. Até que o conjunto de linhas está totalmente inicializado, essa interface se comportará como se estivesse em um estado suspenso e chamar **QueryInterface** para interfaces diferentes de **IID_IDBAsynchStatus** ou **IID_ ISSAsynchStatus** poderá retornar E_NOINTERFACE. A menos que o consumidor solicite processamento assíncrono explicitamente, o conjunto de linhas é inicializado sincronamente. Todas as interfaces solicitadas estão disponíveis quando **idbasynchstaus:: getStatus** ou **issasynchstatus:: Waitforasynchcompletion** retorna com a indicação de que a operação assíncrona é concluída. Isto não significa necessariamente que todo o conjunto de linhas esteja preenchido, mas que está completo e totalmente funcional.  
  
 Se o comando executado não retornar um conjunto de linhas, ainda retornará imediatamente com um objeto que oferece suporte a **IDBAsynchStatus**.  
  
 Se você precisar obter vários resultados da execução de comando assíncrona, deverá:  
  
-   Definir o bit DBPROPVAL_ASYNCH_INITIALIZE da propriedade DBPROP_ROWSET_ASYNCH antes de executar o comando.  
  
-   Chamar **ICommand:: execute**e a solicitação **IMultipleResults**.  
  
 O **IDBAsynchStatus** e **ISSAsynchStatus** interfaces podem ser obtidas consultando várias interface resultados usando **QueryInterface**.  
  
 Quando o comando tiver concluído a execução, **IMultipleResults** pode ser usada como normal, com uma exceção do caso síncrono: DB_S_ASYNCHRONOUS pode ser retornado, caso em que **IDBAsynchStatus** ou **ISSAsynchStatus** pode ser usado para determinar quando a operação é concluída.  
  
## <a name="examples"></a>Exemplos  
 No exemplo a seguir, o aplicativo chama um método sem-bloqueio, executa algum outro processamento e retorna para processar os resultados. **Issasynchstatus:: Waitforasynchcompletion** espera no objeto de evento interno até que a operação de execução assíncrona seja concluída ou o período de tempo especificado por *dwMilisecTimeOut* é passado.  
  
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
  
 **Issasynchstatus:: Waitforasynchcompletion** espera no objeto de evento interno até que a operação de execução assíncrona seja concluída ou o *dwMilisecTimeOut* valor é passado.  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Propriedades e comportamentos do conjunto de linhas](../../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)   
 [ISSAsynchStatus &#40; OLE DB &#41;](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  

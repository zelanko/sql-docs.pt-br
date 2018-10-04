---
title: Exemplo (VC + +) de modelo de eventos ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- Visual C++ code examples [ADO], event model
ms.assetid: 29530153-b963-4a7c-8665-2335f1d604a8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3e9f40c4a5810ab712c4b6f67737fd308594de97
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47614444"
---
# <a name="ado-events-model-example-vc"></a>Exemplo do modelo de eventos ADO (VC++)
A seção do Visual C++ [instanciação de evento ADO por linguagem](../../../ado/guide/data/ado-event-instantiation-by-language.md) fornece uma descrição geral de como criar uma instância do modelo de evento ADO. A seguir está um exemplo específico de instanciar o modelo de evento dentro do ambiente criado pela **#import** diretiva.  
  
 Usa a descrição geral **adoint.h** como uma referência para assinaturas de método. No entanto, alguns detalhes na descrição geral ligeiramente alterado como resultado do uso de **#import** diretiva:  
  
-   O **#import** diretiva resolve **typedef**do, tipos de dados de assinatura de método e modificadores de suas formas fundamentais.  
  
-   Os métodos puros virtuais que devem ser substituídos são prefixados por "**RAW _**".  
  
 Parte do código simplesmente reflete o estilo de codificação.  
  
-   O ponteiro para **IUnknown** usado pelas **Advise** método é obtido explicitamente com uma chamada para **QueryInterface**.  
  
-   Você não precisa codificar explicitamente um destruidor nas definições de classe.  
  
-   Você talvez queira código mais robustas implementações de QueryInterface, AddRef e Release.  
  
-   O **__uuidof()** diretiva é usada extensivamente para obter as IDs de interface.  
  
 Por fim, o exemplo contém algum código de trabalho.  
  
-   O exemplo é escrito como um aplicativo de console.  
  
-   Você deve inserir seu próprio código sob o comentário "`// Do some work`".  
  
-   Todos os eventos manipuladores padrão sem fazer nada e cancelando a notificações. Você deve inserir o código apropriado para seu aplicativo e permitir as notificações se necessário.  
  
```  
// ADO_Events_Model_Example.cpp  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
// The Connection events  
class CConnEvent : public ConnectionEventsVt {  
private:  
   ULONG m_cRef;  
  
public:  
   CConnEvent() { m_cRef = 0; };  
   ~CConnEvent() {};  
  
   STDMETHODIMP QueryInterface(REFIID riid, void ** ppv);  
   STDMETHODIMP_(ULONG) AddRef();  
   STDMETHODIMP_(ULONG) Release();  
  
   STDMETHODIMP raw_InfoMessage( struct Error *pError,   
                                 EventStatusEnum *adStatus,   
                                 struct _Connection *pConnection);  
  
   STDMETHODIMP raw_BeginTransComplete( LONG TransactionLevel,  
                                        struct Error *pError,  
                                        EventStatusEnum *adStatus,  
                                        struct _Connection *pConnection);  
  
   STDMETHODIMP raw_CommitTransComplete( struct Error *pError,   
                                         EventStatusEnum *adStatus,  
                                         struct _Connection *pConnection);  
  
   STDMETHODIMP raw_RollbackTransComplete( struct Error *pError,   
                                           EventStatusEnum *adStatus,  
                                           struct _Connection *pConnection);  
  
   STDMETHODIMP raw_WillExecute( BSTR *Source,  
                                 CursorTypeEnum *CursorType,  
                                 LockTypeEnum *LockType,  
                                 long *Options,  
                                 EventStatusEnum *adStatus,  
                                 struct _Command *pCommand,  
                                 struct _Recordset *pRecordset,  
                                 struct _Connection *pConnection);  
  
   STDMETHODIMP raw_ExecuteComplete( LONG RecordsAffected,  
                                     struct Error *pError,  
                                     EventStatusEnum *adStatus,  
                                     struct _Command *pCommand,  
                                     struct _Recordset *pRecordset,  
                                     struct _Connection *pConnection);  
  
   STDMETHODIMP raw_WillConnect( BSTR *ConnectionString,  
                                 BSTR *UserID,  
                                 BSTR *Password,  
                                 long *Options,  
                                 EventStatusEnum *adStatus,  
                                 struct _Connection *pConnection);  
  
   STDMETHODIMP raw_ConnectComplete( struct Error *pError,  
                                     EventStatusEnum *adStatus,  
                                     struct _Connection *pConnection);  
  
   STDMETHODIMP raw_Disconnect( EventStatusEnum *adStatus, struct _Connection *pConnection);  
};  
  
// The Recordset events  
class CRstEvent : public RecordsetEventsVt {  
private:  
   ULONG m_cRef;     
  
public:  
   CRstEvent() { m_cRef = 0; };  
   ~CRstEvent() {};  
  
   STDMETHODIMP QueryInterface(REFIID riid, void ** ppv);  
   STDMETHODIMP_(ULONG) AddRef();  
   STDMETHODIMP_(ULONG) Release();  
  
   STDMETHODIMP raw_WillChangeField( LONG cFields,        
                                     VARIANT Fields,  
                                     EventStatusEnum *adStatus,  
                                     struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_FieldChangeComplete( LONG cFields,  
                                         VARIANT Fields,  
                                         struct Error *pError,  
                                         EventStatusEnum *adStatus,  
                                         struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_WillChangeRecord( EventReasonEnum adReason,  
                                      LONG cRecords,  
                                      EventStatusEnum *adStatus,  
                                      struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_RecordChangeComplete( EventReasonEnum adReason,  
                                          LONG cRecords,  
                                          struct Error *pError,  
                                          EventStatusEnum *adStatus,  
                                          struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_WillChangeRecordset( EventReasonEnum adReason,  
                                         EventStatusEnum *adStatus,  
                                         struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_RecordsetChangeComplete( EventReasonEnum adReason,  
                                             struct Error *pError,  
                                             EventStatusEnum *adStatus,  
                                             struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_WillMove( EventReasonEnum adReason,  
                              EventStatusEnum *adStatus,  
                              struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_MoveComplete( EventReasonEnum adReason,  
                                  struct Error *pError,  
                                  EventStatusEnum *adStatus,  
                                  struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_EndOfRecordset( VARIANT_BOOL *fMoreData,  
                                    EventStatusEnum *adStatus,  
                                    struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_FetchProgress( long Progress,  
                                   long MaxProgress,  
                                   EventStatusEnum *adStatus,  
                                   struct _Recordset *pRecordset);  
  
   STDMETHODIMP raw_FetchComplete( struct Error *pError,   
                                   EventStatusEnum *adStatus,  
                                   struct _Recordset *pRecordset);  
};  
  
// Implement each connection method  
STDMETHODIMP CConnEvent::raw_InfoMessage( struct Error *pError,   
                                         EventStatusEnum *adStatus,  
                                         struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_BeginTransComplete( LONG TransactionLevel,  
                                                 struct Error *pError,  
                                                 EventStatusEnum *adStatus,  
                                                 struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_CommitTransComplete( struct Error *pError,  
                                                  EventStatusEnum *adStatus,  
                                                  struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_RollbackTransComplete( struct Error *pError,  
                                                    EventStatusEnum *adStatus,  
                                                    struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_WillExecute( BSTR *Source,  
                                          CursorTypeEnum *CursorType,  
                                          LockTypeEnum *LockType,  
                                          long *Options,  
                                          EventStatusEnum *adStatus,  
                                          struct _Command *pCommand,  
                                          struct _Recordset *pRecordset,  
                                          struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_ExecuteComplete( LONG RecordsAffected,  
                                              struct Error *pError,  
                                              EventStatusEnum *adStatus,  
                                              struct _Command *pCommand,  
                                              struct _Recordset *pRecordset,  
                                              struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_WillConnect( BSTR *ConnectionString,  
                                          BSTR *UserID,  
                                          BSTR *Password,  
                                          long *Options,  
                                          EventStatusEnum *adStatus,  
                                          struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_ConnectComplete( struct Error *pError,  
                                              EventStatusEnum *adStatus,  
                                              struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CConnEvent::raw_Disconnect( EventStatusEnum *adStatus, struct _Connection *pConnection) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
// Implement each recordset method  
STDMETHODIMP CRstEvent::raw_WillChangeField( LONG cFields,  
                                             VARIANT Fields,  
                                             EventStatusEnum *adStatus,  
                                             struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_FieldChangeComplete( LONG cFields,  
                                                 VARIANT Fields,  
                                                 struct Error *pError,  
                                                 EventStatusEnum *adStatus,  
                                                 struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_WillChangeRecord( EventReasonEnum adReason,  
                                              LONG cRecords,  
                                              EventStatusEnum *adStatus,  
                                              struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_RecordChangeComplete( EventReasonEnum adReason,  
                                                  LONG cRecords,  
                                                  struct Error *pError,  
                                                  EventStatusEnum *adStatus,  
                                                  struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_WillChangeRecordset( EventReasonEnum adReason,  
                                                 EventStatusEnum *adStatus,  
                                                 struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_RecordsetChangeComplete( EventReasonEnum adReason,  
                                                     struct Error *pError,  
                                                     EventStatusEnum *adStatus,  
                                                     struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_WillMove( EventReasonEnum adReason,   
                                      EventStatusEnum *adStatus,  
                                      struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_MoveComplete( EventReasonEnum adReason,  
                                          struct Error *pError,  
                                          EventStatusEnum *adStatus,  
                                          struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_EndOfRecordset( VARIANT_BOOL *fMoreData,  
                                            EventStatusEnum *adStatus,  
                                            struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_FetchProgress( long Progress,  
                                           long MaxProgress,  
                                           EventStatusEnum *adStatus,  
                                           struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::raw_FetchComplete( struct Error *pError,  
                                           EventStatusEnum *adStatus,  
                                           struct _Recordset *pRecordset) {  
   *adStatus = adStatusUnwantedEvent;  
   return S_OK;  
};  
  
STDMETHODIMP CRstEvent::QueryInterface(REFIID riid, void ** ppv) {  
   *ppv = NULL;  
   if (riid == __uuidof(IUnknown) || riid == __uuidof(RecordsetEventsVt))   
      *ppv = this;  
  
   if (*ppv == NULL)  
      return ResultFromScode(E_NOINTERFACE);  
  
   AddRef();  
   return NOERROR;  
}  
  
STDMETHODIMP_(ULONG) CRstEvent::AddRef() {   
   return ++m_cRef;   
};  
  
STDMETHODIMP_(ULONG) CRstEvent::Release() {   
   if (0 != --m_cRef)   
      return m_cRef;  
   delete this;  
   return 0;  
}  
  
STDMETHODIMP CConnEvent::QueryInterface(REFIID riid, void ** ppv) {  
   *ppv = NULL;  
   if (riid == __uuidof(IUnknown) || riid == __uuidof(ConnectionEventsVt))   
      *ppv = this;  
  
   if (*ppv == NULL)  
      return ResultFromScode(E_NOINTERFACE);  
  
   AddRef();  
   return NOERROR;  
}  
  
STDMETHODIMP_(ULONG) CConnEvent::AddRef() {   
   return ++m_cRef;   
};  
  
STDMETHODIMP_(ULONG) CConnEvent::Release() {   
   if (0 != --m_cRef)   
      return m_cRef;  
   delete this;  
   return 0;  
}  
  
int main() {  
   HRESULT hr;  
   DWORD dwConnEvt;  
   DWORD dwRstEvt;  
   IConnectionPointContainer *pCPC = NULL;  
   IConnectionPoint *pCP = NULL;  
   IUnknown *pUnk = NULL;  
   CRstEvent *pRstEvent = NULL;  
   CConnEvent *pConnEvent= NULL;  
   int rc = 0;  
   _RecordsetPtr pRst;   
   _ConnectionPtr pConn;  
  
   ::CoInitialize(NULL);  
  
   hr = pConn.CreateInstance(__uuidof(Connection));  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pRst.CreateInstance(__uuidof(Recordset));  
  
   if (FAILED(hr))   
      return rc;  
  
   // Start using the Connection events  
   hr = pConn->QueryInterface(__uuidof(IConnectionPointContainer), (void **)&pCPC);  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCPC->FindConnectionPoint(__uuidof(ConnectionEvents), &pCP);  
   pCPC->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   pConnEvent = new CConnEvent();  
   hr = pConnEvent->QueryInterface(__uuidof(IUnknown), (void **) &pUnk);  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCP->Advise(pUnk, &dwConnEvt);  
   pCP->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   // Start using the Recordset events  
   hr = pRst->QueryInterface(__uuidof(IConnectionPointContainer), (void **)&pCPC);  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCPC->FindConnectionPoint(__uuidof(RecordsetEvents), &pCP);  
   pCPC->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   pRstEvent = new CRstEvent();  
   hr = pRstEvent->QueryInterface(__uuidof(IUnknown), (void **) &pUnk);  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCP->Advise(pUnk, &dwRstEvt);  
   pCP->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   // Do some work  
   pConn->Open("dsn=DataPubs;", "", "", adConnectUnspecified);  
   pRst->Open("SELECT * FROM authors", (IDispatch *) pConn, adOpenStatic, adLockReadOnly, adCmdText);  
  
   pRst->MoveFirst();  
   while (pRst->EndOfFile == FALSE) {  
      wprintf(L"Name = '%s'\n", (wchar_t*) ((_bstr_t) pRst->Fields->GetItem("au_lname")->Value));  
      pRst->MoveNext();  
   }  
  
   pRst->Close();  
   pConn->Close();  
  
   // Stop using the Connection events  
   hr = pConn->QueryInterface(__uuidof(IConnectionPointContainer), (void **) &pCPC);  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCPC->FindConnectionPoint(__uuidof(ConnectionEvents), &pCP);  
   pCPC->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCP->Unadvise( dwConnEvt );  
   pCP->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   // Stop using the Recordset events  
   hr = pRst->QueryInterface(__uuidof(IConnectionPointContainer), (void **) &pCPC);  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCPC->FindConnectionPoint(__uuidof(RecordsetEvents), &pCP);  
   pCPC->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   hr = pCP->Unadvise( dwRstEvt );  
   pCP->Release();  
  
   if (FAILED(hr))   
      return rc;  
  
   CoUninitialize();  
}  
```

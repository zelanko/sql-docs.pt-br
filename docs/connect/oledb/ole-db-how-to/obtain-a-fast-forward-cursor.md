---
title: Obter um Cursor FAST_FORWARD | Microsoft Docs
description: Obter um cursor FAST_FORWARD usando o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-how-to
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fast forward-only cursors
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8eef788de7efd7c17b3e8f6c31235f9e82f6458f
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="obtain-a-fastforward-cursor"></a>Obter um cursor FAST_FORWARD
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para obter um cursor somente encaminhamento, somente leitura, defina as propriedades do conjunto de linhas DBPROP_SERVERCURSOR, DBPROP_OTHERINSERT, DBPROP_OTHERUPDATEDELETE, DBPROP_OWNINSERT e DBPROP_OWNUPDATEDELETE como VARIANT_TRUE.  
  
 Um exemplo completo mostra como definir as propriedades de conjunto de linhas para obter um cursor FAST_FORWARD. Após configurar as propriedades, uma instrução SELECT é executada para recuperar e exibir a coluna **Name** da tabela **Purchasing.Vendor** no banco de dados **AdventureWorks** .  
  
> [!IMPORTANT]  
>  Quando possível, use a Autenticação do Windows. Se a Autenticação do Windows não estiver disponível, solicite aos usuários que digitem suas credenciais em tempo de execução. Evite armazenar as credenciais em um arquivo. Se for necessário manter as credenciais, criptografe-as com a [Win32 crypto API](http://go.microsoft.com/fwlink/?LinkId=64532)(em inglês).  
  
### <a name="to-obtain-fastforward-cursor"></a>Para obter o cursor FAST_FORWARD  
  
1.  Estabeleça uma conexão com a fonte de dados.  
  
2.  Defina as propriedades do conjunto de linhas DBPROP_SERVERCURSOR, DBPROP_OTHERINSERT, DBPROP_OTHERUPDATEDELETE, DBPROP_OWNINSERT e DBPROP_OWNUPDATEDELETE como VARIANT_TRUE.  
  
3.  Execute o comando.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como definir as propriedades de conjunto de linhas para obter um cursor de FAST_FORWARD. Após configurar as propriedades, uma instrução SELECT é executada para recuperar e exibir a coluna Name da tabela Purchasing.Vendor no banco de dados AdventureWorks. Este exemplo não tem suporte em IA64.  
  
 Este exemplo exige o banco de dados de exemplo AdventureWorks, que pode ser baixado na home page de [Microsoft SQL Server Samples and Community Projects](http://go.microsoft.com/fwlink/?LinkID=85384) (em inglês).  
  
 Compile com ole32.lib oleaut32.lib e execute a seguinte listagem de código C++. Esse aplicativo se conecta à instância padrão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] do computador. Em alguns sistemas operacionais Windows, será necessário alterar (localhost) ou (local) para o nome de sua instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para se conectar a uma instância nomeada, altere a cadeia de caracteres de conexão de L"(local)" para L"(local)\\\name", onde nome é a instância nomeada. Por padrão, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Express é instalado em uma instância nomeada. Verifique se que a variável de ambiente INCLUDE inclui o diretório que contém msoledbsql.h.  
  
```  
// compile with: ole32.lib oleaut32.lib  
#define INITGUID  
#define DBINITCONSTANTS  
#define OLEDBVER 0x0250   // to include correct interfaces  
  
#include <windows.h>  
#include <stdio.h>  
#include <oledb.h>  
#include <msoledbsql.h>  
#include <oledberr.h>  
  
IDBInitialize* pIDBInitialize = NULL;  
ICommandText* pICommandText = NULL;  
  
// Connect to the server and create a command object.  
int InitializeAndConnect();  
  
// Set the properties to get a FAST_FORWARD cursor.  
int SetRowsetProperties();  
  
// This function executes a command and displays the results.  
int ExecuteAndDisplay();  
  
// Release memory.  
void Cleanup();  
  
int main() {  
   if (InitializeAndConnect() == -1) {  
      // Handle error.  
      printf("Failed to initialize and connect to the server.\n");  
      return -1;  
   }  
  
   // Set the row properties to FAST_FORWARD cursor.  
   if (SetRowsetProperties() == -1) {  
      // Handle error.  
      printf("Failed to set the rowset properties.\n");  
      return -1;  
   }  
  
   // Execute a command and display the results.  
   if (ExecuteAndDisplay() == -1) {  
      // Handle error.  
      printf("Failed to execute a command and display the results.\n");  
      return -1;  
   }  
  
   Cleanup();  
}  
  
int InitializeAndConnect() {  
   HRESULT hr = S_OK;  
  
   IDBProperties* pIDBProperties = NULL;  
   IDBCreateSession* pIDBCreateSession = NULL;  
   IDBCreateCommand* pIDBCreateCommand = NULL;  
  
   DBPROPSET dbPropSet;  
   DBPROP dbProp[4];  
   int iRetVal = 0;  
  
   // Initialize OLE  
   if ( FAILED( hr = OleInitialize( NULL ) ) ) {  
      // Handle errors here.  
      return -1;  
   }  
  
   // Create an instance of Microsoft OLE DB Driver for SQL Server.  
   if ( FAILED( hr =   
      CoCreateInstance(CLSID_MSOLEDBSQL, NULL, CLSCTX_INPROC_SERVER, IID_IDBProperties, (void **) &pIDBProperties ))) {  
      // Handle errors here.  
      return -1;  
   }  
  
   // Set up the connection properties.  
   dbProp[0].dwPropertyID = DBPROP_INIT_DATASOURCE;  
   dbProp[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
   dbProp[0].colid = DB_NULLID;  
   V_VT(&(dbProp[0].vValue)) = VT_BSTR;  
  
   V_BSTR(&(dbProp[0].vValue)) = SysAllocString( L"(local)" );  
  
   dbProp[1].dwPropertyID = DBPROP_AUTH_INTEGRATED;  
   dbProp[1].dwOptions = DBPROPOPTIONS_REQUIRED;  
   dbProp[1].colid = DB_NULLID;  
   V_VT(&(dbProp[1].vValue)) = VT_BSTR;  
   V_BSTR(&(dbProp[1].vValue)) = SysAllocString( L"SSPI" );  
  
   dbProp[2].dwPropertyID = DBPROP_NULLCOLLATION;  
   dbProp[2].dwOptions = DBPROPOPTIONS_REQUIRED;  
   dbProp[2].colid = DB_NULLID;  
   V_VT(&(dbProp[2].vValue)) = VT_BSTR;  
   V_BSTR(&(dbProp[2].vValue)) = SysAllocString( L"" );  
  
   dbProp[3].dwPropertyID = DBPROP_INIT_CATALOG;  
   dbProp[3].dwOptions = DBPROPOPTIONS_REQUIRED;  
   dbProp[3].colid = DB_NULLID;  
   V_VT(&(dbProp[3].vValue)) = VT_BSTR;  
   V_BSTR(&(dbProp[3].vValue)) = SysAllocString( L"AdventureWorks" );  
  
   dbPropSet.rgProperties = dbProp;  
   dbPropSet.cProperties = 4;  
   dbPropSet.guidPropertySet = DBPROPSET_DBINIT;  
  
   if ( FAILED( hr = pIDBProperties->SetProperties( 1, &dbPropSet ))) {  
      // Handle errors here.  
      iRetVal = -1;  
      goto CLEANUP;  
   }  
  
   SysFreeString( V_BSTR(&(dbProp[0].vValue)) );  
   SysFreeString( V_BSTR(&(dbProp[1].vValue)) );  
   SysFreeString( V_BSTR(&(dbProp[2].vValue)) );  
   SysFreeString( V_BSTR(&(dbProp[3].vValue)) );  
  
   // Get an IDBInitialize interface.  
   if ( FAILED( hr =   
      pIDBProperties->QueryInterface( IID_IDBInitialize, (void **) &pIDBInitialize ))) {  
      // Handle errors here.  
      iRetVal = -1;  
      goto CLEANUP;  
   }  
  
   // Call Initialize.  
   if ( FAILED( hr = pIDBInitialize->Initialize())) {  
      // Handle errors here.  
      iRetVal = -1;  
      goto CLEANUP;  
   }  
  
   // Get a IDBCreateSession interface.  
   if ( FAILED( hr =   
      pIDBInitialize->QueryInterface( IID_IDBCreateSession, (void **) &pIDBCreateSession ))) {  
      // Handle errors here.  
      iRetVal = -1;  
      goto CLEANUP;  
   }  
  
   // Create a session  
   if ( FAILED( hr =   
      pIDBCreateSession->CreateSession( NULL, IID_IDBCreateCommand, (IUnknown **) &pIDBCreateCommand))) {  
      // Handle errors here.  
      iRetVal = -1;  
      goto CLEANUP;  
   }  
  
   // Create a command.  
   if ( FAILED( hr =   
      pIDBCreateCommand->CreateCommand( NULL, IID_ICommandText, (IUnknown **) &pICommandText))) {  
      // Handle errors here.  
      iRetVal = -1;  
      goto CLEANUP;  
   }  
  
CLEANUP:  
   // Release all the objects not needed anymore.  
   pIDBProperties->Release();  
   if ( pIDBCreateSession )  
      pIDBCreateSession->Release();  
   if ( pIDBCreateCommand )  
      pIDBCreateCommand->Release();  
  
   return iRetVal;  
}  
  
int SetRowsetProperties() {  
   HRESULT hr = S_OK;  
   ICommandProperties* pICommandProperties = NULL;  
   DBPROPSET dbPropSet;  
   DBPROP dbProp[5];  
   int iRetVal = 0;  
  
   // Get an ICommandProperties object.  
   if ( FAILED( hr =   
      pICommandText->QueryInterface( IID_ICommandProperties, (void **) &pICommandProperties ))) {  
      // Handle errors here.  
      return -1;  
   }  
  
   // Set up the properties to get a FAST_FORWARD cursor.  
   dbProp[0].dwPropertyID       = DBPROP_SERVERCURSOR;  
   dbProp[0].dwOptions          = DBPROPOPTIONS_REQUIRED;  
   dbProp[0].colid              = DB_NULLID;  
   V_VT(&(dbProp[0].vValue))    = VT_BOOL;  
   V_BOOL(&(dbProp[0].vValue))  = VARIANT_TRUE;  
  
   dbProp[1].dwPropertyID       = DBPROP_OTHERINSERT;  
   dbProp[1].dwOptions          = DBPROPOPTIONS_REQUIRED;  
   dbProp[1].colid              = DB_NULLID;  
   V_VT(&(dbProp[1].vValue))    = VT_BOOL;  
   V_BOOL(&(dbProp[1].vValue))  = VARIANT_TRUE;  
  
   dbProp[2].dwPropertyID       = DBPROP_OTHERUPDATEDELETE;  
   dbProp[2].dwOptions          = DBPROPOPTIONS_REQUIRED;  
   dbProp[2].colid              = DB_NULLID;  
   V_VT(&(dbProp[2].vValue))    = VT_BOOL;  
   V_BOOL(&(dbProp[2].vValue))  = VARIANT_TRUE;  
  
   dbProp[3].dwPropertyID       = DBPROP_OWNINSERT;  
   dbProp[3].dwOptions          = DBPROPOPTIONS_REQUIRED;  
   dbProp[3].colid              = DB_NULLID;  
   V_VT(&(dbProp[3].vValue))    = VT_BOOL;  
   V_BOOL(&(dbProp[3].vValue))  = VARIANT_TRUE;  
  
   dbProp[4].dwPropertyID       = DBPROP_OWNUPDATEDELETE;  
   dbProp[4].dwOptions          = DBPROPOPTIONS_REQUIRED;  
   dbProp[4].colid              = DB_NULLID;  
   V_VT(&(dbProp[4].vValue))    = VT_BOOL;  
   V_BOOL(&(dbProp[4].vValue))  = VARIANT_TRUE;  
  
   dbPropSet.rgProperties       = dbProp;  
   dbPropSet.cProperties        = 5;  
   dbPropSet.guidPropertySet    = DBPROPSET_ROWSET;  
  
   if ( FAILED( hr = pICommandProperties->SetProperties( 1, &dbPropSet))) {  
      // Handle errors here.  
      iRetVal = -1;  
   }  
  
   // Release the ICommandProperties object.  
   pICommandProperties->Release();  
  
   return iRetVal;  
}  
  
int ExecuteAndDisplay() {  
   HRESULT hr = S_OK;  
   IRowset* pIRowset = NULL;  
   IAccessor* pIAccessor = NULL;  
  
   BYTE* pData = NULL;  
   DBCOUNTITEM cRowsObtained = 0;  
   ULONG cCount = 0;  
  
   HROW* pRows = new HROW[10];  
   HACCESSOR hAccessor = 0;  
   DBBINDING Bind[1];  
   int iRetVal = 0;  
  
   if (!pRows)  
      return -1;  
  
   // Set the command text.  
   if ( FAILED( hr = pICommandText->SetCommandText( DBGUID_SQL, L"select Name from Purchasing.Vendor")))  
      // Handle errors and free the memory here.  
      return -1;  
  
   // Execute the command.  
   if ( FAILED( hr = pICommandText->Execute( NULL, IID_IRowset, NULL, NULL, (IUnknown **) &pIRowset )))  
      // Handle errors and free the memory here.  
      return -1;  
  
    // Set up the binding structure for Name (nvarchar(50)).  
    Bind[0].dwPart      = DBPART_VALUE;  
    Bind[0].eParamIO    = DBPARAMIO_NOTPARAM;  
    Bind[0].iOrdinal    = 1;  
    Bind[0].pTypeInfo   = NULL;  
    Bind[0].pObject     = NULL;  
    Bind[0].pBindExt    = NULL;  
    Bind[0].dwFlags     = 0;  
    Bind[0].dwMemOwner  = DBMEMOWNER_CLIENTOWNED;  
    Bind[0].obLength    = 0;  
    Bind[0].obStatus    = 0;  
    Bind[0].obValue     = 0;  
    Bind[0].cbMaxLen    = 102;  
    Bind[0].wType       = DBTYPE_WSTR;  
    Bind[0].bPrecision  = 0;  
    Bind[0].bScale      = 0;  
  
   // Get an IAccessor interface.  
   if ( FAILED( hr = pIRowset->QueryInterface( IID_IAccessor, (void **) &pIAccessor))) {  
      // Handle errors and free the memory here.  
      iRetVal = -1;  
      goto CLEANUP;  
   }  
  
   // Create an accessor.  
   if ( FAILED( hr =   
      pIAccessor->CreateAccessor(  DBACCESSOR_ROWDATA, 1, Bind, 0, &hAccessor, NULL))) {  
      // Handle errors and free the memory here.  
      iRetVal = -1;  
      goto CLEANUP;  
   }  
  
   // Allocate memory for the data.  
   pData = new BYTE[102];  
   if (!(pData /* = new BYTE[102] */ )) {  
      // Handle errors and free the memory here.  
      iRetVal = -1;  
      goto CLEANUP;  
   }  
  
   // Loop through all of the rows.  
   for ( ; ; ) {  
      if (FAILED( hr = pIRowset->GetNextRows( NULL, 0, 10, &cRowsObtained, &pRows))) {  
         // Handle errors and free the memory here.  
         iRetVal = -1;  
         goto CLEANUP;  
      }  
  
      // Make sure some rows were obtained.  
      if (cRowsObtained == 0)  
         break;  
  
      // Get the data for the each of the rows.  
      for ( cCount = 0 ; cCount < cRowsObtained ; cCount++ ) {  
         // Get the row data needed.  
         if ( FAILED( hr = pIRowset->GetData( pRows[cCount], hAccessor, pData ))) {  
            // Handle errors and free the memory here.  
            iRetVal = -1;  
            goto CLEANUP;  
         }  
  
         // Display row data.  
         printf( "%S\n", pData);  
      }  
  
      // Release the rows.  
      if ( FAILED( hr = pIRowset->ReleaseRows(cRowsObtained, pRows, NULL, NULL, NULL ))) {  
         // Handle errors and free the memory here.  
         iRetVal = -1;  
         goto CLEANUP;  
      }  
   }  
  
CLEANUP:  
   // Release memory allocated for the data.  
   delete [] pRows;  
   delete [] pData;  
  
   // Release the HACCESSOR.  
   if (pIAccessor) {  
      pIAccessor->ReleaseAccessor( hAccessor, NULL );  
  
      // Release the IAccessor object.  
      pIAccessor->Release();  
   }  
  
   // Release the rowset.  
   pIRowset->Release();  
  
   return iRetVal;  
}  
  
void Cleanup() {  
   HRESULT hr = S_OK;  
  
   // Release the ICommandText object.  
   pICommandText->Release();  
  
   // Uninitialize the IDBInitialize object.  
   if ( FAILED( hr = pIDBInitialize->Uninitialize())) {  
      // Handle errors here.  
   }  
  
   // Release the IDBInitialize object.  
   pIDBInitialize->Release();  
  
   // Uninitialize OLE.  
   OleUninitialize();  
}  
```  
  
  

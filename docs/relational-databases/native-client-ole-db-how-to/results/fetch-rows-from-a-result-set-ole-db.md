---
title: Buscar linhas em um conjunto de resultados (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- rows [OLE DB]
ms.assetid: 8e9916a5-61e1-468e-8a5c-1ab8b5110737
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f3798d8c92100507fe7741381808bc924d3a5656
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37417845"
---
# <a name="fetch-rows-from-a-result-set-ole-db"></a>Buscar linhas em um conjunto de resultados (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Este exemplo mostra como buscar linhas em um conjunto de resultados. Este exemplo não tem suporte em IA64.  
  
 Este exemplo exige o banco de dados de exemplo AdventureWorks, que pode ser baixado na home page de [Microsoft SQL Server Samples and Community Projects](http://go.microsoft.com/fwlink/?LinkID=85384) (em inglês).  
  
> [!IMPORTANT]  
>  Quando possível, use a Autenticação do Windows. Se a Autenticação do Windows não estiver disponível, solicite aos usuários que digitem suas credenciais em tempo de execução. Evite armazenar as credenciais em um arquivo. Se for necessário manter as credenciais, criptografe-as com a [Win32 crypto API](http://go.microsoft.com/fwlink/?LinkId=64532)(em inglês).  
  
## <a name="example"></a>Exemplo  
  
### <a name="description"></a>Description  
 Compile com ole32.lib oleaut32.lib e execute a seguinte listagem de código C++. Esse aplicativo se conecta ao padrão do seu computador [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instância. Em alguns sistemas operacionais Windows, será necessário alterar (localhost) ou (local) para o nome de sua instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para se conectar a uma instância nomeada, altere a cadeia de caracteres de conexão de L"(local)" para L"(local)\\\name", onde o nome é a instância nomeada. Por padrão, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Express é instalado em uma instância nomeada. Verifique se a variável de ambiente INCLUDE inclui o diretório que contém sqlncli.h.  
  
### <a name="code"></a>Código  
  
```  
// compile with: ole32.lib oleaut32.lib  
int InitializeAndEstablishConnection();  
int ProcessResultSet();  
  
#define UNICODE  
#define _UNICODE  
#define DBINITCONSTANTS  
#define INITGUID  
#define OLEDBVER 0x0250   // to include correct interfaces  
  
#include <stdio.h>  
#include <tchar.h>  
#include <stddef.h>  
#include <windows.h>  
#include <iostream>  
#include <oledb.h>  
#include <sqlncli.h>  
#include <msdadc.h>   // for IDataConvert  
#include <msdaguid.h>   // for IDataConvert  
  
using namespace std;  
  
IDBInitialize* pIDBInitialize = NULL;  
IDBProperties* pIDBProperties = NULL;  
IDBCreateSession* pIDBCreateSession = NULL;  
IDBCreateCommand* pIDBCreateCommand = NULL;  
ICommandText* pICommandText = NULL;  
IRowset* pIRowset = NULL;  
IColumnsInfo* pIColumnsInfo = NULL;  
  
DBCOLUMNINFO* pDBColumnInfo = NULL;  
IAccessor* pIAccessor =  NULL;  
DBPROP InitProperties[4];  
DBPROPSET rgInitPropSet[1];  
  
ULONG i, j;  
HRESULT hr;  
DBROWCOUNT cNumRows = 0;  
DBORDINAL lNumCols;  
WCHAR* pStringsBuffer;  
DBBINDING* pBindings;  
DBLENGTH ConsumerBufColOffset = 0;  
HACCESSOR hAccessor;  
DBCOUNTITEM lNumRowsRetrieved;  
HROW hRows[10];  
HROW* pRows = &hRows[0];  
  
int main() {  
   // The command to execute.  
   WCHAR* wCmdString = OLESTR("SELECT StandardCost, ListPrice FROM Production.Product WHERE ListPrice > 14.00");  
  
   // Call a function to initialize and establish connection.   
   if (InitializeAndEstablishConnection() == -1) {  
      // Handle error.  
      cout << "Failed to initialize and connect to the server.\n";  
      return -1;  
   }  
  
   // Create a session object.  
   if (FAILED(pIDBInitialize->QueryInterface( IID_IDBCreateSession,  
      (void**) &pIDBCreateSession))) {  
         cout << "Failed to obtain IDBCreateSession interface.\n";  
         // Handle error.  
         return -1;  
   }  
  
   if (FAILED(pIDBCreateSession->CreateSession( NULL,   
      IID_IDBCreateCommand,   
      (IUnknown**) &pIDBCreateCommand))) {  
         cout << "pIDBCreateSession->CreateSession failed.\n";  
         // Handle error.  
         return -1;  
   }  
  
   // Access the ICommandText interface.  
   if (FAILED(pIDBCreateCommand->CreateCommand( NULL,   
      IID_ICommandText,   
      (IUnknown**) &pICommandText))) {  
         cout << "Failed to access ICommand interface.\n";  
         // Handle error.  
         return -1;  
   }  
  
   // Use SetCommandText() to specify the command text.  
   if (FAILED(pICommandText->SetCommandText(DBGUID_DBSQL, wCmdString))) {  
      cout << "Failed to set command text.\n";  
      // Handle error.  
      return -1;  
   }  
  
   // Execute the command.  
   if (FAILED(hr = pICommandText->Execute( NULL,   
      IID_IRowset,   
      NULL,   
      &cNumRows,   
      (IUnknown **) &pIRowset))) {  
         cout << "Failed to execute command.\n";  
         // Handle error.  
         return -1;  
   }  
  
   // Process the result set.  
   ProcessResultSet();   
  
   pIRowset->Release();  
  
   // Free up memory.  
   pICommandText->Release();  
   pIDBCreateCommand->Release();  
   pIDBCreateSession->Release();  
  
   if (FAILED(pIDBInitialize->Uninitialize())) {  
      // Uninitialize is not required, but it fails if an interface  
      // has not been released.  This can be used for debugging.  
      cout << "Problem uninitializing.\n";  
   }  
  
   pIDBInitialize->Release();  
   CoUninitialize();  
};  
  
int InitializeAndEstablishConnection() {      
   CoInitialize(NULL);  
  
   // Obtain access to the SQLNCLI provider.  
   hr = CoCreateInstance( CLSID_SQLNCLI11,  
      NULL,  
      CLSCTX_INPROC_SERVER,  
      IID_IDBInitialize,  
      (void **) &pIDBInitialize);  
  
   if (FAILED(hr)) {  
      printf("Failed to get IDBInitialize interface.\n");  
      // Handle errors here.  
      return -1;  
   }  
  
   // Initialize the property values needed to establish the connection.  
   for ( i = 0 ; i < 4 ; i++ )  
      VariantInit(&InitProperties[i].vValue);  
  
   // Server name.  
   InitProperties[0].dwPropertyID = DBPROP_INIT_DATASOURCE;  
   InitProperties[0].vValue.vt = VT_BSTR;  
  
   InitProperties[0].vValue.bstrVal= SysAllocString(L"(local)");  
   InitProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
   InitProperties[0].colid = DB_NULLID;  
  
   // Database.  
   InitProperties[1].dwPropertyID = DBPROP_INIT_CATALOG;  
   InitProperties[1].vValue.vt = VT_BSTR;  
   InitProperties[1].vValue.bstrVal = SysAllocString(L"AdventureWorks");  
   InitProperties[1].dwOptions = DBPROPOPTIONS_REQUIRED;  
   InitProperties[1].colid = DB_NULLID;  
  
   InitProperties[2].dwPropertyID = DBPROP_AUTH_INTEGRATED;  
   InitProperties[2].vValue.vt = VT_BSTR;  
   InitProperties[2].vValue.bstrVal = SysAllocString(L"SSPI");  
   InitProperties[2].dwOptions = DBPROPOPTIONS_REQUIRED;  
   InitProperties[2].colid = DB_NULLID;  
  
   // Properties are set, now construct the DBPROPSET structure (rgInitPropSet) used to pass   
   // an array of DBPROP structures (InitProperties) to the SetProperties method.  
   rgInitPropSet[0].guidPropertySet = DBPROPSET_DBINIT;  
   rgInitPropSet[0].cProperties = 4;  
   rgInitPropSet[0].rgProperties = InitProperties;  
  
   // Set initialization properties.  
   hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void **)&pIDBProperties);  
   if (FAILED(hr)) {  
      cout << "Failed to get IDBProperties interface.\n";  
      // Handle errors here.  
      return -1;  
   }  
  
   hr = pIDBProperties->SetProperties(1, rgInitPropSet);   
   if (FAILED(hr)) {  
      cout << "Failed to set initialization properties.\n";  
      // Handle errors here.  
      return -1;  
   }  
  
   pIDBProperties->Release();  
  
   // Now establish the connection to the data source.  
   if (FAILED(pIDBInitialize->Initialize())) {  
      cout << "Problem in establishing connection to the data"  
         "source.\n";  
      // Handle errors here.  
      return -1;  
   }  
   return 0;  
}  
  
// Retrieve and display data resulting from a query.  
int ProcessResultSet() {  
   // Obtain access to the IColumnInfo interface, from the Rowset object.  
   hr = pIRowset->QueryInterface(IID_IColumnsInfo, (void **)&pIColumnsInfo);  
   if (FAILED(hr)) {  
      cout << "Failed to get IColumnsInfo interface.\n";  
      // Handle errors here.  
      return -1;  
   }   
  
   // Retrieve the column information.  
   pIColumnsInfo->GetColumnInfo(&lNumCols, &pDBColumnInfo, &pStringsBuffer);  
  
   // Free the column information interface.  
   pIColumnsInfo->Release();  
  
   // Create a DBBINDING array.  
   DBBINDING * p = (pBindings = new DBBINDING[lNumCols]);  
   if (!(p /* pBindings = new DBBINDING[lNumCols] */ ))  
      return -1;  
  
   // Using the ColumnInfo structure, fill out the pBindings array.  
   for ( j = 0 ; j < lNumCols ; j++ ) {  
      pBindings[j].iOrdinal = j+1;  
      pBindings[j].obValue = ConsumerBufColOffset;  
      pBindings[j].pTypeInfo = NULL;  
      pBindings[j].pObject = NULL;  
      pBindings[j].pBindExt = NULL;  
      pBindings[j].dwPart = DBPART_VALUE;  
      pBindings[j].dwMemOwner = DBMEMOWNER_CLIENTOWNED;  
      pBindings[j].eParamIO = DBPARAMIO_NOTPARAM;  
      pBindings[j].cbMaxLen = (pDBColumnInfo[j].wType == DBTYPE_WSTR) ? pDBColumnInfo[j].ulColumnSize * 2 : pDBColumnInfo[j].ulColumnSize;  
      pBindings[j].dwFlags = 0;  
      pBindings[j].wType = pDBColumnInfo[j].wType;  
      pBindings[j].bPrecision = pDBColumnInfo[j].bPrecision;  
      pBindings[j].bScale = pDBColumnInfo[j].bScale;  
  
      // Compute the next buffer offset.  
      ConsumerBufColOffset =   
         ConsumerBufColOffset + pBindings[j].cbMaxLen;  
   };  
  
   // Get the IAccessor interface.  
   hr = pIRowset->QueryInterface(IID_IAccessor, (void **) &pIAccessor);  
   if (FAILED(hr)) {  
      cout << "Failed to obtain IAccessor interface.\n";  
      // Handle errors here.  
      return -1;  
   }  
  
   // Create an accessor from the set of bindings (pBindings).  
   pIAccessor->CreateAccessor(DBACCESSOR_ROWDATA, lNumCols, pBindings, 0, &hAccessor, NULL);  
  
   // Print column names.  
   for ( j = 0 ; j < lNumCols ; j++ )  
      printf("%-40S", pDBColumnInfo[j].pwszName);  
  
   printf("\n");   // new line after the column names  
  
   // Get a set of 10 rows.  
   pIRowset->GetNextRows( NULL, 0, 10, &lNumRowsRetrieved, &pRows);  
  
   // Allocate space for the row buffer.  
   BYTE * pBuffer = new BYTE[ConsumerBufColOffset];  
   if (!(pBuffer /* = new BYTE[ConsumerBufColOffset] */ )) {  
      // Free up all allocated memory.  
      pIAccessor->ReleaseAccessor(hAccessor, NULL);  
      pIAccessor->Release();  
      delete [] pBindings;  
  
      return 0;  
   }  
  
   // Create an instance of the data conversion library to convert DBTYPE_CY to string for display  
   IDataConvert* pIDataConvert;  
   CoCreateInstance(CLSID_OLEDB_CONVERSIONLIBRARY,  
      NULL,  
      CLSCTX_INPROC_SERVER,  
      IID_IDataConvert,  
      (void**)&pIDataConvert);  
  
   // variables used in DataConvert  
   DBLENGTH cbDstLength;  
   DBSTATUS dbsStatus;  
   char strCurrency0[25];  
   char strCurrency1[25];  
  
   // Display the rows.  
   while ( lNumRowsRetrieved > 0 ) {  
      // For each row, print the column data.  
      for ( j = 0 ; j < lNumRowsRetrieved ; j++ ) {  
         // Clear the buffer.  
         memset(pBuffer, 0, ConsumerBufColOffset);  
  
         // Get the row data values.  
         pIRowset->GetData(hRows[j], hAccessor, pBuffer);  
  
         // Convert DBTYPE_CY values to string   
         pIDataConvert->DataConvert(DBTYPE_CY,   // wSrcType  
            DBTYPE_STR,   // wDstType  
            sizeof(LARGE_INTEGER),   // cbSrcLength   
            &cbDstLength,   // pcbDstLength  
            &pBuffer[pBindings[0].obValue],   // pSrc  
            strCurrency0,   // pDst  
            sizeof(strCurrency0),   //cbDstMaxLength  
            DBSTATUS_S_OK,   // dbsSrcStatus  
            &dbsStatus,   // pdbsStatus  
            0,   // bPrecision (used for DBTYPE_NUMERIC only)  
            0,   // bScale (used for DBTYPE_NUMERIC only)  
            DBDATACONVERT_DEFAULT);   // dwFlags  
  
         pIDataConvert->DataConvert(DBTYPE_CY,   // wSrcType  
            DBTYPE_STR,   // wDstType  
            sizeof(LARGE_INTEGER),   // cbSrcLength   
            &cbDstLength,   // pcbDstLength  
            &pBuffer[pBindings[1].obValue],   // pSrc  
            strCurrency1,   // pDst  
            sizeof(strCurrency1),   // cbDstMaxLength  
            DBSTATUS_S_OK,   // dbsSrcStatus  
            &dbsStatus,   // pdbsStatus  
            0,   // bPrecision (used for DBTYPE_NUMERIC only)  
            0,   // bScale (used for DBTYPE_NUMERIC only)  
            DBDATACONVERT_DEFAULT); // dwFlags  
  
         // Print cost and price values.  
         printf("%-40s%s\n", strCurrency0, strCurrency1); //sparra  
      };  
  
      // Release the rows retrieved.  
      pIRowset->ReleaseRows(lNumRowsRetrieved, hRows, NULL, NULL, NULL);  
  
      // Get the next set of 10 rows.  
      pIRowset->GetNextRows(NULL, 0, 10, &lNumRowsRetrieved, &pRows);  
   }  
  
   // Free up all allocated memory.  
   delete [] pBuffer;  
   pIAccessor->ReleaseAccessor(hAccessor, NULL);  
   pIAccessor->Release();  
   delete [] pBindings;  
  
   return 0;  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tópicos explicativos de resultados de processamento &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-how-to/results/processing-results-how-to-topics-ole-db.md)  
  
  

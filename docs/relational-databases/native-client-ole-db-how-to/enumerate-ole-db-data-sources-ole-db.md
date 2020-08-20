---
description: Enumerar SQL Server Native Client OLE DB fontes de dados (OLE DB)
title: Enumerar fontes de dados de OLE DB (provedor de OLE DB de cliente nativo) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- data sources [OLE DB]
ms.assetid: ba240060-3237-4fb8-b2fb-b87fda2b1e7a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a27332a7948c535b768f6507aad81ca72bbcbb26
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88455952"
---
# <a name="enumerate-sql-server-native-client-ole-db-data-sources-ole-db"></a>Enumerar SQL Server Native Client OLE DB fontes de dados (OLE DB)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Este exemplo mostra como usar o objeto enumerador para listar as fontes de dados disponíveis.  
  
 Para listar as fontes de dados visíveis para o enumerador SQLOLEDB, o consumidor chama o método [ISourcesRowset::GetSourcesRowset](https://go.microsoft.com/fwlink/?LinkId=120312) . Esse método retorna um conjunto de linhas de informações sobre as fontes de dados visíveis no momento.  
  
 Dependendo da biblioteca de rede usada, o domínio apropriado é pesquisado em busca das fontes de dados. Para pipes nomeados, é o domínio no qual o cliente fez logon. Para AppleTalk, é a zona padrão. Para SPX/IPX, é a lista de instalações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontradas no bindery. Para Banyan VINES, são as instalações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] encontradas na rede local. Soquetes TCP/IP e de protocolos múltiplos não são suportados.  
  
 Quando o servidor é desativado ou ativado, pode levar alguns minutos para atualizar as informações nesses domínios.  
  
 Este exemplo exige o banco de dados de exemplo AdventureWorks, que pode ser baixado na home page de [Microsoft SQL Server Samples and Community Projects](https://go.microsoft.com/fwlink/?LinkID=85384) (em inglês).  
  
> [!IMPORTANT]  
>  Quando possível, use a Autenticação do Windows. Se a Autenticação do Windows não estiver disponível, solicite aos usuários que digitem suas credenciais em tempo de execução. Evite armazenar as credenciais em um arquivo. Se for necessário manter as credenciais, criptografe-as com a [Win32 crypto API](https://go.microsoft.com/fwlink/?LinkId=64532)(em inglês).  
  
### <a name="to-enumerate-ole-db-data-sources"></a>Para enumerar fontes de dados OLE DB  
  
1.  Recupere o conjunto de linhas de origem chamando **ISourceRowset::GetSourcesRowset**.  
  
2.  Encontre a descrição do conjunto de linhas de enumeradores chamando **GetColumnInfo::IColumnInfo**.  
  
3.  Crie as estruturas de associação a partir das informações de coluna.  
  
4.  Crie o acessador de conjunto de linhas chamando **IAccessor::CreateAccessor**.  
  
5.  Busque as linhas chamando **IRowset::GetNextRows**.  
  
6.  Recupere os dados da cópia da linha do conjunto de linhas chamando **IRowset::GetData**e processe-os.  
  
## <a name="example"></a>Exemplo  
 Compile com ole32.lib e execute a seguinte listagem de código C++. Esse aplicativo se conecta à instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do computador. Em alguns sistemas operacionais Windows, será necessário alterar (localhost) ou (local) para o nome de sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para se conectar a uma instância nomeada, altere a cadeia de conexão de L "(local)" para L"(local)\\\name", em que name representa a instância nomeada. Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Express é instalado em uma instância nomeada. Verifique se a variável de ambiente INCLUDE inclui o diretório que contém sqlncli.h.  
  
```  
// compile with: ole32.lib  
#define UNICODE  
#define _UNICODE  
#define DBINITCONSTANTS  
#define INITGUID  
#define OLEDBVER 0x0250   // to include correct interfaces  
  
#include <windows.h>  
#include <stddef.h>  
#include <oledb.h>  
#include <oledberr.h>  
#include <sqlncli.h>  
#include <stdio.h>  
  
#define NUMROWS_CHUNK  5  
  
// AdjustLen supports binding on four-byte boundaries.  
_inline DBLENGTH AdjustLen(DBLENGTH cb) {   
   return ( (cb + 3) & ~3 );  
}  
  
// Get the characteristics of the rowset (the IColumnsInfo interface).  
HRESULT GetColumnInfo ( IRowset* pIRowset,   
                        DBORDINAL* pnCols,   
                        DBCOLUMNINFO** ppColumnsInfo,  
                        OLECHAR** ppColumnStrings ) {  
   IColumnsInfo* pIColumnsInfo;  
   HRESULT hr;  
  
   *pnCols = 0;  
   if (FAILED(pIRowset->QueryInterface(IID_IColumnsInfo, (void**) &pIColumnsInfo)))  
      return (E_FAIL);  
  
   hr = pIColumnsInfo->GetColumnInfo(pnCols, ppColumnsInfo, ppColumnStrings);  
  
   if (FAILED(hr)) {}   /* Process error */   
  
   pIColumnsInfo->Release();  
   return (hr);  
}  
  
// Create binding structures from column information. Binding structures  
// will be used to create an accessor that allows row value retrieval.  
void CreateDBBindings ( DBORDINAL nCols,   
                        DBCOLUMNINFO* pColumnsInfo,   
                        DBBINDING** ppDBBindings,  
                        BYTE** ppRowValues ) {  
   ULONG nCol;  
   DBLENGTH cbRow = 0;  
   DBLENGTH cbCol;  
   DBBINDING* pDBBindings;  
   BYTE* pRowValues;  
  
   pDBBindings = new DBBINDING[nCols];  
   if (!(pDBBindings /* = new DBBINDING[nCols] */ ))  
      return;  
  
   for ( nCol = 0 ; nCol < nCols ; nCol++ ) {  
      pDBBindings[nCol].iOrdinal = nCol + 1;  
      pDBBindings[nCol].pTypeInfo = NULL;  
      pDBBindings[nCol].pObject = NULL;  
      pDBBindings[nCol].pBindExt = NULL;  
      pDBBindings[nCol].dwPart = DBPART_VALUE;  
      pDBBindings[nCol].dwMemOwner = DBMEMOWNER_CLIENTOWNED;  
      pDBBindings[nCol].eParamIO = DBPARAMIO_NOTPARAM;  
      pDBBindings[nCol].dwFlags = 0;  
      pDBBindings[nCol].wType = pColumnsInfo[nCol].wType;  
      pDBBindings[nCol].bPrecision = pColumnsInfo[nCol].bPrecision;  
      pDBBindings[nCol].bScale = pColumnsInfo[nCol].bScale;  
  
      cbCol = pColumnsInfo[nCol].ulColumnSize;  
  
      switch (pColumnsInfo[nCol].wType) {  
      case DBTYPE_STR: {  
            cbCol += 1;  
            break;  
         }  
  
      case DBTYPE_WSTR: {  
            cbCol = (cbCol + 1) * sizeof(WCHAR);  
            break;  
         }  
  
      default:  
         break;  
      }  
  
      pDBBindings[nCol].obValue = cbRow;  
      pDBBindings[nCol].cbMaxLen = cbCol;  
      cbRow += AdjustLen(cbCol);  
   }  
  
   pRowValues = new BYTE[cbRow];  
   *ppDBBindings = pDBBindings;  
   *ppRowValues = pRowValues;  
}  
  
int main() {  
   ISourcesRowset* pISourceRowset = NULL;      
   IRowset* pIRowset = NULL;          
   IAccessor* pIAccessor = NULL;  
   DBBINDING* pDBBindings = NULL;              
  
   HROW* pRows = new HROW[500];      
   HACCESSOR hAccessorRetrieve = NULL;          
   ULONG DSSeqNumber = 0;  
  
   HRESULT hr;  
   DBORDINAL nCols;  
   DBCOLUMNINFO* pColumnsInfo = NULL;  
   OLECHAR* pColumnStrings = NULL;  
   DBBINDSTATUS* pDBBindStatus = NULL;  
  
   BYTE* pRowValues = NULL;  
   DBCOUNTITEM cRowsObtained;  
   ULONG iRow;  
   char* pMultiByte = NULL;  
   short* psSourceType = NULL;  
   BYTE* pDatasource = NULL;  
  
   if (!pRows)  
      return (0);  
  
   // Initialize COM library.  
   CoInitialize(NULL);  
  
   // Initialize the enumerator.  
   if (FAILED(CoCreateInstance(CLSID_SQLNCLI11_ENUMERATOR,   
                               NULL,  
                               CLSCTX_INPROC_SERVER,   
                               IID_ISourcesRowset,   
                               (void**)&pISourceRowset))) {  
      // Process error.  
      return TRUE;  
   }  
  
   // Retrieve the source rowset.  
   hr = pISourceRowset->GetSourcesRowset(NULL, IID_IRowset, 0, NULL, (IUnknown**)&pIRowset);  
  
   pISourceRowset->Release();  
   if (FAILED(hr)) {  
      // Process error.  
      return TRUE;  
   }  
  
   // Get the description of the enumerator's rowset.  
   if (FAILED(hr = GetColumnInfo(pIRowset, &nCols, &pColumnsInfo, &pColumnStrings))) {  
      // Process error.  
      goto SAFE_EXIT;  
   }  
  
   // Create the binding structures.  
   CreateDBBindings(nCols, pColumnsInfo, &pDBBindings, &pRowValues);  
   pDBBindStatus = new DBBINDSTATUS[nCols];  
  
   if (sizeof(TCHAR) != sizeof(WCHAR))  
      pMultiByte = new char[pDBBindings[0].cbMaxLen];  
  
   if (FAILED(pIRowset->QueryInterface(IID_IAccessor, (void**)&pIAccessor))) {  
      // Process error.  
      goto SAFE_EXIT;  
   }  
  
   // Create the rowset accessor.  
   if (FAILED(hr = pIAccessor->CreateAccessor(DBACCESSOR_ROWDATA,   
                                              nCols,  
                                              pDBBindings,   
                                              0,   
                                              &hAccessorRetrieve,   
                                              pDBBindStatus))) {  
      // Process error.  
      goto SAFE_EXIT;  
   }  
  
   // Process all the rows, NUMROWS_CHUNK rows at a time.  
   while (SUCCEEDED(hr)) {  
      hr = pIRowset->GetNextRows(NULL, 0, NUMROWS_CHUNK, &cRowsObtained, &pRows);  
      if( FAILED(hr)) {  
         // process error  
      }  
      if (cRowsObtained == 0 || FAILED(hr))  
         break;  
  
      for (iRow = 0 ; iRow < cRowsObtained ; iRow++) {  
         // Get the rowset data.  
         if (SUCCEEDED(hr = pIRowset->GetData(pRows[iRow], hAccessorRetrieve, pRowValues))) {  
            psSourceType = (short *)(pRowValues + pDBBindings[3].obValue);  
  
            if (*psSourceType == DBSOURCETYPE_DATASOURCE) {  
               DSSeqNumber = DSSeqNumber + 1;   // Data source counter.  
               pDatasource = (pRowValues + pDBBindings[0].obValue);  
  
               if ( sizeof(TCHAR) != sizeof(WCHAR) ) {  
                  WideCharToMultiByte(CP_ACP,   
                                      0,  
                                      (WCHAR*)pDatasource,   
                                      -1,   
                                      pMultiByte,  
                                      static_cast<int>(pDBBindings[0].cbMaxLen),   
                                      NULL,   
                                      NULL);  
  
                  printf( "DataSource# %d\tName: %S\n",   
                          DSSeqNumber,   
                          (WCHAR *) pMultiByte );  
               }  
               else {  
                  printf( "DataSource# %d\tName: %S\n",   
                          DSSeqNumber,   
                          (WCHAR *) pDatasource );  
               }  
            }  
         }  
      }  
      pIRowset->ReleaseRows(cRowsObtained, pRows, NULL, NULL, NULL);  
   }  
  
   // Release COM library.  
   CoUninitialize();  
  
SAFE_EXIT:  
   // Do the clean-up.  
   return TRUE;  
}  
```  
  
  

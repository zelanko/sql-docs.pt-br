---
title: IBCPSession2::BCPSetBulkMode | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- BCPSetBulkMode function
ms.assetid: babba19f-e67b-450c-b0e6-523a0f9d23ab
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 80b5776826790bf9026df5d25965c4116367b974
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37419625"
---
# <a name="ibcpsession2bcpsetbulkmode"></a>IBCPSession2::BCPSetBulkMode
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  IBCPSession2::BCPSetBulkMode fornece uma alternativa para [ibcpsession:: BCPColFmt &#40;OLE DB&#41; ](../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md) para especificar o formato de coluna. Ao contrário de ibcpsession:: BCPColFmt, que define os atributos de formato de coluna individual, IBCPSession2::BCPSetBulkMode define todos os atributos.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT BCPSetBulkMode (  
      int property,  
   void * pField,  
   int cbField,  
   void * pRow,  
   int cbRow  
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *property*  
 Uma constante do tipo BYTE. Consulte a tabela na seção Comentários para obter a lista das constantes.  
  
 *pField*  
 O ponteiro para o valor de terminador de campo.  
  
 cbField  
 O comprimento em bytes do valor de terminador de campo.  
  
 pRow  
 O ponteiro para o valor de terminador de linha.  
  
 cbRow  
 O comprimento (em bytes) do valor de terminador de linha.  
  
## <a name="returns"></a>Retorna  
 IBCPSession2::BCPSetBulkMode pode retornar um dos seguintes:  
  
|||  
|-|-|  
|**S_OK**|O método foi bem-sucedido.|  
|**E_FAIL**|Ocorreu um erro específico do provedor, para obter informações detalhadas, use a interface ISQLServerErrorInfo.|  
|**E_UNEXPECTED**|A chamada para o método era inesperada. Por exemplo, o **IBCPSession2::BCPInit** método não foi chamado antes de chamar IBCPSession2::BCPSetBulkMode.|  
|**E_INVALIDARG**|O argumento era inválido.|  
|**E_OUTOFMEMORY**|Erro de memória insuficiente.|  
  
## <a name="remarks"></a>Remarks  
 IBCPSession2::BCPSetBulkMode pode ser usado para fazer cópias fora de uma consulta ou uma tabela em massa. Quando IBCPSession2::BCPSetBulkMode é usado para fazer cópias fora de uma instrução de consulta em massa, ele deve ser chamado antes de chamar `IBCPSession::BCPControl(BCP_OPTIONS_HINTS, …)` para especificar a instrução de consulta.  
  
 Evite combinar a sintaxe de chamada RPC com a sintaxe de consulta em lotes (`{rpc func};SELECT * from Tbl`, por exemplo) no texto de um único comando.  Isso fará com que icommandprepare:: Prepare retornar um erro e impedirá de recuperar metadados. Use a sintaxe de ODBC CALL (`{call func}; SELECT * from Tbl`, por exemplo) se precisar combinar a execução de procedimentos armazenados e a consulta em lotes no texto de um único comando.  
  
 A tabela a seguir lista as constantes do parâmetro *property* .  
  
|property|Description|  
|--------------|-----------------|  
|BCP_OUT_CHARACTER_MODE|Especifica o modo de saída de caractere.<br /><br /> Corresponde à opção – c no BCP. EXE e para ibcpsession:: BCPColFmt com *eUserDataType* propriedade definida como **BCP_TYPE_SQLCHARACTER**.|  
|BCP_OUT_WIDE_CHARACTER_MODE|Especifica o modo de saída de Unicode.<br /><br /> Corresponde à opção – w no BCP. EXE e ibcpsession:: BCPColFmt com *eUserDataType* propriedade definida como **BCP_TYPE_SQLNCHAR**.|  
|BCP_OUT_NATIVE_TEXT_MODE|Especifica tipos nativos para tipos de não caracteres e Unicode para tipos de caracteres.<br /><br /> Corresponde à opção – N no BCP. EXE e ibcpsession:: BCPColFmt com *eUserDataType* propriedade definida como **BCP_TYPE_SQLNCHAR** se o tipo de coluna for uma cadeia de caracteres ou **BCP_TYPE_DEFAULT** se não uma cadeia de caracteres.|  
|BCP_OUT_NATIVE_MODE|Especifica tipos de bancos de dados nativos.<br /><br /> Corresponde à opção – n no BCP. EXE e ibcpsession:: BCPColFmt com *eUserDataType* propriedade definida como **BCP_TYPE_DEFAULT**.|  
  
 Você pode chamar ibcpsession:: Bcpcontrol e IBCPSession2::BCPSetBulkMode para ibcpsession:: Bcpcontrol opções que não entrem em conflito com IBCPSession2::BCPSetBulkMode. Por exemplo, você pode chamar ibcpsession:: Bcpcontrol com **BCP_OPTION_FIRST** e IBCPSession2::BCPSetBulkMode.  
  
 Você não pode chamar ibcpsession:: Bcpcontrol com **BCP_OPTION_TEXTFILE** e IBCPSession2::BCPSetBulkMode.  
  
 Se você tentar chamar IBCPSession2::BCPSetBulkMode com uma sequência de chamadas de função que inclui ibcpsession:: BCPColFmt, ibcpsession:: Bcpcontrol e ibcpsession:: Bcpreadfmt, uma das chamadas de função retornará um erro de falha de sequência. Se você optar por corrigir a falha, chame ibcpsession:: BCPInit para redefinir as configurações e recomeçar.  
  
 Abaixo estão alguns exemplos de chamadas de função que resultam em um erro de sequência de função:  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_IN);  
BCPSetBulkMode();  
```  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPSetBulkMode();  
BCPReadFmt();  
```  
  
```  
BCPInit(NULL, "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_HINTS, "select …");  
BCPSetBulkMode();  
```  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPSetBulkMode();  
BCPColFmt();  
```  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_DELAYREADFMT, true);  
BCPReadFmt();  
BCPColFmt();  
```  
  
```  
BCPInit(NULL, "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_DELAYREADFMT, true);  
BCPSetBulkMode();  
BCPControl(BCP_OPTION_HINTS, "select …");  
BCPReadFmt();  
```  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_DELAYREADFMT, true);  
BCPColumns();  
```  
  
```  
BCPInit("table", "dataFile", "errorFile", BCP_DIRECTION_OUT);  
BCPControl(BCP_OPTION_DELAYREADFMT, true);  
BCPSetColFmt();  
```  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir cria quatro arquivos usando diferentes configurações de IBCPSession2::BCPSetBulkMode.  
  
```  
  
// compile with: sqlncli11.lib oleaut32.lib ole32.lib  
  
#include <stdio.h>  
#include "sqlncli.h"  
  
IDBInitialize*  g_pIDBInitialize = NULL;  
IBCPSession2 * g_pIBcpSession = NULL;  
class COLEDBPropSet : public DBPROPSET {  
public:  
   COLEDBPropSet() {  
      rgProperties = NULL;  
      cProperties = 0;  
   };  
   COLEDBPropSet(const GUID& guid) {  
      rgProperties = NULL;  
      cProperties = 0;  
      guidPropertySet = guid;  
   };  
   ~COLEDBPropSet() {  
      for ( ULONG i = 0 ; i < cProperties ; i++ )  
         VariantClear(&rgProperties[i].vValue);  
      CoTaskMemFree(rgProperties);  
   }  
   void SetGUID(const GUID& guid) {  
      guidPropertySet = guid;  
   };  
   bool AddProperty(DWORD dwPropertyID, bool bValue) {  
      if (!Add())  
         return false;  
      rgProperties[cProperties].dwPropertyID = dwPropertyID;  
      rgProperties[cProperties].vValue.vt = VT_BOOL;  
      rgProperties[cProperties].vValue.boolVal = (bValue) ? VARIANT_TRUE : VARIANT_FALSE;  
      cProperties++;  
      return true;  
   };  
   bool AddProperty(DWORD dwPropertyID, long nValue) {  
      if (!Add())  
         return false;  
      rgProperties[cProperties].dwPropertyID  = dwPropertyID;  
      rgProperties[cProperties].vValue.vt     = VT_I4;  
      rgProperties[cProperties].vValue.lVal   = nValue;  
      cProperties++;  
      return true;  
   };  
   bool AddProperty(DWORD dwPropertyID,LPCWSTR szValue) {  
      if (!Add())  
         return false;  
      rgProperties[cProperties].dwPropertyID = dwPropertyID;  
      rgProperties[cProperties].vValue.vt = VT_BSTR;  
      rgProperties[cProperties].vValue.bstrVal = SysAllocString(szValue);  
      cProperties++;  
      return true;  
   };  
   bool Add() {  
      DBPROP* p = (DBPROP*)CoTaskMemRealloc(rgProperties, (cProperties + 1) * sizeof(DBPROP));  
      if (p != NULL) {  
         rgProperties = p;  
         rgProperties[cProperties].dwOptions = DBPROPOPTIONS_REQUIRED;  
         rgProperties[cProperties].colid = DB_NULLID;  
         rgProperties[cProperties].vValue.vt = VT_EMPTY;  
         return true;  
      }  
      else  
         return false;  
   };  
};  
  
void OLEDBCleanUp() {  
   if (g_pIDBInitialize) {  
      g_pIDBInitialize->Release();  
      g_pIDBInitialize = NULL;  
   }  
   if (g_pIBcpSession) {  
      g_pIBcpSession->Release();  
      g_pIBcpSession = NULL;  
   }  
}  
  
BOOL MakeOLEDBConnect(LPWSTR  pServer) {  
   BOOL ret = true;  
   IDBProperties * pIDBProperties = NULL;  
   IDBCreateSession * pIDBCreateSession = NULL;  
   COLEDBPropSet PropSet(DBPROPSET_DBINIT);  
   COLEDBPropSet BcpProperty(DBPROPSET_SQLSERVERDATASOURCE);  
   try {  
      HRESULT hr = CoInitializeEx(NULL,COINIT_MULTITHREADED);   
      hr = CoCreateInstance(SQLNCLI_CLSID, NULL, CLSCTX_INPROC_SERVER, IID_IDBInitialize, (LPVOID *)&g_pIDBInitialize);  
      if (FAILED(hr)) {  
         printf("CoCreateInstance failed\n");  
         return false;  
      }  
      PropSet.AddProperty(DBPROP_INIT_DATASOURCE, (LPWSTR)pServer);  
      PropSet.AddProperty(DBPROP_AUTH_INTEGRATED, L"SSPI");  
      hr = g_pIDBInitialize->QueryInterface(IID_IDBProperties, (void**) &pIDBProperties);  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->->QueryInterface(IID_IDBProperties...) failed\n");  
         throw false;  
      }  
      hr = pIDBProperties->SetProperties(1, &PropSet);  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->->SetProperties(...) failed\n");  
         throw false;  
      }  
      hr = g_pIDBInitialize->Initialize();  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->->Initialize() failed\n");  
         throw false;  
      }  
      BcpProperty.AddProperty(SSPROP_ENABLEFASTLOAD, true);  
      BcpProperty.AddProperty(SSPROP_ENABLEBULKCOPY, true);  
      hr = pIDBProperties->SetProperties(1, &BcpProperty);  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->->SetProperties() for bcp failed\n");  
         throw false;  
      }  
      hr = g_pIDBInitialize->QueryInterface(IID_IDBCreateSession, (void**) &pIDBCreateSession);  
      if (FAILED(hr)) {  
         printf("g_pIDBInitialize->QueryInterface(IID_IDBCreateSession..) failed\n");  
         throw false;  
      }  
  
      hr = pIDBCreateSession->CreateSession(NULL, IID_IBCPSession2, (IUnknown**) &g_pIBcpSession);  
      if (FAILED(hr)) {  
         printf("g_pIDBCreateSession->CreateSession() failed\n");  
         throw false;  
      }  
   }  
   catch(...) {  
      ret = false;  
   }  
   if (pIDBProperties)  
      pIDBProperties->Release();  
   if (pIDBCreateSession)  
      pIDBCreateSession->Release();  
   return ret;  
}  
  
BOOL BCPSetBulkMode(LPWSTR pszServer, LPTSTR pszQureryOut, char BCPType, LPWSTR pszDataFile) {  
   HRESULThr;  
   if (!MakeOLEDBConnect(pszServer))  
      return false;  
   hr = g_pIBcpSession->BCPInit(NULL, pszDataFile, NULL, BCP_DIRECTION_OUT );   // bcp init for queryout  
   if (FAILED(hr)) {  
      printf("BCP init failed\n");  
      OLEDBCleanUp();  
      return false;  
   }  
   // setbulkmode  
   char ColTerm[] = "\t";  
   char RowTerm[] = "\r\n";  
   wchar_t wColTerm[] = L"\t";  
   wchar_t wRowTerm[] = L"\r\n";  
   BYTE * pColTerm = NULL;  
   int cbColTerm = NULL;  
   BYTE * pRowTerm = 0;  
   int cbRowTerm = 0;  
   int bulkmode = -1;  
  
   if(BCPType == 'c') {   // bcp -c  
      pColTerm = (BYTE*)ColTerm;  
      pRowTerm = (BYTE*)RowTerm;  
      cbColTerm = 1;  
      cbRowTerm = 2;  
      bulkmode = BCP_OUT_CHARACTER_MODE;  
   }  
   else  
      if(BCPType == 'w') {   // bcp -w  
         pColTerm = (BYTE*)wColTerm;  
         pRowTerm = (BYTE*)wRowTerm;  
         cbColTerm = 2;  
         cbRowTerm = 4;  
         bulkmode = BCP_OUT_WIDE_CHARACTER_MODE;  
      }  
      else  
         if (BCPType == 'n')   // bcp -n  
            bulkmode = BCP_OUT_NATIVE_MODE;  
         else  
            if (BCPType == 'N')   // bcp -n  
               bulkmode = BCP_OUT_NATIVE_TEXT_MODE;  
            else {  
               printf("unknown bcp mode\n");  
               OLEDBCleanUp();  
               return false;  
            }  
            hr = g_pIBcpSession->BCPSetBulkMode(bulkmode, pColTerm, cbColTerm, pRowTerm, cbRowTerm);  
            if (FAILED(hr)) {  
               printf("BCPSetBulkMode failed\n");  
               OLEDBCleanUp();  
               return false;  
            }  
  
            // set queryout TSQL statement  
            hr = g_pIBcpSession->BCPControl(BCP_OPTION_HINTS, pszQureryOut);  
            if (FAILED(hr)) {  
               printf("BCPControl failed\n");  
               OLEDBCleanUp();  
               return false;  
            }  
            // bcp copy  
            DBROWCOUNT nRowsInserted = 0;  
            hr = g_pIBcpSession->BCPExec(&nRowsInserted);  
            if (FAILED(hr)) {  
               printf("BCPExec failed\n");  
               OLEDBCleanUp();  
               return false;  
            }  
            printf("bcp done\n");  
            OLEDBCleanUp();  
            return true;  
}  
  
int main() {  
   BCPSetBulkMode(L"localhost", TEXT("SELECT 'this is a bcp -c test', 1,2") , 'c', L"bcpc.dat");  
   BCPSetBulkMode(L"localhost", TEXT("SELECT 'this is a bcp -w test', 1,2") , 'w', L"bcpw.dat");  
   BCPSetBulkMode(L"localhost", TEXT("SELECT 'this is a bcp -c test', 1,2") , 'n', L"bcpn.dat");  
   BCPSetBulkMode(L"localhost", TEXT("SELECT 'this is a bcp -w test', 1,2") , 'N', L"bcp_N.dat");  
}  
```  
  
## <a name="see-also"></a>Consulte também  
 [IBCPSession2 &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/ibcpsession2-ole-db.md)  
  
  

---
title: Exemplo de extensões de Visual C++ | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- ADO, Visual C++
- Visual C++ [ADO], VC++ extensions example
ms.assetid: 9739c278-582c-402b-a158-7f68a1b2c293
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d3517f40b15081ca2ee4621d07455cc13bb577d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926398"
---
# <a name="visual-c-extensions-example"></a>Exemplo de extensões do Visual C++
Este programa mostra como os valores são recuperados de campos e convertidos em variáveis C/C++.  
  
 Este exemplo também aproveita os "apontadores inteligentes", que manipulam automaticamente os detalhes específicos de COM de `QueryInterface` chamada e referência de contagem para a interface **IADORecordBinding** .  
  
 Sem os ponteiros inteligentes, você codificaria:  
  
```cpp
IADORecordBinding   *picRs = NULL;  
...  
TESTHR(pRs->QueryInterface(  
          __uuidof(IADORecordBinding), (LPVOID*)&picRs));  
...  
if (picRs) picRs->Release();  
```  
  
 Com os ponteiros inteligentes, você `IADORecordBindingPtr` deriva o tipo `IADORecordBinding` da interface com esta instrução:  
  
```cpp
_COM_SMARTPTR_TYPEDEF(IADORecordBinding, __uuidof(IADORecordBinding));  
```  
  
 E instancie o ponteiro como este:  
  
```cpp
IADORecordBindingPtr picRs(pRs);  
```  
  
 Como as extensões de Visual C++ são implementadas pelo objeto **Recordset** , o construtor para o ponteiro inteligente `picRs`,, usa o`RecordsetPtr` ponteiro _ `pRs`,. O construtor chama `QueryInterface` o `pRs` uso para localizar `IADORecordBinding` a interface.  
  
```cpp
// Visual_Cpp_Extensions_Example.cpp  
// compile with: /EHsc  
#import "msado15.dll" no_namespace rename("EOF", "EndOfFile")  
  
#include <icrsint.h>  
_COM_SMARTPTR_TYPEDEF(IADORecordBinding, __uuidof(IADORecordBinding));  
  
inline void TESTHR(HRESULT _hr) { if FAILED(_hr) _com_issue_error(_hr); }  
  
class CCustomRs : public CADORecordBinding {  
   BEGIN_ADO_BINDING(CCustomRs)  
      ADO_VARIABLE_LENGTH_ENTRY2(2, adVarChar, m_ch_fname, sizeof(m_ch_fname), m_ul_fnameStatus, false)  
      ADO_VARIABLE_LENGTH_ENTRY2(4, adVarChar, m_ch_lname, sizeof(m_ch_lname), m_ul_lnameStatus, false)  
   END_ADO_BINDING()  
  
public:  
   CHAR m_ch_fname[22];  
   CHAR m_ch_lname[32];  
   ULONG m_ul_fnameStatus;  
   ULONG m_ul_lnameStatus;  
};  
  
int main() {  
   ::CoInitialize(NULL);  
   try {  
      _RecordsetPtr pRs("ADODB.Recordset");  
      CCustomRs rs;  
      IADORecordBindingPtr picRs(pRs);  
  
      pRs->Open(L"SELECT * FROM Employee ORDER BY lname", L"dsn=DataPubs;Trusted_Connection=yes;", adOpenStatic, adLockOptimistic, adCmdText);  
  
      TESTHR(picRs->BindToRecordset(&rs));  
  
      while (!pRs->EndOfFile) {  
         // Process data in the CCustomRs C++ instance variables.  
         printf("Name = %s %s\n",  
            (rs.m_ul_fnameStatus == adFldOK ? rs.m_ch_fname: "<Error>"),   
            (rs.m_ul_lnameStatus == adFldOK ? rs.m_ch_lname: "<Error>") );  
  
         // Move to the next row of the Recordset.   Fields in the new row will   
         // automatically be placed in the CCustomRs C++ instance variables.  
  
         pRs->MoveNext();  
      }  
   }  
   catch (_com_error &e ) {  
      printf("Error:\n");  
      printf("Code = %08lx\n", e.Error());  
      printf("Meaning = %s\n", e.ErrorMessage());  
      printf("Source = %s\n", (LPCSTR) e.Source());  
      printf("Description = %s\n", (LPCSTR) e.Description());  
   }  
   ::CoUninitialize();  
}  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usando extensões de Visual C++](../../../ado/guide/appendixes/using-visual-c-extensions.md)   
 [Cabeçalho de extensões do Visual C++](../../../ado/guide/appendixes/visual-c-extensions-header.md)

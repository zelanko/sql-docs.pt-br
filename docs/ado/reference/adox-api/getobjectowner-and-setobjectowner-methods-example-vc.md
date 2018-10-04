---
title: GetObjectOwner e Setobjectowner de métodos (VC + +) | Microsoft Docs
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
- SetObjectOwner method [ADOX], VC++ example
- GetObjectOwner method [ADOX], VC++ example
ms.assetid: f5f2aa4b-d790-458f-9e70-1643e3e203b2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 176105cafaccafab2fc2a85a716db6dee958d31e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47735074"
---
# <a name="getobjectowner-and-setobjectowner-methods-example-vc"></a>Exemplo dos métodos GetObjectOwner e SetObjectOwner (VC++)
Este exemplo demonstra a [GetObjectOwner](../../../ado/reference/adox-api/getobjectowner-method-adox.md) e [SetObjectOwner](../../../ado/reference/adox-api/setobjectowner-method.md) métodos. Esse código supõe a existência do grupo Contabilidade (consulte a [grupos e usuários, ChangePassword exemplo dos métodos Append (VC + +)](../../../ado/reference/adox-api/groups-and-users-append-changepassword-methods-example-vc.md) para ver como adicionar esse grupo para o sistema). O proprietário da tabela de categorias é definido como contabilidade.  
  
```  
// BeginOwnersCpp.cpp  
// compile with: /EHsc  
#import "msadox.dll" no_namespace  
  
#include "iostream"  
using namespace std;  
  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
  
int main() {  
   if ( FAILED(::CoInitialize(NULL)) )  
      return -1;  
  
   HRESULT hr = S_OK;  
  
   // Define and initialize ADOX object pointers. These are in the ADODB namespace.  
   _TablePtr m_pTable = NULL;  
   _CatalogPtr m_pCatalog = NULL;  
  
   try {  
      TESTHR(hr = m_pCatalog.CreateInstance(__uuidof(Catalog)));  
      TESTHR(hr = m_pTable.CreateInstance(__uuidof(Table)));  
  
      // Open the Catalog.  
      m_pCatalog->PutActiveConnection("Provider='Microsoft.JET.OLEDB.4.0';data source='c:\\Northwind.mdb';jet oledb:system database='c:\\system.mdw'");  
  
      // Print the original owner of Categories  
      _bstr_t strOwner = m_pCatalog->GetObjectOwner("Categories", adPermObjTable);  
      cout << "Owner of Categories: " << strOwner << "\n" << endl;  
  
      //Create and append new group with a string.  
      m_pCatalog->Groups->Append("Accounting");  
  
      //Set the owner of Categories to Accounting.  
      m_pCatalog->SetObjectOwner("Categories", adPermObjTable, "Accounting");  
  
      _variant_t vIndex;  
      // List the owners of all tables and columns in the catalog.  
      for ( long iIndex = 0 ; iIndex < m_pCatalog->Tables->Count ; iIndex++ ) {  
         vIndex = iIndex;  
         m_pTable = m_pCatalog->Tables->GetItem(vIndex);  
         cout << "Table: " << m_pTable->Name << endl;  
         cout << "   Owner: " << m_pCatalog->GetObjectOwner(m_pTable->Name, adPermObjTable) << endl;  
      }  
  
      // Restore the original owner of Categories  
      m_pCatalog->SetObjectOwner("Categories", adPermObjTable, strOwner);  
  
      // Delete Accounting  
      m_pCatalog->Groups->Delete("Accounting");  
   }  
   catch(_com_error &e) {  
      // Notify the user of errors if any.  
      _bstr_t bstrSource(e.Source());  
      _bstr_t bstrDescription(e.Description());  
  
      printf("\n\tSource :  %s \n\tdescription : %s \n ", (LPCSTR)bstrSource, (LPCSTR)bstrDescription);  
   }  
  
   catch(...) {  
      cout << "Error occured in include files...." << endl;  
   }  
   ::CoUninitialize();  
}  
```

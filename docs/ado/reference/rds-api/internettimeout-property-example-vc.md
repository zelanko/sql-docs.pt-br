---
title: Exemplo da propriedade InternetTimeout (VC + +) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/20/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- C++
helpviewer_keywords:
- InternetTimeout property [ADO], VC++ example
ms.assetid: 88b6d05c-d4eb-4ab1-bbe2-95d146237f94
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6465432962ad02d4bc4035197f7fc04a30036b92
ms.sourcegitcommit: 671370ec2d49ed0159a418b9c9ac56acf43249ad
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2019
ms.locfileid: "57973995"
---
# <a name="internettimeout-property-example-vc"></a>Exemplo da propriedade InternetTimeout (VC++)
> [!IMPORTANT]
>  Começando com o Windows 8 e Windows Server 2012, os componentes de servidor RDS não estão mais incluídos no sistema operacional Windows (consulte o Windows 8 e [manual de compatibilidade do Windows Server 2012](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Componentes de cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Devem ser migrados para aplicativos que usam o RDS [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Este exemplo demonstra a [InternetTimeout](../../../ado/reference/rds-api/internettimeout-property-rds.md) propriedade, que existe na [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) e [DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md) objetos. Nesse caso, o **InternetTimeout** propriedade é demonstrada na **DataControl** objeto e o tempo limite é definido como 20 segundos.  
  
```cpp
// BeginInternetTimeoutCpp  
#import "c:\Program Files\Common Files\System\ADO\msado15.dll" \  
    no_namespace rename("EOF", "EndOfFile")  
#import "C:\Program Files\Common Files\System\MSADC\msadco.dll"  
  
#include <ole2.h>  
#include <stdio.h>  
#include <conio.h>  
  
// Function declarations  
inline void TESTHR(HRESULT x) {if FAILED(x) _com_issue_error(x);};  
void InternetTimeOutX(void);  
void PrintProviderError(_ConnectionPtr pConnection);  
void PrintComError(_com_error &e);  
  
//////////////////////////////////////////////////////////  
//                                                      //  
//    Main Function                                     //  
//                                                      //  
//////////////////////////////////////////////////////////  
  
void main()  
{  
    if(FAILED(::CoInitialize(NULL)))  
        return;  
  
    InternetTimeOutX();  
  
    ::CoUninitialize();  
}  
  
//////////////////////////////////////////////////////////  
//                                                      //  
//         InternetTimeOutX Function                    //  
//                                                      //  
//////////////////////////////////////////////////////////  
  
void InternetTimeOutX(void)   
{  
    HRESULT hr = S_OK;  
  
    // Define ADO object pointers.  
    // Initialize pointers on define.  
    // These are in the ADODB::  namespace.  
    _RecordsetPtr  pRst = NULL;  
  
    //Define RDS object pointers  
    RDS::IBindMgrPtr dc ;  
  
    try  
    {  
        TESTHR(dc.CreateInstance(__uuidof(RDS::DataControl)));  
        dc->Server = "https://MyServer";  
        dc->Connect = "Data Source='AuthorDatabase'";  
        dc->SQL = "SELECT * FROM Authors";  
  
        // Wait at least 20 seconds.  
        dc->InternetTimeout = 20000;  
        dc->Refresh();  
  
        // Use another Recordset as a convenience  
        pRst = dc->GetRecordset();  
        while(!(pRst->EndOfFile))  
        {  
            printf("%s %s",(LPSTR) (_bstr_t) pRst->Fields->  
                GetItem("au_fname")->Value,  
               (LPSTR) (_bstr_t) pRst->Fields->  
                GetItem("au_lname")->Value);  
  
            pRst->MoveNext();  
        }  
        pRst->Close();  
    }  
  
    catch (_com_error &e)  
    {  
        PrintProviderError(pRst->GetActiveConnection());  
        PrintComError(e);  
    }  
}  
  
//////////////////////////////////////////////////////////  
//                                                      //  
//     PrintProviderError Function                      //  
//                                                      //  
//////////////////////////////////////////////////////////  
  
void PrintProviderError(_ConnectionPtr pConnection)  
{  
    // Print Provider Errors from Connection object.  
    // pErr is a record object in the Connection's Error collection.  
    ErrorPtr  pErr  = NULL;  
  
    if( (pConnection->Errors->Count) > 0)  
    {  
        long nCount = pConnection->Errors->Count;  
        // Collection ranges from 0 to nCount -1.  
        for(long i = 0; i < nCount; i++)  
        {  
            pErr = pConnection->Errors->GetItem(i);  
            printf("\t Error number: %x\t%s", pErr->Number,   
                pErr->Description);  
        }  
    }  
}  
  
//////////////////////////////////////////////////////////  
//                                                      //  
//     PrintComError Function                           //  
//                                                      //  
//////////////////////////////////////////////////////////  
  
void PrintComError(_com_error &e)  
{  
    _bstr_t bstrSource(e.Source());  
    _bstr_t bstrDescription(e.Description());  
  
    // Print Com errors.    
    printf("Error\n");  
    printf("\tCode = %08lx\n", e.Error());  
    printf("\tCode meaning = %s\n", e.ErrorMessage());  
    printf("\tSource = %s\n", (LPCSTR) bstrSource);  
    printf("\tDescription = %s\n", (LPCSTR) bstrDescription);  
}  
// EndInternetTimeoutCpp  
```  
  
## <a name="see-also"></a>Consulte também  
 [Propriedade InternetTimeout (RDS)](../../../ado/reference/rds-api/internettimeout-property-rds.md)



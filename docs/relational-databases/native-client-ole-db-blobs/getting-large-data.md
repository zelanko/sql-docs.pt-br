---
title: Obtendo dados grandes | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-blobs
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- DBPROP_ACCESSORDER property
- SQL Server Native Client OLE DB provider, BLOBs
- large data, OLE objects
ms.assetid: a31c5632-96aa-483f-a307-004c5149fbc0
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4968f3e95cde1aa5f4fb38ec7271714439e3b0d0
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="getting-large-data"></a>Obtendo dados grandes
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Em geral, os consumidores devem isolar o código que cria um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objeto de armazenamento do Native Client OLE DB provider do código que trata dados não referenciados por meio de um **ISequentialStream** ponteiro de interface.  
  
 Este tópico aborda a funcionalidade disponível nas funções a seguir:  
  
-   IRowset:GetData  
  
-   IRow::GetColumns  
  
-   ICommand::Execute  
  
 Se a propriedade DBPROP_ACCESSORDER (no grupo de propriedades de conjunto de linhas) é definida para qualquer um dos valores DBPROPVAL_AO_SEQUENTIAL ou DBPROPVAL_AO_SEQUENTIALSTORAGEOBJECTS, o consumidor deverá buscar somente uma única linha de dados em uma chamada para o **GetNextRows** método porque não é armazenada em buffer os dados BLOB. Se o valor de DBPROP_ACCESSORDER for definido como DBPROPVAL_AO_RANDOM, o consumidor poderá buscar várias linhas de dados em **GetNextRows**.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client não recupera dados grandes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] até que o solicitado pelo consumidor. O consumidor deve associar todos os dados curtos em um acessador e usar um ou mais acessadores temporários para recuperar valores de dados grandes conforme necessário.  
  
## <a name="example"></a>Exemplo  
 Este exemplo recupera um valor de dados grandes de uma única coluna:  
  
```  
HRESULT GetUnboundData  
    (  
    IRowset* pIRowset,  
    HROW hRow,  
    ULONG nCol,   
    BYTE* pUnboundData  
    )  
    {  
    UINT                cbRow = sizeof(IUnknown*) + sizeof(ULONG);  
    BYTE*               pRow = new BYTE[cbRow];  
  
    DBOBJECT            dbobject;  
  
    IAccessor*          pIAccessor = NULL;  
    HACCESSOR           haccessor;  
  
    DBBINDING           dbbinding;  
    ULONG               ulbindstatus;  
  
    ULONG               dwStatus;  
    ISequentialStream*  pISequentialStream;  
    ULONG               cbRead;  
  
    HRESULT             hr;  
  
    // Set up the DBOBJECT structure.  
    dbobject.dwFlags = STGM_READ;  
    dbobject.iid = IID_ISequentialStream;  
  
    // Create the DBBINDING, requesting a storage-object pointer from  
    // The SQL Server Native Client OLE DB provider.  
    dbbinding.iOrdinal = nCol;  
    dbbinding.obValue = 0;  
    dbbinding.obStatus = sizeof(IUnknown*);  
    dbbinding.obLength = 0;  
    dbbinding.pTypeInfo = NULL;  
    dbbinding.pObject = &dbobject;  
    dbbinding.pBindExt = NULL;  
    dbbinding.dwPart = DBPART_VALUE | DBPART_STATUS;  
    dbbinding.dwMemOwner = DBMEMOWNER_CLIENTOWNED;  
    dbbinding.eParamIO = DBPARAMIO_NOTPARAM;  
    dbbinding.cbMaxLen = 0;  
    dbbinding.dwFlags = 0;  
    dbbinding.wType = DBTYPE_IUNKNOWN;  
    dbbinding.bPrecision = 0;  
    dbbinding.bScale = 0;  
  
    if (FAILED(hr = pIRowset->  
        QueryInterface(IID_IAccessor, (void**) &pIAccessor)))  
        {  
        // Process QueryInterface failure.  
        return (hr);  
        }  
  
    // Create the accessor.  
    if (FAILED(hr = pIAccessor->CreateAccessor(DBACCESSOR_ROWDATA, 1,  
        &dbbinding, 0, &haccessor, &ulbindstatus)))  
        {  
        // Process error from CreateAccessor.  
        pIAccessor->Release();  
        return (hr);  
        }  
  
    // Read and process BLOCK_SIZE bytes at a time.  
    if (SUCCEEDED(hr = pIRowset->GetData(hRow, haccessor, pRow)))  
        {  
        dwStatus = *((ULONG*) (pRow + dbbinding.obStatus));  
  
        if (dwStatus == DBSTATUS_S_ISNULL)  
            {  
            // Process NULL data  
            }  
        else if (dwStatus == DBSTATUS_S_OK)  
            {  
            pISequentialStream = *((ISequentialStream**)   
                (pRow + dbbinding.obValue));  
  
            do  
                {  
                if (SUCCEEDED(hr =  
                    pISequentialStream->Read(pUnboundData,  
                    BLOCK_SIZE, &cbRead)))  
                    {  
                    pUnboundData += cbRead;  
                    }  
                }  
            while (SUCCEEDED(hr) && cbRead >= BLOCK_SIZE);  
  
            pISequentialStream->Release();  
            }  
        }  
    else  
        {  
        // Process error from GetData.  
        }  
  
    pIAccessor->ReleaseAccessor(haccessor, NULL);  
    pIAccessor->Release();  
    delete [] pRow;  
  
    return (hr);  
    }  
```  
  
## <a name="see-also"></a>Consulte também  
 [BLOBs e objetos OLE](../../relational-databases/native-client-ole-db-blobs/blobs-and-ole-objects.md)   
 [Usando tipos de valor grande](../../relational-databases/native-client/features/using-large-value-types.md)  
  
  

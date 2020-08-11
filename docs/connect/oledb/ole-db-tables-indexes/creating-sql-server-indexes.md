---
title: Criar índices do SQL Server (Driver do OLE DB) | Microsoft Docs
description: Criar índices do SQL Server usando o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- CreateIndex function
- constraints [OLE DB]
- OLE DB Driver for SQL Server, indexes
- indexes [OLE DB]
- adding indexes
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 96521e592f1c44d4929c93dca7463d8e20189726
ms.sourcegitcommit: 08f331b6a5fe72d68ef1b2eccc5d16cb80c6ee39
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/23/2020
ms.locfileid: "86977808"
---
# <a name="creating-sql-server-indexes"></a>Criando índices do SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O OLE DB Driver for SQL Server expõe a função **IIndexDefinition::CreateIndex**, permitindo que os consumidores definam novos índices em tabelas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 O Driver do OLE DB para SQL Server cria índices de tabela como índices ou como restrições. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] concede privilégios para criação de restrições ao proprietário da tabela, ao proprietário do banco de dados e aos membros de determinadas funções administrativas. Por padrão, apenas o proprietário da tabela pode criar um índice em uma tabela. Portanto, o êxito ou a falha de **CreateIndex** depende não apenas dos direitos de acesso do usuário do aplicativo, mas também do tipo de índice criado.  
  
 Os consumidores especificam o nome da tabela como uma cadeia de caracteres Unicode no membro *pwszName* da união *uName* no parâmetro *pTableID*. O membro *eKind* de *pTableID* precisa ser DBKIND_NAME.  
  
 O parâmetro *pIndexID* pode ser NULL e, se for, o OLE DB Driver for SQL Server criará um nome exclusivo para o índice. O consumidor pode capturar o nome do índice especificando um ponteiro válido para um DBID no parâmetro *ppIndexID*.  
  
 O consumidor pode especificar o nome do índice como uma cadeia de caracteres Unicode no membro *pwszName* da união *uName* do parâmetro *pIndexID*. O membro *eKind* de *pIndexID* precisa ser DBKIND_NAME.  
  
 O consumidor especifica a coluna ou as colunas que participam do índice por nome. Para cada estrutura DBINDEXCOLUMNDESC usada em **CreateIndex**, o membro *eKind* da *pColumnID* precisa ser DBKIND_NAME. O nome da coluna é especificado como uma cadeia de caracteres Unicode no membro *pwszName* da união *uName* no *pColumnID*.  
  
 O Driver do OLE DB para SQL Server e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] dão suporte à ordem crescente de valores no índice. O OLE DB Driver for SQL Server retorna E_INVALIDARG se o consumidor especifica DBINDEX_COL_ORDER_DESC em qualquer estrutura DBINDEXCOLUMNDESC.  
  
 **CreateIndex** interpreta as propriedades de índice, conforme mostrado a seguir.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|DBPROP_INDEX_AUTOUPDATE|L/G: Leitura/gravação<br /><br /> Padrão: Nenhum<br /><br /> Descrição: o Driver do OLE DB para SQL Server não dá suporte a essa propriedade. As tentativas de definir a propriedade em **CreateIndex** geram um valor retornado DB_S_ERRORSOCCURRED. O membro *dwStatus* da estrutura de propriedade indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_CLUSTERED|L/G: Leitura/gravação<br /><br /> Padrão: VARIANT_FALSE<br /><br /> Descrição: controla o clustering de índice.<br /><br /> VARIANT_TRUE: o Driver do OLE DB para SQL Server tenta criar um índice clusterizado na tabela [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oferece suporte a no máximo um índice clusterizado em qualquer tabela.<br /><br /> VARIANT_FALSE: o Driver do OLE DB para SQL Server tenta criar um índice não clusterizado na tabela [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|DBPROP_INDEX_FILLFACTOR|L/G: Leitura/gravação<br /><br /> Padrão: 0<br /><br /> Descrição: especifica o percentual de uma página de índice usada para armazenamento. Para obter mais informações, confira [CREATE INDEX](../../../t-sql/statements/create-index-transact-sql.md).<br /><br /> O tipo da variante é VT_I4. O valor deve ser maior ou igual a 1 e menor ou igual a 100.|  
|DBPROP_INDEX_INITIALIZE|L/G: Leitura/gravação<br /><br /> Padrão: Nenhum<br /><br /> Descrição: o Driver do OLE DB para SQL Server não dá suporte a essa propriedade. As tentativas de definir a propriedade em **CreateIndex** geram um valor retornado DB_S_ERRORSOCCURRED. O membro *dwStatus* da estrutura de propriedade indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_NULLCOLLATION|L/G: Leitura/gravação<br /><br /> Padrão: Nenhum<br /><br /> Descrição: o Driver do OLE DB para SQL Server não dá suporte a essa propriedade. As tentativas de definir a propriedade em **CreateIndex** geram um valor retornado DB_S_ERRORSOCCURRED. O membro *dwStatus* da estrutura de propriedade indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_NULLS|L/G: Leitura/gravação<br /><br /> Padrão: Nenhum<br /><br /> Descrição: o Driver do OLE DB para SQL Server não dá suporte a essa propriedade. As tentativas de definir a propriedade em **CreateIndex** geram um valor retornado DB_S_ERRORSOCCURRED. O membro *dwStatus* da estrutura de propriedade indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_PRIMARYKEY|L/G: Leitura/gravação<br /><br /> Padrão: Descrição de VARIANT_FALSE: cria o índice como uma integridade referencial, restrição PRIMARY KEY.<br /><br /> VARIANT_TRUE: o índice é criado para dar suporte à restrição PRIMARY KEY da tabela. As colunas devem ser não nulas.<br /><br /> VARIANT_FALSE: o índice não é usado como uma restrição PRIMARY KEY para valores de linha na tabela.|  
|DBPROP_INDEX_SORTBOOKMARKS|L/G: Leitura/gravação<br /><br /> Padrão: Nenhum<br /><br /> Descrição: o Driver do OLE DB para SQL Server não dá suporte a essa propriedade. As tentativas de definir a propriedade em **CreateIndex** geram um valor retornado DB_S_ERRORSOCCURRED. O membro *dwStatus* da estrutura de propriedade indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_TEMPINDEX|L/G: Leitura/gravação<br /><br /> Padrão: Nenhum<br /><br /> Descrição: o Driver do OLE DB para SQL Server não dá suporte a essa propriedade. As tentativas de definir a propriedade em **CreateIndex** geram um valor retornado DB_S_ERRORSOCCURRED. O membro *dwStatus* da estrutura de propriedade indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_TYPE|L/G: Leitura/gravação<br /><br /> Padrão: Nenhum<br /><br /> Descrição: o Driver do OLE DB para SQL Server não dá suporte a essa propriedade. As tentativas de definir a propriedade em **CreateIndex** geram um valor retornado DB_S_ERRORSOCCURRED. O membro *dwStatus* da estrutura de propriedade indica DBPROPSTATUS_BADVALUE.|  
|DBPROP_INDEX_UNIQUE|L/G: Leitura/gravação<br /><br /> Padrão: VARIANT_FALSE<br /><br /> Descrição: cria o índice como uma restrição UNIQUE na coluna ou nas colunas participantes.<br /><br /> VARIANT_TRUE: o índice é usado para restringir valores de linha de maneira exclusiva na tabela.<br /><br /> VARIANT_FALSE: o índice não restringe valores de linha de maneira exclusiva.|  
  
 No conjunto de propriedades específico do provedor DBPROPSET_SQLSERVERINDEX, o OLE DB Driver for SQL Server define as propriedades de informações da fonte de dados a seguir.  
  
|ID da propriedade|Descrição|  
|-----------------|-----------------|  
|SSPROP_INDEX_XML|Tipo: VT_BOOL (leitura/gravação)<br /><br /> Padrão: VARIANT_FALSE<br /><br /> Descrição: quando essa propriedade é especificada com um valor VARIANT_TRUE com IIndexDefinition::CreateIndex, ela resulta na criação de um índice xml principal correspondente à coluna que está sendo indexada. Se essa propriedade for VARIANT_TRUE, cIndexColumnDescs deverá ser 1, caso contrário, será um erro.|  
  
 Este exemplo cria um índice de chave primária:  
  
```  
// This CREATE TABLE statement shows the referential integrity and   
// PRIMARY KEY constraint on the OrderDetails table that will be created   
// by the following example code.  
//  
// CREATE TABLE OrderDetails  
// (  
//    OrderID      int      NOT NULL  
//    ProductID   int      NOT NULL  
//        CONSTRAINT PK_OrderDetails  
//        PRIMARY KEY CLUSTERED (OrderID, ProductID),  
//    UnitPrice   money      NOT NULL,  
//    Quantity   int      NOT NULL,  
//    Discount   decimal(2,2)   NOT NULL  
//        DEFAULT 0  
// )  
//  
HRESULT CreatePrimaryKey  
    (  
    IIndexDefinition* pIIndexDefinition  
    )  
    {  
    HRESULT             hr = S_OK;  
  
    DBID                dbidTable;  
    DBID                dbidIndex;  
    const ULONG         nCols = 2;  
    ULONG               nCol;  
    const ULONG         nProps = 2;  
    ULONG               nProp;  
  
    DBINDEXCOLUMNDESC   dbidxcoldesc[nCols];  
    DBPROP              dbpropIndex[nProps];  
    DBPROPSET           dbpropset;  
  
    DBID*               pdbidIndexOut = NULL;  
  
    // Set up identifiers for the table and index.  
    dbidTable.eKind = DBKIND_NAME;  
    dbidTable.uName.pwszName = L"OrderDetails";  
  
    dbidIndex.eKind = DBKIND_NAME;  
    dbidIndex.uName.pwszName = L"PK_OrderDetails";  
  
    // Set up column identifiers.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        dbidxcoldesc[nCol].pColumnID = new DBID;  
        dbidxcoldesc[nCol].pColumnID->eKind = DBKIND_NAME;  
  
        dbidxcoldesc[nCol].eIndexColOrder = DBINDEX_COL_ORDER_ASC;  
        }  
    dbidxcoldesc[0].pColumnID->uName.pwszName = L"OrderID";  
    dbidxcoldesc[1].pColumnID->uName.pwszName = L"ProductID";  
  
    // Set properties for the index. The index is clustered,  
    // PRIMARY KEY.  
    for (nProp = 0; nProp < nProps; nProp++)  
        {  
        dbpropIndex[nProp].dwOptions = DBPROPOPTIONS_REQUIRED;  
        dbpropIndex[nProp].colid = DB_NULLID;  
  
        VariantInit(&(dbpropIndex[nProp].vValue));  
  
        dbpropIndex[nProp].vValue.vt = VT_BOOL;  
        }  
    dbpropIndex[0].dwPropertyID = DBPROP_INDEX_CLUSTERED;  
    dbpropIndex[0].vValue.boolVal = VARIANT_TRUE;  
  
    dbpropIndex[1].dwPropertyID = DBPROP_INDEX_PRIMARYKEY;  
    dbpropIndex[1].vValue.boolVal = VARIANT_TRUE;  
  
    dbpropset.rgProperties = dbpropIndex;  
    dbpropset.cProperties = nProps;  
    dbpropset.guidPropertySet = DBPROPSET_INDEX;  
  
    hr = pIIndexDefinition->CreateIndex(&dbidTable, &dbidIndex, nCols,  
        dbidxcoldesc, 1, &dbpropset, &pdbidIndexOut);  
  
    // Clean up dynamically allocated DBIDs.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        delete dbidxcoldesc[nCol].pColumnID;  
        }  
  
    return (hr);  
    }  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas e índices](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  

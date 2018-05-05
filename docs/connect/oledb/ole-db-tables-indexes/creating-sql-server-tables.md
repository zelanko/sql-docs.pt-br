---
title: Criando tabelas do SQL Server | Microsoft Docs
description: Criando tabelas do SQL Server usando o Driver do OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-tables-indexes
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- tables [OLE DB]
- OLE DB Driver for SQL Server, tables
- DBCOLUMNDESC usage
- adding tables
- CreateTable function
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 5497a74c256282fd14f7c5301f7eea4cfa9aa596
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="creating-sql-server-tables"></a>Criando tabelas do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  O Driver OLE DB para SQL Server expõe o **itabledefinition:: CreateTable** função, permitindo que os consumidores criem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabelas. Os consumidores usam **CreateTable** para criar tabelas permanentes nomeadas pelo consumidor e tabelas permanentes ou temporárias com nomes exclusivos gerados pelo Driver OLE DB para SQL Server.  
  
 Quando o consumidor chama **itabledefinition:: CreateTable**, se o valor da propriedade DBPROP_TBL_TEMPTABLE é VARIANT_TRUE, o Driver OLE DB para SQL Server gera um nome de tabela temporária para o consumidor. O consumidor define o *pTableID* parâmetro o **CreateTable** método como NULL. As tabelas temporárias com nomes gerados pelo Driver OLE DB para SQL Server não aparecem no **tabelas** conjunto de linhas, mas são acessíveis por meio de **IOpenRowset** interface.  
  
 Quando os consumidores especificam o nome da tabela no *pwszName* membro do *uName* união no *pTableID* parâmetro, o Driver OLE DB para SQL Server cria um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]tabela com esse nome. As restrições de nomeação de tabela [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se aplicam, e o nome da tabela pode indicar uma tabela permanente, ou uma tabela temporária local ou global. Para obter mais informações, consulte [CREATE TABLE](../../../t-sql/statements/create-table-transact-sql.md). O *ppTableID* parâmetro pode ser NULL.  
  
 O Driver OLE DB para SQL Server pode gerar os nomes de tabelas permanentes ou temporárias. Quando o consumidor define o *pTableID* parâmetro como NULL e define *ppTableID* para apontar para um DBID válido\*, o Driver OLE DB para SQL Server retorna o nome gerado da tabela no *pwszName* membro o *uName* união do DBID apontado pelo valor de *ppTableID*. Para criar um temporário, OLE DB Driver para tabela nomeadas do SQL Server, o consumidor inclui a propriedade de tabela DBPROP_TBL_TEMPTABLE do OLE DB em uma propriedade de tabela definida referenciada no *rgPropertySets* parâmetro. OLE DB Driver para tabelas temporárias nomeadas do SQL Server são locais.  
  
 **CreateTable** retornará DB_E_BADTABLEID se o *eKind* membro o *pTableID* parâmetro não indica DBKIND_NAME.  
  
## <a name="dbcolumndesc-usage"></a>Uso de DBCOLUMNDESC  
 O consumidor pode indicar um tipo de dados de coluna usando o *pwszTypeName* membro ou *wType* membro. Se o consumidor Especifica o tipo de dados em *pwszTypeName*, o Driver OLE DB para SQL Server ignora o valor de *wType*.  
  
 Se usar o *pwszTypeName* membro, o consumidor Especifica o tipo de dados usando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nomes de tipo de dados. Os nomes de tipo de dados válidos são aqueles retornados na coluna de TYPE_NAME do conjunto de linhas de esquema de PROVIDER_TYPES.  
  
 O Driver OLE DB para SQL Server reconhece um subconjunto de valores DBTYPE enumerados por OLE DB a *wType* membro. Para obter mais informações, consulte [mapeamento de tipo de dados em ITableDefinition](../../oledb/ole-db-data-types/data-type-mapping-in-itabledefinition.md).  
  
> [!NOTE]  
>  **CreateTable** retornará DB_E_BADTYPE se o consumidor define o *pTypeInfo* ou *pclsid* membro para especificar o tipo de dados de coluna.  
  
 O consumidor Especifica o nome da coluna no *pwszName* membro o *uName* união de DBCOLUMNDESC *dbcid* membro. O nome da coluna é especificado como uma cadeia de caracteres Unicode. O *eKind* membro *dbcid* deve ser DBKIND_NAME. **CreateTable** retornará DB_E_BADCOLUMNID se *eKind* é inválido, *pwszName* for NULL, ou se o valor de *pwszName* não é válido [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] identificador.  
  
 Todas as propriedades de coluna estão disponíveis em todas as colunas definidas para a tabela. **CreateTable** poderá retornar DB_S_ERRORSOCCURRED ou DB_E_ERRORSOCCURRED se os valores de propriedade são definidos em conflito. **CreateTable** retorna um erro quando fazem com que as configurações de propriedade de coluna inválido [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Falha na criação de tabela.  
  
 As propriedades de coluna em um DBCOLUMNDESC são interpretadas da seguinte maneira.  
  
|ID da propriedade|Description|  
|-----------------|-----------------|  
|DBPROP_COL_AUTOINCREMENT|Leitura/gravação: leitura/gravação<br /><br /> Padrão: VARIANT_FALSE Descrição: define a propriedade de identidade na coluna criada. Para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a propriedade de identidade é válida para uma única coluna de uma tabela. Definir a propriedade como VARIANT_TRUE para mais de uma única coluna gera um erro quando o Driver OLE DB para SQL Server tenta criar a tabela no servidor.<br /><br /> O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] propriedade de identidade só é válida para o **inteiro**, **numérico**, e **decimal** tipos quando a escala é 0. Definir a propriedade como VARIANT_TRUE em uma coluna de qualquer outro tipo de dados gera um erro quando o Driver OLE DB para SQL Server tenta criar a tabela no servidor.<br /><br /> O Driver OLE DB para SQL Server retorna DB_S_ERRORSOCCURRED quando DBPROP_COL_AUTOINCREMENT e DBPROP_COL_NULLABLE são ambos VARIANT_TRUE e o *dwOption* de DBPROP_COL_NULLABLE não é DBPROPOPTIONS_REQUIRED. DB_E_ERRORSOCCURRED é retornado quando DBPROP_COL_AUTOINCREMENT e DBPROP_COL_NULLABLE são ambos VARIANT_TRUE e o *dwOption* de DBPROP_COL_NULLABLE é igual a DBPROPOPTIONS_REQUIRED. A coluna é definida com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] propriedade de identidade e de DBPROP_COL_NULLABLE *dwStatus* membro é definido como DBPROPSTATUS_CONFLICTING.|  
|DBPROP_COL_DEFAULT|Leitura/gravação: leitura/gravação<br /><br /> Padrão: nenhum<br /><br /> Descrição: Cria uma restrição [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] DEFAULT para a coluna.<br /><br /> O *vValue* membro DBPROP pode ser qualquer um dos vários tipos. O *Vvalue* membro deve especificar um tipo compatível com o tipo de dados da coluna. Por exemplo, a definição de BSTR N/A como o valor padrão para uma coluna definida como DBTYPE_WSTR é uma correspondência compatível. Definir o mesmo padrão em uma coluna definida como DBTYPE_R8 gera um erro quando o Driver OLE DB para SQL Server tenta criar a tabela no servidor.|  
|DBPROP_COL_DESCRIPTION|Leitura/gravação: leitura/gravação<br /><br /> Padrão: nenhum<br /><br /> Descrição: A propriedade de coluna DBPROP_COL_DESCRIPTION não é implementada pelo Driver OLE DB para SQL Server.<br /><br /> O *dwStatus* membro da estrutura DBPROP retorna DBPROPSTATUS_NOTSUPPORTED quando o consumidor tentar escrever o valor da propriedade.<br /><br /> Definindo a propriedade não constitui um erro fatal para o Driver OLE DB para SQL Server. Se todos os outros valores de parâmetro forem válidos, será criada a tabela do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|DBPROP_COL_FIXEDLENGTH|Leitura/gravação: leitura/gravação<br /><br /> Padrão: VARIANT_FALSE<br /><br /> Descrição: O Driver OLE DB para SQL Server usa DBPROP_COL_FIXEDLENGTH para determinar o mapeamento de tipo de dados quando o consumidor define o tipo de dados de uma coluna usando o *wType* membro de DBCOLUMNDESC. Para obter mais informações, consulte [mapeamento de tipo de dados em ITableDefinition](../../oledb/ole-db-data-types/data-type-mapping-in-itabledefinition.md).|  
|DBPROP_COL_NULLABLE|Leitura/gravação: leitura/gravação<br /><br /> Padrão: nenhum<br /><br /> Descrição: Ao criar a tabela, o Driver OLE DB para SQL Server indica se a coluna deve aceitar valores nulos se a propriedade é definida. Quando a propriedade não é definida, a capacidade da coluna de aceitar NULL como valor é determinado pela opção de banco de dados padrão ANSI_NULLS do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> O Driver OLE DB para SQL Server é um provedor compatível com ISO. Sessões conectadas exibem comportamentos de ISO. Se o consumidor não definir DBPROP_COL_NULLABLE, as colunas aceitarão valores nulos.|  
|DBPROP_COL_PRIMARYKEY|Leitura/gravação: leitura/gravação<br /><br /> Padrão: VARIANT_FALSE Descrição: quando VARIANT_TRUE, o Driver OLE DB para SQL Server cria a coluna com uma restrição de chave primária.<br /><br /> Quando definido como uma propriedade de coluna, só uma única coluna pode determinar a restrição. Definição da propriedade como VARIANT_TRUE para mais de uma única coluna gera um erro quando o Driver OLE DB para SQL Server tenta criar a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabela.<br /><br /> Observação: O consumidor pode usar **iindexdefinition:: CreateIndex** para criar uma restrição de chave primária em duas ou mais colunas.<br /><br /> O Driver OLE DB para SQL Server retorna DB_S_ERRORSOCCURRED quando DBPROP_COL_PRIMARYKEY e DBPROP_COL_UNIQUE são ambos VARIANT_TRUE e o *dwOption* de DBPROP_COL_UNIQUE não é DBPROPOPTIONS_REQUIRED.<br /><br /> DB_E_ERRORSOCCURRED é retornado quando DBPROP_COL_PRIMARYKEY e DBPROP_COL_UNIQUE são ambos VARIANT_TRUE e o *dwOption* de DBPROP_COL_UNIQUE é igual a DBPROPOPTIONS_REQUIRED. A coluna é definida com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] propriedade de identidade e o DBPROP_COL_PRIMARYKEY *dwStatus* membro é definido como DBPROPSTATUS_CONFLICTING.<br /><br /> O Driver OLE DB para SQL Server retornará um erro quando DBPROP_COL_PRIMARYKEY e DBPROP_COL_NULLABLE são ambos VARIANT_TRUE.<br /><br /> O Driver OLE DB para SQL Server retornará um erro de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando o consumidor tenta criar uma restrição de chave primária em uma coluna de inválido [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de dados. Restrições de chave primária não podem ser definidas em colunas criadas com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipos de dados **bit**, **texto**, **ntext**, e **imagem**.|  
|DBPROP_COL_UNIQUE|Leitura/gravação: leitura/gravação<br /><br /> Padrão: VARIANT_FALSE Descrição: aplica uma restrição UNIQUE do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] à coluna.<br /><br /> Quando definido como uma propriedade de coluna, a restrição só é aplicada em uma única coluna. O consumidor pode usar **iindexdefinition:: CreateIndex** para aplicar uma restrição exclusiva em valores combinados das duas ou mais colunas.<br /><br /> O Driver OLE DB para SQL Server retorna DB_S_ERRORSOCCURRED quando DBPROP_COL_PRIMARYKEY e DBPROP_COL_UNIQUE são ambos VARIANT_TRUE e *dwOption* não é DBPROPOPTIONS_REQUIRED.<br /><br /> DB_E_ERRORSOCCURRED é retornado quando DBPROP_COL_PRIMARYKEY e DBPROP_COL_UNIQUE são ambos VARIANT_TRUE e *dwOption* é igual a DBPROPOPTIONS_REQUIRED. A coluna é definida com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] propriedade de identidade e o DBPROP_COL_PRIMARYKEY *dwStatus* membro é definido como DBPROPSTATUS_CONFLICTING.<br /><br /> O Driver OLE DB para SQL Server retorna DB_S_ERRORSOCCURRED quando DBPROP_COL_NULLABLE e DBPROP_COL_UNIQUE são ambos VARIANT_TRUE e *dwOption* não é DBPROPOPTIONS_REQUIRED.<br /><br /> DB_E_ERRORSOCCURRED é retornado quando DBPROP_COL_NULLABLE e DBPROP_COL_UNIQUE são ambos VARIANT_TRUE e *dwOption* é igual a DBPROPOPTIONS_REQUIRED. A coluna é definida com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] propriedade de identidade e de DBPROP_COL_NULLABLE *dwStatus* membro é definido como DBPROPSTATUS_CONFLICTING.<br /><br /> O Driver OLE DB para SQL Server retornará um erro de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando o consumidor tenta criar uma restrição exclusiva em uma coluna de inválido [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tipo de dados. Restrições exclusivas não podem ser definidas em colunas criadas com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **bit** tipo de dados.|  
  
 Quando o consumidor chama **itabledefinition:: CreateTable**, o Driver OLE DB para SQL Server interpreta as propriedades de tabela da seguinte maneira.  
  
|ID da propriedade|Description|  
|-----------------|-----------------|  
|DBPROP_TBL_TEMPTABLE|Leitura/gravação: leitura/gravação<br /><br /> Padrão: VARIANT_FALSE Descrição: por padrão, o Driver OLE DB para SQL Server cria tabelas nomeadas pelo consumidor. Quando VARIANT_TRUE, o OLE DB Driver para SQL Server gera um nome de tabela temporária para o consumidor. O consumidor define o *pTableID* parâmetro **CreateTable** como NULL. O *ppTableID* parâmetro deve conter um ponteiro válido.|  
  
 Se o consumidor solicita que um conjunto de linhas seja aberto em uma tabela criada com êxito, o Driver OLE DB para SQL Server abre um conjunto de linhas com suporte de cursor. Qualquer propriedade de conjunto de linhas pode ser indicada nos conjuntos de propriedade passados.  
  
 O exemplo a seguir cria uma tabela do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
```  
// This CREATE TABLE statement shows the details of the table created by   
// the following example code.  
//  
// CREATE TABLE OrderDetails  
// (  
//    OrderID      int      NOT NULL  
//    ProductID   int      NOT NULL  
//    CONSTRAINT PK_OrderDetails  
//         PRIMARY KEY CLUSTERED (OrderID, ProductID),  
//    UnitPrice   money      NOT NULL,  
//    Quantity   int      NOT NULL,  
//    Discount   decimal(2,2)   NOT NULL  
//        DEFAULT 0  
// )  
//  
// The PRIMARY KEY constraint is created in an additional example.  
HRESULT CreateTable  
    (  
    ITableDefinition* pITableDefinition  
    )  
    {  
    DBID            dbidTable;  
    const ULONG     nCols = 5;  
    ULONG           nCol;  
    ULONG           nProp;  
    DBCOLUMNDESC    dbcoldesc[nCols];  
  
    HRESULT         hr;  
  
    // Set up column descriptions. First, set default property values for  
    //  the columns.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        dbcoldesc[nCol].pwszTypeName = NULL;  
        dbcoldesc[nCol].pTypeInfo = NULL;  
        dbcoldesc[nCol].rgPropertySets = new DBPROPSET;  
        dbcoldesc[nCol].pclsid = NULL;  
        dbcoldesc[nCol].cPropertySets = 1;  
        dbcoldesc[nCol].ulColumnSize = 0;  
        dbcoldesc[nCol].dbcid.eKind = DBKIND_NAME;  
        dbcoldesc[nCol].wType = DBTYPE_I4;  
        dbcoldesc[nCol].bPrecision = 0;  
        dbcoldesc[nCol].bScale = 0;  
  
        dbcoldesc[nCol].rgPropertySets[0].rgProperties =   
            new DBPROP[NCOLPROPS_MAX];  
        dbcoldesc[nCol].rgPropertySets[0].cProperties = NCOLPROPS_MAX;  
        dbcoldesc[nCol].rgPropertySets[0].guidPropertySet =  
            DBPROPSET_COLUMN;  
  
        for (nProp = 0; nProp < NCOLPROPS_MAX; nProp++)  
            {  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                dwOptions = DBPROPOPTIONS_REQUIRED;  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].colid  
                 = DB_NULLID;  
  
            VariantInit(  
                &(dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                    vValue));  
  
            dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                vValue.vt = VT_BOOL;  
            }  
        }  
  
    // Set the column-specific information.  
    dbcoldesc[0].dbcid.uName.pwszName = L"OrderID";  
    dbcoldesc[0].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[0].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[0].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[1].dbcid.uName.pwszName = L"ProductID";  
    dbcoldesc[1].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[1].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[1].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[2].dbcid.uName.pwszName = L"UnitPrice";  
    dbcoldesc[2].wType = DBTYPE_CY;  
    dbcoldesc[2].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[2].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[2].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[3].dbcid.uName.pwszName = L"Quantity";  
    dbcoldesc[3].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[3].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[3].rgPropertySets[0].cProperties = 1;  
  
    dbcoldesc[4].dbcid.uName.pwszName = L"Discount";  
    dbcoldesc[4].wType = DBTYPE_NUMERIC;  
    dbcoldesc[4].bPrecision = 2;  
    dbcoldesc[4].bScale = 2;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[0].dwPropertyID =   
        DBPROP_COL_NULLABLE;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[0].vValue.boolVal =   
        VARIANT_FALSE;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].dwPropertyID =   
        DBPROP_COL_DEFAULT;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].vValue.vt = VT_BSTR;  
    dbcoldesc[4].rgPropertySets[0].rgProperties[1].vValue.bstrVal =  
        SysAllocString(L"0");  
    dbcoldesc[4].rgPropertySets[0].cProperties = 2;  
  
    // Set up the dbid for OrderDetails.  
    dbidTable.eKind = DBKIND_NAME;  
    dbidTable.uName.pwszName = L"OrderDetails";  
  
    if (FAILED(hr = pITableDefinition->CreateTable(NULL, &dbidTable,  
        nCols, dbcoldesc, NULL, 0, NULL, NULL, NULL)))  
        {  
        DumpError(pITableDefinition, IID_ITableDefinition);  
        goto SAFE_EXIT;  
        }  
  
SAFE_EXIT:  
    // Clean up dynamic allocation in the property sets.  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        for (nProp = 0; nProp < NCOLPROPS_MAX; nProp++)  
            {  
            if (dbcoldesc[nCol].rgPropertySets[0].rgProperties[nProp].  
                vValue.vt == VT_BSTR)  
                {  
                SysFreeString(dbcoldesc[nCol].rgPropertySets[0].  
                    rgProperties[nProp].vValue.bstrVal);  
                }  
            }  
  
        delete [] dbcoldesc[nCol].rgPropertySets[0].rgProperties;  
        delete [] dbcoldesc[nCol].rgPropertySets;  
        }  
  
    return (hr);  
    }  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas e índices](../../oledb/ole-db-tables-indexes/tables-and-indexes.md)  
  
  

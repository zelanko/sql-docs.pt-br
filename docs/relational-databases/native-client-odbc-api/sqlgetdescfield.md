---
title: SQLGetDescField | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetDescField function
ms.assetid: 3e59a37a-28ee-4c91-8968-7fe3b966739d
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 30a665ee8db2b7de1e0469b7af8d17ec92c2cde8
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35698157"
---
# <a name="sqlgetdescfield"></a>SQLGetDescField
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client expõe campos de descritor específicos de driver para implementação linha IRD (descritor de) apenas. Dentro do IRD, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] campos de descritor são referenciados por meio de atributos de coluna específicos de driver. Para obter informações sobre uma lista completa dos campos de descritor de específicos de driver disponíveis, consulte [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md).  
  
 Os campos de descritor que contêm cadeias de caracteres de identificador de coluna são, em geral, cadeias de comprimento zero. Todos os valores de campos de descritor específicos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são somente leitura.  
  
 Como os atributos recuperados com SQLColAttribute, campos de descritor que os atributos de nível de linha do relatório (como SQL_CA_SS_COMPUTE_ID) são relatados para todas as colunas no conjunto de resultados.  
  
## <a name="sqlgetdescfield-and-table-valued-parameters"></a>SQLGetDescField e parâmetros com valor de tabela  
 SQLGetDescField pode ser usado para obter valores de atributos estendidos de parâmetros com valor de tabela e colunas de parâmetro com valor de tabela. Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;ODBC&#41;](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlgetdescfield-support-for-enhanced-date-and-time-features"></a>Suporte do SQLGetDescField a recursos avançados de data e hora  
 Para obter informações sobre os campos de descritor disponíveis com os tipos de data/hora novo, consulte [parâmetro e metadados de resultado](../../relational-databases/native-client-odbc-date-time/metadata-parameter-and-result.md).  
  
 Para obter mais informações, consulte [data e hora melhorias &#40;ODBC&#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
 A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], pode retornar SQLGetDescField **SQL_C_SS_TIME2** (para **tempo** tipos) ou **SQL_C_SS_TIMESTAMPOFFSET** (para  **DateTimeOffset**) em vez de **SQL_C_BINARY**, se seu aplicativo usar o ODBC 3.8.  
  
## <a name="sqlgetdescfield-support-for-large-clr-udts"></a>Suporte do SQLGetDescField a UDTs de CLR grandes  
 O**SQLGetDescField** dá suporte a UDTs (tipos definidos pelo usuário) de CLR grandes. Para obter mais informações, consulte [Large CLR User-Defined tipos &#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="sqlgetdescfield-support-for-sparse-columns"></a>Suporte do SQLGetDescField a colunas esparsas  
 SQLGetDescField pode ser usado para consultar o novo campo IRD SQL_CA_SS_IS_COLUMN_SET para determinar se uma coluna é uma **column_set** coluna.  
  
 Para obter mais informações, consulte [suporte a colunas esparsas &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sparse-columns-support-odbc.md).  
  
## <a name="example"></a>Exemplo  
  
```  
typedef struct tagCOMPUTEBYLIST  
    {  
    SQLSMALLINT nBys;  
    SQLSMALLINT aByList[1];  
    } COMPUTEBYLIST;  
typedef COMPUTEBYLIST* PCOMPUTEBYLIST;   
  
SQLHDESC    hIRD;   
SQLINTEGER  cbIRD;   
SQLINTEGER  nSet = 0;   
  
// . . .  
// Execute a statement that contains a COMPUTE clause,  
//  then get the descriptor handle of the IRD and  
//  get some IRD values.  
  
SQLGetStmtAttr(g_hStmt, SQL_ATTR_IMP_ROW_DESC,  
    (SQLPOINTER) &hIRD, sizeof(SQLHDESC), &cbIRD);  
  
// For statement-wide column attributes, any  
//  descriptor record will do. You know that 1 exists,  
//  so use it.  
SQLGetDescField(hIRD, 1, SQL_CA_SS_NUM_COMPUTES,  
    (SQLPOINTER) &nComputes, SQL_IS_INTEGER, &cbIRD);  
  
if (nSet == 0)  
    {  
    SQLINTEGER      nOrderID;  
  
    printf_s("Normal result set.\n");  
  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        SQLGetDescField(hIRD, nCol+1,  
            SQL_CA_SS_COLUMN_ORDER,  
            (SQLPOINTER) &nOrderID, SQL_IS_INTEGER,  
            &cbIRD);  
  
        if (nOrderID != 0)  
            {  
            printf_s("Col in ORDER BY, pos: %ld",  
                nOrderID);  
            }  
            printf_s("\n");  
        }  
  
    printf_s("\n");  
    }  
else  
    {  
    PCOMPUTEBYLIST  pByList;  
    SQLSMALLINT     nBy;  
    SQLINTEGER      nColID;  
  
    printf_s("Computed result set number: %lu\n",  
        nSet);  
  
    SQLGetDescField(hIRD, 1, SQL_CA_SS_COMPUTE_BYLIST,  
        (SQLPOINTER) &pByList, SQL_IS_INTEGER,  
        &cbIRD);  
  
    if (pByList != NULL)  
        {  
        printf_s("Clause ordered by columns: ");  
        for (nBy = 0; nBy < pByList->nBys; )  
            {  
            printf_s("%u", pByList->aByList[nBy]);  
            nBy++;  
  
            if (nBy == pByList->nBys)  
                {  
                printf_s("\n");  
                }  
            else  
                {  
                printf_s(", ");  
                }  
            }  
        }  
    else  
        {  
        printf_s("Compute clause set not ordered.\n");  
        }  
  
    for (nCol = 0; nCol < nCols; nCol++)  
        {  
        SQLGetDescField(hIRD, nCol+1,  
            SQL_CA_SS_COLUMN_ID, (SQLPOINTER) &nColID,  
            SQL_IS_INTEGER, &cbIRD);  
        printf_s("ColumnID: %lu, nColID);  
        }  
    printf_s("\n");  
    }  
  
if (SQLMoreResults(g_hStmt) == SQL_SUCCESS)  
    {  
    // Determine the result set indicator.  
    SQLGetDescField(hIRD, 1, SQL_CA_SS_COMPUTE_ID,  
        (SQLPOINTER) &nSet, SQL_IS_INTEGER, &cbIRD);  
    }  
```  
  
## <a name="see-also"></a>Consulte também  
 [Função SQLGetDescField](http://go.microsoft.com/fwlink/?LinkId=59351)   
 [Detalhes da implementação da API do ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  

---
title: Usando a classificação de dados com Microsoft ODBC Driver for SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver
ms.assetid: f78b81ed-5214-43ec-a600-9bfe51c5745a
author: v-makouz
ms.author: v-makouz
manager: kenvh
ms.openlocfilehash: 8f0f821890cabe25a9abb572e453c9846c75ec94
ms.sourcegitcommit: 512acc178ec33b1f0403b5b3fd90e44dbf234327
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/08/2019
ms.locfileid: "72041135"
---
# <a name="data-classification"></a>Classificação de dados
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="overview"></a>Visão geral
Com a finalidade de gerenciar dados confidenciais, o SQL Server e o SQL Server do Azure introduziram a capacidade de fornecer colunas de dados com metadados de sensibilidade que permitem ao aplicativo cliente lidar com diferentes tipos de informações confidenciais (como saúde, financeira etc. ) de acordo com as políticas de proteção de dados.

Para obter mais informações sobre como atribuir classificação a colunas, consulte [descoberta e classificação de dados SQL](https://docs.microsoft.com/sql/relational-databases/security/sql-data-discovery-and-classification?view=sql-server-2017).

O Microsoft ODBC Driver 17,2 permite a recuperação desses metadados por meio de SQLGetDescField usando o identificador de campo SQL_CA_SS_DATA_CLASSIFICATION.

## <a name="format"></a>Formato
SQLGetDescField tem a seguinte sintaxe:

```  
SQLRETURN SQLGetDescField(  
     SQLHDESC        DescriptorHandle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     FieldIdentifier,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```
*DescriptorHandle*  
 Entrada Identificador de IRD (descritor de linha de implementação). Pode ser recuperado por uma chamada para SQLGetStmtAttr com o atributo de instrução SQL_ATTR_IMP_ROW_DESC
  
 *RecNumber*  
 [Input] 0
  
 *FieldIdentifier*  
 [Entrada] SQL_CA_SS_DATA_CLASSIFICATION
  
 *ValuePtr*  
 Der Buffer de saída
  
 *BufferLength*  
 Entrada Comprimento do buffer de saída em bytes

 *StringLengthPtr* [output] aponta para o buffer no qual retornar o número total de bytes disponíveis para retornar em *ValuePtr*.
 
> [!NOTE]
> Se o tamanho do buffer for desconhecido, ele poderá ser determinado chamando SQLGetDescField com *ValuePtr* como nulo e examinando o valor de *StringLengthPtr*.
 
Se as informações de classificação de dados não estiverem disponíveis, um erro de *campo de descritor inválido* será retornado.

Após uma chamada bem-sucedida para SQLGetDescField, o buffer apontado por *ValuePtr* conterá os seguintes dados:

 `nn nn [n sensitivitylabels] tt tt [t informationtypes] cc cc [c columnsensitivitys]`

> [!NOTE]
> `nn nn`, `tt tt` e `cc cc` são inteiros multibyte, que são armazenados com o byte menos significativo no endereço mais baixo.

*`sensitivitylabel`* e *`informationtype`* estão no formato

 `nn [n bytes name] ii [i bytes id]`

*`columnsensitivity`* está no formato

 `nn nn [n sensitivityprops]`

Para cada coluna *(c)* , *n* 4 bytes *`sensitivityprops`* estão presentes:

 `ss ss tt tt`

índice s na matriz *`sensitivitylabels`* , `FF FF` se não rotulado

índice t na matriz *`informationtypes`* , `FF FF` se não rotulado


<br><br>
O formato dos dados pode ser expresso como as seguintes pseudos estruturas:

```
struct IDnamePair {
 BYTE nameLen;
 USHORT name[nameLen];
 BYTE idLen;
 USHORT id[idLen];
};

struct SensitivityProp {
 USHORT labelIdx;
 USHORT infoTypeIdx;
};

USHORT nLabels;
struct IDnamePair labels[nLabels];
USHORT nInfoTypes;
struct IDnamePair infotypes[nInfoTypes];
USHORT nColumns;
struct {
 USHORT nProps;
 struct SensitivityProp[nProps];
} columnClassification[nColumns];
```


## <a name="code-sample"></a>Exemplo de código
Aplicativo de teste que demonstra como ler metadados de classificação de dados. No Windows, ele pode ser compilado usando `cl /MD dataclassification.c /I (directory of msodbcsql.h) /link odbc32.lib` e executado com uma cadeia de conexão e uma consulta SQL (que retorna colunas classificadas) como parâmetros:

```
#ifdef _WIN32
#include <windows.h>
#endif
#include <sql.h>
#include <sqlext.h>
#include <msodbcsql.h>
#include <stdio.h>
SQLHANDLE env, dbc, stmt;
void checkRC_exit(SQLRETURN rc, SQLHANDLE hand, SQLSMALLINT htype, int retcode, char *action)
{
    if ((rc == SQL_ERROR || rc == SQL_SUCCESS_WITH_INFO) && hand)
    {
        char msg[1024], state[6];
        int i = 0;
        SQLRETURN rc2;
        SQLINTEGER err;
        SQLSMALLINT lenout;
        while ((rc2 = SQLGetDiagRec(htype, hand, ++i, state, &err, msg, sizeof(msg), &lenout)) == SQL_SUCCESS ||
            rc2 == SQL_SUCCESS_WITH_INFO)
            printf("%d (%d)[%s]%s\n", i, err, state, msg);
    }
    if (rc == SQL_ERROR && retcode)
    {
        printf("Error occurred%s%s\n", action ? " upon " : "", action ? action : "");
        exit(retcode);
    }
}
void printLabelInfo(char *type, char **pptr)
{
    char *ptr = *pptr;
    unsigned short nlabels;
    printf("----- %s(%u) -----\n", type, nlabels = *(unsigned short*)ptr);
    ptr += sizeof(unsigned short);
    while (nlabels--)
    {
        int namelen, idlen;
        char *nameptr, *idptr;
        namelen = *ptr++;
        nameptr = ptr;
        ptr += namelen * 2;
        idlen = *ptr++;
        idptr = ptr;
        ptr += idlen * 2;
        wprintf(L"Name: \"%.*s\" Id: \"%.*s\"\n", namelen, nameptr, idlen, idptr);
    }
    *pptr = ptr;
}
int main(int argc, char **argv)
{
    unsigned char *dcbuf;
    unsigned int dclen = 0;
    SQLRETURN rc;
    SQLHANDLE ird;
    if (argc < 3)
    {
        fprintf(stderr, "usage: dataclassification connstr query\n");
        return 1;
    }
    checkRC_exit(SQLAllocHandle(SQL_HANDLE_ENV, 0, &env), 0, 0,
        2, "allocate environment");
    checkRC_exit(SQLSetEnvAttr(env, SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, 0), env, SQL_HANDLE_ENV,
        3, "set ODBC version");
    checkRC_exit(SQLAllocHandle(SQL_HANDLE_DBC, env, &dbc), env, SQL_HANDLE_ENV,
        4, "allocate connection");
    checkRC_exit(SQLDriverConnect(dbc, 0, argv[1], SQL_NTS, 0, 0, 0, SQL_DRIVER_NOPROMPT), dbc, SQL_HANDLE_DBC,
        5, "connect to server");
    checkRC_exit(SQLAllocHandle(SQL_HANDLE_STMT, dbc, &stmt), dbc, SQL_HANDLE_DBC,
        6, "allocate statement");
    checkRC_exit(SQLExecDirect(stmt, argv[2], SQL_NTS), stmt, SQL_HANDLE_STMT,
        7, "execute query");
    checkRC_exit(SQLGetStmtAttr(stmt, SQL_ATTR_IMP_ROW_DESC, (SQLPOINTER)&ird, SQL_IS_POINTER, 0), stmt, SQL_HANDLE_STMT,
        8, "get IRD handle");
    rc = SQLGetDescFieldW(ird, 0, SQL_CA_SS_DATA_CLASSIFICATION, dcbuf, 0, &dclen);
    if (rc != SQL_SUCCESS && rc != SQL_SUCCESS_WITH_INFO)
    {
        checkRC_exit(rc, ird, SQL_HANDLE_DESC, 0, 0);
        printf("Error reading SQL_CA_SS_DATA_CLASSIFICATION IRD field. Ensure that the driver and\n"
            "server both support the Data Classification feature, and that the query returns columns\n"
            "with classification information.\n");
    }
    else
    {
        SQLINTEGER dclenout;
        unsigned char *dcptr;
        unsigned short ncols;
        printf("Data Classification information (%u bytes):\n", dclen);
        if (!(dcbuf = malloc(dclen)))
        {
            printf("Memory Allocation Error");
            return 9;
        }
        checkRC_exit(SQLGetDescFieldW(ird, 0, SQL_CA_SS_DATA_CLASSIFICATION, dcbuf, dclen, &dclenout),
            ird, SQL_HANDLE_DESC, 10, "reading SQL_CA_SS_DATA_CLASSIFICATION");
        dcptr = dcbuf;
        printLabelInfo("Labels", &dcptr);
        printLabelInfo("Information Types", &dcptr);
        printf("----- Column Sensitivities(%u) -----\n", ncols = *(unsigned short*)dcptr);
        dcptr += sizeof(unsigned short);
        while (ncols--)
        {
            unsigned short nprops = *(unsigned short*)dcptr;
            dcptr += sizeof(unsigned short);
            while (nprops--)
            {
                unsigned short labelidx, typeidx;
                labelidx = *(unsigned short*)dcptr; dcptr += sizeof(unsigned short);
                typeidx = *(unsigned short*)dcptr; dcptr += sizeof(unsigned short);
                printf(labelidx == 0xFFFF ? "(none) " : "%u ", labelidx);
                printf(typeidx == 0xFFFF ? "(none)\n" : "%u\n", typeidx);
            }
            printf("-----\n");
        }
        if (dcptr != dcbuf + dclen)
        {
            printf("Error: unexpected parse of DATACLASSIFICATION data\n");
            return 11;
        }
        free(dcbuf);
    }
    return 0;
}
```

## <a name="bkmk-version"></a>Versão com suporte
O Microsoft ODBC Driver 17,2 permite as informações de classificação de dados de recuperação por meio de `SQLGetDescField` se `FieldIdentifier` estiver definido como `SQL_CA_SS_DATA_CLASSIFICATION` (1237). 

A partir do Microsoft ODBC Driver 17.4.1.1, é possível recuperar a versão da classificação de dados com suporte por um servidor via `SQLGetDescField` usando o identificador de campo `SQL_CA_SS_DATA_CLASSIFICATION_VERSION` (1238). Em 17.4.1.1, a versão de classificação de dados com suporte é definida como "2".

 

A partir de 17.4.2.1 introduziu a versão padrão da classificação de dados que está definida como "1" e é o driver de versão que está relatando para SQL Server com suporte. O novo atributo de conexão `SQL_COPT_SS_DATACLASSIFICATION_VERSION` (1400) pode permitir que o aplicativo altere a versão com suporte da classificação de dados de "1" até o máximo com suporte.  

Exemplo: 

Para definir a versão, essa chamada deve ser feita imediatamente antes da chamada de SQLConnect ou SQLDriverConnect:
```
ret = SQLSetConnectAttr(dbc, SQL_COPT_SS_DATACLASSIFICATION_VERSION, (SQLPOINTER)2, SQL_IS_INTEGER);
```

O valor da versão com suporte no momento da classificação de dados pode ser retirved por meio da chamada SQLGetConnectAttr: 
```
ret = SQLGetConnectAttr(dbc, SQL_COPT_SS_DATACLASSIFICATION_VERSION, (SQLPOINTER)&dataClassVersion, SQL_IS_INTEGER, 0);
```


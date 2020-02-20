---
title: Como usar a Classificação de Dados com o Microsoft ODBC Driver for SQL Server | Microsoft Docs
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
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "72041135"
---
# <a name="data-classification"></a>Classificação de dados
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="overview"></a>Visão geral
Com a finalidade de gerenciar dados confidenciais, o SQL Server e o SQL Server do Azure introduziram a capacidade de fornecer colunas de bancos de dados com metadados de sensibilidade que permitem ao aplicativo cliente lidar com diferentes tipos de dados confidenciais (como saúde, finanças etc.) de acordo com as políticas de proteção de dados.

Para obter mais informações sobre como atribuir classificação a colunas, confira [Descoberta e classificação de dados SQL](https://docs.microsoft.com/sql/relational-databases/security/sql-data-discovery-and-classification?view=sql-server-2017).

O Microsoft ODBC Driver 17.2 permite a recuperação desses metadados por meio de SQLGetDescField usando o identificador de campo SQL_CA_SS_DATA_CLASSIFICATION.

## <a name="format"></a>Formatar
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
 [Entrada] Identificador de IIRD (descritor de linha de implementação). Pode ser recuperado por uma chamada para SQLGetStmtAttr com o atributo de instrução SQL_ATTR_IMP_ROW_DESC
  
 *RecNumber*  
 [Input] 0
  
 *FieldIdentifier*  
 [Entrada] SQL_CA_SS_DATA_CLASSIFICATION
  
 *ValuePtr*  
 [Saída] Buffer de saída
  
 *BufferLength*  
 [Entrada] Comprimento do buffer de saída em bytes

 *StringLengthPtr* [Saída] Ponteiro para o buffer no qual se deve retornar o número total de bytes disponível para retornar em *ValuePtr*.
 
> [!NOTE]
> Se o tamanho do buffer for desconhecido, ele poderá ser determinado chamando SQLGetDescField com *ValuePtr* como NULL e examinando o valor de *StringLengthPtr*.
 
Se as informações de classificação de dados não estiverem disponíveis, um erro de *Campo Descritor Inválido* será retornado.

Após uma chamada bem-sucedida para SQLGetDescField, o buffer apontado por *ValuePtr* conterá os seguintes dados:

 `nn nn [n sensitivitylabels] tt tt [t informationtypes] cc cc [c columnsensitivitys]`

> [!NOTE]
> `nn nn`, `tt tt` e `cc cc` são inteiros multibyte, que são armazenados com o byte menos significativo no endereço mais baixo.

*`sensitivitylabel`* e *`informationtype`* são ambos do formulário

 `nn [n bytes name] ii [i bytes id]`

*`columnsensitivity`* é do formulário

 `nn nn [n sensitivityprops]`

Para cada coluna *(c)* , *n* *`sensitivityprops`* s de 4 bytes estão presentes:

 `ss ss tt tt`

s – índice na matriz *`sensitivitylabels`* , `FF FF` se não rotulado

t – índice na matriz *`informationtypes`* , `FF FF` se não rotulado


<br><br>
O formato dos dados pode ser expresso como nas seguintes pseudoestruturas:

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

## <a name="bkmk-version"></a>Versão compatível
O Microsoft ODBC Driver 17.2 permite recuperação de informações de classificação de dados por meio de `SQLGetDescField` se `FieldIdentifier` está definido como `SQL_CA_SS_DATA_CLASSIFICATION` (1237). 

Na versão 17.4.1.1 do Microsoft ODBC Driver e em versões posteriores, é possível recuperar a versão da Classificação de Dados compatível com um servidor por meio de `SQLGetDescField` usando o identificador de campo `SQL_CA_SS_DATA_CLASSIFICATION_VERSION` (1238). Na 17.4.1.1, a versão de classificação de dados compatível é definida como "2".

 

Na versão 17.4.2.1, foi introduzida a definição da versão padrão da classificação de dados como "1", que é a versão que o driver está relatando para o SQL Server como compatível. O novo atributo de conexão `SQL_COPT_SS_DATACLASSIFICATION_VERSION` (1400) pode permitir que o aplicativo altere a versão compatível da classificação de dados de "1" até o valor máximo compatível.  

Exemplo: 

Para definir a versão, essa chamada deve ser feita imediatamente antes da chamada a SQLConnect ou SQLDriverConnect:
```
ret = SQLSetConnectAttr(dbc, SQL_COPT_SS_DATACLASSIFICATION_VERSION, (SQLPOINTER)2, SQL_IS_INTEGER);
```

O valor da versão da Classificação de Dados compatível no momento pode ser recuperada por meio de uma chamada a SQLGetConnectAttr: 
```
ret = SQLGetConnectAttr(dbc, SQL_COPT_SS_DATACLASSIFICATION_VERSION, (SQLPOINTER)&dataClassVersion, SQL_IS_INTEGER, 0);
```


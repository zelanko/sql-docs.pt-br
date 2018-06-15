---
title: Recuperar dados numéricos com SQL_NUMERIC_STRUCT | Microsoft Docs
description: C/C++ usando o ODBC recupera o tipo de dados numérico do SQL Server usando SQL_NUMERIC_STRUCT, relacionados a SQL_C_NUMERIC.
documentationCenter: ''
authors: MightyPen
manager: craigg
editor: ''
ms.prod: sql
ms.prod_service: connectivity
ms.suite: sql
ms.technology: dbe-data-tier-apps
ms.devlang: C++
ms.topic: conceptual
ms.custom: ''
ms.tgt_pltfrm: NA
ms.date: 07/13/2017
ms.author: genemi
ms.openlocfilehash: 57bd5ffbe1adb9c0ecbefda8d99434767ed6c3e0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913221"
---
# <a name="retrieve-numeric-data-with-sqlnumericstruct"></a>Recuperar dados numéricos com SQL\_NUMÉRICO\_STRUCT

Este artigo descreve como recuperar dados numéricos do driver ODBC do SQL Server em uma estrutura numérica. Ele também descreve como obter os valores corretos usando precisão específica e os valores de escala.

Esse tipo de dados permite que os aplicativos lidar diretamente com dados numéricos. Uma solução alternativa para o ano de 2003, ODBC 3.0 introduziu um novo tipo de dados do ODBC C, identificado por **SQL\_C\_NUMÉRICO**. Esse tipo de dados ainda é relevante a partir de 2017.

O buffer de C que será usado tem a definição de tipo de **SQL\_NUMÉRICO\_STRUCT**. Essa estrutura tem campos para armazenar a precisão, escala, logon e o valor dos dados numéricos. O valor em si é armazenado como um inteiro dimensionado com o início de byte menos significativo na posição mais à esquerda. 

O artigo [tipos de dados C](c-data-types.md) fornece mais informações sobre o formato e o uso do SQL\_NUMÉRICO\_STRUCT. Geralmente o [Apêndice D](appendix-d-data-types.md) de referência do programador de ODBC 3.0 aborda os tipos de dados.


## <a name="sqlnumericstruct-overview"></a>SQL\_NUMÉRICO\_visão geral da estrutura


O SQL\_NUMÉRICO\_STRUCT é definido no arquivo de cabeçalho sqlext da seguinte maneira:


``` C
#define SQL_MAX_NUMERIC_LEN    16
typedef struct tagSQL_NUMERIC_STRUCT
{
   SQLCHAR    precision;
   SQLSCHAR   scale;
   SQLCHAR    sign;   /* 1 if positive, 0 if negative */
   SQLCHAR    val[SQL_MAX_NUMERIC_LEN];
} SQL_NUMERIC_STRUCT;
```

            
Os campos de precisão e escala da estrutura numérica nunca são usados para entrada de um aplicativo, apenas para a saída de driver para o aplicativo.

O driver usa a precisão padrão (definido pelo driver) e a escala padrão (0) sempre que retornar dados para o aplicativo. A menos que o aplicativo especifica valores de precisão e escala, o driver assume o padrão e trunca a parte decimal dos dados numéricos.

## <a name="sqlnumericstruct-code-sample"></a>SQL\_NUMÉRICO\_exemplo de código de estrutura

Este exemplo de código mostra como para:

- Defina a precisão.
- Defina a escala.
- Recupere os valores corretos. 

> [!Note]
> QUALQUER USO QUE VOCÊ O CÓDIGO FORNECIDO NESTE ARTIGO É DE SUA RESPONSABILIDADE. 
>
> A Microsoft fornece estes exemplos de código "como está" sem garantias de qualquer tipo, expressas ou implícitas, incluindo, mas não limitado a garantias implícitas de comercialização e/ou adequação a uma finalidade específica.

``` C
#include <stdio.h>
#include <string.h>
#include <conio.h>
#include <stdlib.h>
#include <ctype.h>
#include <windows.h>
#include <sql.h>
#include <sqlext.h>

#define MAXDSN       25
#define MAXUID       25
#define MAXAUTHSTR   25
#define MAXBUFLEN   255

SQLHENV     henv   = SQL_NULL_HENV;
SQLHDBC     hdbc1  = SQL_NULL_HDBC;     
SQLHSTMT    hstmt1 = SQL_NULL_HSTMT;
SQLHDESC    hdesc  = NULL;


SQL_NUMERIC_STRUCT NumStr;

int main()
{
   RETCODE retcode;

//Change the values below as appropriate to make a successful connection.
//szDSN: DataSourceName, szUID=userid, szAuthStr: password

UCHAR szDSN[MAXDSN+1] = "sql33",szUID[MAXUID+1]="sa", szAuthStr[MAXAUTHSTR+1] = "";
SQLINTEGER strlen1;
SQLINTEGER a;
int i,sign =1;
long myvalue, divisor;
float final_val;
   
// Allocate the Environment handle. Set the Env attribute, allocate the
//connection handle, connect to the database and allocate the statement //handle.

retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);
retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION,(SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);
retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);
retcode = SQLConnect(hdbc1, szDSN,SQL_NTS,szUID,SQL_NTS,szAuthStr,SQL_NTS);
retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc1, &hstmt1);

// Execute the select statement. Here it is assumed that numeric_test
//table is created using the following statements:

// Create table numeric_test (col1 numeric(5,3))
//insert into numeric_test values (25.212)

retcode = SQLExecDirect(hstmt1,(UCHAR *)"select * from numeric_test",SQL_NTS);

// Use SQLBindCol to bind the NumStr to the column that is being retrieved.

retcode = SQLBindCol(hstmt1,1,SQL_C_NUMERIC,&NumStr,19,&strlen1);

// Get the application row descriptor for the statement handle using
//SQLGetStmtAttr.

retcode = SQLGetStmtAttr(hstmt1, SQL_ATTR_APP_ROW_DESC,&hdesc, 0, NULL);

// You can either use SQLSetDescRec or SQLSetDescField when using
// SQLBindCol. However, if you prefer to call SQLGetData, you have to
// call SQLSetDescField instead of SQLSetDescRec. For more information on
// descriptors, please refer to the ODBC 3.0 Programmers reference or
// your Online documentation.

//Used when using SQLSetDescRec
//a=b=sizeof(NumStr);

// Set the datatype, precision and scale fields of the descriptor for the 
//numeric column. Otherwise the default precision (driver defined) and 
//scale (0) are returned.

// In this case, the table contains only one column, hence the second 
//parameter contains one. Zero applies to bookmark columns. Please check 
//the programmers guide for more information.

//retcode=SQLSetDescRec(hdesc,1,SQL_NUMERIC,NULL,sizeof(NumStr),5,3,&NumStr,&a,&b);

retcode = SQLSetDescField (hdesc,1,SQL_DESC_TYPE,(VOID*)SQL_C_NUMERIC,0);
retcode = SQLSetDescField (hdesc,1,SQL_DESC_PRECISION,(VOID*) 5,0);
retcode = SQLSetDescField (hdesc,1,SQL_DESC_SCALE,(VOID*) 3,0);
    
// Initialize the val array in the numeric structure.

memset(NumStr.val,0,16);
   
// Call SQLFetch to fetch the first record.

while((retcode =SQLFetch(hstmt1)) != SQL_NO_DATA)
  {
// Notice that the TargetType (3rd Parameter) is SQL_ARD_TYPE, which  
//forces the driver to use the Application Row Descriptor with the 
//specified scale and precision.

   retcode = SQLGetData(hstmt1, 1, SQL_ARD_TYPE, &NumStr, 19, &a); 

// Check for null indicator.

   if ( SQL_NULL_DATA == a )
   {
   printf( "The final value: NULL\n" );
   continue;
   }

// Call to convert the little endian mode data into numeric data.

   myvalue = strtohextoval();

// The returned value in the above code is scaled to the value specified
//in the scale field of the numeric structure. For example 25.212 would
//be returned as 25212. The scale in this case is 3 hence the integer 
//value needs to be divided by 1000.

   divisor = 1;
   if(NumStr.scale > 0)
     {
    for (i=0;i< NumStr.scale; i++)   
         divisor = divisor * 10;
     }
   final_val =  (float) myvalue /(float) divisor;

// Examine the sign value returned in the sign field for the numeric
//structure.
//NOTE: The ODBC 3.0 spec required drivers to return the sign as 
//1 for positive numbers and 2 for negative number. This was changed in the
//ODBC 3.5 spec to return 0 for negative instead of 2.

      if(!NumStr.sign) sign = -1;
      else sign  =1;

   final_val *= sign;
   printf("The final value: %f\n",final_val);
    }

   while ( ( retcode = SQLMoreResults(hstmt1) ) != SQL_NO_DATA_FOUND);

   /* clean up */ 
   SQLFreeHandle(SQL_HANDLE_STMT, hstmt1);
   SQLDisconnect(hdbc1);
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);
   SQLFreeHandle(SQL_HANDLE_ENV, henv);
   return(0);
}
```


### <a name="interim-results"></a>Resultados intermediários:


```
//  C  ==> 12 * 1    =     12
//  7  ==> 07 * 16   =    112
//  2  ==> 02 * 256  =    512
//  6  ==> 06 * 4096 =  24576
===============================
                 Sum =  25212
```


Na estrutura de numérico, o campo de valor é uma matriz de caracteres de 16 elementos. Por exemplo, 25.212 é dimensionada 25212 e a escala é 3. Em formato hexadecimal esse número deve ser c 627.

O driver retorna os seguintes itens:

- O caractere equivalente de 7C, que é ' |' (redirecionar) no primeiro elemento da matriz de caracteres.
- O equivalente de 62, que é 'b' o segundo elemento.
- O restante dos elementos da matriz contêm zeros, portanto, o buffer contém ' | b \ 0 '.

Agora, o desafio é construir o inteiro dimensionado sem essa matriz de cadeia de caracteres. Cada caractere na cadeia de caracteres corresponde a dois dígitos hexadecimais, digamos que menos significativo (LSD) e mais significativos dígitos (MSD). O valor inteiro em escala pode ser gerado multiplicando cada dígito (LSD & MSD) com um múltiplo de 16, começando com 1.

Código que implementa a conversão de modo endian pequeno para o inteiro em escala. É responsabilidade do desenvolvedor do aplicativo para implementar essa funcionalidade. O exemplo de código a seguir é apenas uma das maneiras possíveis.


``` C
long strtohextoval()
{
    long val=0,value=0;
    int i=1,last=1,current;
    int a=0,b=0;

        for(i=0;i<=15;i++)
        {
         current = (int) NumStr.val[i];
         a= current % 16; //Obtain LSD
         b= current / 16; //Obtain MSD
            
         value += last* a;   
         last = last * 16;   
         value += last* b;
         last = last * 16;   
        }
     return value;
}
```


### <a name="applies-to-versions"></a>Se aplica a versões


As informações anteriores sobre SQL\_NUMÉRICO\_STRUCT se aplica às seguintes versões do produto:

- Microsoft ODBC Driver para Microsoft SQL Server 3.7
- Microsoft Data Access Components 2.1
- Microsoft Data Access Components 2.5
- Microsoft Data Access Components 2.6
- Microsoft Data Access Components 2.7


## <a name="sqlcnumeric-overview"></a>SQL\_C\_visão geral NUMÉRICO


O programa de exemplo a seguir ilustra o uso do SQL\_C\_NUMÉRICO, inserindo 123,45 em uma tabela. Na tabela, a coluna é definida como um numérico ou um decimal com precisão 5 e 2 da escala.

O driver ODBC que você usa para executar este programa deve dar suporte à funcionalidade de ODBC 3.0.


``` C
#include <windows.h>
#include <sql.h>
#include <sqlext.h>

void main() {

   SQLHENV    henv  = NULL;
   SQLHDBC    hdbc  = NULL;
   SQLHSTMT   hstmt = NULL;

   SQL_NUMERIC_STRUCT   NumStr;
   SQLINTEGER           cbNumStr = sizeof (NumStr);

   SQLAllocHandle(SQL_HANDLE_ENV, NULL, &henv);

   /* Set the ODBC behavior version. */ 
   SQLSetEnvAttr(henv,
         SQL_ATTR_ODBC_VERSION,
         (SQLPOINTER) SQL_OV_ODBC3,
         SQL_IS_INTEGER);

   SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);

   /* Substitute your own connection information */ 
   SQLConnect(hdbc,
      (SQLCHAR *) "MyDSN", 5,
      (SQLCHAR *) "UserID", 6,
      (SQLCHAR *) "Password", 8);

   SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);

   /*
      Set up the SQL_NUMERIC_STRUCT, NumStr, to hold "123.45".

      First, we need to scale 123.45 to an integer: 12345
      One way to switch the bytes is to convert 12345 to Hex:  0x3039
      Since the least significant byte will be stored starting from the
      leftmost byte, "0x3039" will be stored as "0x3930".

      The precision and scale fields are not used for input to the driver,
      only for output from the driver. The precision and scale will be set
      in the application parameter descriptor later.
   */ 

   NumStr.sign = 1;   /* 1 if positive, 2 if negative */ 

   memset (NumStr.val, 0, 16);
   NumStr.val [0] = 0x39;
   NumStr.val [1] = 0x30;

   /* SQLBindParameter needs to be called before SQLSetDescField */ 
   SQLBindParameter(hstmt,
          1,
          SQL_PARAM_INPUT,
          SQL_C_NUMERIC,
          SQL_NUMERIC,
          5,
          2,
          &NumStr,
          0,
          (SQLINTEGER *) &cbNumStr);

   /* Modify the fields in the implicit application parameter descriptor */ 
   SQLHDESC   hdesc = NULL;

   SQLGetStmtAttr(hstmt, SQL_ATTR_APP_PARAM_DESC, &hdesc, 0, NULL);
   SQLSetDescField(hdesc, 1, SQL_DESC_TYPE, (SQLPOINTER) SQL_C_NUMERIC, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_PRECISION, (SQLPOINTER) 5, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_SCALE, (SQLPOINTER) 2, 0);
   SQLSetDescField(hdesc, 1, SQL_DESC_DATA_PTR, (SQLPOINTER) &NumStr, 0);

   SQLExecDirect(hstmt,
         (SQLCHAR *) "INSERT INTO table (numeric_column) VALUES (?)",
         SQL_NTS);

   SQLFreeHandle(SQL_HANDLE_STMT, hstmt);

   SQLDisconnect (hdbc);

   SQLFreeHandle(SQL_HANDLE_DBC, hdbc);
   SQLFreeHandle(SQL_HANDLE_ENV, henv);
}
```


<!--
GeneMi historical notes, 2017/July/12. Per Jason.C

http://go.microsoft.com/fwlink/?LinkId=147596

https://support.microsoft.com/en-us/help/222831

http://web.archive.org/web/20140319133434/http:/support.microsoft.com:80/kb/222831

http://web.archive.org/web/20080505073901/http:/support.microsoft.com:80/kb/181254

https://docs.microsoft.com/en-us/sql/odbc/reference/appendixes/c-data-types
-->


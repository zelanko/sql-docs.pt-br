---
title: bcp_init | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-extensions-bulk-copy-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- bcp_init
apilocation:
- sqlncli11.dll
apitype: DLLExport
helpviewer_keywords:
- bcp_init function
ms.assetid: 6a25862c-7f31-4873-ab65-30f3abde89d2
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 174c487c16f9e76fec6493dac0c77db15394df8d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32948231"
---
# <a name="bcpinit"></a>bcp_init
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Inicializa a operação de cópia em massa.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RETCODE bcp_init (  
        HDBC hdbc,  
        LPCTSTR szTable,  
        LPCTSTR szDataFile,  
        LPCTSTR szErrorFile,  
        INT eDirection);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HDBC*  
 É o identificador de conexão ODBC habilitado para cópia em massa.  
  
 *szTable*  
 É o nome da tabela do banco de dados a ser copiada de ou para. Este nome também pode incluir o nome do banco de dados ou o nome do proprietário. Por exemplo, **pubs.gracie.titles**, **pubs... títulos**, **gracie**, e **títulos** são todos os nomes de tabela válidos.  
  
 Se *eDirection* for DB_OUT, *szTable* também pode ser o nome de uma exibição de banco de dados.  
  
 Se *eDirection* for DB_OUT e uma instrução SELECT é especificada usando [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) antes de [bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md) é chamado, **bcp_init** *szTable* deve ser definido como NULL.  
  
 *szDataFile*  
 É o nome do arquivo de usuário a ser copiado de ou para. Se os dados estão sendo copiados diretamente de variáveis usando [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md), defina *szDataFile* como NULL.  
  
 *szErrorFile*  
 É o nome do arquivo de erro a ser preenchido com mensagens de progresso, mensagens de erro e cópias das linhas que, por algum motivo, não puderam ser copiadas de um arquivo de usuário para uma tabela. Se NULL for passado como *szErrorFile*, nenhum arquivo de erro será usado.  
  
 *eDirection*  
 É a direção da cópia, DB_IN ou DB_OUT. DB_IN indica uma cópia de variáveis do programa ou de um arquivo de usuário para uma tabela. DB_OUT indica uma cópia de uma tabela do banco de dados para um arquivo de usuário. Especifique um nome de arquivo de usuário com DB_OUT.  
  
## <a name="returns"></a>Retorna  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Remarks  
 Chamar **bcp_init** antes de chamar qualquer outra função de cópia em massa. **bcp_init** executa as inicializações necessárias para uma cópia em massa de dados entre a estação de trabalho e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O **bcp_init** função deve ser fornecida com um identificador de conexão ODBC habilitado para uso com funções de cópia em massa. Para habilitar o identificador, use [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) com SQL_COPT_SS_BCP definido como SQL_BCP_ON em um identificador de conexão alocado, mas não conectado. A tentativa de atribuir o atributo em um identificador conectado resulta em erro.  
  
 Quando um arquivo de dados é especificado, **bcp_init** examina a estrutura de banco de dados fonte ou destino tabela, não o arquivo de dados. **bcp_init** especifica valores de formato de dados para o arquivo de dados com base em cada coluna na tabela de banco de dados, exibição ou conjunto de resultados de SELECT. Essa especificação inclui o tipo de dados de cada coluna, a presença ou ausência de um indicador de comprimento ou nulo e cadeias de caracteres de bytes de terminador nos dados, além da largura de tipos de dados de comprimento fixo. **bcp_init** define esses valores da seguinte maneira:  
  
-   O tipo de dados especificado é o tipo de dados da coluna na tabela, exibição ou conjunto de resultados de SELECT do banco de dados. O tipo de dados é enumerado por tipos de dados nativos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificados em sqlncli.h. Os dados são representados em seu próprio formato de computador. Ou seja, os dados de uma coluna de **inteiro** tipo de dados é representado por uma sequência de quatro bytes big- ou little endian com base no computador que criou o arquivo de dados.  
  
-   Se um tipo de dados de banco de dados tiver comprimento fixo, os dados do arquivo de dados também terão comprimento fixo. Funções de cópia em massa que processam dados (por exemplo, [bcp_exec](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-exec.md)) analisam as linhas de dados esperando que o comprimento dos dados no arquivo de dados seja idêntico ao comprimento dos dados especificados no banco de dados tabela, exibição ou lista de colunas SELECT. Por exemplo, os dados de uma coluna de banco de dados definido como **char (13)** devem ser representados por 13 caracteres para cada linha de dados no arquivo. Os dados de comprimento fixo podem ser prefixados com um indicador nulo se a coluna do banco de dados permitir valores nulos.  
  
-   Quando a sequência de bytes de terminador é definida, o comprimento da sequência de bytes de terminador é definido como 0.  
  
-   Ao copiar para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o arquivo de dados deve ter dados em cada coluna na tabela do banco de dados. Ao copiar do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os dados de todas as colunas na tabela, exibição ou conjunto de resultados de SELECT do banco de dados são copiados para o arquivo de dados.  
  
-   Ao copiar para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a posição ordinal de uma coluna no arquivo de dados deve ser idêntica à posição ordinal da coluna na tabela do banco de dados. Ao copiar do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **bcp_exec** coloca dados com base na posição ordinal da coluna na tabela de banco de dados.  
  
-   Se um tipo de dados do banco de dados é de comprimento variável (por exemplo, **varbinary (22)**) ou se uma coluna de banco de dados pode conter valores nulos, os dados no arquivo de dados serão prefixados com um indicador de comprimento/nulo. A largura do indicador varia dependendo do tipo de dados e da versão da cópia em massa.  
  
 Para alterar valores de formato de dados especificados para um arquivo de dados, chame [bcp_columns](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-columns.md) e [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md).  
  
 As cópias em massa para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem ser otimizadas para tabelas que não contêm índices, definindo o modelo de recuperação de banco de dados como SIMPLE ou BULK_LOGGED. Para obter mais informações, consulte [pré-requisitos para log mínimo em importação em massa](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md) e [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md).  
  
 Se nenhum arquivo de dados for usado, você deve chamar [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md) para especificar o formato e o local na memória dos dados para cada coluna, em seguida, copie as linhas de dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando [bcp_sendrow](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-sendrow.md).  
  
## <a name="example"></a>Exemplo  
 Este exemplo mostra como usar a função ODBC bcp_init com um arquivo de formato.  
  
 Antes de compilar e executar o código C++, você precisa fazer o seguinte:  
  
-   Crie uma fonte de dados ODBC chamada Teste. Você pode associar essa fonte de dados a qualquer banco de dados.  
  
-   Execute o seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] no banco de dados:  
  
    ```  
    CREATE TABLE BCPDate (cola int, colb datetime);  
    ```  
  
-   No diretório onde você executará o aplicativo, adicione um arquivo chamado Bcpfmt.fmt e adicione isto ao arquivo:  
  
    ```  
    8.0  
    2  
    1SQLCHAR04"\t"1colaSQL_Latin1_General_Cp437_Bin  
    2SQLCHAR08"\r\n"2colbSQL_Latin1_General_Cp437_Bin  
    ```  
  
-   No diretório onde você executará o aplicativo, adicione um arquivo chamado Bcpodbc.bcp e adicione isto ao arquivo:  
  
    ```  
    1  
    2  
    ```  
  
 Agora você está pronto para compilar e executar o código C++.  
  
```  
// compile with: odbc32.lib sqlncli11.lib  
#include <stdio.h>  
#include <windows.h>  
#include <sql.h>  
#include <sqlext.h>  
#include <odbcss.h>  
  
SQLHENV henv = SQL_NULL_HENV;  
HDBC hdbc1 = SQL_NULL_HDBC;   
  
void Cleanup() {  
   if (hdbc1 != SQL_NULL_HDBC) {  
      SQLDisconnect(hdbc1);  
      SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   }  
  
   if (henv != SQL_NULL_HENV)  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
int main() {  
   RETCODE retcode;  
   SDWORD cRows;  
  
   // Allocate the ODBC environment and save handle.  
   retcode = SQLAllocHandle (SQL_HANDLE_ENV, NULL, &henv);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(Env) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Notify ODBC that this is an ODBC 3.0 app.  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER) SQL_OV_ODBC3, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetEnvAttr(ODBC version) Failed\n\n");  
      Cleanup();  
      return(9);      
   }  
  
   // Allocate ODBC connection handle, set BCP mode, and connect.  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc1);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLAllocHandle(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   retcode = SQLSetConnectAttr(hdbc1, SQL_COPT_SS_BCP, (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
   if ( (retcode != SQL_SUCCESS_WITH_INFO) && (retcode != SQL_SUCCESS)) {  
      printf("SQLSetConnectAttr(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Sample uses Integrated Security. Create SQL Server DSN using Windows NT authentication.  
   retcode = SQLConnect(hdbc1, (UCHAR*)"Test", SQL_NTS, (UCHAR*)"", SQL_NTS, (UCHAR*)"", SQL_NTS);  
   if ( (retcode != SQL_SUCCESS) && (retcode != SQL_SUCCESS_WITH_INFO) ) {  
      printf("SQLConnect() Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Initialize the bulk copy.  
   retcode = bcp_init(hdbc1, "BCPDate", "BCPODBC.bcp", NULL, DB_IN);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_init(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Read the format file.  
   retcode = bcp_readfmt(hdbc1, "BCPFMT.fmt");  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_readfmt(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   // Execute the bulk copy.  
   retcode = bcp_exec(hdbc1, &cRows);  
   if ( (retcode != SUCCEED) ) {  
      printf("bcp_exec(hdbc1) Failed\n\n");  
      Cleanup();  
      return(9);  
   }  
  
   printf("Number of rows bulk copied in = %d.\n", cRows);  
  
   // Cleanup  
   SQLDisconnect(hdbc1);  
   SQLFreeHandle(SQL_HANDLE_DBC, hdbc1);  
   SQLFreeHandle(SQL_HANDLE_ENV, henv);  
}  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Funções de cópia em massa](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  

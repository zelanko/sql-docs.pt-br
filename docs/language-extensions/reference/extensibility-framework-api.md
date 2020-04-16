---
title: API Extensibility Framework
titleSuffix: SQL Server Language Extensions
description: É possível usar a estrutura de extensibilidade para escrever extensões de linguagem de programação para o SQL Server. A API Extensibility Framework para Microsoft SQL Server pode ser usada por uma extensão de linguagem para interagir e trocar dados com o SQL Server.
author: dphansen
ms.author: davidph
ms.date: 04/09/2020
ms.topic: reference
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bc33ebc4ae271841cba2de73cb9168e1a41e7b69
ms.sourcegitcommit: fbe0ab88fa8d5aa3ea96629f4ccfa4da5caf74f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/10/2020
ms.locfileid: "81012422"
---
# <a name="extensibility-framework-api-for-sql-server"></a>API Extensibility Framework para SQL Server

É possível usar a estrutura de extensibilidade para escrever extensões de linguagem de programação para o SQL Server. A API Extensibility Framework para Microsoft SQL Server pode ser usada por uma extensão de linguagem para interagir e trocar dados com o SQL Server.

Como autor da extensão de linguagem, você pode usar essa referência junto com a [extensão de linguagem Java para SQL Server](../how-to/extensibility-sdk-java-sql-server.md) de software livre para entender como usar a API com a finalidade de escrever suas próprias extensões de linguagem. Encontro o código-fonte da extensão de linguagem Java em [aka.ms/mssql-lang-extensions](https://aka.ms/mssql-lang-extensions).

Localize as informações de sintaxe e argumento sobre todas as funções de API abaixo.

## <a name="return-value"></a>Valor retornado

Todas as funções retornam o parâmetro *SQLRETURN*. Se o valor for diferente de *SQL_SUCCESS*, será tratado como um erro e a execução do script será interrompida.

## <a name="standard-output"></a>Saída padrão

A saída da extensão para a saída padrão ou os fluxos de erros serão rastreados para o arquivo de log da sessão e, eventualmente, rastreados de volta para o SQL Server (semelhante a algo exibido na guia de mensagens do SSMS).


## <a name="init"></a>Init

Função chamada somente uma vez e usada para inicializar o runtime para a execução. Por exemplo, a extensão Java inicializa o JVM.

### <a name="syntax"></a>Sintaxe

```cpp
SQLRETURN Init(
    SQLCHAR *ExtensionParams,
    SQLULEN ExtensionParamsLength,
    SQLCHAR *ExtensionPath,
    SQLULEN ExtensionPathLength,
    SQLCHAR *PublicLibraryPath,
    SQLULEN PublicLibraryPathLength,
    SQLCHAR *PrivateLibraryPath,
    SQLULEN PrivateLibraryPathLength
);
```

### <a name="arguments"></a>Argumentos

*ExtensionParams*  
\[Entrada\] Cadeia de caracteres terminada em nulo que contém o valor `PARAMETERS` fornecido durante [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md) ou [ALTER EXTERNAL LANGUAGE](../../t-sql/statements/alter-external-language-transact-sql.md).

*ExtensionParamsLength*  
\[Entrada\] Comprimento em bytes de *ExtensionParams* (excluindo o caractere de terminação nula).

*ExtensionPath*  
\[Entrada\] Cadeia de caracteres UTF-8 terminada em nulo que contém o caminho absoluto para o diretório de instalação da extensão.

*ExtensionPathLength*  
\[Entrada\] Comprimento em bytes de *ExtensionPath* (excluindo o caractere de terminação nula).

*PublicLibraryPath*  
\[Entrada\] Cadeia de caracteres UTF-8 terminada em nulo que contém o caminho absoluto para o diretório de bibliotecas externas públicas dessa linguagem externa.

*PublicLibraryPathLength*  
\[Entrada\] Comprimento em bytes de *PublicLibraryPath* (excluindo o caractere de terminação nula).

*PrivateLibraryPath*  
\[Entrada\] Cadeia de caracteres UTF-8 terminada em nulo que contém o caminho absoluto para o diretório de bibliotecas externas privadas dessa linguagem externa.

*PrivateLibraryPathLength*  
\[Entrada\] Comprimento em bytes de *PrivateLibraryPath* (excluindo o caractere de terminação nula).

## <a name="initsession"></a>InitSession

Função chamada uma vez por sessão que inicializa configurações específicas da sessão.

### <a name="syntax"></a>Sintaxe

```cpp
SQLRETURN InitSession(
    SQLGUID         SessionId,
    SQLUSMALLINT    TaskId,
    SQLCHAR*        Script,
    SQLULEN         ScriptLength,
    SQLUSMALLINT    InputSchemaColumnsNumber,
    SQLUSMALLINT    ParametersNumber
    SQLCHAR*        InputDataName,
    SQLUSMALLINT    InputDataNameLength,
    SQLCHAR*        OutputDataName,
    SQLUSMALLINT    OutputDataNameLength
);
```

### <a name="arguments"></a>Argumentos

*SessionId*  
\[Entrada\] GUID que identifica exclusivamente a sessão de script.

*TaskId*  
\[Entrada\] Um inteiro que identifica exclusivamente o processo de execução.

Quando `@parallel = 1` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), esse valor varia de zero ao grau de paralelismo da consulta.

*Script*  
\[Entrada\] Cadeia de caracteres UTF-8 terminada em nulo que contém o `@script` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

*ScriptLength*  
\[Entrada\] Comprimento em bytes de *ScriptScript* (excluindo o caractere de terminação nula).

*InputSchemaColumnsNumber*  
\[Entrada\] Número de colunas no conjunto de resultados de `@input_data_1` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

*ParametersNumber*  
\[Entrada\] Número de parâmetros de entrada de `@params` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

*InputDataName*  
\[Entrada\] Cadeia de caracteres UTF-8 terminada em nulo que contém o `@input_data_1_name` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

*InputDataNameLength*  
\[Entrada\] Comprimento em bytes de *InputDataName* (excluindo o caractere de terminação nula).

*OutputDataName*  
\[Entrada\] Cadeia de caracteres UTF-8 terminada em nulo que contém o `@output_data_1_name` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

*OutputDataNameLength*  
\[Entrada\] Comprimento em bytes de *OutputDataName* (excluindo o caractere de terminação nula).

## <a name="initcolumn"></a>InitColumn

Inicializa as informações de uma determinada coluna para uma sessão específica.

Função chamada para cada coluna no conjunto de resultados de `@input_data_1` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

A estrutura de coluna desse conjunto de resultados será referida como o *esquema de entrada*.

### <a name="syntax"></a>Sintaxe

```cpp
SQLRETURN InitColumn(
    SQLGUID       SessionId,
    SQLUSMALLINT  TaskId,
    SQLUSMALLINT  ColumnNumber,
    SQLCHAR*      ColumnName,
    SQLSMALLINT   ColumnNameLength,
    SQLSMALLINT   DataType,
    SQLULEN       ColumnSize,
    SQLSMALLINT   DecimalDigits,
    SQLSMALLINT   Nullable,
    SQLSMALLINT   PartitionByNumber,
    SQLSMALLINT   OrderByNumber
);
```

### <a name="arguments"></a>Argumentos

*SessionId*  
\[Entrada\] GUID que identifica exclusivamente a sessão de script.

*TaskId*  
\[Entrada\] Um inteiro que identifica exclusivamente o processo de execução.

Quando `@parallel = 1` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), esse valor varia de zero ao grau de paralelismo da consulta.

*ColumnNumber*  
\[Entrada\] Um inteiro que identifica o índice da coluna no esquema de entrada. As colunas são numeradas sequencialmente em ordem crescente, começando em 0.

*ColumnName*  
\[Entrada\] Cadeia de caracteres UTF-8 terminada em nulo que contém o nome da coluna.

*ColumnNameLength*  
\[Entrada\] Comprimento em bytes de *ColumnName* (excluindo o caractere de terminação nula).

*DataType*  
\[Entrada\] O tipo C do ODBC que identifica o tipo de dados da coluna.

*ColumnSize*  
\[Entrada\] O tamanho máximo em bytes dos dados subjacentes na coluna.

Para os tipos de dados SQL_C_CHAR, SQL_C_WCHAR e SQL_C_BINARY, valores maiores que 8000 indicam que a coluna representa um objeto LOBs com tamanhos de até 2 GB.

*DecimalDigits*  
\[Entrada\] Os dígitos decimais dos dados subjacentes na coluna, conforme definidos por [Dígitos decimais](../../odbc/reference/appendixes/decimal-digits.md).

*Permite valor nulo*  
\[Entrada\] Um valor que indica se a coluna pode conter valores NULL. Valores possíveis:

- SQL_NO_NULLS: a coluna não pode conter valores NULL.
- SQL_NULLABLE: a coluna pode conter valores NULL.

*PartitionByNumber*  
\[Entrada\] Um valor que indica o índice da coluna na sequência `@input_data_1_partition_by_columns` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). As colunas são numeradas sequencialmente em ordem crescente, começando em 0. Se essa coluna não for incluída na sequência, o valor será -1.

*OrderByNumber*  
\[Entrada\] Um valor que indica o índice da coluna na sequência `@input_data_1_order_by_columns` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md). As colunas são numeradas sequencialmente em ordem crescente, começando em 0. Se essa coluna não for incluída na sequência, o valor será -1.

## <a name="initparam"></a>InitParam

Inicializa as informações sobre um determinado parâmetro de entrada para uma sessão específica.

Função chamada para cada parâmetro de `@params` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

### <a name="syntax"></a>Sintaxe

```cpp
SQLRETURN InitParam(
    SQLGUID      SessionId,
    SQLUSMALLINT TaskId,
    SQLUSMALLINT ParamNumber,
    SQLCHAR*     ParamName,
    SQLSMALLINT  ParamNameLength,
    SQLSMALLINT  DataType,
    SQLULEN      ParamSize,
    SQLSMALLINT  DecimalDigits,
    SQLPOINTER   ParamValue,
    SQLINTEGER   StrLen_or_Ind,
    SQLSMALLINT  InputOutputType
);
```

### <a name="arguments"></a>Argumentos

*SessionId*  
\[Entrada\] GUID que identifica exclusivamente a sessão de script.

*TaskId*  
\[Entrada\] Um inteiro que identifica exclusivamente o processo de execução.

Quando `@parallel = 1` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), esse valor varia de zero ao grau de paralelismo da consulta.

*ParamNumber*  
\[Entrada\] Um inteiro que identifica o índice do parâmetro. Os parâmetros são numerados sequencialmente em ordem crescente, começando em 0.

*ParamName*  
\[Entrada\] Cadeia de caracteres UTF-8 terminada em nulo que contém o nome do parâmetro.

*ParamNameLength*  
\[Entrada\] Comprimento em bytes de *ParamName* (excluindo o caractere de terminação nula).

*DataType*  
\[Entrada\] O tipo C do ODBC que identifica o tipo de dados do parâmetro.

*ParamSize*  
\[Entrada\] O tamanho máximo em bytes dos dados subjacentes nesse parâmetro.

Para os tipos de dados SQL_C_CHAR, SQL_C_WCHAR e SQL_C_BINARY, valores maiores que 8000 indicam que o parâmetro representa um objeto LOBs com tamanhos de até 2 GB.

*DecimalDigits*  
\[Entrada\] Os dígitos decimais dos dados subjacentes no parâmetro, conforme definidos por [Dígitos decimais](../../odbc/reference/appendixes/decimal-digits.md).

*ParamValue*  
\[Entrada\] Um ponteiro para um buffer que contém o valor do parâmetro.

*StrLen_or_Ind*  
\[Entrada\] Um valor inteiro que indica o comprimento em bytes de *ParamValue* ou SQL_NULL_DATA para indicar que os dados são NULL.

StrLen_or_Ind\[col\] poderá ser ignorado se uma coluna não for anulável e não representar um dos seguintes tipos de dados: SQL_C_CHAR, SQL_C_WCHAR e SQL_C_BINARY, SQL_C_NUMERIC ou SQL_C_TYPE_TIMESTAMP. Caso contrário, ele apontará para uma matriz válida com elementos \[RowsNumber\], em que cada elemento contém o comprimento ou os dados de indicador nulos.

*InputOutputType*  
\[Entrada\] O tipo do parâmetro. O argumento *InputOutputType* é um dos seguintes valores:

- SQL_PARAM_INPUT
- SQL_PARAM_INPUT_OUTPUT

## <a name="execute"></a>Execute (executar)

Execute o `@script` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Essa função pode ser chamada várias vezes. Uma vez para cada parte do fluxo e para cada partição em `@input_data_1_partition_by_columns` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).


### <a name="syntax"></a>Sintaxe

```cpp
SQLRETURN Execute(
    SQLGUID         SessionId,
    SQLUSMALLINT    TaskId,
    SQLULEN         RowsNumber,
    SQLPOINTER*     Data,
    SQLINTEGER**    StrLen_or_Ind,
    SQLUSMALLINT*   OutputSchemaColumnsNumber
);
```

### <a name="arguments"></a>Argumentos

*SessionId*  
\[Entrada\] GUID que identifica exclusivamente a sessão de script.

*TaskId*  
\[Entrada\] Um inteiro que identifica exclusivamente o processo de execução.

Quando `@parallel = 1` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), esse valor varia de zero ao grau de paralelismo da consulta.

*RowsNumber*  
\[Entrada\] O número de linhas em *Dados*.

*Dados*  
\[Entrada\] Uma matriz bidimensional que contém o conjunto de resultados de `@input_data_1` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

O número total de colunas é *InputSchemaColumnsNumber*, recebido na chamada [InitSession](#initsession). Cada coluna contém elementos *RowsNumber* que devem ser interpretados de acordo com o tipo de coluna de [InitColumn](#initcolumn).

Elementos indicados como NULL em *StrLen_or_Ind* não têm garantia de serem válidos e devem ser ignorados.

*StrLen_or_Ind*  
\[Entrada\] Uma matriz bidimensional que contém o indicador de comprimento/NULL para cada valor em *Dados*. Valores possíveis de cada célula:

- n, em que n > 0, indicando o comprimento dos dados em bytes
- SQL_NULL_DATA, indicando um valor nulo.

O número total de colunas é *InputSchemaColumnsNumber*, recebido na chamada [InitSession](#initsession). Cada coluna contém elementos *RowsNumber* que devem ser interpretados de acordo com o tipo de coluna de [InitColumn](#initcolumn).

StrLen_or_Ind\[col\] poderá ser ignorado se uma coluna não for anulável nem representar um dos seguintes tipos de dados: SQL_C_CHAR, SQL_C_WCHAR e SQL_C_BINARY, SQL_C_NUMERIC ou SQL_C_TYPE_TIMESTAMP. Caso contrário, ele apontará para uma matriz válida com elementos *RowsNumber*, em que cada elemento contém o comprimento ou dados de indicador nulos.

*OutputSchemaColumnsNumber*  
\[Saída\] Ponteiro para um buffer no qual retornar o número de colunas no conjunto de resultados esperado do `@script` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

## <a name="getresultcolumn"></a>GetResultColumn

Recupera as informações sobre uma determinada coluna de saída para uma sessão específica.

Função chamada para cada coluna no conjunto de resultados de `@script` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).
A estrutura de coluna desse conjunto de resultados será referida como o "esquema de saída".

### <a name="syntax"></a>Sintaxe

```cpp
SQLRETURN GetResultColumn(
    SQLGUID         SessionId,
    SQLUSMALLINT    TaskId,
    SQLUSMALLINT    ColumnNumber,
    SQLSMALLINT*    DataType,
    SQLINTEGER*     ColumnSize,
    SQLSMALLINT*    DecimalDigits,
    SQLSMALLINT*    Nullable
);
```

### <a name="arguments"></a>Argumentos

*SessionId*  
\[Entrada\] GUID que identifica exclusivamente a sessão de script.

*TaskId*  
\[Entrada\] Um inteiro que identifica exclusivamente o processo de execução.

Quando `@parallel = 1` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), esse valor varia de zero ao grau de paralelismo da consulta.

*ColumnNumber*  
\[Entrada\] Um inteiro que identifica o índice da coluna no esquema de saída. As colunas são numeradas sequencialmente em ordem crescente, começando em 0.

*DataType*  
\[Saída\] Um ponteiro para o buffer que contém o tipo C do ODBC que identifica o tipo de dados da coluna.

*ColumnSize*  
\[Saída\] Um ponteiro para um buffer que contém o tamanho máximo em bytes dos dados subjacentes na coluna.

*DecimalDigits*  
\[Saída\] Um ponteiro para um buffer que contém os dígitos decimais dos dados subjacentes na coluna, conforme definidos por [Dígitos decimais](../../odbc/reference/appendixes/decimal-digits.md). Se o número de dígitos decimais não puder ser determinado ou não for aplicável, o valor será descartado.

*Permite valor nulo*  
\[Saída\] Um ponteiro para um buffer que contém um valor que indica se a coluna pode conter valores NULL. Valores possíveis:

- SQL_NO_NULLS: a coluna não pode conter valores NULL.
- SQL_NULLABLE: a coluna pode conter valores NULL.

Se outros valores forem passados, a execução será interrompida.

## <a name="getresults"></a>GetResults

Recupere o conjunto de resultados da execução de `@script` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Essa função pode ser chamada várias vezes. Uma vez para cada parte do fluxo e para cada partição em `@input_data_1_partition_by_columns` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).


### <a name="syntax"></a>Sintaxe

```cpp
SQLRETURN GetResults(
    SQLGUID         SessionId,
    SQLUSMALLINT    TaskId,
    SQLULEN*        RowsNumber,
    SQLPOINTER**    Data,
    SQLINTEGER***   StrLen_or_Ind
);
```

### <a name="arguments"></a>Argumentos

*SessionId*  
\[Entrada\] GUID que identifica exclusivamente a sessão de script.

*TaskId*  
\[Entrada\] Um inteiro que identifica exclusivamente o processo de execução.

Quando `@parallel = 1` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), esse valor varia de zero ao grau de paralelismo da consulta.

*RowsNumber*  
\[Saída\] Um ponteiro para um buffer que contém o número de linhas em *Dados*.

*Dados*  
\[Saída\] Um ponteiro para uma matriz bidimensional alocada pela extensão que contém o conjunto de resultados de `@script` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

O número total de colunas deve ser o *OutputSchemaColumnsNumber* recuperado na chamada [Executar](#execute). Cada coluna precisa conter elementos *RowsNumber* que devem ser interpretados de acordo com o tipo de coluna de [GetResultColumn](#getresultcolumn).

*StrLen_or_Ind*  
\[Saída\] Um ponteiro para uma matriz bidimensional alocada pela extensão que contém o indicador de comprimento/NULL de cada valor em *Dados*. Valores possíveis de cada célula:

- n, em que n > 0, indicando o comprimento dos dados em bytes
- SQL_NULL_DATA, indicando um valor nulo.

O número total de colunas deve ser o *OutputSchemaColumnsNumber* recebido na chamada [Executar](#execute). Cada coluna contém elementos *RowsNumber* que devem ser interpretados de acordo com o tipo de coluna de [GetResultColumn](#getresultcolumn).

StrLen_or_Ind\[col\] será ignorado se uma coluna não for anulável e não representar um dos seguintes tipos de dados: SQL_C_CHAR, SQL_C_WCHAR e SQL_C_BINARY [adicionar datas]. Caso contrário, ele apontará para uma matriz válida com elementos *RowsNumber*, em que cada elemento contém o comprimento ou dados de indicador nulos.

## <a name="getoutputparam"></a>GetOutputParam

Recupera as informações sobre um determinado parâmetro de saída para uma sessão específica.

Função chamada para cada parâmetro de `@params` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) marcado com OUTPUT.

### <a name="syntax"></a>Sintaxe

```cpp
SQLRETURN GetOutputParam(
    SQLGUID        SessionId,
    SQLUSMALLINT   ParamNumber,
    SQLPOINTER*    ParamValue,
    SQLINTEGER*    StrLen_or_Ind
);
```

### <a name="arguments"></a>Argumentos

*SessionId*  
\[Entrada\] GUID que identifica exclusivamente a sessão de script.

*ParamValue*  
\[Saída\] Um ponteiro para um buffer que contém o valor do parâmetro.

*StrLen_or_Ind* \[Saída\] Um ponteiro para um buffer que contém um valor inteiro que indica o comprimento em bytes de *ParamValue* ou SQL_NULL_DATA para indicar que os dados são NULL.

## <a name="getinterfaceversion"></a>GetInterfaceVersion

Recupera a versão da interface.
Essa função retorna um inteiro que representa a versão da interface da extensão. Valores com suporte:
1. A versão 1 é a versão inicial da API. Compatível com o SQL Server 2019 RTM.
1. A versão 2 agora é compatível com as APIs InstallExternalLibrary e UninstallExternalLibrary e com o SQL Server 2019 CU3.                            

### <a name="syntax"></a>Sintaxe

```cpp
SQLUSMALLINT GetInterfaceVersion();
```

## <a name="cleanupsession"></a>CleanupSession

Limpar informações por sessão.

### <a name="syntax"></a>Sintaxe

```cpp
SQLRETURN CleanupSession(
    SQLGUID        SessionId,
    SQLUSMALLINT   TaskId
);
```

### <a name="arguments"></a>Argumentos

*SessionId*  
\[Entrada\] GUID que identifica exclusivamente a sessão de script.

*TaskId*  
\[Entrada\] Um inteiro que identifica exclusivamente o processo de execução.

Quando `@parallel = 1` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), esse valor varia de zero ao grau de paralelismo da consulta.

## <a name="cleanup"></a>Limpeza

Limpar informações globais e compartilhadas (por exemplo, JVM).

### <a name="syntax"></a>Sintaxe

```cpp
SQLRETURN Cleanup();
```

## <a name="gettelemetryresults"></a>GetTelemetryResults

Recupera dados de telemetria (pares chave-valor) da extensão. A função é opcional e não requer implementação. A telemetria é exposta pelo DMV (exibição de gerenciamento dinâmico) `dm_db_external_script_execution_stats`.

Há um contador chamado script_executions, que é enviado pela estrutura. A extensão não deve usar esse nome.

Cada entrada de telemetria é um par chave-valor. As chaves são cadeias de caracteres, os valores são inteiros de 64 bits – contadores. Assim, a saída é composta por duas matrizes lógicas: os nomes e contadores correspondentes. Cada matriz é saída.

O comprimento de cada matriz é *RowsNumber*, que é uma saída. A primeira saída lógica contém ponteiros para cadeias de caracteres, portanto, ela é representada por duas matrizes: *CounterNames* (os dados reais da cadeia de caracteres) e *CounterNamesLength* (o comprimento de cada cadeia de caracteres). A segunda saída lógica é armazenada no ponteiro *CounterValues*.

### <a name="syntax"></a>Sintaxe

```cpp
SQLRETURN GetTelemetryResults(
    SQLGUID        SessionId,
    SQLUSMALLINT   TaskId,
    SQLUINTEGER    *RowsNumber,
    SQLCHAR        ***CounterNames,
    SQLINTEGER      **CounterNamesLength,
    SQLBIGINT       **CounterValues
);
```

### <a name="arguments"></a>Argumentos

*SessionId*  
\[Entrada\] GUID que identifica exclusivamente a sessão de script.

*TaskId*  
\[Entrada\] Um inteiro que identifica exclusivamente o processo de execução.

Quando `@parallel = 1` em [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), esse valor varia de zero ao grau de paralelismo da consulta.

*RowsNumber*  
\[Saída\] O número de pares chave-valor.

*CounterNames*  
\[Saída\] Os dados de cadeia de caracteres que contêm as chaves.

*CounterNamesLength*  
\[Saída\] O comprimento de cada cadeia de caracteres de chave.

*CounterValues*  
\[Saída\] Os dados inteiros de 64 bits que contêm os valores.

## <a name="installexternallibrary"></a>InstallExternalLibrary

Instala uma biblioteca. A função é opcional e não requer implementação. A implementação padrão é copiar o conteúdo da biblioteca (confira [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)) em um arquivo no local correto. O nome do arquivo é o nome da biblioteca.

### <a name="syntax"></a>Sintaxe

```cpp
SQLRETURN InstallExternalLibrary(
    SQLGUID    SetupSessionId,
    SQLCHAR    *LibraryName,
    SQLINTEGER LibraryNameLength,
    SQLCHAR    *LibraryFile,
    SQLINTEGER LibraryFileLength,
    SQLCHAR    *LibraryInstallDirectory,
    SQLINTEGER LibraryInstallDirectoryLength,
    SQLCHAR    **LibraryError,
    SQLINTEGER *LibraryErrorLength
);
```

### <a name="arguments"></a>Argumentos

*SetupSessionId*  
\[Entrada\] GUID que identifica exclusivamente a sessão de script.

*LibraryName*  
\[Entrada\] O nome da biblioteca.

*LibraryNameLength*  
\[Entrada\] O comprimento do nome da biblioteca.

*LibraryFile*  
\[Entrada\] O caminho (como uma cadeia de caracteres) para o arquivo de biblioteca que contém o conteúdo binário especificado por [CRIAR BIBLIOTEA EXTERNA](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql).

*LibraryFileLength*  
\[Entrada\] O comprimento da cadeia de caracteres LibraryFile.

*LibraryInstallDirectory:*  
\[Entrada\] O diretório raiz para instalar a biblioteca.

*LibraryInstallDirectoryLength*  
\[Entrada\] O comprimento da cadeia de caracteres LibraryInstallDirectory.

*LibraryError*  
\[Saída\] Um parâmetro de saída opcional. Caso haja um erro durante a instalação da biblioteca, LibraryError apontará para uma cadeia de caracteres que descreve o erro.

*LibraryErrorLength*  
\[Saída\] O comprimento da cadeia de caracteres LibraryError.

## <a name="uninstalllibrary"></a>UninstallLibrary

Desinstala uma biblioteca. A função é opcional e não requer implementação. A implementação padrão é desfazer o trabalho realizado pela implementação padrão de InstallExternalLibrary. A implementação padrão exclui o conteúdo do arquivo *LibraryName* em *LibraryInstallDirectory*.

### <a name="syntax"></a>Sintaxe

```cpp
SQLRETURN UninstallExternalLibrary(
    SQLGUID    SetupSessionId,
    SQLCHAR    *LibraryName,
    SQLINTEGER LibraryNameLength,
    SQLCHAR    *LibraryInstallDirectory,
    SQLINTEGER LibraryInstallDirectoryLength,
    SQLCHAR    **LibraryError,
    SQLINTEGER *LibraryErrorLength
);
```

### <a name="arguments"></a>Argumentos

*SetupSessionId*  
\[Entrada\] GUID que identifica exclusivamente a sessão de script.

*LibraryName*  
\[Entrada\] O nome da biblioteca

*LibraryNameLength*  
\[Entrada\] O comprimento do nome da biblioteca

*LibraryFile*  
\[Entrada\] O caminho (como uma cadeia de caracteres) para o arquivo de biblioteca que contém o conteúdo binário especificado por CRIAR BIBLIOTEA EXTERNA

*LibraryFileLength*  
\[Entrada\] O comprimento da cadeia de caracteres LibraryFile

*LibraryInstallDirectory*  
\[Entrada\] O diretório raiz para instalar a biblioteca

*LibraryInstallDirectoryLength*  
\[Entrada\] O comprimento da cadeia de caracteres LibraryInstallDirectory.

*LibraryError*  
\[Saída\] A cadeia de caracteres de erro da biblioteca.

*LibraryErrorLength*  
\[Saída\] O comprimento da cadeia de caracteres LibraryError.

## <a name="next-steps"></a>Próximas etapas

- [SDK de Extensibilidade da Microsoft para Java para o SQL Server](../how-to/extensibility-sdk-java-sql-server.md) 

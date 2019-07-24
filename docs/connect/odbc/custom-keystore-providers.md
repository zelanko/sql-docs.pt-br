---
title: Provedores de repositório de chaves personalizados | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a6166d7d-ef34-4f87-bd1b-838d3ca59ae7
ms.author: v-chojas
author: MightyPen
ms.openlocfilehash: 0cf2946517be732094d01ff9889faf080a36e85b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006486"
---
# <a name="custom-keystore-providers"></a>Provedores de repositório de chaves personalizado
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="overview"></a>Visão geral

O recurso de criptografia de coluna do SQL Server 2016 requer que as chaves de criptografia de coluna criptografadas (ECEKs) armazenadas no servidor sejam recuperadas pelo cliente e descriptografadas para CEKs (chaves de criptografia de coluna) para acessar os dados armazenados em colunas criptografadas. ECEKs são criptografadas por CMKs (chaves mestras de coluna), e a segurança do CMK é importante para a segurança da criptografia de coluna. Portanto, o CMK deve ser armazenado em um local seguro; a finalidade de um provedor de repositório de chaves de criptografia de coluna é fornecer uma interface para permitir que o driver ODBC Acesse esses CMKs armazenados com segurança. Para usuários com seu próprio armazenamento seguro, a interface do provedor de repositório de chaves personalizado fornece uma estrutura para implementar o acesso ao armazenamento seguro do CMK para o driver ODBC, que pode ser usado para executar criptografia e descriptografia do CEK.

Cada provedor de repositório de chaves contém e gerencia um ou mais CMKs, que são identificados por caminhos de chave – cadeias de caracteres de um formato definido pelo provedor. Isso, juntamente com o algoritmo de criptografia, também uma cadeia de caracteres definida pelo provedor, pode ser usado para executar a criptografia de um CEK e a descriptografia de um ECEK. O algoritmo, junto com o ECEK e o nome do provedor, são armazenados nos metadados de criptografia do banco de dados; consulte [criar chave mestra de coluna](../../t-sql/statements/create-column-master-key-transact-sql.md) e [criar chave de criptografia de coluna](../../t-sql/statements/create-column-encryption-key-transact-sql.md) para obter mais informações. Portanto, as duas operações fundamentais do gerenciamento de chaves são:

```
CEK = DecryptViaCEKeystoreProvider(CEKeystoreProvider_name, Key_path, Key_algorithm, ECEK)

-and-

ECEK = EncryptViaCEKeystoreProvider(CEKeyStoreProvider_name, Key_path, Key_algorithm, CEK)
```

em que `CEKeystoreProvider_name` o é usado para identificar o provedor de repositório de chaves de criptografia de coluna específico (CEKeystoreProvider) e os outros argumentos são usados pelo CEKeystoreProvider para criptografar/descriptografar o (E) CEK. O nome e KeyPath são fornecidos pelos metadados do CMK, enquanto o algoritmo e o valor de ECEK são fornecidos pelos metadados do CEK. Vários provedores de repositório de chaves podem estar presentes junto com os provedores internos padrão. Após executar uma operação que exige o CEK, o driver usa os metadados do CMK para localizar o provedor de keystore apropriado por nome e executa sua operação de descriptografia, que pode ser expressa como:

```
CEK = CEKeyStoreProvider_specific_decrypt(Key_path, Key_algorithm, ECEK)
```

Embora o driver não precise criptografar CEKs, uma ferramenta de gerenciamento de chaves pode precisar fazer isso para implementar operações como a criação e a rotação de CMK; Isso requer a execução da operação inversa:

```
ECEK = CEKeyStoreProvider_specific_encrypt(Key_path, Key_algorithm, CEK)
```

### <a name="cekeystoreprovider-interface"></a>Interface CEKeyStoreProvider

Este documento descreve detalhadamente a interface CEKeyStoreProvider. Um provedor de repositório de chaves que implementa essa interface pode ser usado pelo Microsoft ODBC Driver for SQL Server. Os implementadores de CEKeyStoreProvider podem usar este guia para desenvolver provedores de keystore personalizados utilizáveis pelo driver.

Uma biblioteca de provedores de repositório de chaves ("biblioteca de provedores") é uma biblioteca de vínculo dinâmico que pode ser carregada pelo driver ODBC e contém um ou mais provedores de repositório de chaves. O símbolo `CEKeystoreProvider` deve ser exportado por uma biblioteca de provedores e ser o endereço de uma matriz terminada em nulo `CEKeystoreProvider` de ponteiros para estruturas, um para cada provedor de repositório de chaves na biblioteca.

Uma `CEKeystoreProvider` estrutura define os pontos de entrada de um único provedor de repositório de chaves:

```
typedef struct CEKeystoreProvider {
    wchar_t *Name;
    int (*Init)(CEKEYSTORECONTEXT *ctx, errFunc *onError);
    int (*Read)(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int *len);
    int (*Write)(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int len);
    int (*DecryptCEK)(  CEKEYSTORECONTEXT *ctx,
                        errFunc *onError,
                        const wchar_t *keyPath,
                        const wchar_t *alg,
                        unsigned char *ecek,
                        unsigned short ecekLen,
                        unsigned char **cekOut,
                        unsigned short *cekLen);
    int (*EncryptCEK)(  CEKEYSTORECONTEXT *ctx,
                        errFunc *onError,
                        const wchar_t *keyPath,
                        const wchar_t *alg,
                        unsigned char *cek,
                        unsigned short cekLen,
                        unsigned char **ecekOut,
                        unsigned short *ecekLen);
    void (*Free)();
} CEKEYSTOREPROVIDER;
```

|Nome do Campo|Descrição|
|:--|:--|
|`Name`|O nome do provedor de keystore. Ele não deve ser o mesmo que qualquer outro provedor de repositório de chaves carregado anteriormente pelo driver ou presente nesta biblioteca. Cadeia de caracteres largos* terminada em nulo.|
|`Init`|Função de inicialização. Se uma função de inicialização não for necessária, esse campo poderá ser nulo.|
|`Read`|Função de leitura do provedor. Pode ser NULL se não for necessário.|
|`Write`|Função de gravação do provedor. Necessário se Read não for NULL. Pode ser NULL se não for necessário.|
|`DecryptCEK`|Função de descriptografia ECEK. Essa função é o motivo da existência de um provedor de repositório de chaves e não deve ser nula.|
|`EncryptCEK`|Função de criptografia CEK. O driver não chama essa função, mas é fornecido para permitir acesso programático à criação de ECEK por ferramentas de gerenciamento de chaves. Pode ser NULL se não for necessário.|
|`Free`|Função de encerramento. Pode ser NULL se não for necessário.|

Com a exceção de Free, as funções nessa interface têm um par de parâmetros **, CTX** e **OnError**. O primeiro identifica o contexto no qual a função é chamada, enquanto o último é usado para relatar erros. Consulte [contextos](#context-association) e [tratamento de erros](#error-handling) abaixo para obter mais informações.

```
int Init(CEKEYSTORECONTEXT *ctx, errFunc onError);
```
Nome do espaço reservado para uma função de inicialização definida pelo provedor. O driver chama essa função uma vez, depois que um provedor é carregado, mas antes da primeira vez necessário para realizar a descriptografia ECEK ou solicitações/Write () de leitura (). Use essa função para executar qualquer inicialização necessária. 

|Argumento|Descrição|
|:--|:--|
|`ctx`|Entrada Contexto de operação.|
|`onError`|Entrada Função de relatório de erros.|
|`Return Value`|Retornar diferente de zero para indicar êxito ou zero para indicar falha.|

```
int Read(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int *len);
```

Nome do espaço reservado para uma função de comunicação definida pelo provedor. O driver chama essa função quando o aplicativo solicita a leitura de dados de um provedor (anteriormente-gravado-para) usando o atributo de conexão SQL_COPT_SS_CEKEYSTOREDATA, permitindo que o aplicativo leia dados arbitrários do provedor. Consulte [comunicando-se com provedores](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers) de keystore para obter mais informações.

|Argumento|Descrição|
|:--|:--|
|`ctx`|Entrada Contexto de operação.|
|`onError`|Entrada Função de relatório de erros.|
|`data`|Der Ponteiro para um buffer no qual o provedor grava dados a serem lidos pelo aplicativo. Isso corresponde ao campo de dados da estrutura CEKEYSTOREDATA.|
|`len`|InOut Ponteiro para um valor de comprimento; na entrada, esse é o comprimento máximo do buffer de dados e o provedor não deve gravar mais de * Len bytes nele. No retorno, o provedor deve atualizar * Len com o número de bytes realmente gravados.|
|`Return Value`|Retornar diferente de zero para indicar êxito ou zero para indicar falha.|

```
int Write(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int len);
```
Nome do espaço reservado para uma função de comunicação definida pelo provedor. O driver chama essa função quando o aplicativo solicita a gravação de dados em um provedor usando o atributo de conexão SQL_COPT_SS_CEKEYSTOREDATA, permitindo que o aplicativo grave dados arbitrários no provedor. Consulte [comunicando-se com provedores](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers) de keystore para obter mais informações.

|Argumento|Descrição|
|:--|:--|
|`ctx`|Entrada Contexto de operação.|
|`onError`|Entrada Função de relatório de erros.|
|`data`|Entrada Ponteiro para um buffer que contém os dados para o provedor ler. Isso corresponde ao campo de dados da estrutura CEKEYSTOREDATA. O provedor não deve ler mais de Len bytes desse buffer.|
|`len`|Entrada O número de bytes disponíveis nos dados. Isso corresponde ao campo DataSize da estrutura CEKEYSTOREDATA.|
|`Return Value`|Retornar diferente de zero para indicar êxito ou zero para indicar falha.|

```
int (*DecryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen);
```
Nome do espaço reservado para uma função de descriptografia de ECEK definida pelo provedor. O driver chama essa função para descriptografar um ECEK criptografado por um CMK associado a esse provedor em um CEK.

|Argumento|Descrição|
|:--|:--|
|`ctx`|Entrada Contexto de operação.|
|`onError`|Entrada Função de relatório de erros.|
|`keyPath`|Entrada O valor do atributo de metadados [KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) para o CMK referenciado pelo ECEK fornecido. Cadeia de caracteres largos* terminada em nulo. Isso se destina a identificar um CMK manipulado por esse provedor.|
|`alg`|Entrada O valor do atributo de metadados do [algoritmo](../../t-sql/statements/create-column-encryption-key-transact-sql.md) para o determinado ECEK. Cadeia de caracteres largos* terminada em nulo. Isso se destina a identificar o algoritmo de criptografia usado para criptografar o determinado ECEK.|
|`ecek`|Entrada Ponteiro para o ECEK a ser descriptografado.|
|`ecekLen`|Entrada Comprimento do ECEK.|
|`cekOut`|Der O provedor deve alocar memória para o ECEK descriptografado e gravar seu endereço no ponteiro apontado por cekOut. Deve ser possível liberar esse bloco de memória usando a função [LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) ou gratuita (Linux/Mac). Se nenhuma memória foi alocada devido a um erro ou, caso contrário, o provedor deverá definir * cekOut como um ponteiro nulo.|
|`cekLen`|Der O provedor deve gravar no endereço apontado por cekLen o comprimento do ECEK descriptografado que foi gravado em * * cekOut.|
|`Return Value`|Retornar diferente de zero para indicar êxito ou zero para indicar falha.|

```
int (*EncryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *cek,unsigned short cekLen, unsigned char **ecekOut, unsigned short *ecekLen);
```
Nome do espaço reservado para uma função de criptografia CEK definida pelo provedor. O driver não chama essa função nem expõe sua funcionalidade por meio da interface ODBC, mas é fornecido para permitir acesso programático à criação de ECEK por ferramentas de gerenciamento de chaves.

|Argumento|Descrição|
|:--|:--|
|`ctx`|Entrada Contexto de operação.|
|`onError`|Entrada Função de relatório de erros.|
|`keyPath`|Entrada O valor do atributo de metadados [KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) para o CMK referenciado pelo ECEK fornecido. Cadeia de caracteres largos* terminada em nulo. Isso se destina a identificar um CMK manipulado por esse provedor.|
|`alg`|Entrada O valor do atributo de metadados do [algoritmo](../../t-sql/statements/create-column-encryption-key-transact-sql.md) para o determinado ECEK. Cadeia de caracteres largos* terminada em nulo. Isso se destina a identificar o algoritmo de criptografia usado para criptografar o determinado ECEK.|
|`cek`|Entrada Ponteiro para o CEK a ser criptografado.|
|`cekLen`|Entrada Comprimento do CEK.|
|`ecekOut`|Der O provedor deve alocar memória para o CEK criptografado e gravar seu endereço para o ponteiro apontado por ecekOut. Deve ser possível liberar esse bloco de memória usando a função [LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) ou gratuita (Linux/Mac). Se nenhuma memória foi alocada devido a um erro ou, caso contrário, o provedor deverá definir * ecekOut como um ponteiro nulo.|
|`ecekLen`|Der O provedor deve gravar no endereço apontado por ecekLen o comprimento do CEK criptografado que foi gravado em * * ecekOut.|
|`Return Value`|Retornar diferente de zero para indicar êxito ou zero para indicar falha.|

```
void (*Free)();
```
Nome do espaço reservado para uma função de encerramento definida pelo provedor. O driver pode chamar essa função após o encerramento normal do processo.

> [!NOTE]
> *Cadeias de caracteres largos são caracteres de 2 bytes (UTF-16) devido a como os SQL Server os armazena.*


### <a name="error-handling"></a>Tratamento de erros

Como podem ocorrer erros durante o processamento de um provedor, um mecanismo é fornecido para permitir que ele Relate erros de volta ao driver em detalhes mais específicos do que um êxito/falha booliano. Muitas das funções têm um par de parâmetros **, CTX** e **OnError**, que são usados juntos para essa finalidade, além do valor de retorno de êxito/falha.

O parâmetro **CTX** identifica o contexto no qual ocorre uma operação de provedor.

O **parâmetro OnError** aponta para uma função de relatório de erros, com o seguinte protótipo:

`typedef void errFunc(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...);`

|Argumento|Descrição|
|:--|:--|
|`ctx`|Entrada O contexto no qual relatar o erro.|
|`msg`|Entrada A mensagem de erro a ser reportada. Cadeia de caracteres largos terminada em nulo. Para permitir que informações parametrizadas estejam presentes, essa cadeia de caracteres pode conter sequências de formatação de inserção do formulário aceito pela função [FormatMessage](/windows/desktop/api/winbase/nf-winbase-formatmessage) . A funcionalidade estendida pode ser especificada por esse parâmetro, conforme descrito abaixo.|
|...|Entrada Parâmetros Variadic adicionais para ajustar os especificadores de formato em MSG, conforme apropriado.|

Para relatar quando ocorreu um erro, o provedor chama OnError, fornecendo o parâmetro de contexto passado para a função de provedor pelo driver e uma mensagem de erro com parâmetros adicionais opcionais a serem formatados nele. O provedor pode chamar essa função várias vezes para postar várias mensagens de erro consecutivamente dentro de uma invocação de função de provedor. Por exemplo:

```
    if (!doSomething(...))
    {
        onError(ctx, L"An error occurred in doSomething.");
        onError(ctx, L"Additional error message with more details.");
        return 0;
    }
```


O `msg` parâmetro é normalmente uma cadeia de caracteres largos, mas extensões adicionais estão disponíveis:

Usando um dos valores predefinidos especiais com a macro IDS_MSG, as mensagens de erro genéricas já existentes e em uma forma local no driver podem ser utilizadas. Por exemplo, se um provedor falhar ao alocar memória, `IDS_S1_001` a mensagem "falha na alocação de memória" poderá ser usada:

`onError(ctx, IDS_MSG(IDS_S1_001));`

Para que o erro seja reconhecido pelo driver, a função do provedor deve retornar uma falha. Quando isso é executado no contexto de uma operação ODBC, os erros postados se tornarão acessíveis na conexão ou no identificador de instrução por meio do mecanismo de`SQLError`diagnóstico `SQLGetDiagRec`ODBC padrão `SQLGetDiagField`(,, e).


### <a name="context-association"></a>Associação de contexto

A `CEKEYSTORECONTEXT` estrutura, além de fornecer contexto para o retorno de chamada de erro, também pode ser usada para determinar o contexto ODBC no qual uma operação de provedor é executada. Isso permite que um provedor associe dados a cada um desses contextos, por exemplo, para implementar a configuração por conexão. Para essa finalidade, a estrutura contém 3 ponteiros opacos correspondentes ao contexto de ambiente, conexão e instrução:

```
typedef struct CEKeystoreContext
{
void *envCtx;
void *dbcCtx;
void *stmtCtx;
} CEKEYSTORECONTEXT;
```

|Campo|Descrição|
|:--|:--|
|`envCtx`|Contexto do ambiente.|
|`dbcCtx`|Contexto de conexão.|
|`stmtCtx`|Contexto da instrução.|

Cada um desses contextos é um valor opaco que, embora não seja o mesmo que o identificador ODBC correspondente, pode ser usado como um identificador exclusivo para o identificador: se o identificador *X* estiver associado ao valor de contexto *Y*, então nenhum outro ambiente, conexão ou os identificadores de instrução que existem simultaneamente ao mesmo tempo que *X* terão um valor de contexto de *Y*e nenhum outro valores de contexto serão associados ao identificador *X*. Se a operação do provedor que está sendo realizada não tiver um contexto de identificador específico, (por exemplo, chamadas SQLSetConnectAttr para carregar e configurar provedores, em que não há nenhum identificador de instrução), o valor de contexto correspondente na estrutura será nulo.


## <a name="example"></a>Exemplo

### <a name="keystore-provider"></a>Provedor de repositório de chaves

O código a seguir é um exemplo de uma implementação mínima do provedor de repositório de chaves.

```
/* Custom Keystore Provider Example

Windows:   compile with cl MyKSP.c /LD /MD /link /out:MyKSP.dll
Linux/Mac: compile with gcc -fshort-wchar -fPIC -o MyKSP.so -shared MyKSP.c

 */

#ifdef _WIN32
#include <windows.h>
#else
#define __stdcall
#endif

#include <stdlib.h>
#include <sqltypes.h>
#include "msodbcsql.h"
#include <sql.h>
#include <sqlext.h>

int __stdcall KeystoreInit(CEKEYSTORECONTEXT *ctx, errFunc *onError) {
    printf("KSP Init() function called\n");
    return 1;
}

static unsigned char *g_encryptKey;
static unsigned int g_encryptKeyLen;

int __stdcall KeystoreWrite(CEKEYSTORECONTEXT *ctx, errFunc *onError, void *data, unsigned int len) {
    printf("KSP Write() function called (%d bytes)\n", len);
    if (len) {
        if (g_encryptKey)
            free(g_encryptKey);
        g_encryptKey = malloc(len);
        if (!g_encryptKey) {
            onError(ctx, L"Memory Allocation Error");
            return 0;
        }
        memcpy(g_encryptKey, data, len);
        g_encryptKeyLen = len;
    }
    return 1;
}

// Very simple "encryption" scheme - rotating XOR with the key
int __stdcall KeystoreDecrypt(CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg,
    unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen) {
    unsigned int i;
    printf("KSP Decrypt() function called (keypath=%S alg=%S ecekLen=%u)\n", keyPath, alg, ecekLen);
    if (wcscmp(keyPath, L"TheOneAndOnlyKey")) {
        onError(ctx, L"Invalid key path");
        return 0;
    }
    if (wcscmp(alg, L"none")) {
        onError(ctx, L"Invalid algorithm");
        return 0;
    }
    if (!g_encryptKey) {
        onError(ctx, L"Keystore provider not initialized with key");
        return 0;
    }
#ifndef _WIN32
    *cekOut = malloc(ecekLen);
#else
    *cekOut = LocalAlloc(LMEM_FIXED, ecekLen);
#endif
    if (!*cekOut) {
        onError(ctx, L"Memory Allocation Error");
        return 0;
    }
    *cekLen = ecekLen;
    for (i = 0; i < ecekLen; i++)
        (*cekOut)[i] = ecek[i] ^ g_encryptKey[i % g_encryptKeyLen];
    return 1;
}

// Note that in the provider interface, this function would be referenced via the CEKEYSTOREPROVIDER
// structure. However, that does not preclude keystore providers from exporting their own functions,
// as illustrated by this example where the encryption is performed via a separate function (with a
// different prototype than the one in the KSP interface.)
#ifdef _WIN32
__declspec(dllexport)
#endif
int KeystoreEncrypt(CEKEYSTORECONTEXT *ctx, errFunc *onError,
    unsigned char *cek, unsigned short cekLen,
    unsigned char **ecekOut, unsigned short *ecekLen) {
    unsigned int i;
    printf("KSP Encrypt() function called (cekLen=%u)\n", cekLen);
    if (!g_encryptKey) {
        onError(ctx, L"Keystore provider not initialized with key");
        return 0;
    }
    *ecekOut = malloc(cekLen);
    if (!*ecekOut) {
        onError(ctx, L"Memory Allocation Error");
        return 0;
    }
    *ecekLen = cekLen;
    for (i = 0; i < cekLen; i++)
        (*ecekOut)[i] = cek[i] ^ g_encryptKey[i % g_encryptKeyLen];
    return 1;
}

CEKEYSTOREPROVIDER MyCustomKSPName_desc = {
    L"MyCustomKSPName",
    KeystoreInit,
    0,
    KeystoreWrite,
    KeystoreDecrypt,
    0
};

#ifdef _WIN32
__declspec(dllexport)
#endif
CEKEYSTOREPROVIDER *CEKeystoreProvider[] = {
    &MyCustomKSPName_desc,
    0
};
```

### <a name="odbc-application"></a>Aplicativo ODBC

O código a seguir é um aplicativo de demonstração que usa o provedor de keystore acima. Ao executá-lo, verifique se a biblioteca do provedor está no mesmo diretório que o binário do aplicativo e se a cadeia de conexão especifica (ou especifica um DSN que contém `ColumnEncryption=Enabled` ) a configuração.

```
/*
 Example application for demonstration of custom keystore provider usage

Windows:   compile with cl /MD kspapp.c /link odbc32.lib
Linux/Mac: compile with gcc -o kspapp -fshort-wchar kspapp.c -lodbc -ldl
 
 usage: kspapp connstr

 */

#define KSPNAME L"MyCustomKSPName"
#define PROV_ENCRYPT_KEY "JHKCWYT06N3RG98J0MBLG4E3"

#include <stdio.h>
#include <stdlib.h>
#ifdef _WIN32
#include <windows.h>
#else
#define __stdcall
#include <dlfcn.h>
#endif
#include <sql.h>
#include <sqlext.h>
#include "msodbcsql.h"

/* Convenience functions */

int checkRC(SQLRETURN rc, char *msg, int ret, SQLHANDLE h, SQLSMALLINT ht) {
    if (rc == SQL_ERROR) {
        fprintf(stderr, "Error occurred upon %s\n", msg);
        if (h) {
            SQLSMALLINT i = 0;
            SQLSMALLINT outlen = 0;
            char errmsg[1024];
            while ((rc = SQLGetDiagField(
                ht, h, ++i, SQL_DIAG_MESSAGE_TEXT, errmsg, sizeof(errmsg), &outlen)) == SQL_SUCCESS
                || rc == SQL_SUCCESS_WITH_INFO) {
                fprintf(stderr, "Err#%d: %s\n", i, errmsg);
            }
        }
        if (ret)
            exit(ret);
        return 0;
    }
    else if (rc == SQL_SUCCESS_WITH_INFO && h) {
        SQLSMALLINT i = 0;
        SQLSMALLINT outlen = 0;
        char errmsg[1024];
        printf("Success with info for %s:\n", msg);
        while ((rc = SQLGetDiagField(
            ht, h, ++i, SQL_DIAG_MESSAGE_TEXT, errmsg, sizeof(errmsg), &outlen)) == SQL_SUCCESS
            || rc == SQL_SUCCESS_WITH_INFO) {
            fprintf(stderr, "Msg#%d: %s\n", i, errmsg);
        }
    }
    return 1;
}

void postKspError(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...) {
    if (msg > (wchar_t*)65535)
        wprintf(L"Provider emitted message: %s\n", msg);
    else
        wprintf(L"Provider emitted message ID %d\n", msg);
}

int main(int argc, char **argv) {
    char sqlbuf[1024];
    SQLHENV env;
    SQLHDBC dbc;
    SQLHSTMT stmt;
    SQLRETURN rc;
    unsigned char CEK[32];
    unsigned char *ECEK;
    unsigned short ECEKlen;
#ifdef _WIN32
    HMODULE hProvLib;
#else
    void *hProvLib;
#endif
    CEKEYSTORECONTEXT ctx = {0};
    CEKEYSTOREPROVIDER **ppKsp, *pKsp;
    int(__stdcall *pEncryptCEK)(CEKEYSTORECONTEXT *, errFunc *, unsigned char *, unsigned short, unsigned char **, unsigned short *);
    int i;
    if (argc < 2) {
        fprintf(stderr, "usage: kspapp connstr\n");
        return 1;
    }

    /* Load the provider library */
#ifdef _WIN32
    if (!(hProvLib = LoadLibrary("MyKSP.dll"))) {
#else
    if (!(hProvLib = dlopen("./MyKSP.so", RTLD_NOW))) {
#endif
        fprintf(stderr, "Error loading KSP library\n");
        return 2;
    }
#ifdef _WIN32
    if (!(ppKsp = (CEKEYSTOREPROVIDER**)GetProcAddress(hProvLib, "CEKeystoreProvider"))) {
#else
    if (!(ppKsp = (CEKEYSTOREPROVIDER**)dlsym(hProvLib, "CEKeystoreProvider"))) {
#endif
        fprintf(stderr, "The export CEKeystoreProvider was not found in the KSP library\n");
        return 3;
    }
    while (pKsp = *ppKsp++) {
        if (!memcmp(KSPNAME, pKsp->Name, sizeof(KSPNAME)))
            goto FoundProv;
    }
    fprintf(stderr, "Could not find provider in the library\n");
    return 4;
FoundProv:
    if (pKsp->Init && !pKsp->Init(&ctx, postKspError)) {
        fprintf(stderr, "Could not initialize provider\n");
        return 5;
    }
#ifdef _WIN32
    if (!(pEncryptCEK = (LPVOID)GetProcAddress(hProvLib, "KeystoreEncrypt"))) {
#else
    if (!(pEncryptCEK = dlsym(hProvLib, "KeystoreEncrypt"))) {
#endif
        fprintf(stderr, "The export KeystoreEncrypt was not found in the KSP library\n");
        return 6;
    }
    if (!pKsp->Write) {
        fprintf(stderr, "Provider does not support configuration\n");
        return 7;
    }

    /* Configure the provider with the key */
    if (!pKsp->Write(&ctx, postKspError, PROV_ENCRYPT_KEY, strlen(PROV_ENCRYPT_KEY))) {
        fprintf(stderr, "Error writing to KSP\n");
        return 8;
    }

    /* Generate a CEK and encrypt it with the provider */
    srand(time(0) ^ getpid());
    for (i = 0; i < sizeof(CEK); i++)
        CEK[i] = rand();

    if (!pEncryptCEK(&ctx, postKspError, CEK, sizeof(CEK), &ECEK, &ECEKlen)) {
        fprintf(stderr, "Error encrypting CEK\n");
        return 9;
    }

    /* Connect to Server */
    rc = SQLAllocHandle(SQL_HANDLE_ENV, NULL, &env);
    checkRC(rc, "allocating environment handle", 2, 0, 0);
    rc = SQLSetEnvAttr(env, SQL_ATTR_ODBC_VERSION, (SQLPOINTER)SQL_OV_ODBC3, 0);
    checkRC(rc, "setting ODBC version to 3.0", 3, env, SQL_HANDLE_ENV);
    rc = SQLAllocHandle(SQL_HANDLE_DBC, env, &dbc);
    checkRC(rc, "allocating connection handle", 4, env, SQL_HANDLE_ENV);
    rc = SQLDriverConnect(dbc, 0, argv[1], strlen(argv[1]), NULL, 0, NULL, SQL_DRIVER_NOPROMPT);
    checkRC(rc, "connecting to data source", 5, dbc, SQL_HANDLE_DBC);
    rc = SQLAllocHandle(SQL_HANDLE_STMT, dbc, &stmt);
    checkRC(rc, "allocating statement handle", 6, dbc, SQL_HANDLE_DBC);

    /* Create a CMK definition on the server */
    {
        static char cmkSql[] = "CREATE COLUMN MASTER KEY CustomCMK WITH ("
            "KEY_STORE_PROVIDER_NAME = 'MyCustomKSPName',"
            "KEY_PATH = 'TheOneAndOnlyKey')";
        printf("Create CMK: %s\n", cmkSql);
        SQLExecDirect(stmt, cmkSql, SQL_NTS);
    }

    /* Create a CEK definition on the server */
    {
        const char cekSqlBefore[] = "CREATE COLUMN ENCRYPTION KEY CustomCEK WITH VALUES ("
            "COLUMN_MASTER_KEY = CustomCMK,"
            "ALGORITHM = 'none',"
            "ENCRYPTED_VALUE = 0x";
        char *cekSql = malloc(sizeof(cekSqlBefore) + 2 * ECEKlen + 2); /* 1 for ')', 1 for null terminator */
        strcpy(cekSql, cekSqlBefore);
        for (i = 0; i < ECEKlen; i++)
            sprintf(cekSql + sizeof(cekSqlBefore) - 1 + 2 * i, "%02x", ECEK[i]);
        strcat(cekSql, ")");
        printf("Create CEK: %s\n", cekSql);
        SQLExecDirect(stmt, cekSql, SQL_NTS);
        free(cekSql);
#ifdef _WIN32
        LocalFree(ECEK);
#else
        free(ECEK);
#endif
    }

#ifdef _WIN32
    FreeLibrary(hProvLib);
#else
    dlclose(hProvLib);
#endif

    /* Create a table with encrypted columns */
    {
        static char *tableSql = "CREATE TABLE CustomKSPTestTable ("
            "c1 int,"
            "c2 varchar(255) COLLATE Latin1_General_BIN2 ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = CustomCEK, ENCRYPTION_TYPE = DETERMINISTIC, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256'))";
        printf("Create table: %s\n", tableSql);
        SQLExecDirect(stmt, tableSql, SQL_NTS);
    }

    /* Load provider into the ODBC Driver and configure it */
    {
        unsigned char ksd[sizeof(CEKEYSTOREDATA) + sizeof(PROV_ENCRYPT_KEY) - 1];
        CEKEYSTOREDATA *pKsd = (CEKEYSTOREDATA*)ksd;
        pKsd->name = L"MyCustomKSPName";
        pKsd->dataSize = sizeof(PROV_ENCRYPT_KEY) - 1;
        memcpy(pKsd->data, PROV_ENCRYPT_KEY, sizeof(PROV_ENCRYPT_KEY) - 1);
#ifdef _WIN32
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREPROVIDER, "MyKSP.dll", SQL_NTS);
#else
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREPROVIDER, "./MyKSP.so", SQL_NTS);
#endif
        checkRC(rc, "Loading KSP into ODBC Driver", 7, dbc, SQL_HANDLE_DBC);
        rc = SQLSetConnectAttr(dbc, SQL_COPT_SS_CEKEYSTOREDATA, (SQLPOINTER)pKsd, SQL_IS_POINTER);
        checkRC(rc, "Configuring the KSP", 7, dbc, SQL_HANDLE_DBC);
    }

    /* Insert some data */
    {
        int c1;
        char c2[256];
        rc = SQLBindParameter(stmt, 1, SQL_PARAM_INPUT, SQL_C_LONG, SQL_INTEGER, 0, 0, &c1, 0, 0);
        checkRC(rc, "Binding parameters for insert", 9, stmt, SQL_HANDLE_STMT);
        rc = SQLBindParameter(stmt, 2, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_VARCHAR, 255, 0, c2, 255, 0);
        checkRC(rc, "Binding parameters for insert", 9, stmt, SQL_HANDLE_STMT);
        for (i = 0; i < 10; i++) {
            c1 = i * 10 + i + 1;
            sprintf(c2, "Sample data %d for column 2", i);
            rc = SQLExecDirect(stmt, "INSERT INTO CustomKSPTestTable (c1, c2) values (?, ?)", SQL_NTS);
            checkRC(rc, "Inserting rows query", 10, stmt, SQL_HANDLE_STMT);
        }
        printf("(Encrypted) data has been inserted into the [CustomKSPTestTable]. You may inspect the data now.\n"
            "Press Enter to continue...\n");
        getchar();
    }

    /* Retrieve the data */
    {
        int c1;
        char c2[256];
        rc = SQLBindCol(stmt, 1, SQL_C_LONG, &c1, 0, 0);
        checkRC(rc, "Binding columns for select", 11, stmt, SQL_HANDLE_STMT);
        rc = SQLBindCol(stmt, 2, SQL_C_CHAR, c2, sizeof(c2), 0);
        checkRC(rc, "Binding columns for select", 11, stmt, SQL_HANDLE_STMT);
        rc = SQLExecDirect(stmt, "SELECT c1, c2 FROM CustomKSPTestTable", SQL_NTS);
        checkRC(rc, "Retrieving rows query", 12, stmt, SQL_HANDLE_STMT);
        while (SQL_SUCCESS == (rc = SQLFetch(stmt)))
            printf("Retrieved data: c1=%d c2=%s\n", c1, c2);
        SQLFreeStmt(stmt, SQL_CLOSE);
        printf("Press Enter to clean up and exit...\n");
        getchar();
    }

    /* Clean up */
    {
        SQLExecDirect(stmt, "DROP TABLE CustomKSPTestTable", SQL_NTS);
        SQLExecDirect(stmt, "DROP COLUMN ENCRYPTION KEY CustomCEK", SQL_NTS);
        SQLExecDirect(stmt, "DROP COLUMN MASTER KEY CustomCMK", SQL_NTS);
        printf("Removed table, CEK, and CMK\n");
    }
    SQLDisconnect(dbc);
    SQLFreeHandle(SQL_HANDLE_DBC, dbc);
    SQLFreeHandle(SQL_HANDLE_ENV, env);
    return 0;
}

```

## <a name="see-also"></a>Consulte Também

[Uso do Always Encrypted com o Driver ODBC](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)

---
title: Provedores de armazenamento de chaves personalizado | Microsoft Docs
ms.custom: ''
ms.date: 07/12/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a6166d7d-ef34-4f87-bd1b-838d3ca59ae7
ms.author: v-chojas
manager: craigg
author: MightyPen
ms.openlocfilehash: 59a1458c98fb12f2f053bfd71649f40ddc5d1e4e
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55047210"
---
# <a name="custom-keystore-providers"></a>Provedores de repositório de chaves personalizado
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

## <a name="overview"></a>Visão geral

O recurso de criptografia de coluna do SQL Server 2016 requer que o criptografados coluna chaves de criptografia (ECEKs) armazenados no servidor ser recuperada pelo cliente e, em seguida, descriptografadas para chaves de criptografia de coluna (CEKs) para acessar os dados armazenados em colunas criptografadas. ECEKs são criptografadas por chaves mestras de coluna (CMKs) e a segurança de CMK é importante para a segurança de criptografia de coluna. Portanto, a CMK deve ser armazenada em um local seguro; a finalidade de um provedor de repositório de chaves de criptografia de coluna é fornecer uma interface para permitir que o driver ODBC para acessá-los com segurança armazenados CMKs. Para usuários com seu próprio armazenamento seguro, a Interface do provedor de repositório de chaves personalizado fornece uma estrutura para a implementação de acesso para proteger o armazenamento de CMK para o driver ODBC, que pode ser usado para executar a descriptografia e criptografia de CEK.

Cada provedor de repositório de chaves contém e gerencia um ou mais CMKs, que são identificados por caminhos de chave - cadeias de caracteres de um formato definido pelo provedor. Isso, com o algoritmo de criptografia, e também uma cadeia de caracteres definido pelo provedor, pode ser usado para executar a criptografia de uma CEK e a descriptografia de um ECEK. O algoritmo, juntamente com o ECEK e o nome do provedor, são armazenados em metadados de criptografia do banco de dados. ver [CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md) e [CREATE COLUMN ENCRYPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md) para obter mais informações. Assim, as duas operações fundamentais de gerenciamento de chaves são:

```
CEK = DecryptViaCEKeystoreProvider(CEKeystoreProvider_name, Key_path, Key_algorithm, ECEK)

-and-

ECEK = EncryptViaCEKeystoreProvider(CEKeyStoreProvider_name, Key_path, Key_algorithm, CEK)
```

onde o `CEKeystoreProvider_name` é usado para identificar o provedor específico de repositório de chaves de criptografia do coluna (CEKeystoreProvider), e os outros argumentos são usados pelo CEKeystoreProvider para criptografar/descriptografar a CEK (E). O nome e caminho-chave são fornecidas pelos metadados CMK, enquanto o algoritmo e o valor ECEK são fornecidas pelos metadados CEK. Vários provedores de repositório de chaves podem estar presentes junto com os provedores internos de padrão. Após realizar uma operação que exige a CEK, o driver usa os metadados CMK para localizar o provedor de keystore apropriado por nome e executa sua operação de descriptografia, que pode ser expresso como:

```
CEK = CEKeyStoreProvider_specific_decrypt(Key_path, Key_algorithm, ECEK)
```

Embora o driver tem não criptografam CEKs é necessário, uma ferramenta de gerenciamento de chaves talvez precise fazer isso para implementar operações como criação de CMK e rotação. Isso requer que a operação inversa:

```
ECEK = CEKeyStoreProvider_specific_encrypt(Key_path, Key_algorithm, CEK)
```

### <a name="cekeystoreprovider-interface"></a>Interface CEKeyStoreProvider

Este documento descreve detalhadamente a interface CEKeyStoreProvider. Um provedor de repositório de chaves que implementa essa interface pode ser usado pelo Microsoft ODBC Driver para SQL Server. Os implementadores de CEKeyStoreProvider podem usar este guia para desenvolver provedores de armazenamento de chaves personalizado utilizáveis pelo driver.

Uma biblioteca do provedor de repositório de chaves ("biblioteca de provedor") é uma biblioteca de vínculo dinâmico que pode ser carregada pelo driver ODBC e contém um ou mais provedores de repositório de chaves. O símbolo `CEKeystoreProvider` deve ser exportado por uma biblioteca de provedor e seja o endereço de uma matriz terminada em nulo de ponteiros para `CEKeystoreProvider` estruturas, uma para cada provedor de repositório de chaves dentro da biblioteca.

Um `CEKeystoreProvider` estrutura define os pontos de entrada de um provedor de repositório de chaves único:

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
|`Name`|O nome do provedor de repositório de chaves. Ele não deve ser o mesmo que qualquer outro provedor de repositório de chaves carregado anteriormente pelo driver ou presente nessa biblioteca. Cadeia de caracteres largos* terminada em nulo.|
|`Init`|Função de inicialização. Se uma função de inicialização não for necessária, esse campo pode ser nulo.|
|`Read`|Função read do provedor. Pode ser nulo se não é necessário.|
|`Write`|Função de gravação do provedor. Obrigatório se a leitura não for nula. Pode ser nulo se não é necessário.|
|`DecryptCEK`|Função de descriptografia do ECEK. Essa função é o motivo da existência de um provedor de repositório de chaves e não pode ser nula.|
|`EncryptCEK`|Função de criptografia de CEK. O driver não chama essa função, mas ele é fornecido para permitir o acesso programático a criação de ECEK pelas ferramentas de gerenciamento de chaves. Pode ser nulo se não é necessário.|
|`Free`|Função de terminação. Pode ser nulo se não é necessário.|

Exceto gratuito, as funções nessa interface todos têm um par de parâmetros, **ctx** e **onError**. O primeiro identifica o contexto no qual a função é chamada, enquanto o segundo é usado para relatar erros. Ver [contextos](#context-association) e [tratamento de erros](#error-handling) abaixo para obter mais informações.

```
int Init(CEKEYSTORECONTEXT *ctx, errFunc onError);
```
Nome do espaço reservado para uma função de inicialização definidos pelo provedor. O driver chama essa função uma vez, depois que um provedor foi carregado, mas antes da primeira vez que ele precisa para executar a descriptografia ECEK ou Read()/Write() solicita. Use esta função para executar qualquer inicialização que ele precisa. 

|Argumento|Descrição|
|:--|:--|
|`ctx`|[Entrada] Contexto de operação.|
|`onError`|[Entrada] Função de relatório de erros.|
|`Return Value`|Retorne diferente de zero para indicar êxito, ou zero para indicar falha.|

```
int Read(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int *len);
```

Nome do espaço reservado para uma função definida pelo provedor de comunicação. O driver chama essa função quando o aplicativo solicita para ler dados de um (anteriormente-gravados-to) provedor usando o atributo de conexão SQL_COPT_SS_CEKEYSTOREDATA, permitindo que o aplicativo ler dados arbitrários do provedor. Ver [comunicando-se com provedores de repositório de chaves](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers) para obter mais informações.

|Argumento|Descrição|
|:--|:--|
|`ctx`|[Entrada] Contexto de operação.|
|`onError`|[Entrada] Função de relatório de erros.|
|`data`|[Saída] Ponteiro para um buffer no qual o provedor grava os dados a serem lidos pelo aplicativo. Isso corresponde ao campo de dados da estrutura CEKEYSTOREDATA.|
|`len`|[Entrada/saída] Ponteiro para um valor de comprimento; Após a entrada, isso é o comprimento máximo do buffer de dados e o provedor não deverá gravar mais de * len bytes a ele. Após o retorno, o provedor deve atualizar * len com o número de bytes gravados.|
|`Return Value`|Retorne diferente de zero para indicar êxito, ou zero para indicar falha.|

```
int Write(CEKEYSTORECONTEXT *ctx, errFunc onError, void *data, unsigned int len);
```
Nome do espaço reservado para uma função definida pelo provedor de comunicação. O driver chama essa função quando o aplicativo solicita para gravar dados em um provedor usando o atributo de conexão SQL_COPT_SS_CEKEYSTOREDATA, permitindo que o aplicativo gravar dados arbitrários para o provedor. Ver [comunicando-se com provedores de repositório de chaves](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#communicating-with-keystore-providers) para obter mais informações.

|Argumento|Descrição|
|:--|:--|
|`ctx`|[Entrada] Contexto de operação.|
|`onError`|[Entrada] Função de relatório de erros.|
|`data`|[Entrada] Ponteiro para um buffer que contém os dados para o provedor de ler. Isso corresponde ao campo de dados da estrutura CEKEYSTOREDATA. O provedor não deve ler mais do que bytes de len nesse buffer.|
|`len`|[Entrada] O número de bytes disponíveis nos dados. Isso corresponde ao campo dataSize da estrutura CEKEYSTOREDATA.|
|`Return Value`|Retorne diferente de zero para indicar êxito, ou zero para indicar falha.|

```
int (*DecryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *ecek, unsigned short ecekLen, unsigned char **cekOut, unsigned short *cekLen);
```
Nome do espaço reservado para uma função definida pelo provedor de descriptografia de ECEK. O driver chama essa função para descriptografar um ECEK criptografado por uma CMK associada a este provedor em uma CEK.

|Argumento|Descrição|
|:--|:--|
|`ctx`|[Entrada] Contexto de operação.|
|`onError`|[Entrada] Função de relatório de erros.|
|`keyPath`|[Entrada] O valor de [KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) atributo de metadados para a CMK referenciado pelo ECEK determinado. Cadeia de caracteres largos* terminada em nulo. Isso serve para identificar uma CMK manipulada por esse provedor.|
|`alg`|[Entrada] O valor da [ALGORITMO](../../t-sql/statements/create-column-encryption-key-transact-sql.md) atributo de metadados para o determinado ECEK. Cadeia de caracteres largos* terminada em nulo. Isso serve para identificar o algoritmo de criptografia usado para criptografar o ECEK determinado.|
|`ecek`|[Entrada] Ponteiro para o ECEK a ser descriptografado.|
|`ecekLen`|[Entrada] Comprimento do ECEK.|
|`cekOut`|[Saída] O provedor deverá alocar memória para o ECEK descriptografado e gravar seu endereço de ponteiro apontado por cekOut. Deve ser possível liberar este bloco de memória usando o [LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) ou libere a função (Linux/Mac). Se nenhuma memória foi alocada devido a um erro ou caso contrário, o provedor deverá definir * cekOut como um ponteiro nulo.|
|`cekLen`|[Saída] O provedor deve gravar para o endereço apontado pelo cekLen quanto o ECEK descriptografado que ele foi escrito para * * cekOut.|
|`Return Value`|Retorne diferente de zero para indicar êxito, ou zero para indicar falha.|

```
int (*EncryptCEK)( CEKEYSTORECONTEXT *ctx, errFunc *onError, const wchar_t *keyPath, const wchar_t *alg, unsigned char *cek,unsigned short cekLen, unsigned char **ecekOut, unsigned short *ecekLen);
```
Nome do espaço reservado para uma função definida pelo provedor de criptografia de CEK. O driver não chamar essa função nem expor sua funcionalidade por meio da interface do ODBC, mas ele é fornecido para permitir o acesso programático a criação de ECEK pelas ferramentas de gerenciamento de chaves.

|Argumento|Descrição|
|:--|:--|
|`ctx`|[Entrada] Contexto de operação.|
|`onError`|[Entrada] Função de relatório de erros.|
|`keyPath`|[Entrada] O valor de [KEY_PATH](../../t-sql/statements/create-column-master-key-transact-sql.md) atributo de metadados para a CMK referenciado pelo ECEK determinado. Cadeia de caracteres largos* terminada em nulo. Isso serve para identificar uma CMK manipulada por esse provedor.|
|`alg`|[Entrada] O valor da [ALGORITMO](../../t-sql/statements/create-column-encryption-key-transact-sql.md) atributo de metadados para o determinado ECEK. Cadeia de caracteres largos* terminada em nulo. Isso serve para identificar o algoritmo de criptografia usado para criptografar o ECEK determinado.|
|`cek`|[Entrada] Ponteiro para a CEK sejam criptografados.|
|`cekLen`|[Entrada] Comprimento da CEK.|
|`ecekOut`|[Saída] O provedor deverá alocar memória para a CEK criptografada e gravar seu endereço de ponteiro apontado por ecekOut. Deve ser possível liberar este bloco de memória usando o [LocalFree](/windows/desktop/api/winbase/nf-winbase-localfree) (Windows) ou libere a função (Linux/Mac). Se nenhuma memória foi alocada devido a um erro ou caso contrário, o provedor deverá definir * ecekOut como um ponteiro nulo.|
|`ecekLen`|[Saída] O provedor deve gravar para o endereço apontado pelo ecekLen o comprimento da CEK criptografado que ele foi escrito para * * ecekOut.|
|`Return Value`|Retorne diferente de zero para indicar êxito, ou zero para indicar falha.|

```
void (*Free)();
```
Nome do espaço reservado para uma função definida pelo provedor de encerramento. O driver pode chamar essa função após o término normal do processo.

> [!NOTE]
> *Cadeias de caracteres largos são caracteres de 2 bytes (UTF-16) devido a como o SQL Server armazena-os.*


### <a name="error-handling"></a>Tratamento de erros

Poderão ocorrer erros durante o processamento de um provedor, um mecanismo é fornecido para permitir que ele para relatar erros de volta para o driver em detalhes mais específicos do que um booliano êxito/falha. Muitas das funções têm um par de parâmetros, **ctx** e **onError**, que são usados em conjunto para essa finalidade, além do valor de retorno de êxito/falha.

O **ctx** parâmetro identifica o contexto no qual ocorre uma operação do provedor.

O **onError** parâmetro aponta para uma função de relatório de erros, com o seguinte protótipo:

`typedef void errFunc(CEKEYSTORECONTEXT *ctx, const wchar_t *msg, ...);`

|Argumento|Descrição|
|:--|:--|
|`ctx`|[Entrada] O contexto para relatar o erro.|
|`msg`|[Entrada] A mensagem de erro para o relatório. Cadeia de caracteres largos terminada em nulo. Para permitir que as informações com parâmetros esteja presente, essa cadeia de caracteres pode conter as sequências de formatação de inserção no formato aceito pelo [FormatMessage](/windows/desktop/api/winbase/nf-winbase-formatmessage) função. Funcionalidade estendida pode ser especificada por esse parâmetro, conforme descrito abaixo.|
|...|[Entrada] Parâmetros adicionais variadic para caber especificadores de formato na mensagem, conforme apropriado.|

Para relatar quando ocorreu um erro, o provedor chamadas onError, fornecendo o parâmetro de contexto passado para a função de provedor, o driver e uma mensagem de erro com parâmetros adicionais opcionais a serem formatados nele. O provedor pode chamar essa função várias vezes para enviar várias mensagens de erro consecutivamente na invocação de uma função de provedor. Por exemplo:

```
    if (!doSomething(...))
    {
        onError(ctx, L"An error occurred in doSomething.");
        onError(ctx, L"Additional error message with more details.");
        return 0;
    }
```


O `msg` parâmetro normalmente é uma cadeia de caracteres largos, mas extensões adicionais estão disponíveis:

Usando um dos valores predefinidos especiais com a macro IDS_MSG, mensagens de erro genéricas já existentes e em um formulário implementações localizado no driver podem ser utilizada. Por exemplo, se um provedor falhar ao alocar memória, o `IDS_S1_001` mensagem "Falha de alocação de memória" pode ser usada:

`onError(ctx, IDS_MSG(IDS_S1_001));`

Para o erro a ser reconhecido pelo driver, a função de provedor deve retornar a falha. Quando isso é executado no contexto de uma operação de ODBC, os erros lançados se tornará acessíveis no identificador de conexão ou instrução por meio do mecanismo de diagnóstico ODBC padrão (`SQLError`, `SQLGetDiagRec`, e `SQLGetDiagField`).


### <a name="context-association"></a>Associação de contexto

O `CEKEYSTORECONTEXT` estrutura, além de fornecer contexto para o retorno de chamada do erro, também pode ser usada para determinar o contexto ODBC, no qual uma operação de provedor é executada. Isso permite que um provedor associar dados a cada um desses contextos, por exemplo, para implementar a configuração por conexão. Para essa finalidade, a estrutura contém 3 ponteiros opacos correspondente ao contexto de ambiente, conexão e instrução:

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
|`dbcCtx`|Contexto de Conexão.|
|`stmtCtx`|Contexto de instrução.|

Cada um desses contextos é um valor opaco que, ao mesmo tempo em que não o mesmo que o identificador de ODBC correspondente, pode ser usado como um identificador exclusivo para o identificador: se tratar *X* está associado com o valor de contexto *Y*, em seguida, Nenhum outros ambiente, conexão ou instrução alças que existe simultaneamente no mesmo tempo em que *X* terá um valor de contexto do *Y*, e não será associado a nenhum outro valor de contexto manipular *X*. Se a operação de provedor que está sendo feita não tiver um contexto de identificador em particular, (por exemplo, chamadas de SQLSetConnectAttr para carregar e configurar provedores, em que não há nenhum identificador de instrução) correspondente, o valor de contexto na estrutura é nulo.


## <a name="example"></a>Exemplo

### <a name="keystore-provider"></a>Provedor de repositório de chaves

O código a seguir é um exemplo de uma implementação de provedor de repositório de chaves mínima.

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

### <a name="odbc-application"></a>Aplicativo de ODBC

O código a seguir é um aplicativo de demonstração que usa o provedor de repositório de chaves acima. Ao executá-lo, certifique-se de que a biblioteca do provedor está no mesmo diretório que o binário do aplicativo, e que especifica a cadeia de caracteres de conexão (ou especifica um DSN que contém) o `ColumnEncryption=Enabled` configuração.

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

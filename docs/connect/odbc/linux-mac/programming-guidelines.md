---
title: Diretrizes de programação (Driver ODBC)
description: Os recursos de programação do Microsoft ODBC Driver for SQL Server no macOS e Linux são baseados em ODBC no SQL Server Native Client (ODBC).
ms.custom: ''
ms.date: 01/12/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: v-makouz
ms.author: v-daenge
ms.openlocfilehash: ecaa595fa08a4a37c9a5d3146dd03af440aa4453
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81632786"
---
# <a name="programming-guidelines"></a>Diretrizes de programação

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Os recursos de programação do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em macOS e Linux são baseados em ODBC no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ([SQL Server Native Client (ODBC)](https://go.microsoft.com/fwlink/?LinkID=134151)). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client é baseado em ODBC no Windows Data Access Components ([Referência do Programador de ODBC](https://go.microsoft.com/fwlink/?LinkID=45250)).  

Um aplicativo ODBC pode usar MARS (conjuntos de resultados ativos múltiplos) e outros recursos específicos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], incluindo `/usr/local/include/msodbcsql.h`, após a inclusão dos cabeçalhos unixODBC (`sql.h`, `sqlext.h`, `sqltypes.h` e `sqlucode.h`). Em seguida, use os mesmos nomes simbólicos para os itens específicos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que você usaria em seus aplicativos ODBC do Windows.

## <a name="available-features"></a>Recursos disponíveis  
As seguintes seções da documentação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para ODBC ([SQL Server Native Client (ODBC)](https://go.microsoft.com/fwlink/?LinkID=134151)) são válidas ao usar o driver ODBC em macOS e Linux:  

-   [Comunicando-se com o SQL Server (ODBC)](https://msdn.microsoft.com/library/ms131692.aspx)  
-   [Suporte de tempo limite de conexão e consulta](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
-   [Cursores](../../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
-   [Aprimoramentos de data/hora (ODBC)](https://msdn.microsoft.com/library/bb677319.aspx)  
-   [Executando consultas (ODBC)](https://msdn.microsoft.com/library/ms131677.aspx)  
-   [Tratando de erros e mensagens](../../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
-   [Autenticação Kerberos](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)  
-   [Tipos de dados CLR grandes definidos pelo usuário (ODBC)](https://msdn.microsoft.com/library/bb677316.aspx)  
-   [Executando transações (ODBC) (exceto transações distribuídas)](https://msdn.microsoft.com/library/ms131706.aspx)  
-   [Processando resultados (ODBC)](https://msdn.microsoft.com/library/ms130812.aspx)  
-   [Executando procedimentos armazenados](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)
-   [Suporte a colunas esparsas (ODBC)](https://msdn.microsoft.com/library/cc280357.aspx)
-   [Usando criptografia sem validação](../../../relational-databases/native-client/features/using-encryption-without-validation.md)
-   [Parâmetros com valor de tabela](https://docs.microsoft.com/sql/relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc)
-   [UTF-8 e UTF-16 para a API de comando e dados](https://msdn.microsoft.com/library/ff878241.aspx)
-   [Usando funções de catálogo](../../../relational-databases/native-client/odbc/using-catalog-functions.md)  

## <a name="unsupported-features"></a>Recursos sem suporte

Os recursos a seguir não foram verificados para funcionar corretamente nesta versão do driver ODBC em Linux e macOS:

-   Conexão de cluster de failover
-   [Resolução IP de Rede Transparente](../using-transparent-network-ip-resolution.md) (antes do ODBC Driver 17)
-   [Rastreamento de Driver Avançado](https://blogs.msdn.microsoft.com/mattn/2012/05/15/enabling-advanced-driver-tracing-for-the-sql-native-client-odbc-drivers/)

Os seguintes recursos não estão disponíveis nesta versão do driver ODBC em macOS e Linux: 

-   Transações distribuídas (não há suporte para o atributo SQL_ATTR_ENLIST_IN_DTC)  
-   Espelhamento de banco de dados  
-   FILESTREAM  
-   Criação de perfil de desempenho do driver ODBC, discutido em [SQLSetConnectAttr](https://go.microsoft.com/fwlink/?LinkId=234099), e dos seguintes atributos de conexão relacionados ao desempenho:  
    -   SQL_COPT_SS_PERF_DATA  
    -   SQL_COPT_SS_PERF_DATA_LOG  
    -   SQL_COPT_SS_PERF_DATA_LOG_NOW  
    -   SQL_COPT_SS_PERF_QUERY  
    -   SQL_COPT_SS_PERF_QUERY_INTERVAL  
    -   SQL_COPT_SS_PERF_QUERY_LOG  
-   SQLBrowseConnect (antes da versão 17.2)
-   Tipos de intervalo de C, como SQL_C_INTERVAL_YEAR_TO_MONTH (documentado em [Identificadores e descritores de tipo de dados](https://msdn.microsoft.com/library/ms716351(VS.85).aspx))
-   O valor SQL_CUR_USE_ODBC do atributo SQL_ATTR_ODBC_CURSORS da função SQLSetConnectAttr.

## <a name="character-set-support"></a>Suporte a conjuntos de caracteres

Para o ODBC Driver 13 e 13.1, os dados SQLCHAR devem ser UTF-8. Não há suporte para nenhuma outra codificação.

Para o ODBC Driver 17, há suporte para dados SQLCHAR em um dos seguintes conjuntos/codificações de caracteres:

> [!NOTE]  
> Devido a diferenças de `iconv` em `musl` e `glibc`, muitos desses locais não são compatíveis com o Alpine Linux.
>
> Para saber mais, confira [Diferenças funcionais do glibc](https://wiki.musl-libc.org/functional-differences-from-glibc.html)

|Nome|Descrição|
|-|-|
|UTF-8|Unicode|
|CP437|MS-DOS Latim EUA|
|CP850|MS-DOS Latim 1|
|CP874|Latim/tailandês|
|CP932|Japonês, Shift-JIS|
|CP936|Chinês simplificado, GBK|
|CP949|Coreano, EUC-KR|
|CP950|Chinês tradicional, Big5|
|CP1251|Cirílico|
|CP1253|Grego|
|CP1256|Árabe|
|CP1257|Báltico|
|CP1258|Vietnamita|
|ISO-8859-1/CP1252|Latim-1|
|ISO-8859-2/CP1250|Latim-2|
|ISO-8859-3|Latim-3|
|ISO-8859-4|Latim-4|
|ISO-8859-5|Latim/cirílico|
|ISO-8859-6|Latim/árabe|
|ISO-8859-7|Latim/grego|
|ISO-8859-8/CP1255|Hebraico|
|ISO-8859-9/CP1254|Turco|
|ISO-8859-13|Latim-7|
|ISO-8859-15|Latim-9|

Após a conexão, o driver detecta a localidade atual do processo em que ele é carregado. Se ele usa uma das codificações acima, o driver usa a codificação para dados (caractere estreito) SQLCHAR; caso contrário, o padrão é UTF-8. Como todos os processos se iniciam na localidade "C" por padrão (e, portanto, fazem o driver usar UTF-8 como padrão), se um aplicativo precisar usar uma das codificações acima, ele deverá usar a função **setlocale** para definir a localidade adequadamente antes de conectar-se, seja especificando explicitamente a localidade desejada, seja usando uma cadeia de caracteres vazia, por exemplo `setlocale(LC_ALL, "")`, para usar as configurações de localidade do ambiente.

Assim, em um ambiente macOS ou Linux típico no qual a codificação é UTF-8, os usuários do ODBC Driver 17 que atualizarem da versão 13 ou 13.1 não notarão nenhuma diferença. No entanto, aplicativos que usam uma codificação não UTF-8 na lista acima por meio de `setlocale()` precisam usar essa codificação para dados de/para o driver, em vez de UTF-8.

Os dados SQLWCHAR devem ser UTF-16LE (Little Endian).

Ao associar parâmetros de entrada a SQLBindParameter, se o tipo SQL de um caractere estreito, como SQL_VARCHAR, for especificado, o driver converterá os dados fornecidos no da codificação do cliente na codificação [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] padrão (normalmente, página de código 1252). Para parâmetros de saída, o driver converte da codificação especificada nas informações de ordenação associadas aos dados na codificação do cliente. No entanto, é possível haver perda de dados: os caracteres na codificação de origem não representáveis na codificação de destino serão convertidos em um ponto de interrogação ('? ').

Para evitar essa perda de dados ao associar parâmetros de entrada, especifique um tipo de caractere SQL Unicode, como SQL_NVARCHAR. Nesse caso, o driver converte da codificação do cliente em UTF-16, que pode representar todos os caracteres Unicode. Além disso, a coluna ou parâmetro de destino no servidor também pode ser um tipo de Unicode (**nchar**, **nvarchar**, **ntext**) ou um arquivo com uma ordenação/codificação, que pode representar todos os caracteres dos dados de origem originais. Para evitar a perda de dados com parâmetros de saída, especifique um tipo SQL de Unicode e um Unicode tipo C (SQL_C_WCHAR), fazendo o driver retornar dados como UTF-16, ou um tipo C estreito, e verifique se a codificação do cliente pode representar todos os caracteres dos dados de origem (isso sempre é possível com UTF-8.)

Para obter mais informações sobre ordenações e codificações, confira [Compatibilidade com ordenação e Unicode](../../../relational-databases/collations/collation-and-unicode-support.md).

Há algumas diferenças de conversão de codificação entre o Windows e várias versões da biblioteca iconv no Linux e no macOS. Dados de texto na página de código 1255 (hebraico) têm um ponto de código (0xCA) que se comporta de forma diferente após a conversão em Unicode. No Windows, esse caractere converte no ponto de código UTF-16 de 0x05BA. Em macOS e Linux com versões de libiconv anteriores à 1.15, ele converte em 0x00CA. Em Linux com bibliotecas iconv que não dão suporte para a revisão de 2003 de Big5/CP950 (chamada `BIG5-2003`), caracteres adicionados com essa revisão não serão convertidos corretamente. Na página de código 932 (japonês, Shift-JIS), o resultado da decodificação não originalmente definido no padrão de codificação de caracteres também é diferente. Por exemplo, o byte 0x80 é convertido em U+0080 no Windows, mas pode se tornar U+30FB no Linux e no macOS, dependendo da versão iconv.

No ODBC Driver 13 e 13.1, quando caracteres multibyte UTF-8 ou UTF-16 substitutos são divididos em buffers SQLPutData, isso resulta em dados corrompidos. Use buffers para transmitir SQLPutData que não terminem em codificações parciais de caracteres. Essa limitação foi removida com o ODBC Driver 17.

## <a name="openssl"></a><a name="bkmk-openssl"></a>OpenSSL
Da versão 17.4 em diante, o driver carrega o OpenSSL dinamicamente, o que permite que ele seja executado em sistemas com as versões 1.0 ou 1.1 sem precisar de arquivos de driver separados. Quando várias versões do OpenSSL estiverem presentes, o driver tentará carregar a mais recente. O driver é compatível com o OpenSSL 1.0.x e 1.1.x no momento

> [!NOTE]  
> Poderá ocorrer um possível conflito se o aplicativo que usa o driver (ou um de seus componentes) estiver vinculado ou carregar dinamicamente uma versão diferente do OpenSSL. Se várias versões do OpenSSL estiverem presentes no sistema e o aplicativo o usar, tenha cuidado extra para garantir que a versão carregada pelo aplicativo e o driver não sejam incompatíveis, pois os erros podem corromper a memória e, portanto, não serão necessariamente manifestados de maneiras óbvias ou consistentes.

## <a name="alpine-linux"></a><a name="bkmk-alpine"></a>Alpine Linux
No momento em que este artigo foi escrito, o tamanho da pilha padrão em MUSL é de 128 mil, o suficiente para a funcionalidade básica do driver ODBC. No entanto, de acordo com a função do aplicativo, não é difícil exceder esse limite, especialmente ao chamar o driver de vários threads. É recomendável que um aplicativo ODBC no Alpine Linux seja compilado com `-Wl,-z,stack-size=<VALUE IN BYTES>` para aumentar o tamanho da pilha. Para referência, o tamanho de pilha padrão na maioria dos sistemas GLIBC é de 2 MB.

## <a name="additional-notes"></a>Observações adicionais  

1.  Você pode fazer uma conexão de administrador dedicada (DAC) usando autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e **host,porta**. Um membro da função Sysadmin precisa primeiro detectar a porta DAC. Veja [Conexão de diagnóstico para administradores de banco de dados](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators#dac-port) para descobrir como. Por exemplo, se a porta DAC for 33000, você poderá conectá-la ao `sqlcmd` da seguinte maneira:  

    ```
    sqlcmd -U <user> -P <pwd> -S <host>,33000
    ```

    > [!NOTE]  
    > As conexões DAC devem usar a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
    
2.  O gerenciador de driver UnixODBC retorna "identificador de atributo/opção inválido" para todos os atributos de instrução quando eles são passados por meio do SQLSetConnectAttr. No Windows, quando o SQLSetConnectAttr recebe um valor de atributo de instrução, ele faz o driver definir esse valor em todas as instruções ativas que sejam filhos do identificador de conexão.  

3.  Ao usar o driver com aplicativos altamente multi-threaded, a validação do identificador do unixODBC pode se tornar um gargalo de desempenho. Nesses cenários, um desempenho significativamente maior pode ser obtido com a compilação de unixODBC com a opção `--enable-fastvalidate`. No entanto, saiba que isso pode fazer com que os aplicativos que passam identificadores inválidos para APIs do ODBC falhem em vez de retornar erros de `SQL_INVALID_HANDLE`.

## <a name="see-also"></a>Consulte Também  
[Perguntas frequentes](frequently-asked-questions-faq-for-odbc-linux.md)

[Problemas conhecidos nesta versão do driver](known-issues-in-this-version-of-the-driver.md)

[Notas de Versão](release-notes-odbc-sql-server-linux-mac.md)

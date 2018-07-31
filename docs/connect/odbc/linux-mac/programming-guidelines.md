---
title: Diretrizes de programação (Driver ODBC para SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fd77c85b089c0167306aeaad5c6d65a313e77624
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38983432"
---
# <a name="programming-guidelines"></a>Diretrizes de programação

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Os recursos de programação do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] em macOS e Linux são baseados em ODBC no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151)). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client é baseado em ODBC no Windows Data Access Components ([Referência do Programador de ODBC](http://go.microsoft.com/fwlink/?LinkID=45250)).  

Um aplicativo ODBC pode usar Multiple Active Result Sets (MARS) e outras [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] recursos específicos, incluindo `/usr/local/include/msodbcsql.h` após a inclusão dos cabeçalhos de unixODBC (`sql.h`, `sqlext.h`, `sqltypes.h`, e `sqlucode.h`). Em seguida, use os mesmos nomes simbólicos para os itens específicos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] que você usaria em seus aplicativos ODBC do Windows.

## <a name="available-features"></a>Recursos disponíveis  
As seguintes seções da documentação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client para ODBC ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151)) são válidas ao usar o driver ODBC em macOS e Linux:  

-   [Comunicando-se com o SQL Server (ODBC)](http://msdn.microsoft.com/library/ms131692.aspx)  
-   [Suporte de tempo limite de conexão e consulta](http://msdn.microsoft.com/library/ms130822.aspx)  
-   [Cursores](http://msdn.microsoft.com/library/ms130794(SQL.110).aspx)  
-   [Aprimoramentos de data/hora (ODBC)](http://msdn.microsoft.com/library/bb677319.aspx)  
-   [Executando consultas (ODBC)](http://msdn.microsoft.com/library/ms131677.aspx)  
-   [Tratando de erros e mensagens](http://msdn.microsoft.com/library/ms131289.aspx)  
-   [Autenticação Kerberos](http://msdn.microsoft.com/library/cc280459.aspx)  
-   [Tipos de dados CLR grandes definidos pelo usuário (ODBC)](http://msdn.microsoft.com/library/bb677316.aspx)  
-   [Executando transações (ODBC) (exceto transações distribuídas)](http://msdn.microsoft.com/library/ms131706.aspx)  
-   [Processando resultados (ODBC)](http://msdn.microsoft.com/library/ms130812.aspx)  
-   [Executando procedimentos armazenados](http://msdn.microsoft.com/library/ms131440.aspx)
-   [Suporte a colunas esparsas (ODBC)](http://msdn.microsoft.com/library/cc280357.aspx)
-   [Criptografia SSL](http://msdn.microsoft.com/library/ms131691.aspx)
-   [Parâmetros com valor de tabela](https://docs.microsoft.com/sql/relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc)
-   [UTF-8 e UTF-16 para a API de comando e dados](http://msdn.microsoft.com/library/ff878241.aspx)
-   [Usando funções de catálogo](http://msdn.microsoft.com/library/ms131490.aspx)  

## <a name="unsupported-features"></a>Recursos sem suporte

Os recursos a seguir não foram verificados para funcionar corretamente nesta versão do driver ODBC no Linux e macOS:

-   Conexão de Cluster de failover
-   [Resolução IP de rede transparente](https://docs.microsoft.com/sql/connect/odbc/linux/using-transparent-network-ip-resolution) (antes do ODBC Driver 17)
-   [Rastreamento de Driver Avançado](https://blogs.msdn.microsoft.com/mattn/2012/05/15/enabling-advanced-driver-tracing-for-the-sql-native-client-odbc-drivers/)

Os seguintes recursos não estão disponíveis nesta versão do driver ODBC em macOS e Linux: 

-   Transações distribuídas (não há suporte para o atributo SQL_ATTR_ENLIST_IN_DTC)  
-   Espelhamento de banco de dados  
-   FILESTREAM  
-   Criação de perfil de desempenho do driver ODBC, discutido em [SQLSetConnectAttr](http://go.microsoft.com/fwlink/?LinkId=234099), e dos seguintes atributos de conexão relacionados ao desempenho:  
    -   SQL_COPT_SS_PERF_DATA  
    -   SQL_COPT_SS_PERF_DATA_LOG  
    -   SQL_COPT_SS_PERF_DATA_LOG_NOW  
    -   SQL_COPT_SS_PERF_QUERY  
    -   SQL_COPT_SS_PERF_QUERY_INTERVAL  
    -   SQL_COPT_SS_PERF_QUERY_LOG  
-   SQLBrowseConnect  
-   Tipos de intervalo de C, como SQL_C_INTERVAL_YEAR_TO_MONTH (documentado em [Identificadores e descritores de tipo de dados](http://msdn.microsoft.com/library/ms716351(VS.85).aspx))
-   O valor SQL_CUR_USE_ODBC do atributo SQL_ATTR_ODBC_CURSORS da função SQLSetConnectAttr.

## <a name="character-set-support"></a>Suporte a conjunto de caracteres

Para o ODBC Driver 13 e 13.1, os dados SQLCHAR devem ser UTF-8. Não há outras codificações são suportadas.

Para o ODBC Driver 17, há suporte para dados SQLCHAR em um dos seguintes conjuntos/codificações de caracteres:

|Nome|Descrição|
|-|-|
|UTF-8|Unicode|
|CP437|Latino MS-DOS dos EUA|
|CP850|MS-DOS Latin 1|
|CP874|Latino/tailandês|
|CP932|Japonês, Shift-JIS|
|CP936|Chinês simplificado, GBK|
|CP949|Coreano, EUC-KR|
|CP950|Chinês tradicional, Big5|
|CP1251|Cirílico|
|CP1253|Greek|
|CP1256|Árabe|
|CP1257|Báltico|
|CP1258|Vietnamita|
|ISO-8859-1 / CP1252|Latim-1|
|ISO 8859-2 / CP1250|Latino-2|
|ISO-8859-3|Latino-3|
|ISO-8859-4|Latino-4|
|ISO-8859-5|Latino/cirílico|
|ISO-8859-6|Latino/árabe|
|ISO-8859-7|Latino/grego|
|ISO 8859-8 / CP1255|Hebraico|
|ISO 8859-9 / CP1254|Turco|
|ISO-8859-13|Latino-7|
|ISO 8859-15|Latino 9|

Após a conexão, o driver detecta a localidade atual do processo que é carregado na. Se ele usa uma das codificações acima, o driver usa a codificação de dados (caractere estreito) de SQLCHAR; Caso contrário, o padrão é UTF-8. Como todos os processos iniciar na localidade "C" por padrão (e, portanto, fazer com que o driver padrão para UTF-8), se um aplicativo precisar usar uma das codificações acima, ele deve usar o **setlocale** função para definir a localidade adequadamente antes conectar-se; especificação explícita de localidade desejada, ou usando uma cadeia de caracteres vazia, por exemplo `setlocale(LC_ALL, "")` para usar as configurações de localidade do ambiente.

Assim, em um Mac ou Linux ambiente típico no qual a codificação é UTF-8, os usuários de ODBC Driver 17 atualizar do 13 ou 13.1 não irá observar quaisquer diferenças. No entanto, aplicativos que usam uma codificação não-UTF-8 na lista acima por meio de `setlocale()` precisa usar a codificação para dados de/para o driver em vez de UTF-8.

Os dados SQLWCHAR devem ser UTF-16LE (Little Endian).

Ao associar parâmetros de entrada com SQLBindParameter, se o tipo de SQL de um caractere estreito, como SQL_VARCHAR for especificado, o driver converte os dados fornecidos no cliente de codificação para o padrão (normalmente página de código 1252) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] codificação. Para parâmetros de saída, o driver converte da codificação especificada nas informações de agrupamento associadas aos dados para o cliente de codificação. No entanto, é possível a perda de dados---os caracteres em codificação de origem não representáveis na codificação de destino serão convertida em um ponto de interrogação ('? ').

Para evitar essa perda de dados ao associar parâmetros de entrada, especifique um tipo de caractere SQL Unicode, como SQL_NVARCHAR. Nesse caso, o driver converte do cliente de codificação para UTF-16, que pode representar todos os caracteres Unicode. Além disso, a coluna de destino ou parâmetro no servidor também pode ser um tipo de Unicode (**nchar**, **nvarchar**, **ntext**) ou um arquivo com uma agrupamento/codificação, que pode representa todos os caracteres da fonte de dados original. Para evitar a perda de dados com parâmetros de saída, especifique um tipo SQL de Unicode e um Unicode C tipo (SQL_C_WCHAR), fazendo com que o driver retornar dados como UTF-16. ou uma estreita C de tipo e certifique-se de que o cliente de codificação pode representar todos os caracteres da fonte de dados (Isso é sempre possível com UTF-8.)

Para obter mais informações sobre codificações e agrupamentos, consulte [Collation and Unicode Support](../../../relational-databases/collations/collation-and-unicode-support.md).

Há algumas diferenças de conversão de codificação entre o Windows e várias versões da biblioteca iconv no Linux e macOS. Dados de texto na página de código 1255 (hebraico) tem um ponto de código (0xCA) que se comporta de forma diferente após a conversão para Unicode. No Windows, esse caractere converte para o ponto de código UTF-16 de 0x05BA. No macOS e Linux com libiconv versões anteriores à 1.15, ele converte em 0x00CA. No Linux com iconv bibliotecas que dão suporte a revisão de 2003 da Big5/CP950 (chamado `BIG5-2003`), caracteres adicionados com essa revisão não converterá corretamente. Na página de código 932 (japonês, Shift-JIS), o resultado de decodificação não originalmente definido no padrão de codificação de caracteres também é diferente. Por exemplo, o byte 0x80 converte a U + 0080 no Windows, mas pode se tornar a U + 30FB no Linux e macOS, dependendo da versão iconv.

No ODBC Driver 13 e 13.1, quando caracteres multibyte UTF-8 ou UTF-16 substitutos são divididos em buffers SQLPutData, isso resulta em dados corrompidos. Use buffers para transmitir SQLPutData que não terminem em codificações parciais de caracteres. Essa limitação foi removida com o ODBC Driver 17.

## <a name="additional-notes"></a>Observações adicionais  

1.  Você pode fazer uma conexão de administrador dedicada (DAC) usando autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] e **host,porta**. Um membro da função Sysadmin precisa primeiro detectar a porta DAC. Ver [Conexão de diagnóstico para administradores de banco de dados](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators#dac-port) para descobrir como. Por exemplo, se a porta DAC for 33000, você poderá conectá-la ao `sqlcmd` da seguinte maneira:  

    ```
    sqlcmd –U <user> -P <pwd> -S <host>,33000
    ```

    > [!NOTE]  
    > As conexões DAC devem usar a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
    
2.  O gerenciador de driver UnixODBC retorna "identificador de atributo/opção inválido" para todos os atributos de instrução quando eles são passados por meio do SQLSetConnectAttr. No Windows, quando o SQLSetConnectAttr recebe um valor de atributo de instrução, ele faz o driver definir esse valor em todas as instruções ativas que sejam filhos do identificador de conexão.  

## <a name="see-also"></a>Consulte Também  
[Perguntas frequentes](../../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)

[Problemas conhecidos nesta versão do driver](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[Notas de versão](../../../connect/odbc/linux-mac/release-notes.md)

---
title: "Diretrizes de programação | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2e3aac41bd87f52998edf366d7c3da2326de3f26
ms.contentlocale: pt-br
ms.lasthandoff: 10/10/2017

---
# <a name="programming-guidelines"></a>Diretrizes de programação
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)] Os recursos de programação do [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 e 13.1 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] em macOS e Linux são baseados em ODBC no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151)). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]Native Client é baseado em ODBC no Windows Data Access Components ([referência do programador de ODBC](http://go.microsoft.com/fwlink/?LinkID=45250)).  

Um aplicativo ODBC pode usar vários conjuntos de MARS (resultados ativos) e outros [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] recursos específicos, incluindo `/usr/local/include/msodbcsql.h` depois de incluir os cabeçalhos de unixODBC (`sql.h`, `sqlext.h`, `sqltypes.h`, e `sqlucode.h`). Em seguida, usar os mesmos nomes simbólicos para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]-itens específicos que você usaria em seus aplicativos de ODBC do Windows.  

## <a name="available-features"></a>Recursos disponíveis  
As seções a seguir do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] documentação Native Client para ODBC ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151)) são válidas ao usar o driver ODBC no macOS e Linux:  

-   [Comunicação com o SQL Server (ODBC)](http://msdn.microsoft.com/library/ms131692.aspx)  
-   [Suporte de tempo limite de Conexão e consulta](http://msdn.microsoft.com/library/ms130822.aspx)  
-   [Cursores](http://msdn.microsoft.com/library/ms130794(SQL.110).aspx)  
-   [Data/hora melhorias (ODBC)](http://msdn.microsoft.com/library/bb677319.aspx)  
-   [Executando consultas (ODBC)](http://msdn.microsoft.com/library/ms131677.aspx)  
-   [Tratamento de erros e mensagens](http://msdn.microsoft.com/library/ms131289.aspx)  
-   [Autenticação Kerberos](http://msdn.microsoft.com/library/cc280459.aspx)  
-   [Tipos definidos pelo usuário do CLR grandes (ODBC)](http://msdn.microsoft.com/library/bb677316.aspx)  
-   [Executando transações (ODBC) (exceto transações distribuídas)](http://msdn.microsoft.com/library/ms131706.aspx)  
-   [Processando resultados (ODBC)](http://msdn.microsoft.com/library/ms130812.aspx)  
-   [Executando procedimentos armazenados](http://msdn.microsoft.com/library/ms131440.aspx)
-   [Suporte a colunas esparsas (ODBC)](http://msdn.microsoft.com/library/cc280357.aspx)
-   [Criptografia SSL](http://msdn.microsoft.com/library/ms131691.aspx)
-   [Parâmetros com valor de tabela](https://docs.microsoft.com/en-us/sql/relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc)
-   [UTF-8 e UTF-16 para a API de comando e dados](http://msdn.microsoft.com/library/ff878241.aspx)
-   [Usando funções de catálogo](http://msdn.microsoft.com/library/ms131490.aspx)  

## <a name="unsupported-features"></a>Recursos sem suporte

Os recursos a seguir não foram confirmados para funcionar corretamente nesta versão do driver ODBC no macOS e Linux:

-   Conexão de Cluster de failover
-   [Resolução IP de rede transparente](https://docs.microsoft.com/en-us/sql/connect/odbc/linux/using-transparent-network-ip-resolution)
-   [Rastreamento de Driver Avançado](https://blogs.msdn.microsoft.com/mattn/2012/05/15/enabling-advanced-driver-tracing-for-the-sql-native-client-odbc-drivers/)

Os seguintes recursos não estão disponíveis nesta versão do driver ODBC no macOS e Linux: 

-   Transações distribuídas (o atributo SQL_ATTR_ENLIST_IN_DTC não tem suporte)  
-   Espelhamento de Banco de Dados  
-   FILESTREAM  
-   Criação de perfil de desempenho do driver ODBC, discutido em [SQLSetConnectAttr](http://go.microsoft.com/fwlink/?LinkId=234099)e os seguintes atributos de conexão relacionados ao desempenho:  
    -   SQL_COPT_SS_PERF_DATA  
    -   SQL_COPT_SS_PERF_DATA_LOG  
    -   SQL_COPT_SS_PERF_DATA_LOG_NOW  
    -   SQL_COPT_SS_PERF_QUERY  
    -   SQL_COPT_SS_PERF_QUERY_INTERVAL  
    -   SQL_COPT_SS_PERF_QUERY_LOG  
-   SQLBrowseConnect  
-   Tipos de intervalo de C, como SQL_C_INTERVAL_YEAR_TO_MONTH (documentado em [identificadores de tipo de dados e os descritores de](http://msdn.microsoft.com/library/ms716351(VS.85).aspx))
-   O valor SQL_CUR_USE_ODBC do atributo SQL_ATTR_ODBC_CURSORS da função SQLSetConnectAttr.

## <a name="character-set-support"></a>Suporte de conjunto de caracteres

O cliente codificação pode ser um dos seguintes:
  -  UTF-8
  -  ISO 8859-1
  -  ISO 8859-2
  -  ISO 8859-3
  -  ISO 8859-4
  -  ISO 8859-5
  -  ISO-8859-6
  -  ISO-8859-7
  -  ISO-8859-8
  -  ISO-8859-9
  -  ISO-8859-13
  -  ISO 8859-15
  
Os dados SQLCHAR devem ser um dos conjuntos de caracteres com suporte. Os dados SQLWCHAR devem ser UTF-16LE (Little Endian).  

Se o SQLDescribeParameter não especificar um tipo SQL no servidor, o driver usará o tipo SQL especificado no parâmetro *ParameterType* do SQLBindParameter. Se um tipo SQL de caractere estreito, como SQL_VARCHAR, for especificado em SQLBindParameter, o driver converte os dados fornecidos da página de código de cliente para o padrão [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] página de código. (O padrão [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] página de código geralmente é 1252.) Se não há suporte para a página de código do cliente, ele será definido como UTF-8. Nesse caso, o driver converte os dados UTF-8 para a página de código padrão. Porém, é possível haver perda de dados. Se a página de código 1252 não puder representar um caractere, o driver converterá o caractere em um ponto de interrogação (“?”). Para evitar essa perda de dados, especifique um tipo de caractere SQL Unicode, como SQL_NVARCHAR, no SQLBindParameter. Nesse caso, o driver converte os dados Unicode fornecidos em codificação UTF-8 em UTF-16 sem perda de dados.

Há uma diferença de conversão de codificação de texto entre o Windows e várias versões da biblioteca iconv no Linux e macOS. Dados de texto que são codificados na página de código 1255 (hebraico) tem um ponto de código (0xCA) que se comporta de maneira diferente após a conversão. Converter esse caractere em Unicode no Windows produz um ponto de código UTF-16 de 0x05BA. Converter em Unicode no macOS e Linux com libiconv versões anteriores 1.15 produz um ponto de código UTF-16 de 0x00CA.

Quando caracteres multibyte UTF-8 ou UTF-16 substitutos são divididos em buffers SQLPutData, isso resulta em corrupção de dados. Use buffers para transmitir SQLPutData que não terminem em codificações parciais de caracteres.  

## <a name="additional-notes"></a>Observações adicionais  

1.  Você pode fazer uma conexão de administrador dedicada (DAC) usando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] autenticação e **host, porta**. Um membro da função Sysadmin precisa primeiro detectar a porta DAC. Consulte [Conexão de diagnóstico para administradores de banco de dados](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators#dac-port) para descobrir como. Por exemplo, se a porta DAC for 33000, você pode se conectar a ele com `sqlcmd` da seguinte maneira:  

    ```
    sqlcmd –U <user> -P <pwd> -S <host>,33000
    ```

    > [!NOTE]  
    > Conexões DAC devem usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] autenticação.  
    
2.  O gerenciador de driver UnixODBC retorna "identificador de atributo/opção inválido" para todos os atributos de instrução quando eles são passados por meio do SQLSetConnectAttr. No Windows, quando o SQLSetConnectAttr recebe um valor de atributo de instrução, ele faz o driver definir esse valor em todas as instruções ativas que são filhos do identificador de conexão.  

## <a name="see-also"></a>Consulte também  
[Perguntas frequentes](../../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)

[Problemas conhecidos nesta versão do driver](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[Notas de versão](../../../connect/odbc/linux-mac/release-notes.md)


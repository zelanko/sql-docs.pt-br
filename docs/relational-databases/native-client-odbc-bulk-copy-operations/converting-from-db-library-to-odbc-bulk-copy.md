---
description: Convertendo de cópia em massa DB-Library em ODBC
title: Convertendo de DB-Library para cópia em massa ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- converting DB-Library to ODBC bulk copy
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], DB-Library bulk copy
- ODBC, bulk copy operations
- DB-Library bulk copy
ms.assetid: 0bc15bdb-f19f-4537-ac6c-f249f42cf07f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 488f3f1583a58431c5606fade81e9eb3f56bd076
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465027"
---
# <a name="converting-from-db-library-to-odbc-bulk-copy"></a>Convertendo de cópia em massa DB-Library em ODBC
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  A conversão de um DB-Library programa de cópia em massa para ODBC é fácil porque as funções de cópia em massa com suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client são semelhantes às funções de cópia em massa do DB-Library, com as seguintes exceções:  
  
-   Os aplicativos DB-Library passam, para uma estrutura DBPROCESS, um ponteiro como o primeiro parâmetro de funções de cópia em massa. Em aplicativos ODBC, o ponteiro DBPROCESS é substituído por um identificador de conexão ODBC.  
  
-   DB-Library aplicativos chamam **BCP_SETL** antes de se conectar para habilitar operações de cópia em massa em um DBPROCESS. Aplicativos ODBC, em vez disso, chamam [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) antes de se conectar para habilitar operações em massa em um identificador de conexão:  
  
    ```  
    SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP,  
        (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
    ```  
  
-   O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client não dá suporte a DB-Library manipuladores de mensagens e erros; você deve chamar **SQLGetDiagRec** para obter erros e mensagens geradas pelas funções de cópia em massa do ODBC. As versões ODBC das funções de cópia em massa retornam os códigos de retorno padrão da cópia em massa, SUCCEED ou FAILED, e não os códigos de retorno ODBC, como SQL_SUCCESS ou SQL_ERROR.  
  
-   Os valores especificados para o parâmetro DB-Library [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)*varlen* são interpretados de forma diferente do parâmetro _cbData_ do ODBC **bcp_bind**.  
  
    |Condição indicada|DB-Library valor de *varlen*|Valor de *CBDATA* ODBC|  
    |-------------------------|--------------------------------|-------------------------|  
    |Valores nulos fornecidos|0|-1 (SQL_NULL_DATA)|  
    |Dados de variável fornecidos|-1|-10 (SQL_VARLEN_DATA)|  
    |Cadeia binária ou de caracteres de comprimento zero|NA|0|  
  
     Na biblioteca de banco de dados, um valor de *varlen* de-1 indica que os dados de comprimento variável estão sendo fornecidos, que no *cbData* ODBC é interpretado para significar que apenas valores nulos estão sendo fornecidos. Altere quaisquer DB-Library especificações de *varlen* de-1 para SQL_VARLEN_DATA e quaisquer especificações de *varlen* de 0 a SQL_NULL_DATA.  
  
-   O DB-Library **bcp_colfmt**_FILE_COLLEN_ e o ODBC [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)*cbUserData* têm o mesmo problema que os parâmetros **bcp_bind**_varlen_ e *cbData* indicados acima. Altere qualquer DB-Library *file_collen* especificações de-1 para SQL_VARLEN_DATA e quaisquer especificações de *file_collen* de 0 a SQL_NULL_DATA.  
  
-   O parâmetro *iValue* da função ODBC [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) é um ponteiro void. Em DB-Library, *iValue* era um número inteiro. Converta os valores para o *IVALUE* ODBC em void *.  
  
-   A opção **BCP_CONTROL** BCPMAXERRS especifica quantas linhas individuais podem ter erros antes de uma operação de cópia em massa falhar. O padrão para BCPMAXERRS é 0 (falha no primeiro erro) na versão DB-Library do **bcp_control** e 10 na versão do ODBC. DB-Library aplicativos que dependem do padrão de 0 para encerrar uma operação de cópia em massa devem ser alterados para chamar o **BCP_CONTROL** ODBC para definir BCPMAXERRS como 0.  
  
-   A função de **BCP_CONTROL** ODBC dá suporte às seguintes opções sem suporte da versão DB-Library do **bcp_control**:  
  
    -   BCPODBC  
  
         Quando definido como TRUE, especifica que os valores **DateTime** e **smalldatetime** salvos no formato de caractere terão o prefixo e o sufixo da sequência de saída do carimbo de data e hora do ODBC. Isso se aplica apenas a operações BCP_OUT.  
  
         Com BCPODBC definido como FALSE, um valor **DateTime** convertido em uma cadeia de caracteres é resultado como:  
  
        ```  
        1997-01-01 00:00:00.000  
        ```  
  
         Com BCPODBC definido como TRUE, o mesmo valor **DateTime** é output as:  
  
        ```  
        {ts '1997-01-01 00:00:00.000' }  
        ```  
  
    -   BCPKEEPIDENTITY  
  
         Quando definido como TRUE, especifica que as funções de cópia em massa inserem valores de dados fornecidos para colunas com restrições de identidade. Se essa opção não for definida, novos valores de identidade serão gerados para as linhas inseridas.  
  
    -   BCPHINTS  
  
         Especifica várias otimizações de cópia em massa. Essa opção não pode ser usada na versão 6.5 nem em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   BCPFILECP  
  
         Especifica a página de código do arquivo de cópia em massa.  
  
    -   BCPUNICODEFILE  
  
         Especifica que um arquivo de cópia em massa em modo de caractere é um arquivo Unicode.  
  
-   A função de **BCP_COLFMT** ODBC não dá suporte ao indicador de *file_type* de SQLCHAR porque está em conflito com o TYPEDEF SQLCHAR do ODBC. Use SQLCHARACTER em vez de **bcp_colfmt**.  
  
-   Nas versões ODBC das funções de cópia em massa, o formato para trabalhar com valores **DateTime** e **smalldatetime** em cadeias de caracteres é o formato ODBC de aaaa-mm-dd hh: mm: SS. SSS; os valores **smalldatetime** usam o formato ODBC de aaaa-mm-dd hh: mm: SS.  
  
     As versões DB-Library das funções de cópia em massa aceitam valores **DateTime** e **smalldatetime** em cadeias de caracteres usando vários formatos:  
  
    -   O formato padrão é *Mmm dd aaaa hh: mmxx* , em que *XX* é AM ou PM.  
  
    -   cadeias de caracteres **DateTime** e **smalldatetime** em qualquer formato com suporte pela função DB-Library **DBConvert** .  
  
    -   Quando a caixa **usar configurações internacionais** é marcada na guia **Opções** de DB-Library do utilitário de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rede do cliente, as funções de cópia em massa do DB-Library também aceitam datas no formato de data regional definido para a configuração de localidade do registro do computador cliente.  
  
     As funções de cópia em massa DB-Library não aceitam os formatos ODBC **DateTime** e **smalldatetime** .  
  
     Se o atributo da instrução SQL_SOPT_SS_REGIONALIZE estiver definido como SQL_RE_ON, as funções de cópia em massa do ODBC aceitarão datas no formato de data regional definido para a configuração de localidade do registro do computador cliente.  
  
-   Ao gerar valores **monetários** no formato de caractere, as funções de cópia em massa ODBC fornecem quatro dígitos de precisão e nenhum separador de vírgula; DB-Library versões fornecem apenas dois dígitos de precisão e incluem os separadores de vírgulas.  
  
## <a name="see-also"></a>Consulte Também  
 [Executando operações de cópia em massa &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)   
 [Bulk Copy Functions](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  

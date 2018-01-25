---
title: "Conversão de DB-Library em cópia em massa ODBC | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-bulk-copy-operations
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- converting DB-Library to ODBC bulk copy
- SQL Server Native Client ODBC driver, bulk copy
- bulk copy [ODBC], DB-Library bulk copy
- ODBC, bulk copy operations
- DB-Library bulk copy
ms.assetid: 0bc15bdb-f19f-4537-ac6c-f249f42cf07f
caps.latest.revision: "30"
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: abdb8b529914a3ebb09ed0d5d933c30e0ef43f9d
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="converting-from-db-library-to-odbc-bulk-copy"></a>Convertendo de cópia em massa DB-Library em ODBC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Convertendo um programa de cópia em massa DB-Library em ODBC é fácil porque oferece suporte às funções de copiar em massa a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client são semelhantes às funções de cópia em massa do DB-Library, com as seguintes exceções:  
  
-   Os aplicativos DB-Library passam, para uma estrutura DBPROCESS, um ponteiro como o primeiro parâmetro de funções de cópia em massa. Em aplicativos ODBC, o ponteiro DBPROCESS é substituído por um identificador de conexão ODBC.  
  
-   Chamada de aplicativos DB-Library **BCP_SETL** antes da conexão para permitir operações de cópia em massa em um DBPROCESS. Aplicativos ODBC chamam [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) antes de se conectar para habilitar operações em massa em um identificador de conexão:  
  
    ```  
    SQLSetConnectAttr(hdbc, SQL_COPT_SS_BCP,  
        (void *)SQL_BCP_ON, SQL_IS_INTEGER);  
    ```  
  
-   O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client não dá suporte a identificadores de erros e mensagens de DB-Library; você deve chamar **SQLGetDiagRec** para obter erros e as mensagens geradas pelas funções de cópia em massa do ODBC. As versões ODBC das funções de cópia em massa retornam os códigos de retorno padrão da cópia em massa, SUCCEED ou FAILED, e não os códigos de retorno ODBC, como SQL_SUCCESS ou SQL_ERROR.  
  
-   Os valores especificados para a biblioteca de banco de dados [bcp_bind](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-bind.md)*varlen* parâmetro são interpretados de forma diferente de ODBC **bcp_bind * cbData* parâmetro.  
  
    |Condição indicada|DB-Library *varlen* valor|ODBC *cbData* valor|  
    |-------------------------|--------------------------------|-------------------------|  
    |Valores nulos fornecidos|0|-1 (SQL_NULL_DATA)|  
    |Dados de variável fornecidos|-1|-10 (SQL_VARLEN_DATA)|  
    |Cadeia binária ou de caracteres de comprimento zero|NA|0|  
  
     Em DB-Library, um *varlen* valor -1 indica que dados de comprimento variável estão sendo fornecidos, que no ODBC *cbData* significa que somente valores NULL estão sendo fornecidos. Alterar qualquer DB-Library *varlen* especificações de -1 para SQL_VARLEN_DATA e qualquer *varlen* especificações de 0 para SQL_NULL_DATA.  
  
-   O DB-Library  **bcp_colfmt * file_collen* e ODBC [bcp_colfmt](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-colfmt.md)*cbUserData * têm o mesmo problema que o **bcp_bind * varlen*e *cbData* parâmetros indicado acima. Alterar qualquer DB-Library *file_collen* especificações de -1 para SQL_VARLEN_DATA e qualquer *file_collen* especificações de 0 para SQL_NULL_DATA.  
  
-   O *iValue* parâmetro do ODBC [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md) função é um ponteiro nulo. Em DB-Library, *iValue* era um inteiro. Converter os valores do ODBC *iValue* para void *.  
  
-   O **bcp_control** opção BCPMAXERRS Especifica quantas linhas individuais podem ter erros antes de uma operação de cópia em massa falha. O padrão de BCPMAXERRS é 0 (Falha no primeiro erro) na versão DB-Library do **bcp_control** e 10 na versão do ODBC. Aplicativos DB-Library que dependem do padrão de 0 para finalizar uma operação de cópia em massa devem ser alterados para chamar o ODBC **bcp_control** definir BCPMAXERRS como 0.  
  
-   O ODBC **bcp_control** função oferece suporte para as opções a seguir não são suportadas pela versão DB-Library de **bcp_control**:  
  
    -   BCPODBC  
  
         Quando definido como TRUE, especifica que **datetime** e **smalldatetime** valores salvos no formato de caractere terão o prefixo de sequência de escape de carimbo de hora ODBC e o sufixo. Isso se aplica apenas a operações BCP_OUT.  
  
         Com BCPODBC definido como FALSE, um **datetime** valor convertido em uma cadeia de caracteres é produzido como:  
  
        ```  
        1997-01-01 00:00:00.000  
        ```  
  
         Com BCPODBC definido como TRUE, o mesmo **datetime** valor é produzido como:  
  
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
  
-   O ODBC **bcp_colfmt** função não oferece suporte a *file_type* indicador de SQLCHAR porque ela está em conflito com o typedef ODBC SQLCHAR. Use SQLCHARACTER em vez disso, para **bcp_colfmt**.  
  
-   Nas versões ODBC das funções de cópia em massa, o formato para trabalhar com **datetime** e **smalldatetime** valores em cadeias de caracteres é o formato ODBC de aaaa-mm-dd SS.SSS; **smalldatetime** valores usam o formato ODBC de aaaa-mm-dd hh.  
  
     Aceitam as versões DB-Library das funções de cópia em massa **datetime** e **smalldatetime** valores em cadeias de caracteres com vários formatos:  
  
    -   O formato padrão é *mmm dd aaaa hh: mmxx* onde *xx* é AM ou PM.  
  
    -   **DateTime** e **smalldatetime** cadeias de caracteres em qualquer formato aceito pela biblioteca de banco de dados de caractere **dbconvert** função.  
  
    -   Quando o **usar configurações internacionais** caixa está marcada em DB-Library **opções** guia do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client Network Utility, as funções de cópia em massa DB-Library também aceitarão datas no regional formato de data definido para a configuração de localidade do registro do computador cliente.  
  
     As funções de cópia em massa DB-Library não aceitam o ODBC **datetime** e **smalldatetime** formatos.  
  
     Se o atributo da instrução SQL_SOPT_SS_REGIONALIZE estiver definido como SQL_RE_ON, as funções de cópia em massa do ODBC aceitarão datas no formato de data regional definido para a configuração de localidade do registro do computador cliente.  
  
-   Na saída **money** valores em formato de caractere, ODBC bulk copy funções fornecem quatro dígitos de precisão e sem separadores de vírgula; Versões DB-Library apenas fornecem dois dígitos de precisão e incluem os separadores de vírgula.  
  
## <a name="see-also"></a>Consulte também  
 [Executando operações de cópia em massa &#40; ODBC &#41;](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)   
 [Funções de cópia em massa](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)  
  
  

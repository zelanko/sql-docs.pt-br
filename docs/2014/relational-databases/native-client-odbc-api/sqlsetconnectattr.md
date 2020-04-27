---
title: SQLSetConnectAttr | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLSetConnectAttr function
ms.assetid: d21b5cf1-3724-43f7-bc96-5097df0677b4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b1b48f9ee2e7ee3092e3f31fd6ef97e91c5cd9db
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68207105"
---
# <a name="sqlsetconnectattr"></a>SQLSetConnectAttr
  O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ignora a configuração de SQL_ATTR_CONNECTION_TIMEOUT.  
  
 SQL_ATTR_TRANSLATE_LIB também é ignorado; não há suporte para a especificação de outra biblioteca de conversão. Para permitir que os aplicativos sejam aprovados com facilidade para usar um driver Microsoft ODBC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], qualquer valor definido com SQL_ATTR_TRANSLATE_LIB será copiado dentro e fora de um buffer no Gerenciador de Driver.  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client implementa isolamento de transação de leitura repetida como serializável.  
  
 O [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] introduziu o suporte a um novo atributo de isolamento de transação, SQL_COPT_SS_TXN_ISOLATION. Configurar SQL_COPT_SS_TXN_ISOLATION como SQL_TXN_SS_SNAPSHOT indica que a transação ocorrerá no nível de isolamento do instantâneo.  
  
> [!NOTE]  
>  SQL_ATTR_TXN_ISOLATION pode ser usado para definir todos os outros níveis de isolamento, com exceção de SQL_TXN_SS_SNAPSHOT. Se quiser usar isolamento do instantâneo, deverá definir SQL_TXN_SS_SNAPSHOT através de SQL_COPT_SS_TXN_ISOLATION. Porém, você pode recuperar o nível de isolamento usando SQL_ATTR_TXN_ISOLATION ou SQL_COPT_SS_TXN_ISOLATION.  
  
 A promoção de atributos de instrução ODBC a atributos de conexão pode ter consequências não intencionais. Os atributos de instrução que solicitam cursores de servidor para processamento de conjuntos de resultados podem ser promovidos a conexões. Por exemplo, configurar o atributo de instrução ODBC SQL_ATTR_CONCURRENCY para um valor mais restritivo que o padrão SQL_CONCUR_READ_ONLY orienta o servidor a usar cursores dinâmicos para todas as instruções enviadas na conexão. Executar uma função de catálogo ODBC em uma instrução na conexão retorna SQL_SUCCESS_WITH_INFO e um registro de diagnóstico que indica que o comportamento do cursor foi alterado para somente leitura. A tentativa de executar uma instrução SELECT do Transact-SQL contendo uma cláusula COMPUTE na mesma conexão causa uma falha.  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte a várias extensões específicas para atributos da conexão ODBC definidos em sqlncli.h. O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client poderá exigir que o atributo seja definido antes da conexão, ou poderá ignorar o atributo se ele já tiver sido definido. A seguinte tabela apresenta as restrições.  
  
|Atributo do SQL Server|Defina antes ou depois da conexão com o servidor|  
|--------------------------|----------------------------------------------|  
|SQL_COPT_SS_ANSI_NPW|Antes de|  
|SQL_COPT_SS_APPLICATION_INTENT|Antes de|  
|SQL_COPT_SS_ATTACHDBFILENAME|Antes de|  
|SQL_COPT_SS_BCP|Antes de|  
|SQL_COPT_SS_BROWSE_CONNECT|Antes de|  
|SQL_COPT_SS_BROWSE_SERVER|Antes de|  
|SQL_COPT_SS_CONCAT_NULL|Antes de|  
|SQL_COPT_SS_CONNECTION_DEAD|After (após)|  
|SQL_COPT_SS_ENCRYPT|Antes de|  
|SQL_COPT_SS_ENLIST_IN_DTC|After (após)|  
|SQL_COPT_SS_ENLIST_IN_XA|After (após)|  
|SQL_COPT_SS_FALLBACK_CONNECT|Antes de|  
|SQL_COPT_SS_FAILOVER_PARTNER|Antes de|  
|SQL_COPT_SS_INTEGRATED_SECURITY|Antes de|  
|SQL_COPT_SS_MARS_ENABLED|Antes de|  
|SQL_COPT_SS_MULTISUBMIT_FAILOVER|Antes de|  
|SQL_COPT_SS_OLDPWD|Antes de|  
|SQL_COPT_SS_PERF_DATA|After (após)|  
|SQL_COPT_SS_PERF_DATA_LOG|After (após)|  
|SQL_COPT_SS_PERF_DATA_LOG_NOW|After (após)|  
|SQL_COPT_SS_PERF_QUERY|After (após)|  
|SQL_COPT_SS_PERF_QUERY_INTERVAL|After (após)|  
|SQL_COPT_SS_PERF_QUERY_LOG|After (após)|  
|SQL_COPT_SS_PRESERVE_CURSORS|Antes de|  
|SQL_COPT_SS_QUOTED_IDENT|Você pode usar o|  
|SQL_COPT_SS_TRANSLATE|Você pode usar o|  
|SQL_COPT_SS_TRUST_SERVER_CERTIFICATE|Antes de|  
|SQL_COPT_SS_TXN_ISOLATION|Você pode usar o|  
|SQL_COPT_SS_USE_PROC_FOR_PREP|Você pode usar o|  
|SQL_COPT_SS_USER_DATA|Você pode usar o|  
|SQL_COPT_SS_WARN_ON_CP_ERROR|Antes de|  
  
 O uso de um atributo da conexão e do comando equivalente de [!INCLUDE[tsql](../../includes/tsql-md.md)] para a mesma sessão, banco de dados ou estado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode gerar um comportamento inesperado. Por exemplo,  
  
```  
SQLSetConnectAttr(SQL_COPT_SS_QUOTED_IDENT, SQL_QI_ON) // turn ON via attribute  
SQLDriverConnect(...);  
SQLExecDirect("SET QUOTED_IDENTIFIER OFF") // turn OFF via Transact-SQL  
SQLSetConnectAttr(SQL_ATTR_CURRENT_CATALOG, ...) // restores to pre-connect attribute value  
```  
  
## <a name="sql_copt_ss_ansi_npw"></a>SQL_COPT_SS_ANSI_NPW  
 SQL_COPT_SS_ANSI_NPW habilita ou desabilita o uso de manuseio ISO de NULL em comparações e concatenação, preenchimento do tipo de dados caractere e advertências. Para obter mais informações, consulte SET ANSI_NULLS, SET ANSI_PADDING, SET ANSI_WARNINGS e SET CONCAT_NULL_YIELDS_NULL.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_AD_ON|Padrão. A conexão usa comportamento padrão do ANSI para manusear comparações de NULL, preenchimento, advertências e concatenações de NULL.|  
|SQL_AD_OFF|A conexão usa a manipulação de NULL, preenchimento de tipo de dados caractere e advertências definida pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
 Se você usar o pool de conexões, SQL_COPT_SS_ANSI_NPW deverá ser definida na cadeia de conexão, em vez de com SQLSetConnectAttr. Depois que uma conexão for estabelecida, qualquer tentativa para alterar esse atributo falhará em modo silencioso quando o pool de conexões for usado.  
  
## <a name="sql_copt_ss_application_intent"></a>SQL_COPT_SS_APPLICATION_INTENT  
 Declara o tipo de carga de trabalho de aplicativo ao conectar-se a um servidor. Os valores possíveis são `Readonly` e `ReadWrite`. Por exemplo:  
  
```  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_APPLICATION_INTENT, TEXT("Readonly"), SQL_NTS)  
```  
  
 O padrão é `ReadWrite`. Para obter mais informações [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sobre o suporte nativo do [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] cliente para AGS, consulte [suporte de SQL Server Native Client para alta disponibilidade e recuperação de desastre](../native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
## <a name="sql_copt_ss_attachdbfilename"></a>SQL_COPT_SS_ATTACHDBFILENAME  
 SQL_COPT_SS_ATTACHDBFILENAME especifica o nome do arquivo primário de um banco de dados anexável. Esse banco de dados é anexado e torna-se o banco de dados padrão da conexão. Para usar SQL_COPT_SS_ATTACHDBFILENAME você deve especificar o nome do banco de dados como o valor do atributo de conexão SQL_ATTR_CURRENT_CATALOG ou no parâmetro DATABASE = de um [SQLDriverConnect](sqldriverconnect.md). Se o banco de dados tiver sido anexado previamente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não o anexará novamente.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQLPOINTER para uma cadeia de caracteres|A cadeia de caracteres contém o nome do arquivo primário para o banco de dados se anexar. Inclua o caminho completo do nome do arquivo.|  
  
## <a name="sql_copt_ss_bcp"></a>SQL_COPT_SS_BCP  
 SQL_COPT_SS_BCP habilita funções de cópia em massa em uma conexão. Para obter mais informações, consulte [funções de cópia em massa](../native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md).  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_BCP_OFF|Padrão. Funções de cópia em massa não estão disponíveis na conexão.|  
|SQL_BCP_ON|Funções de cópia em massa estão disponíveis na conexão.|  
  
## <a name="sql_copt_ss_browse_connect"></a>SQL_COPT_SS_BROWSE_CONNECT  
 Esse atributo é usado para personalizar o conjunto de resultados retornado por [SQLBrowseConnect](sqlbrowseconnect.md). SQL_COPT_SS_BROWSE_CONNECT habilita ou desabilita o retorno de informações adicionais de uma instância enumerada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Isto pode incluir informações como se o servidor é um cluster, nomes de instâncias diferentes e o número de versão.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_MORE_INFO_NO|Padrão. Retorna uma lista de servidores.|  
|SQL_MORE_INFO_YES|**SQLBrowseConnect** retorna uma cadeia de caracteres estendida das propriedades do servidor.|  
  
## <a name="sql_copt_ss_browse_server"></a>SQL_COPT_SS_BROWSE_SERVER  
 Esse atributo é usado para personalizar o conjunto de resultados retornado por **SQLBrowseConnect**. SQL_COPT_SS_BROWSE_SERVER especifica o nome do servidor para o qual **SQLBrowseConnect** retorna as informações.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|computername|**SQLBrowseConnect** retorna uma lista de instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador especificado. As barras invertidas\\\\duplas () não devem ser usadas para o nome do servidor (por \\exemplo, em vez de \MyServer, meuservidor deve ser usado).|  
|NULO|Padrão. **SQLBrowseConnect** retorna informações para todos os servidores no domínio.|  
  
## <a name="sql_copt_ss_concat_null"></a>SQL_COPT_SS_CONCAT_NULL  
 SQL_COPT_SS_CONCAT_NULL habilita ou desabilita o uso de manuseio ISO de NULL ao concatenar cadeias. Para obter mais informações, consulte SET CONCAT_NULL_YIELDS_NULL.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_CN_ON|Padrão. A conexão usa o comportamento padrão ISO para manusear valores NULL ao concatenar cadeias.|  
|SQL_CN_OFF|A conexão usa o comportamento definido por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para manusear valores NULL ao concatenar cadeias.|  
  
## <a name="sql_copt_ss_encrypt"></a>SQL_COPT_SS_ENCRYPT  
 Controla a criptografia de uma conexão.  
  
 A criptografia usa o certificado no servidor. Isto deve ser verificado por uma autoridade de certificação, a menos que o atributo da conexão SQL_COPT_SS_TRUST_SERVER_CERTIFICATE seja definido como SQL_TRUST_SERVER_CERTIFICATE_YES ou a cadeia de conexão contenha "TrustServerCertificate=yes". Se qualquer uma destas condições for verdadeira, um certificado gerado e assinado pelo servidor poderá ser usado para criptografar a conexão se não houver nenhum certificado no servidor.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_EN_ON|A conexão será criptografada.|  
|SQL_EN_OFF|A conexão não será criptografada. Esse é o padrão.|  
  
## <a name="sql_copt_ss_enlist_in_dtc"></a>SQL_COPT_SS_ENLIST_IN_DTC  
 O cliente chama o método Microsoft Coordenador de Transações Distribuídas (MS DTC) OLE DB **ITransactionDispenser:: BeginTransaction** para iniciar uma transação do MS DTC e criar um objeto de transação MS DTC que representa a transação. Em seguida, o `SQLSetConnectAttr` aplicativo chama a opção SQL_COPT_SS_ENLIST_IN_DTC para associar o objeto de transação à conexão ODBC. Todas as atividades de banco de dados relacionadas serão executadas sob a proteção da transação do MS DTC. O aplicativo chama `SQLSetConnectAttr` com SQL_DTC_DONE para encerrar a associação DTC da conexão.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|Objeto DTC*|O objeto de transação OLE do MS DTC que especifica a transação a ser exportada para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|SQL_DTC_DONE|Delimita o término de uma transação de DTC.|  
  
## <a name="sql_copt_ss_enlist_in_xa"></a>SQL_COPT_SS_ENLIST_IN_XA  
 Para iniciar uma transação XA com um processador de transação compatível com XA (TP), o cliente chama a função de **tx_begin** de grupo aberta. Em seguida, o `SQLSetConnectAttr` aplicativo chama um parâmetro SQL_COPT_SS_ENLIST_IN_XA de true para associar a transação XA à conexão ODBC. Todas as atividades de banco de dados relacionadas serão executadas sob a proteção da transação XA. Para finalizar uma associação XA com uma conexão ODBC, o cliente deve `SQLSetConnectAttr` chamar com um parâmetro SQL_COPT_SS_ENLIST_IN_XA de false. Para obter mais informações, consulte a documentação do Coordenador de Transações Distribuídas da Microsoft.  
  
## <a name="sql_copt_ss_fallback_connect"></a>SQL_COPT_SS_FALLBACK_CONNECT  
 Não há mais suporte para este atributo.  
  
## <a name="sql_copt_ss_failover_partner"></a>SQL_COPT_SS_FAILOVER_PARTNER  
 Usado para especificar ou recuperar o nome do parceiro de failover usado para espelhamento de banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. É uma cadeia de caracteres terminada em nulo que deve ser definida antes que a conexão ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja estabelecida inicialmente.  
  
 Depois de fazer a conexão, o aplicativo pode consultar esse atributo usando [SQLGetConnectAttr](sqlgetconnectattr.md) para determinar a identidade do parceiro de failover. Se o servidor primário não tiver nenhum parceiro de failover, esta propriedade retornará uma cadeia de caracteres vazia. Isto permite que um aplicativo inteligente armazene em cache o servidor de backup determinado mais recentemente, mas tais aplicativos devem estar cientes de que as informações serão atualizadas somente depois que a conexão for estabelecida ou redefinida, se estiver em pool, e poderão ficar desatualizadas em conexões de longo prazo.  
  
 Para obter mais informações, confira [Usando o espelhamento de banco de dados](../native-client/features/using-database-mirroring.md).  
  
## <a name="sql_copt_ss_integrated_security"></a>SQL_COPT_SS_INTEGRATED_SECURITY  
 SQL_COPT_SS_INTEGRATED_SECURITY força o uso da autenticação do Windows para validação de acesso no logon do servidor. Quando a autenticação do Windows é usada, o driver ignora os valores de identificador de usuário e senha fornecidos como parte do processamento de **SQLConnect**, [SQLDriverConnect](sqldriverconnect.md)ou [SQLBrowseConnect](sqlbrowseconnect.md) .  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_IS_OFF|Padrão. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Autenticação é usada para validar o identificador de usuário e a senha no logon.|  
|SQL_IS_ON|O modo de autenticação do Windows é usado para validar os direitos de acesso de um usuário ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="sql_copt_ss_mars_enabled"></a>SQL_COPT_SS_MARS_ENABLED  
 Este atributo habilita ou desabilita MARS (Vários Conjuntos de Resultados Ativos). Por padrão, MARS está desabilitado. Este atributo deve ser definido antes de fazer uma conexão com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Depois que a conexão com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é aberta, o MARS permanecerá habilitado ou desabilitado durante toda a duração da conexão.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_MARS_ENABLED_NO|Padrão. MARS está desabilitado.|  
|SQL_MARS_ENABLED_YES|O MARS está habilitado.|  
  
 Para obter mais informações sobre MARS, consulte [usando vários conjuntos de resultados ativos &#40;MARS&#41;](../native-client/features/using-multiple-active-result-sets-mars.md).  
  
## <a name="sql_copt_ss_multisubnet_failover"></a>SQL_COPT_SS_MULTISUBNET_FAILOVER  
 Se o seu aplicativo estiver se conectando a um grupo de disponibilidade [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] em várias sub-redes, essa propriedade de conexão configurará o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para fornecer detecção mais rápida do servidor ativo (atualmente) e conexão a ele. Por exemplo:  
  
```  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_MULTISUBMIT_FAILOVER, SQL_IS_ON, SQL_IS_INTEGER)  
```  
  
 Para obter mais informações [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sobre o suporte nativo do [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] cliente para AGS, consulte [suporte de SQL Server Native Client para alta disponibilidade e recuperação de desastre](../native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_IS_ON|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client fornecerá reconexão mais rápida se houver um failover.|  
|SQL_IS_OFF|O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client não fornecerá reconexão mais rápida se houver um failover.|  
  
## <a name="sql_copt_ss_oldpwd"></a>SQL_COPT_SS_OLDPWD  
 A expiração de senha para Autenticação do SQL Server foi incorporada no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. O atributo SQL_COPT_SS_OLDPWD foi adicionado para permitir que o cliente forneça tanto a senha antiga quanto a nova para a conexão. Quando essa propriedade estiver definida, o provedor não usará o pool de conexões na primeira conexão nem nas conexões seguintes, já que a cadeia de conexão conterá a "senha antiga", que agora foi alterada.  
  
 Confira mais informações em [Alterar senhas programaticamente](../native-client/features/changing-passwords-programmatically.md).  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_COPT_SS_OLD_PASSWORD|SQLPOINTER para uma cadeia de caracteres que contém a senha antiga. Este é um valor somente gravação e deve ser definido antes da conexão ao servidor.|  
  
## <a name="sql_copt_ss_perf_data"></a>SQL_COPT_SS_PERF_DATA  
 SQL_COPT_SS_PERF_DATA inicia ou para log de dados de desempenho. O nome do arquivo de log de dados deve ser definido antes de iniciar o log de dados. Consulte SQL_COPT_SS_PERF_DATA_LOG, a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_PERF_START|Inicia o driver de amostragem de dados de desempenho.|  
|SQL_PERF_STOP|Para a amostragem de dados de desempenho pelos contadores.|  
  
 Para obter mais informações, consulte [SQLGetConnectAttr](sqlgetconnectattr.md).  
  
## <a name="sql_copt_ss_perf_data_log"></a>SQL_COPT_SS_PERF_DATA_LOG  
 SQL_COPT_SS_PERF_DATA_LOG atribui o nome do arquivo de log usado para registrar dados de desempenho. O nome de arquivo de log é uma cadeia de caracteres ANSI ou Unicode terminada por null, dependendo da compilação do aplicativo. O argumento *StringLength* deve ser SQL_NTS.  
  
## <a name="sql_copt_ss_perf_data_log_now"></a>SQL_COPT_SS_PERF_DATA_LOG_NOW  
 SQL_COPT_SS_PERF_DATA_LOG_NOW instrui o driver a escrever uma entrada de log de estatística em disco. O argumento *StringLength* deve ser SQL_NTS.  
  
## <a name="sql_copt_ss_perf_query"></a>SQL_COPT_SS_PERF_QUERY  
 SQL_COPT_SS_PERF_QUERY inicia ou para de gerar logs para consultas de longa execução. O nome do arquivo de log da consulta deve ser fornecido antes de iniciar a geração de log. O aplicativo pode definir o que é “longa execução” definindo o intervalo para geração de log.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_PERF_START|Inicia a geração de log de consultas de longa execução.|  
|SQL_PERF_STOP|Para a geração de log de consultas de longa execução.|  
  
 Para obter mais informações, consulte [SQLGetConnectAttr](sqlgetconnectattr.md).  
  
## <a name="sql_copt_ss_perf_query_interval"></a>SQL_COPT_SS_PERF_QUERY_INTERVAL  
 SQL_COPT_SS_PERF_QUERY_INTERVAL define o limite de log de consultas em milissegundos. Consultas que não são resolvidas dentro do limite são registradas no arquivo de log de consultas de longa execução. Não há nenhum limite superior para o limite de consulta. Um valor de limite de consulta igual a zero faz todas as consultas serem registradas no log.  
  
## <a name="sql_copt_ss_perf_query_log"></a>SQL_COPT_SS_PERF_QUERY_LOG  
 SQL_COPT_SS_PERF_QUERY_LOG atribui o nome de um arquivo de log para registrar dados de consultas de longa execução. O nome de arquivo de log é uma cadeia de caracteres ANSI ou Unicode terminada por null, dependendo da compilação do aplicativo. O argumento *StringLength* deve ser SQL_NTS ou o comprimento da cadeia de caracteres em bytes.  
  
## <a name="sql_copt_ss_preserve_cursors"></a>SQL_COPT_SS_PRESERVE_CURSORS  
 Este atributo permite consultar e definir se a conexão preservará o(s) cursor(es) quando você confirmar/reverter uma transação. A configuração é SQL_PC_ON ou SQL_PC_OFF. O valor padrão é SQL_PC_OFF. Essa configuração controla se o driver fechará os Cursors para você quando você chamar [SQLEndTran](sqlendtran.md) (ou SQLTransact).  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_PC_OFF|Padrão. Os cursores são fechados quando a transação é confirmada ou revertida usando **SQLEndTran**.|  
|SQL_PC_ON|Os cursores não são fechados quando a transação é confirmada ou revertida usando **SQLEndTran**, exceto ao usar um cursor estático ou de conjunto de chaves no modo assíncrono. Se uma reversão for emitida enquanto o preenchimento do cursor não estiver terminado, o cursor será fechado.|  
  
## <a name="sql_copt_ss_quoted_ident"></a>SQL_COPT_SS_QUOTED_IDENT  
 SQL_COPT_SS_QUOTED_IDENT permite identificadores entre aspas em instruções de ODBC e Transact-SQL enviadas na conexão. Fornecendo identificadores entre aspas, o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client permite nomes de objetos que seriam inválidos de outras formas, como "My Table", que contém um caractere de espaço no identificador. Para obter mais informações, consulte SET QUOTED_IDENTIFIER.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_QI_OFF|A conexão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não permite identificadores entre aspas em [!INCLUDE[tsql](../../includes/tsql-md.md)] enviados.|  
|SQL_QI_ON|Padrão. A conexão permite identificadores entre aspas em [!INCLUDE[tsql](../../includes/tsql-md.md)] enviados.|  
  
## <a name="sql_copt_ss_translate"></a>SQL_COPT_SS_TRANSLATE  
 SQL_COPT_SS_TRANSLATE faz o driver traduzir caracteres entre as páginas de código de cliente e de servidor à medida que os dados de MBCS são trocados. O atributo afeta apenas os dados armazenados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]nas colunas **Char**, **varchar**e **Text** .  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_XL_OFF|O driver não traduz caracteres de uma página de código para outra em dados de caractere trocados entre o cliente e o servidor.|  
|SQL_XL_ON|Padrão. O driver traduz caracteres de uma página de código para outra em dados de caractere trocados entre o cliente e o servidor. O driver configura a tradução de caractere automaticamente, determinando a página de código instalada no servidor e aquela que está sendo usada pelo cliente.|  
  
## <a name="sql_copt_ss_trust_server_certificate"></a>SQL_COPT_SS_TRUST_SERVER_CERTIFICATE  
 SQL_COPT_SS_TRUST_SERVER_CERTIFICATE faz o driver habilitar ou desabilitar a validação de certificado ao usar criptografia. Este atributo é um valor de leitura/gravação, mas defini-lo depois que uma conexão é estabelecida não tem nenhum efeito.  
  
 Aplicativos cliente podem consultar esta propriedade depois que uma conexão foi aberta para determinar as configurações efetivas de criptografia e validação em uso.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_TRUST_SERVER_CERTIFICATE_NO|Padrão. A criptografia sem validação de certificado não está habilitada.|  
|SQL_TRUST_SERVER_CERTIFICATE_YES|A criptografia sem validação de certificado está habilitada.|  
  
## <a name="sql_copt_ss_txn_isolation"></a>SQL_COPT_SS_TXN_ISOLATION  
 SQL_COPT_SS_TXN_ISOLATION define o atributo de isolamento de instantâneo específico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O isolamento de instantâneo não pode ser definido usando SQL_ATTR_TXN_ISOLATION porque o valor é específico do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Entretanto, ele pode ser recuperado usando SQL_ATTR_TXN_ISOLATION ou SQL_COPT_SS_TXN_ISOLATION.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_TXN_SS_SNAPSHOT|Indica que, a partir de uma transação, você não pode consultar alterações feitas em outras transações e que você não pode ver as alterações, nem mesmo quando refizer a consulta.|  
  
 Para obter mais informações sobre isolamento de instantâneo, consulte [trabalhando com isolamento de instantâneo](../native-client/features/working-with-snapshot-isolation.md).  
  
## <a name="sql_copt_ss_use_proc_for_prep"></a>SQL_COPT_SS_USE_PROC_FOR_PREP  
 Não há mais suporte para este atributo.  
  
## <a name="sql_copt_ss_user_data"></a>SQL_COPT_SS_USER_DATA  
 SQL_COPT_SS_USER_DATA define o ponteiro de dados do usuário. Os dados do usuário são uma memória de propriedade do cliente registrada para cada conexão.  
  
 Para obter mais informações, consulte [SQLGetConnectAttr](sqlgetconnectattr.md).  
  
## <a name="sql_copt_ss_warn_on_cp_error"></a>SQL_COPT_SS_WARN_ON_CP_ERROR  
 Este atributo determina se você receberá um aviso se houver perda de dados durante uma conversão de página de código. Isto se aplica somente a dados que vêm do servidor.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SQL_WARN_YES|Gera avisos quando há perda de dados durante uma conversão de página de código.|  
|SQL_WARN_NO|(Padrão) Não gera avisos quando há perda de dados durante uma conversão de página de código.|  
  
## <a name="sqlsetconnectattr-support-for-service-principal-names-spns"></a>Suporte do SQLSetConnectAttr a SPNs (Nomes da Entidade de Serviço)  
 SQLSetConnectAttr pode ser usado para definir o valor dos novos atributos de conexão SQL_COPT_SS_SERVER_SPN e SQL_COPT_SS_FAILOVER_PARTNER_SPN. Estes atributos não podem ser definidos quando uma conexão estiver aberta; se você tentar definir estes atributos quando uma conexão estiver aberta, o erro HY011 será passado como retorno, com a mensagem "Operação inválida neste momento". (SQLSetConnectOption também pode ser usado para definir esses valores.)  
  
 Para obter mais informações sobre SPNs, consulte [nomes de entidade de serviço &#40;SPNs&#41; em conexões de cliente &#40;&#41;ODBC ](../native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="sql_copt_ss_connection_dead"></a>SQL_COPT_SS_CONNECTION_DEAD  
 Este é um atributo somente leitura.  
  
 Para obter mais informações sobre SQL_COPT_SS_CONNECTION_DEAD, consulte [SQLGetConnectAttr](sqlgetconnectattr.md) e [conectando-se a uma fonte de dados &#40;ODBC&#41;](../native-client-odbc-communication/connecting-to-a-data-source-odbc.md).  
  
## <a name="example"></a>Exemplo  
 Este exemplo faz o log de dados de desempenho.  
  
```  
SQLPERF*     pSQLPERF;  
SQLINTEGER   nValue;  
  
// See if you are already logging. SQLPERF* will be NULL if not.  
SQLGetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA, &pSQLPERF,  
    sizeof(SQLPERF*), &nValue);  
  
if (pSQLPERF == NULL)  
    {  
    // Set the performance log file name.  
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG,  
        (SQLPOINTER) "\\My LogDirectory\\MyServerLog.txt", SQL_NTS);  
  
    // Start logging...  
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA,  
        (SQLPOINTER) SQL_PERF_START, SQL_IS_INTEGER);  
    }  
else  
    {  
    // Take a snapshot now so that your performance statistics are discernible.  
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG_NOW, NULL, 0);  
    }  
  
    // ...perform some action...  
  
// ...take a performance data snapshot...  
SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG_NOW, NULL, 0);  
  
    // ...perform more actions...  
  
// ...take another snapshot...  
SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG_NOW, NULL, 0);  
  
// ...and disable logging.  
SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA,  
    (SQLPOINTER) SQL_PERF_STOP, SQL_IS_INTEGER);  
  
// Continue on...  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLSetConnectAttr](https://go.microsoft.com/fwlink/?LinkId=59368)   
 [Detalhes de implementação da API ODBC](odbc-api-implementation-details.md)   
 [Funções de cópia em massa](../native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)   
 [DEFINIR ANSI_NULLS &#40;&#41;Transact-SQL](/sql/t-sql/statements/set-ansi-nulls-transact-sql)   
 [DEFINIR ANSI_PADDING &#40;&#41;Transact-SQL](/sql/t-sql/statements/set-ansi-padding-transact-sql)   
 [DEFINIR ANSI_WARNINGS &#40;&#41;Transact-SQL](/sql/t-sql/statements/set-ansi-warnings-transact-sql)   
 [DEFINIR CONCAT_NULL_YIELDS_NULL &#40;&#41;Transact-SQL](/sql/t-sql/statements/set-concat-null-yields-null-transact-sql)   
 [DEFINIR QUOTED_IDENTIFIER &#40;&#41;Transact-SQL](/sql/t-sql/statements/set-quoted-identifier-transact-sql)   
 [Função SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360)   
 [SQLGetInfo](../../relational-databases/native-client-odbc-api/sqlgetinfo.md)  
  
  

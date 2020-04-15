---
title: Funções de API de nível principal (Driver ODBC para Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- core level API functions [ODBC]
- ODBC core level API functions [ODBC]
ms.assetid: 8596eed7-bda6-4cac-ae1f-efde1aab785f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19751bb6d0556b117d0a73967d4db00c408733ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281016"
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>Funções de API de nível do núcleo (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 As funções neste nível compreendem o nível mínimo de conformidade de interface para drivers ODBC.  
  
|Função API|Observações|  
|------------------|-----------|  
|**SQLAllocConnect**|Aloca memória para uma alça de conexão, *hdbc,* dentro do ambiente identificado pela *henv*. O Driver Manager processa essa chamada e chama a função **SQLAllocConnect** do driver sempre que **SQLConnect,** **SQLBrowseConnect**ou **SQLDriverConnect** forem chamados.|  
|**SQLAllocEnv**|Exibe uma caixa de diálogo especificando o requisito para o software Oracle Client e, em seguida, retorna SQL_NULL_HANDLE. Se o software Oracle Client não estiver instalado, essa função alocará memória para uma alça de ambiente, *henv*e inicializa a interface de nível de chamada ODBC para uso por um aplicativo.|  
|**SQLAllocStmt**|Aloca a memória para uma alça de declaração e associa a alça da declaração com a conexão especificada pelo hdbc. O Driver Manager passa esta chamada para o driver, que aloca a memória para a estrutura hstmt.|  
|**SQLBindCol**|Atribui espaço de armazenamento a uma coluna de resultados e especifica o tipo do resultado.|  
|**SQLCancel**|Cancela o processamento em uma alça de declaração, hstmt. Em alguns casos, a Oracle não permite o cancelamento de uma declaração em execução. Isso significa que uma instrução em execução continuará até que a Oracle complete o processo, momento em que os resultados das declarações são cancelados pelo Driver ODBC para Oracle.|  
|**SQLColAttributea**|Retorna informações do descritor para uma coluna em um conjunto de resultados. As informações do descritor são retornadas como uma seqüência de caracteres, um valor dependente do descritor de 32 bits ou um valor inteiro.|  
|**SQLConnect**|Conecta-se a uma fonte de dados. Para usar a autenticação do sistema operacional Oracle, especifique "/" como parâmetro *szUID* e "" como parâmetro *szAuthStr.*|  
|**SQLDescribeCol**|Retorna o nome, tipo, precisão, escala e nulidade da coluna de resultados dada. **Nota: SQLDescribeCol** relata colunas calculadas como SQL_VARCHAR.|  
|**Sqldisconnect**|Fecha uma conexão. Se o pool de conexões estiver habilitado para um ambiente compartilhado e um aplicativo chamar **sqldisconnect** em uma conexão nesse ambiente, a conexão será devolvida ao pool de conexões e ainda está disponível para outros componentes usando o mesmo ambiente compartilhado.|  
|**Sqlerror**|Retorna informações de erro ou status sobre o último erro. O driver mantém uma pilha ou lista de erros que podem ser devolvidos para os argumentos *hstmt*, *hdbc*e *henv,* dependendo de como a chamada para **SQLError** é feita. A fila de erros é lavada após cada declaração. Normalmente recupera uma mensagem de erro Oracle e está vazia de outra forma.|  
|**SQLExecDirect**|Executa uma nova declaração SQL despreparada. O driver usa os valores atuais das variáveis de marcador de parâmetro se houver algum parâmetro na declaração. Se a sua tabela, exibição ou nomes de campo contiverem espaços, feche os nomes nas marcas de aspas traseiras. Por exemplo, se o seu banco de dados contiver uma tabela chamada *Minha Tabela* e o campo *Meu Campo,* indescesse cada elemento do identificador assim:<br /><br /> SELECIONE \`\`minha mesa . \`Meu Campo1\`,; \`Minha\`mesa. \`Meu\` campo2 \`da minha mesa\`|  
|**SQLExecute**|Executa uma declaração SQL preparada (uma declaração já preparada pelo **SQLPrepare**). O driver usa os valores atuais das variáveis de marcador de parâmetro se houver algum parâmetro na declaração.|  
|**SQLFetch**|Recupera uma linha de um resultado definido nos locais especificados pelas chamadas anteriores para **SQLBindCol**. Prepara o driver para uma chamada para **SQLGetData** para as colunas não vinculadas.|  
|**SQLFreeConnect**|Libera uma alça de conexão e libera toda a memória alocada para o cabo.|  
|**SQLFreeEnv**|Fecha o Driver ODBC para Oracle e libera toda a memória associada ao driver.|  
|**SQLFreeStmt**|Interrompe o processamento associado a um hstmt específico, fecha todos os cursores abertos associados ao hstmt, descarta resultados pendentes e, opcionalmente, libera todos os recursos associados à alça da instrução.|  
|**SQLGetCursorName**|Retorna o nome do cursor associado com o hstmt dado.|  
|**SQLNumResultCols**|Retorna o número de colunas em um cursor definido por resultados.|  
|**SQLPrepare**|Prepara uma declaração SQL planejando como otimizar e executar a declaração. A declaração SQL é compilada para execução pelo **SQLExecDirect**.<br /><br /> Se a sua tabela, exibição ou nomes de campo contiverem espaços, feche os nomes nas marcas de aspas traseiras. Por exemplo, se o seu banco de dados contiver uma tabela chamada *Minha Tabela* e o campo *Meu Campo,* indescesse cada elemento do identificador da seguinte forma:<br /><br /> SELECIONE \`\`minha mesa . \`Meu\` campo \`da minha mesa\`<br /><br /> Para obter informações sobre o uso de conjuntos de resultados contendo matrizes como parâmetros formais, consulte [''''''''''''''''''''''''''''''''''''''''''''''''''](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md)|  
|**SQLRowCount**|A Oracle não fornece uma maneira de determinar o número de linhas em um resultado definido até depois de buscar a última linha, por isso retorna -1.|  
|**Sqlsetcursorname**|Associa um nome de cursor com uma alça de declaração ativa, *hstmt*.|  
|**SQLSetParam**|Substituído por SQLBindParameter em ODBC 2. *x*.|  
|**SQLTransact**|Solicita uma operação de confirmação ou reversão para todas as operações ativas em todas as alças de declaração (hstmts) associadas a uma conexão, ou para todas as conexões associadas ao cabo do ambiente, *henv*. Se um compromisso falhar quando estiver no modo manual, a transação permanecerá ativa; você pode optar por reverter a transação ou tentar novamente a operação de confirmação. Se uma operação de confirmação falhar quando estiver no modo de transação automática, a transação será revertida automaticamente; a transação não pode ser inativa.|

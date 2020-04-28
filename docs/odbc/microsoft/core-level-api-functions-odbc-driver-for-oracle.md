---
title: Funções de API de nível de núcleo (driver ODBC para Oracle) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81281016"
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>Funções de API de nível do núcleo (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 As funções nesse nível compõem o nível mínimo de conformidade de interface para drivers ODBC.  
  
|Função de API|Observações|  
|------------------|-----------|  
|**SQLAllocConnect**|Aloca memória para um identificador de conexão, *HDBC*, dentro do ambiente identificado por *HENV*. O Gerenciador de driver processa essa chamada e chama a função **SQLAllocConnect** do driver sempre que **SQLConnect**, **SQLBrowseConnect**ou **SQLDriverConnect** é chamado.|  
|**SQLAllocEnv**|Exibe uma caixa de diálogo especificando o requisito para o software cliente Oracle e, em seguida, retorna SQL_NULL_HANDLE. Se o software cliente Oracle não estiver instalado, essa função alocará memória para um identificador de ambiente, *HENV*, e inicializará a interface de nível de chamada ODBC para uso por um aplicativo.|  
|**SQLAllocStmt**|Aloca memória para um identificador de instrução e associa o identificador de instrução à conexão especificada por HDBC. O Gerenciador de driver passa essa chamada para o driver, que aloca a memória para a estrutura HSTMT.|  
|**SQLBindCol**|Atribui espaço de armazenamento para uma coluna de resultado e especifica o tipo do resultado.|  
|**SQLCancel**|Cancela o processamento em um identificador de instrução, HSTMT. Em alguns casos, a Oracle não permite o cancelamento de uma instrução em execução. Isso significa que uma instrução em execução continuará até que o Oracle conclua o processo e, nesse momento, os resultados das instruções serão cancelados pelo driver ODBC para Oracle.|  
|**SQLColAttributes**|Retorna informações de descritor para uma coluna em um conjunto de resultados. As informações do descritor são retornadas como uma cadeia de caracteres, um valor dependente de descritor de 32 bits ou um valor inteiro.|  
|**SQLConnect**|Conecta-se a uma fonte de dados. Para usar a autenticação do sistema operacional Oracle, especifique "/" como o parâmetro *szUID* e "" como o parâmetro *szAuthStr* .|  
|**SQLDescribeCol**|Retorna o nome, o tipo, a precisão, a escala e a nulidade da coluna de resultado especificada. **Observação: SQLDescribeCol** relata colunas calculadas como SQL_VARCHAR.|  
|**SQLDisconnect**|Fecha uma conexão. Se o pool de conexões estiver habilitado para um ambiente compartilhado e um aplicativo chamar **SQLDisconnect** em uma conexão nesse ambiente, a conexão será retornada ao pool de conexões e ainda estará disponível para outros componentes usando o mesmo ambiente compartilhado.|  
|**SQLError**|Retorna informações de erro ou de status sobre o último erro. O driver mantém uma pilha ou lista de erros que podem ser retornados para os argumentos *HSTMT*, *HDBC*e *HENV* , dependendo de como a chamada a **SqlError** é feita. A fila de erros é liberada após cada instrução. Geralmente recupera uma mensagem de erro do Oracle e, de outra forma, está vazia.|  
|**SQLExecDirect**|Executa uma nova instrução SQL despreparada. O driver usará os valores atuais das variáveis de marcador de parâmetro se existirem parâmetros na instrução. Se os nomes de tabela, exibição ou campo contiverem espaços, coloque os nomes nas aspas de fundo. Por exemplo, se o seu banco de dados contiver uma tabela denominada *minha tabela* e o campo *meu*campo, coloque cada elemento do identificador da seguinte forma:<br /><br /> Selecione \`minha tabela\`. \`Meu campo1\`,; \`Minha tabela\`. \`Meu campo2\` da \`minha tabela\`|  
|**SQLExecute**|Executa uma instrução SQL preparada (uma instrução já preparada por **SQLPrepare**). O driver usará os valores atuais das variáveis de marcador de parâmetro se existirem parâmetros na instrução.|  
|**SQLFetch**|Recupera uma linha de um conjunto de resultados para os locais especificados pelas chamadas anteriores para **SQLBindCol**. Prepara o driver para uma chamada para **SQLGetData** para as colunas desassociadas.|  
|**SQLFreeConnect**|Libera um identificador de conexão e libera toda a memória alocada para o identificador.|  
|**SQLFreeEnv**|Fecha o driver ODBC para Oracle e libera toda a memória associada ao driver.|  
|**SQLFreeStmt**|Interrompe o processamento associado a um HSTMT específico, fecha os cursores abertos associados ao HSTMT, descarta os resultados pendentes e, opcionalmente, libera todos os recursos associados ao identificador da instrução.|  
|**SQLGetCursorName**|Retorna o nome do cursor associado ao HSTMT fornecido.|  
|**SQLNumResultCols**|Retorna o número de colunas em um cursor de conjunto de resultados.|  
|**SQLPrepare**|Prepara uma instrução SQL planejando como otimizar e executar a instrução. A instrução SQL é compilada para execução por **SQLExecDirect**.<br /><br /> Se os nomes de tabela, exibição ou campo contiverem espaços, coloque os nomes nas aspas de fundo. Por exemplo, se seu banco de dados contiver uma tabela denominada *minha tabela* e o campo *meu*campo, coloque cada elemento do identificador da seguinte maneira:<br /><br /> Selecione \`minha tabela\`. \`Meu campo\` da \`minha tabela\`<br /><br /> Para obter informações sobre como usar conjuntos de resultados contendo matrizes como parâmetros formais, consulte [retornando parâmetros de matriz de procedimentos armazenados](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLRowCount**|O Oracle não fornece uma maneira de determinar o número de linhas em um conjunto de resultados até que você busque a última linha, portanto, retorna-1.|  
|**SQLSetCursorName**|Associa um nome de cursor a um identificador de instrução ativo, *HSTMT*.|  
|**SQLSetParam**|Substituído por SQLBindParameter no ODBC 2. *x*.|  
|**SQLTransact**|Solicita uma operação de confirmação ou reversão para todas as operações ativas em todos os identificadores de instrução (hstmts) associados a uma conexão ou para todas as conexões associadas ao identificador de ambiente, *HENV*. Se uma confirmação falhar quando estiver no modo manual, a transação permanecerá ativa; Você pode optar por reverter a transação ou tentar novamente a operação de confirmação. Se uma operação de confirmação falhar quando estiver no modo de transação automática, a transação será revertida automaticamente; a transação não pode ficar inativa.|

---
title: Escrevendo aplicativos ODBC 3.x | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], about upgrading
- ODBC drivers [ODBC], backward compatibility
- upgrading applications [ODBC]
- compatibility [ODBC], upgrading applications
- application upgrades [ODBC]
- upgrading applications [ODBC], about upgrading
- backward compatibility [ODBC], upgrading applications
ms.assetid: 19c54fc5-9dd6-49b6-8c9f-a38961b40a65
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 93c8510bb23bb57244590a472073fc882f9fe64f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47769140"
---
# <a name="writing-odbc-3x-applications"></a>Escrever aplicativos ODBC 3.x
Quando um ODBC 2. *x* aplicativo é atualizado para o ODBC 3. *x*, ele deve ser escrito de forma que ele funciona com os dois ODBC 2. *x* e 3. *x* drivers. O aplicativo deve incorporar o código condicional para aproveitar ao máximo o ODBC 3. *x* recursos.  
  
 O atributo de ambiente SQL_ATTR_ODBC_VERSION deve ser definido como SQL_OV_ODBC2. Isso garantirá que o driver se comporta como um ODBC 2 *. x* driver em relação as alterações descritas na seção [alterações comportamentais](../../../odbc/reference/develop-app/behavioral-changes.md).  
  
 Se o aplicativo usar qualquer um dos recursos descritos na seção [novos recursos](../../../odbc/reference/develop-app/new-features.md), código condicional deve ser usado para determinar se o driver é um ODBC 3. *x* ou o ODBC 2 *. x* driver. O aplicativo usa **SQLGetDiagField** e **SQLGetDiagRec** para obter o ODBC 3. *x* SQLSTATEs enquanto faz esses fragmentos de código condicional de processamento de erro. Os seguintes pontos sobre a nova funcionalidade devem ser considerados:  
  
-   Um aplicativo afetado pela mudança no comportamento de tamanho do conjunto de linhas deve ter cuidado para não chame **SQLFetch** quando o tamanho da matriz é maior que 1. Esses aplicativos devem substituir chamadas para **SQLExtendedFetch** com chamadas para **SQLSetStmtAttr** para definir o atributo de instrução SQL_ATTR_ARRAY_STATUS_PTR e **SQLFetchScroll**, de modo que eles têm código comum que funciona com os dois ODBC 3. *x* e o ODBC 2. *x* drivers. Porque **SQLSetStmtAttr** com SQL_ATTR_ROW_ARRAY_SIZE será mapeado para **SQLSetStmtAttr** com SQL_ROWSET_SIZE para ODBC 2. *x* drivers, aplicativos podem apenas definir SQL_ATTR_ROW_ARRAY_SIZE para suas operações de busca multilinha.  
  
-   A maioria dos aplicativos que estão sendo atualizados, na verdade, não são afetados pelas alterações nos códigos de SQLSTATE. Para os aplicativos que são afetados, eles podem fazer uma pesquisa mecânica e substituir na maioria dos casos, usando a tabela de conversão de erro na seção "Mapeamento de SQLSTATE" para converter o ODBC 3. *x* códigos de erro para o ODBC 2 *. x* códigos. Desde o ODBC 3 *. x* Gerenciador de Driver realizará o mapeamento do ODBC 2. *x* SQLSTATEs ODBC 3. *x* SQLSTATEs, esses criadores de aplicativo precisam verificação apenas para o ODBC 3. *x* SQLSTATEs e não se preocupe sobre como incluir o ODBC 2. *x* SQLSTATEs no código condicional.  
  
-   Se um aplicativo faz muito uso de data, hora e tipos de dados de carimbo de hora, o aplicativo pode declarar propriamente ditos tenham um ODBC 2. *x* aplicativo e como usar as existentes de código em vez de usar código condicionado.  
  
 A atualização também deve incluir as seguintes etapas:  
  
-   Chame **SQLSetEnvAttr** antes de alocar uma conexão para definir o atributo de ambiente SQL_ATTR_ODBC_VERSION SQL_OV_ODBC2.  
  
-   Substitua todas as chamadas para **SQLAllocEnv**, **SQLAllocConnect**, ou **SQLAllocStmt** com chamadas para **SQLAllocHandle** com os devidos *HandleType* argumento SQL_HANDLE_ENV, SQL_HANDLE_DBC ou SQL_HANDLE_STMT.  
  
-   Substitua todas as chamadas para **SQLFreeEnv** ou **SQLFreeConnect** com chamadas para **SQLFreeHandle** com os devidos *HandleType* argumento de SQL_HANDLE_DBC ou SQL_HANDLE_STMT.  
  
-   Substitua todas as chamadas para **SQLSetConnectOption** com chamadas para **SQLSetConnectAttr**. Se definir um atributo cujo valor é uma cadeia de caracteres, defina as *StringLength* argumento adequadamente. Alteração *atributo* argumento de SQL_XXXX para SQL_ATTR_XXXX.  
  
-   Substitua todas as chamadas para **SQLGetConnectOption** com chamadas para **SQLGetConnectAttr**. Se obter uma cadeia de caracteres ou um atributo binário, defina *BufferLength* para o valor apropriado e passar uma *StringLength* argumento. Alteração *atributo* argumento de SQL_XXXX para SQL_ATTR_XXXX.  
  
-   Substitua todas as chamadas para **SQLSetStmtOption** com chamadas para **SQLSetStmtAttr**. Se definir um atributo cujo valor é uma cadeia de caracteres, defina as *StringLength* argumento adequadamente. Alteração *atributo* argumento de SQL_XXXX para SQL_ATTR_XXXX.  
  
-   Substitua todas as chamadas para **SQLGetStmtOption** com chamadas para **SQLGetStmtAttr**. Se obter uma cadeia de caracteres ou um atributo binário, defina *BufferLength* para o valor apropriado e passar uma *StringLength* argumento. Alteração *atributo* argumento de SQL_XXXX para SQL_ATTR_XXXX.  
  
-   Substitua todas as chamadas para **SQLTransact** com chamadas para **SQLEndTran**. Se o identificador válido mais à direita na **SQLTransact** chamada é um identificador de ambiente, um *HandleType* argumento SQL_HANDLE_ENV deve ser usado no **SQLEndTran** chamar com apropriado *manipular* argumento. Se o identificador válido mais à direita em sua **SQLTransact** chamada é um identificador de conexão, um *HandleType* argumento SQL_HANDLE_DBC deve ser usado no **SQLEndTran** chamar com apropriado *manipular* argumento.  
  
-   Substitua todas as chamadas para **SQLColAttributes** com chamadas para **SQLColAttribute**. Se o *FieldIdentifier* argumento é SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE ou SQL_COLUMN_LENGTH, não altere nada diferente do nome da função. Caso contrário, altere *FieldIdentifier* de SQL_COLUMN_XXXX para SQL_DESC_XXXX. Se *FieldIdentifier* é SQL_DESC_CONCISE_TYPE e o tipo de dados é um tipo de dados de data e hora, altere para o ODBC 3 correspondente *. x* tipo de dados.  
  
-   Se usar cursores em bloco, cursores roláveis ou ambos, o aplicativo faz o seguinte:  
  
    -   Define o tamanho de conjunto de linhas, o tipo de cursor e a simultaneidade de cursor usando **SQLSetStmtAttr**.  
  
    -   Chamadas **SQLSetStmtAttr** defina sql_attr_row_status_ptr de modo que aponte para uma matriz de registros de status.  
  
    -   Chamadas **SQLSetStmtAttr** definir SQL_ATTR_ROWS_FETCHED_PTR para apontar para um sqlinteger que contém.  
  
    -   Executa as associações necessárias e executa a instrução SQL.  
  
    -   Chamadas **SQLFetchScroll** em um loop para buscar linhas e mover-se no resultado definido.  
  
    -   Se desejar buscar por indicador, o aplicativo chama **SQLSetStmtAttr** para definir SQL_ATTR_FETCH_BOOKMARK_PTR como uma variável que contém o indicador para a linha que deseja buscar e chama **SQLFetchScroll** com um *FetchOrientation* argumento de SQL_FETCH_BOOKMARK.  
  
-   Se o uso de matrizes de parâmetros, o aplicativo faz o seguinte:  
  
    -   Chamadas **SQLSetStmtAttr** para definir o atributo SQL_ATTR_PARAMSET_SIZE como o tamanho da matriz de parâmetros.  
  
    -   Chamadas **SQLSetStmtAttr** definir SQL_ATTR_ROWS_PROCESSED_PTR para apontar para uma variável UDWORD interna.  
  
    -   Executa a se preparar, associar e executar operações conforme apropriado.  
  
    -   Se a execução for interrompida por algum motivo (por exemplo, SQL_NEED_DATA), ele pode encontrar a linha "atual" de parâmetros inspecionando o local apontado pela SQL_ATTR_ROWS_PROCESSED_PTR.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Mapeando funções de substituição para compatibilidade com versões anteriores de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [Calling SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [Chamando SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [Chamando SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [Operações de biblioteca de cursor](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [Mapeando os tipos de informações dos atributos1 de cursor](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)

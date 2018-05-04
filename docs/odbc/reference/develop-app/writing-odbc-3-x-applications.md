---
title: Gravando os aplicativos ODBC 3. x | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 61809072272ae91c32d4780971735c29c53fe977
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="writing-odbc-3x-applications"></a>Gravação de ODBC 3. x aplicativos
Quando um ODBC 2. *x* aplicativo é atualizado para o ODBC 3. *x*, ele deve ser escrito, de modo que ele funciona com os dois ODBC 2. *x* e 3. *x* drivers. O aplicativo deve incorporar o código condicional para aproveitar ao máximo o ODBC 3. *x* recursos.  
  
 O atributo de ambiente SQL_ATTR_ODBC_VERSION deve ser definido como SQL_OV_ODBC2. Isso irá garantir que o driver se comporta como um ODBC 2 *. x* driver em relação as alterações descritas na seção [alterações de comportamento](../../../odbc/reference/develop-app/behavioral-changes.md).  
  
 Se o aplicativo usar qualquer um dos recursos descritos na seção [novos recursos](../../../odbc/reference/develop-app/new-features.md), código condicional deve ser usado para determinar se o driver é um ODBC 3. *x* ou ODBC 2 *. x* driver. O aplicativo usa **SQLGetDiagField** e **SQLGetDiagRec** obter ODBC 3. *x* SQLSTATEs durante esses fragmentos de código condicional de processamento de erro. Os seguintes pontos sobre a nova funcionalidade devem ser considerados:  
  
-   Um aplicativo afetado pela mudança no comportamento de tamanho do conjunto de linhas deve ter cuidado para não chamar **SQLFetch** quando o tamanho da matriz é maior que 1. Esses aplicativos devem substituir chamadas para **SQLExtendedFetch** com chamadas para **SQLSetStmtAttr** para definir o atributo de instrução SQL_ATTR_ARRAY_STATUS_PTR e **SQLFetchScroll**, de modo que eles têm código comum que funciona com os dois ODBC 3. *x* e ODBC 2. *x* drivers. Porque **SQLSetStmtAttr** com SQL_ATTR_ROW_ARRAY_SIZE serão mapeados para **SQLSetStmtAttr** com SQL_ROWSET_SIZE do ODBC 2. *x* drivers, aplicativos podem apenas definir SQL_ATTR_ROW_ARRAY_SIZE em suas operações de busca multilinha.  
  
-   A maioria dos aplicativos que está atualizando, na verdade, não são afetados pelas alterações nos códigos SQLSTATE. Para os aplicativos que são afetados, podem fazer uma pesquisa mecânica e substituir na maioria dos casos, usando a tabela de conversão de erro na seção "Mapeamento de SQLSTATE" para converter o ODBC 3. *x* códigos de erro de ODBC 2 *. x* códigos. Desde o ODBC 3 *. x* Gerenciador de Driver irá realizar o mapeamento do ODBC 2. *x* SQLSTATEs ODBC 3. *x* SQLSTATEs, esses programadores precisam somente a seleção para o ODBC 3. *x* SQLSTATEs e não se preocupe incluindo ODBC 2. *x* SQLSTATEs no código condicional.  
  
-   Se um aplicativo grande uso de data, hora e tipos de dados de carimbo de hora, o aplicativo pode declarar automaticamente para ser um ODBC 2. *x* aplicativo e como usar a existente de código em vez de usar o código de condição.  
  
 A atualização também deve incluir as seguintes etapas:  
  
-   Chamar **SQLSetEnvAttr** antes de alocar uma conexão para definir o atributo de ambiente SQL_ATTR_ODBC_VERSION SQL_OV_ODBC2.  
  
-   Substitua todas as chamadas para **SQLAllocEnv**, **SQLAllocConnect**, ou **SQLAllocStmt** com chamadas para **SQLAllocHandle** com apropriada *HandleType* argumento SQL_HANDLE_ENV, SQL_HANDLE_DBC ou SQL_HANDLE_STMT.  
  
-   Substitua todas as chamadas para **SQLFreeEnv** ou **SQLFreeConnect** com chamadas para **SQLFreeHandle** com apropriada *HandleType* argumento SQL_HANDLE_DBC ou SQL_HANDLE_STMT.  
  
-   Substitua todas as chamadas para **SQLSetConnectOption** com chamadas para **SQLSetConnectAttr**. Se definir um atributo cujo valor é uma cadeia de caracteres, defina o *StringLength* argumento adequadamente. Alterar *atributo* argumento de SQL_XXXX para SQL_ATTR_XXXX.  
  
-   Substitua todas as chamadas para **SQLGetConnectOption** com chamadas para **SQLGetConnectAttr**. Se receber uma cadeia de caracteres ou um atributo binário, defina *BufferLength* para o valor apropriado e passar uma *StringLength* argumento. Alterar *atributo* argumento de SQL_XXXX para SQL_ATTR_XXXX.  
  
-   Substitua todas as chamadas para **SQLSetStmtOption** com chamadas para **SQLSetStmtAttr**. Se definir um atributo cujo valor é uma cadeia de caracteres, defina o *StringLength* argumento adequadamente. Alterar *atributo* argumento de SQL_XXXX para SQL_ATTR_XXXX.  
  
-   Substitua todas as chamadas para **SQLGetStmtOption** com chamadas para **SQLGetStmtAttr**. Se receber uma cadeia de caracteres ou um atributo binário, defina *BufferLength* para o valor apropriado e passar uma *StringLength* argumento. Alterar *atributo* argumento de SQL_XXXX para SQL_ATTR_XXXX.  
  
-   Substitua todas as chamadas para **SQLTransact** com chamadas para **SQLEndTran**. Se o identificador válido mais à direita no **SQLTransact** chamada é um identificador de ambiente, uma *HandleType* argumento SQL_HANDLE_ENV deve ser usado no **SQLEndTran** chamar com apropriada *tratar* argumento. Se o identificador válido mais à direita em sua **SQLTransact** chamada é um identificador de conexão, um *HandleType* argumento SQL_HANDLE_DBC deve ser usado no **SQLEndTran** chamar com apropriada *tratar* argumento.  
  
-   Substitua todas as chamadas para **SQLColAttributes** com chamadas para **SQLColAttribute**. Se o *FieldIdentifier* argumento é SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE ou SQL_COLUMN_LENGTH, não altere nada diferente do nome da função. Se não estiver, altere *FieldIdentifier* de SQL_COLUMN_XXXX para SQL_DESC_XXXX. Se *FieldIdentifier* é SQL_DESC_CONCISE_TYPE e o tipo de dados é um tipo de dados datetime, altere para o ODBC 3 correspondente *. x* tipo de dados.  
  
-   Se usar cursores em bloco, cursores roláveis ou ambos, o aplicativo faz o seguinte:  
  
    -   Define o tamanho do conjunto de linhas, o tipo de cursor e a simultaneidade de cursor usando **SQLSetStmtAttr**.  
  
    -   Chamadas **SQLSetStmtAttr** defina sql_attr_row_status_ptr de modo que aponte para uma matriz de registros de status.  
  
    -   Chamadas **SQLSetStmtAttr** para definir SQL_ATTR_ROWS_FETCHED_PTR para apontar para um sqlinteger que contém.  
  
    -   Executa as associações necessárias e executa a instrução SQL.  
  
    -   Chamadas **SQLFetchScroll** em um loop para buscar linhas e percorrer o resultado definido.  
  
    -   Se desejar buscar pelo indicador, o aplicativo chama **SQLSetStmtAttr** para definir SQL_ATTR_FETCH_BOOKMARK_PTR como uma variável que contém o indicador para a linha que deseja buscar e chamadas **SQLFetchScroll** com um *FetchOrientation* argumento de SQL_FETCH_BOOKMARK.  
  
-   Se usar matrizes de parâmetros, o aplicativo faz o seguinte:  
  
    -   Chamadas **SQLSetStmtAttr** para definir o atributo SQL_ATTR_PARAMSET_SIZE como o tamanho da matriz de parâmetros.  
  
    -   Chamadas **SQLSetStmtAttr** para definir SQL_ATTR_ROWS_PROCESSED_PTR para apontar para uma variável UDWORD interna.  
  
    -   Executa preparar, associar e executar operações conforme apropriado.  
  
    -   Se a execução é interrompida por algum motivo (como SQL_NEED_DATA), ele pode localizar a linha "atual" de parâmetros inspecionando o local apontado pelo SQL_ATTR_ROWS_PROCESSED_PTR.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Mapeando funções de substituição para compatibilidade com versões anteriores de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [Calling SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [Chamando SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [Chamando SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [Operações de biblioteca de cursor](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [Mapeando os tipos de informações dos atributos1 de cursor](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)

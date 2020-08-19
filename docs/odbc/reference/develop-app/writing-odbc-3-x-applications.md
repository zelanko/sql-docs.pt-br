---
description: Escrever aplicativos ODBC 3.x
title: Gravando aplicativos ODBC 3. x | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7df97b99df10e613ee45aaa3c01174b46160e740
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421350"
---
# <a name="writing-odbc-3x-applications"></a>Escrever aplicativos ODBC 3.x
Quando um aplicativo ODBC *2. x* é atualizado para o ODBC *3. x*, ele deve ser escrito de forma que funcione com os drivers ODBC *2. x* e *3. x* . O aplicativo deve incorporar o código condicional para aproveitar ao máximo os recursos do ODBC *3. x* .  
  
 O atributo de ambiente SQL_ATTR_ODBC_VERSION deve ser definido como SQL_OV_ODBC2. Isso garantirá que o driver se comporta como um driver ODBC *2. x* , com relação às alterações descritas na seção [alterações comportamentais](../../../odbc/reference/develop-app/behavioral-changes.md).  
  
 Se o aplicativo usar qualquer um dos recursos descritos na seção [novos recursos](../../../odbc/reference/develop-app/new-features.md), o código condicional deverá ser usado para determinar se o driver é um driver ODBC *3. x* ou ODBC *2. x* . O aplicativo usa **SQLGetDiagField** e **SQLGetDiagRec** para obter o ODBC *3. x* sqlstates enquanto realiza o processamento de erro nesses fragmentos de código condicional. Os seguintes pontos sobre a nova funcionalidade devem ser considerados:  
  
-   Um aplicativo afetado pela alteração no comportamento do tamanho do conjunto de linhas deve ter cuidado para não chamar **SQLFetch** quando o tamanho da matriz for maior que 1. Esses aplicativos devem substituir chamadas para **SQLExtendedFetch** com chamadas para **SQLSetStmtAttr** para definir o atributo de instrução SQL_ATTR_ARRAY_STATUS_PTR e como **SQLFetchScroll**, para que eles tenham um código comum que funcione com os drivers ODBC *3. x* e ODBC *2. x* . Como **SQLSetStmtAttr** com SQL_ATTR_ROW_ARRAY_SIZE será mapeado para **SQLSetStmtAttr** com SQL_ROWSET_SIZE para drivers ODBC *2. x* , os aplicativos podem apenas definir SQL_ATTR_ROW_ARRAY_SIZE para suas operações de busca de multirow.  
  
-   A maioria dos aplicativos que estão sendo atualizados não é realmente afetada por alterações nos códigos SQLSTATE. Para os aplicativos que são afetados, eles podem fazer uma pesquisa mecânica e substituir na maioria dos casos usando a tabela de conversão de erros na seção "mapeamento de SQLSTATE" para converter códigos de erro ODBC *3. x* em códigos ODBC *2. x* . Como o Gerenciador de driver ODBC *3. x* executará o mapeamento dos sqlstates do ODBC *2.* x para o ODBC *3. x* , esses gravadores só precisarão verificar o ODBC *3. x* sqlstates e não se preocupar com a inclusão de ODBC *2. x* sqlstates no código condicional.  
  
-   Se um aplicativo fizer grande uso de tipos de dados de data, hora e timestamp, o aplicativo poderá declarar-se como um aplicativo ODBC *2. x* e usar seu código existente em vez de usar código de condicionamento.  
  
 A atualização também deve incluir as seguintes etapas:  
  
-   Chame **SQLSetEnvAttr** antes de alocar uma conexão para definir o atributo de ambiente SQL_ATTR_ODBC_VERSION como SQL_OV_ODBC2.  
  
-   Substitua todas as chamadas para **SQLAllocEnv**, **SQLAllocConnect**ou **SQLAllocStmt** por chamadas para **SQLAllocHandle** com o argumento *HandleType* apropriado de SQL_HANDLE_ENV, SQL_HANDLE_DBC ou SQL_HANDLE_STMT.  
  
-   Substitua todas as chamadas para **SQLFreeEnv** ou **SQLFreeConnect** com chamadas para **SQLFreeHandle** com o argumento *HandleType* apropriado de SQL_HANDLE_DBC ou SQL_HANDLE_STMT.  
  
-   Substitua todas as chamadas para **SQLSetConnectOption** com chamadas para **SQLSetConnectAttr**. Se estiver definindo um atributo cujo valor é uma cadeia de caracteres, defina o argumento *StringLength* adequadamente. Altere o argumento de *atributo* de SQL_XXXX para SQL_ATTR_XXXX.  
  
-   Substitua todas as chamadas para **SQLGetConnectOption** com chamadas para **SQLGetConnectAttr**. Se obter uma cadeia de caracteres ou um atributo binário, defina *BufferLength* como o valor apropriado e passe um argumento *StringLength* . Altere o argumento de *atributo* de SQL_XXXX para SQL_ATTR_XXXX.  
  
-   Substitua todas as chamadas para **SQLSetStmtOption** com chamadas para **SQLSetStmtAttr**. Se estiver definindo um atributo cujo valor é uma cadeia de caracteres, defina o argumento *StringLength* adequadamente. Altere o argumento de *atributo* de SQL_XXXX para SQL_ATTR_XXXX.  
  
-   Substitua todas as chamadas para **SQLGetStmtOption** com chamadas para **SQLGetStmtAttr**. Se obter uma cadeia de caracteres ou um atributo binário, defina *BufferLength* como o valor apropriado e passe um argumento *StringLength* . Altere o argumento de *atributo* de SQL_XXXX para SQL_ATTR_XXXX.  
  
-   Substitua todas as chamadas para **Sqltransacted** por chamadas para **SQLEndTran**. Se o identificador válido mais à direita na chamada **SQLTransact** for um identificador de ambiente, um argumento *handletype* de SQL_HANDLE_ENV deverá ser usado na chamada **SQLEndTran** com o argumento *Handle* apropriado. Se o identificador válido mais à direita em sua chamada **SQLTransact** for um identificador de conexão, um argumento *handletype* de SQL_HANDLE_DBC deverá ser usado na chamada **SQLEndTran** com o argumento *Handle* apropriado.  
  
-   Substitua todas as chamadas para **SQLColAttributes** com chamadas para **SQLColAttribute**. Se o argumento *FieldIdentifier* for SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE ou SQL_COLUMN_LENGTH, não altere nada além do nome da função. Caso contrário, altere *FieldIdentifier* de SQL_COLUMN_XXXX para SQL_DESC_XXXX. Se *FieldIdentifier* for SQL_DESC_CONCISE_TYPE e o tipo de dados for um tipo de dados DateTime, altere para o tipo de dados ODBC *3. x* correspondente.  
  
-   Se estiver usando cursores de bloco, cursores roláveis ou ambos, o aplicativo fará o seguinte:  
  
    -   Define o tamanho do conjunto de linhas, o tipo de cursor e a simultaneidade do cursor usando **SQLSetStmtAttr**.  
  
    -   Chama **SQLSetStmtAttr** para definir SQL_ATTR_ROW_STATUS_PTR para apontar para uma matriz de registros de status.  
  
    -   Chama **SQLSetStmtAttr** para definir SQL_ATTR_ROWS_FETCHED_PTR para apontar para um sqlinteiro.  
  
    -   Executa as associações necessárias e executa a instrução SQL.  
  
    -   Chama **SQLFetchScroll** em um loop para buscar linhas e mover-se no conjunto de resultados.  
  
    -   Se quiser buscar por indicador, o aplicativo chamará **SQLSetStmtAttr** para definir SQL_ATTR_FETCH_BOOKMARK_PTR para uma variável que conterá o indicador para a linha que deseja buscar e chamará **SQLFetchScroll** com um argumento *FetchOrientation* de SQL_FETCH_BOOKMARK.  
  
-   Se estiver usando matrizes de parâmetros, o aplicativo fará o seguinte:  
  
    -   Chama **SQLSetStmtAttr** para definir o atributo SQL_ATTR_PARAMSET_SIZE como o tamanho da matriz de parâmetros.  
  
    -   Chama **SQLSetStmtAttr** para definir SQL_ATTR_ROWS_PROCESSED_PTR para apontar para uma variável UDWORD interna.  
  
    -   Executa as operações de preparação, ligação e execução conforme apropriado.  
  
    -   Se a execução for interrompida por algum motivo (como SQL_NEED_DATA), ela poderá encontrar a linha "atual" dos parâmetros inspecionando o local apontado por SQL_ATTR_ROWS_PROCESSED_PTR.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Mapeando funções de substituição para compatibilidade com versões anteriores de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [Calling SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [Chamar SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [Chamar SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [Operações de biblioteca de cursor](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [Mapear os tipos de informações dos atributos1 de cursor](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)

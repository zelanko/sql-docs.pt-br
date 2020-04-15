---
title: Redação de aplicações ODBC 3.x | Microsoft Docs
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
ms.openlocfilehash: 3ba48d76babcaa5fcc49a541088f7c4cc349b569
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288984"
---
# <a name="writing-odbc-3x-applications"></a>Escrever aplicativos ODBC 3.x
Quando um aplicativo ODBC *2.x* é atualizado para ODBC *3.x,* ele deve ser escrito de modo que ele funcione com drivers ODBC *2.x* e *3.x.* O aplicativo deve incorporar código condicional para aproveitar ao máximo os recursos do ODBC *3.x.*  
  
 O SQL_ATTR_ODBC_VERSION atributo ambiente deve ser definido como SQL_OV_ODBC2. Isso garantirá que o driver se comporte como um driver ODBC *2.x* em relação às alterações descritas na seção [Mudanças comportamentais](../../../odbc/reference/develop-app/behavioral-changes.md).  
  
 Se o aplicativo utilizar qualquer um dos recursos descritos na seção [Novos Recursos,](../../../odbc/reference/develop-app/new-features.md)o código condicional deve ser usado para determinar se o driver é um driver ODBC *3.x* ou ODBC *2.x.* O aplicativo usa **SQLGetDiagField** e **SQLGetDiagRec** para obter ODBC *3.x* SQLSTATEs enquanto faz o processamento de erros nesses fragmentos de código condicional. Os seguintes pontos sobre a nova funcionalidade devem ser considerados:  
  
-   Um aplicativo afetado pela alteração no comportamento de tamanho do conjunto de linhas deve ter cuidado para não chamar **sqlfetch** quando o tamanho da matriz for maior que 1. Esses aplicativos devem substituir as chamadas para **SQLExtendedFetch** por chamadas para **SQLSetStmtAttr** para definir o atributo de declaração SQL_ATTR_ARRAY_STATUS_PTR e para **SQLFetchScroll,** para que eles tenham um código comum que funcione com drivers ODBC *3.x* e ODBC *2.x.* Como **o SQLSetStmtAttr** com SQL_ATTR_ROW_ARRAY_SIZE será mapeado para **o SQLSetStmtAttr** com SQL_ROWSET_SIZE para drivers ODBC *2.x,* os aplicativos podem simplesmente definir SQL_ATTR_ROW_ARRAY_SIZE para suas operações de busca multirow.  
  
-   A maioria dos aplicativos que estão sendo atualizados não são realmente afetados por alterações nos códigos SQLSTATE. Para aqueles aplicativos que são afetados, eles podem fazer uma pesquisa mecânica e substituir na maioria dos casos usando a tabela de conversão de erros na seção "SQLSTATE Mapping" para converter códigos de erro ODBC *3.x* para códigos ODBC *2.x.* Uma vez que o ODBC *3.x* Driver Manager realizará o mapeamento de ODBC *2.x* SQLSTATEs para ODBC *3.x* SQLSTATEs, esses escritores de aplicativos só precisam verificar o ODBC *3.x* SQLSTATEs e não se preocupar em incluir ODBC *2.x* SQLSTATEs em código condicional.  
  
-   Se um aplicativo fizer grande uso dos tipos de dados de data, hora e carimbo de tempo, o aplicativo pode declarar-se um aplicativo ODBC *2.x* e usar seu código existente em vez de usar código de condicionamento.  
  
 A atualização também deve incluir as seguintes etapas:  
  
-   Ligue para **sqlsetenvAttr** antes de alocar uma conexão para definir o atributo do ambiente SQL_ATTR_ODBC_VERSION para SQL_OV_ODBC2.  
  
-   Substitua todas as chamadas para **SQLAllocEnv,** **SQLAllocConnect**ou **SQLAllocStmt** por chamadas para **SQLAllocHandle** com o argumento *handleType* apropriado de SQL_HANDLE_ENV, SQL_HANDLE_DBC ou SQL_HANDLE_STMT.  
  
-   Substitua todas as chamadas para **SQLFreeEnv** ou **SQLFreeConnect** por chamadas para **SQLFreeHandle** com o argumento *handleType* apropriado de SQL_HANDLE_DBC ou SQL_HANDLE_STMT.  
  
-   Substitua todas as chamadas para **SQLSetConnectOption** por chamadas para **SQLSetConnectAttr**. Se definir um atributo cujo valor é uma seqüência de string, defina o argumento *StringLength* apropriadamente. Alterar *argumento de atributo* de SQL_XXXX para SQL_ATTR_XXXX.  
  
-   Substitua todas as chamadas para **SQLGetConnectOption** por chamadas para **SQLGetConnectAttr**. Se obter um atributo de seqüência ou binário, defina *BufferLength* para o valor apropriado e passe em um argumento *StringLength.* Alterar *argumento de atributo* de SQL_XXXX para SQL_ATTR_XXXX.  
  
-   Substitua todas as chamadas para **SQLSetStmtOption** por chamadas para **SQLSetStmtAttr**. Se definir um atributo cujo valor é uma seqüência de string, defina o argumento *StringLength* apropriadamente. Alterar *argumento de atributo* de SQL_XXXX para SQL_ATTR_XXXX.  
  
-   Substitua todas as chamadas para **SQLGetStmtOption** por chamadas para **SQLGetStmtAttr**. Se obter um atributo de seqüência ou binário, defina *BufferLength* para o valor apropriado e passe em um argumento *StringLength.* Alterar *argumento de atributo* de SQL_XXXX para SQL_ATTR_XXXX.  
  
-   Substitua todas as chamadas para **SQLTransact** por chamadas para **SQLEndTran**. Se a alça mais válida na chamada **SQLTransact** for uma alça de ambiente, um argumento *HandleType* de SQL_HANDLE_ENV deve ser usado na chamada **SQLEndTran** com o argumento *Handle* apropriado. Se a alça mais válida na chamada **SQLTransact** for uma alça de conexão, um argumento *HandleType* de SQL_HANDLE_DBC deve ser usado na chamada **SQLEndTran** com o argumento *Handle* apropriado.  
  
-   Substitua todas as chamadas para **SQLColAttributes** por chamadas para **SQLColAttribute**. Se o argumento *FieldIdentifier* for SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE ou SQL_COLUMN_LENGTH, não altere nada além do nome da função. Caso assim, mude *o FieldIdentifier* de SQL_COLUMN_XXXX para SQL_DESC_XXXX. Se *o FieldIdentifier* estiver SQL_DESC_CONCISE_TYPE e o tipo de dados for um tipo de dados de data-hora, altere para o tipo de dados ODBC *3.x* correspondente.  
  
-   Se usar cursores de bloco, cursores roláveis ou ambos, o aplicativo faz o seguinte:  
  
    -   Define o tamanho do conjunto de linhas, o tipo de cursor e a concorrência do cursor usando **SQLSetStmtAttr**.  
  
    -   Chama **SQLSetStmtAttr** para definir SQL_ATTR_ROW_STATUS_PTR para apontar para uma matriz de registros de status.  
  
    -   Chama **SQLSetStmtAttr** para definir SQL_ATTR_ROWS_FETCHED_PTR apontar para um SQLINTEGER.  
  
    -   Executa as vinculações necessárias e executa a declaração SQL.  
  
    -   Chama **SQLFetchScroll** em um loop para buscar linhas e mover-se no conjunto de resultados.  
  
    -   Se ele quiser buscar por marcador, o aplicativo chama **SQLSetStmtAttr** para definir SQL_ATTR_FETCH_BOOKMARK_PTR para uma variável que conterá o marcador para a linha que ele deseja buscar, e chama **SQLFetchScroll** com um argumento *FetchOrientation* de SQL_FETCH_BOOKMARK.  
  
-   Se usar matrizes de parâmetros, o aplicativo faz o seguinte:  
  
    -   Chama **SQLSetStmtAttr** para definir o atributo SQL_ATTR_PARAMSET_SIZE ao tamanho da matriz de parâmetros.  
  
    -   Chama **SQLSetStmtAttr** para definir SQL_ATTR_ROWS_PROCESSED_PTR para apontar para uma variável UDWORD interna.  
  
    -   Realiza a preparação, vinculação e execução de operações conforme apropriado.  
  
    -   Se a execução parar por algum motivo (como SQL_NEED_DATA), ele pode encontrar a linha "atual" de parâmetros inspecionando o local apontado por SQL_ATTR_ROWS_PROCESSED_PTR.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Mapeando funções de substituição para compatibilidade com versões anteriores de aplicativos](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [Calling SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [Chamar SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [Chamar SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [Operações de biblioteca de cursor](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [Mapear os tipos de informações dos atributos1 de cursor](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)

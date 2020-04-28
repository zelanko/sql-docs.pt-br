---
title: Recuperando parâmetros de saída usando SQLGetData | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], retrieving output parameters
- output parameters [ODBC]
- retrieving output parameters [ODBC]
ms.assetid: 7a8c298a-2160-491d-a300-d36f45568d9c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c96a3f9fc81d081ce16fe8e75746aafe8962fd0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81294586"
---
# <a name="retrieving-output-parameters-using-sqlgetdata"></a>Recuperar parâmetros de saída usando SQLGetData
Antes do ODBC 3,8, um aplicativo poderia recuperar apenas os parâmetros de saída de uma consulta com um buffer de saída associado. No entanto, é difícil alocar um buffer muito grande quando o tamanho do valor do parâmetro é muito grande (por exemplo, uma imagem grande). O ODBC 3,8 apresenta uma nova maneira de recuperar parâmetros de saída em partes. Um aplicativo agora pode chamar **SQLGetData** com um pequeno buffer várias vezes para recuperar um valor de parâmetro grande. Isso é semelhante à recuperação de dados de coluna grandes.  
  
 Para associar um parâmetro de saída ou um parâmetro de entrada/saída a ser recuperado em partes, chame **SQLBindParameter** com o argumento *InputOutputType* definido como SQL_PARAM_OUTPUT_STREAM ou SQL_PARAM_INPUT_OUTPUT_STREAM. Com SQL_PARAM_INPUT_OUTPUT_STREAM, um aplicativo pode usar **SQLPutData** para inserir dados no parâmetro e, em seguida, usar **SQLGetData** para recuperar o parâmetro de saída. Os dados de entrada devem estar no formato DAE (dados em execução), usando **SQLPutData** em vez de associá-los a um buffer pré-alocado.  
  
 Esse recurso pode ser usado por aplicativos ODBC 3,8 ou aplicativos ODBC 3. x e ODBC 2. x recompilados, e esses aplicativos devem ter um driver ODBC 3,8 que dá suporte à recuperação de parâmetros de saída usando o **SQLGetData** e o Gerenciador de driver do ODBC 3,8. Para obter informações sobre como habilitar um aplicativo mais antigo para usar novos recursos ODBC, consulte [matriz de compatibilidade](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
## <a name="usage-example"></a>Exemplo de uso  
 Por exemplo, considere a execução de um procedimento armazenado, **{CALL sp_f (?,?)}**, onde ambos os parâmetros são associados como SQL_PARAM_OUTPUT_STREAM e o procedimento armazenado não retorna nenhum conjunto de resultados (posteriormente neste tópico, você encontrará um cenário mais complexo):  
  
1.  Para cada parâmetro, chame **SQLBindParameter** com *InputOutputType* definido como SQL_PARAM_OUTPUT_STREAM e *ParameterValuePtr* definido como um token, como um número de parâmetro, um ponteiro para dados ou um ponteiro para uma estrutura que o aplicativo usa para associar parâmetros de entrada. Este exemplo usará o ordinal do parâmetro como o token.  
  
2.  Execute a consulta com **SQLExecDirect** ou **SQLExecute**. SQL_PARAM_DATA_AVAILABLE será retornado, indicando que há parâmetros de saída em fluxo disponíveis para recuperação.  
  
3.  Chame **SQLParamData** para obter o parâmetro que está disponível para recuperação. **SQLParamData** retornará SQL_PARAM_DATA_AVAILABLE com o token do primeiro parâmetro disponível, que é definido em **SQLBindParameter** (etapa 1). O token é retornado no buffer para o qual o *ValuePtrPtr* aponta.  
  
4.  Chame **SQLGetData** com o argumento *Col*_or\_*Param_Num* definido como o ordinal do parâmetro para recuperar os dados do primeiro parâmetro disponível. Se **SQLGetData** retornar SQL_SUCCESS_WITH_INFO e SQLSTATE 01004 (dados truncados) e o tipo for de comprimento variável no cliente e no servidor, haverá mais dados a serem recuperados do primeiro parâmetro disponível. Você pode continuar a chamar **SQLGetData** até que ele retorne SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO com um **SQLSTATE**diferente.  
  
5.  Repita a etapa 3 e a etapa 4 para recuperar o parâmetro atual.  
  
6.  Chame **SQLParamData** novamente. Se ele retornar qualquer coisa, exceto SQL_PARAM_DATA_AVAILABLE, não haverá mais dados de parâmetro transmitidos a serem recuperados e o código de retorno será o código de retorno da próxima instrução executada.  
  
7.  Chame **SQLMoreResults** para processar o próximo conjunto de parâmetros até que ele retorne SQL_NO_DATA. **SQLMoreResults** retornará SQL_NO_DATA neste exemplo se o atributo de instrução SQL_ATTR_PARAMSET_SIZE foi definido como 1. Caso contrário, **SQLMoreResults** retornará SQL_PARAM_DATA_AVAILABLE para indicar que há parâmetros de saída em fluxo disponíveis para o próximo conjunto de parâmetros a serem recuperados.  
  
 Semelhante a um parâmetro de entrada do DAE, o token usado no argumento *ParameterValuePtr* em **SQLBindParameter** (etapa 1) pode ser um ponteiro que aponta para uma estrutura de dados de aplicativo, que contém o ordinal do parâmetro e mais informações específicas do aplicativo, se necessário.  
  
 A ordem dos parâmetros de saída de fluxo retornados ou de entrada/saída é específica do driver e nem sempre é a mesma que a ordem especificada na consulta.  
  
 Se o aplicativo não chamar **SQLGetData** na etapa 4, o valor do parâmetro será Descartado. Da mesma forma, se o aplicativo chamar **SQLParamData** antes que todo o valor de um parâmetro tenha sido lido por **SQLGetData**, o restante do valor será descartado e o aplicativo poderá processar o próximo parâmetro.  
  
 Se o aplicativo chamar **SQLMoreResults** antes que todos os parâmetros de saída transmitidos sejam processados (o**SQLParamData** ainda retorna SQL_PARAM_DATA_AVAILABLE), todos os parâmetros restantes serão descartados. Da mesma forma, se o aplicativo chamar **SQLMoreResults** antes que todo o valor de um parâmetro tenha sido lido por **SQLGetData**, o restante do valor e todos os parâmetros restantes serão descartados e o aplicativo poderá continuar processando o próximo conjunto de parâmetros.  
  
 Observe que um aplicativo pode especificar o tipo de dados C em **SQLBindParameter** e **SQLGetData**. O tipo de dados C especificado com **SQLGetData** substitui o tipo de dados c especificado em **SQLBindParameter**, a menos que o tipo de dados c especificado em **SQLGetData** seja SQL_APD_TYPE.  
  
 Embora um parâmetro de saída em fluxo seja mais útil quando o tipo de dados do parâmetro de saída for do tipo BLOB, essa funcionalidade também poderá ser usada com qualquer tipo de dados. Os tipos de dados com suporte pelos parâmetros de saída em fluxo são especificados no driver.  
  
 Se houver SQL_PARAM_INPUT_OUTPUT_STREAM parâmetros a serem processados, **SQLExecute** ou **SQLExecDirect** retornará SQL_NEED_DATA primeiro. Um aplicativo pode chamar **SQLParamData** e **SQLPutData** para enviar dados de parâmetro do DAE. Quando todos os parâmetros de entrada do DAE são processados, **SQLParamData** retorna SQL_PARAM_DATA_AVAILABLE para indicar que os parâmetros de saída transmitidos estão disponíveis.  
  
 Quando há parâmetros de saída em fluxo e parâmetros de saída associados a serem processados, o driver determina a ordem de processamento de parâmetros de saída. Portanto, se um parâmetro de saída estiver associado a um buffer (o parâmetro **SQLBindParameter** *InputOutputType* estiver definido como SQL_PARAM_INPUT_OUTPUT ou SQL_PARAM_OUTPUT), o buffer poderá não ser preenchido até que **SQLParamData** retorne SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO. Um aplicativo deve ler um buffer associado somente depois que **SQLParamData** retornar SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO depois que todos os parâmetros de saída transmitidos forem processados.  
  
 A fonte de dados pode retornar um aviso e um conjunto de resultados, além do parâmetro de saída transmitido. Em geral, os avisos e os conjuntos de resultados são processados separadamente de um parâmetro de saída transmitido chamando **SQLMoreResults**. Processar avisos e o conjunto de resultados antes de processar o parâmetro de saída transmitido.  
  
 A tabela a seguir descreve diferentes cenários de um único comando enviado para o servidor e como o aplicativo deve funcionar.  
  
|Cenário|Valor de retorno de SQLExecute ou SQLExecDirect|O que fazer em seguida|  
|--------------|---------------------------------------------------|---------------------|  
|Os dados incluem apenas parâmetros de saída em fluxo|SQL_PARAM_DATA_AVAILABLE|Use **SQLParamData** e **SQLGetData** para recuperar parâmetros de saída transmitidos.|  
|Os dados incluem um conjunto de resultados e parâmetros de saída em fluxo|SQL_SUCCESS|Recupere o conjunto de resultados com **SQLBindCol** e **SQLGetData**.<br /><br /> Chame **SQLMoreResults** para iniciar o processamento de parâmetros de saída transmitidos. Ele deve retornar SQL_PARAM_DATA_AVAILABLE.<br /><br /> Use **SQLParamData** e **SQLGetData** para recuperar parâmetros de saída transmitidos.|  
|Os dados incluem uma mensagem de aviso e parâmetros de saída transmitidos|SQL_SUCCESS_WITH_INFO|Use **SQLGetDiagRec** e **SQLGetDiagField** para processar mensagens de aviso.<br /><br /> Chame **SQLMoreResults** para iniciar o processamento de parâmetros de saída transmitidos. Ele deve retornar SQL_PARAM_DATA_AVAILABLE.<br /><br /> Use **SQLParamData** e **SQLGetData** para recuperar parâmetros de saída transmitidos.|  
|Os dados incluem uma mensagem de aviso, um conjunto de resultados e parâmetros de saída em fluxo|SQL_SUCCESS_WITH_INFO|Use **SQLGetDiagRec** e **SQLGetDiagField** para processar mensagens de aviso. Em seguida, chame **SQLMoreResults** para iniciar o processamento do conjunto de resultados.<br /><br /> Recupere um conjunto de resultados com **SQLBindCol** e **SQLGetData**.<br /><br /> Chame **SQLMoreResults** para iniciar o processamento de parâmetros de saída transmitidos. **SQLMoreResults** deve retornar SQL_PARAM_DATA_AVAILABLE.<br /><br /> Use **SQLParamData** e **SQLGetData** para recuperar parâmetros de saída transmitidos.|  
|Consulta com parâmetros de entrada do DAE, por exemplo, um parâmetro de entrada/saída (DAE) em fluxo|NEED_DATA DO SQL|Chame **SQLParamData** e **SQLPutData** para enviar dados de parâmetro de entrada do DAE.<br /><br /> Depois que todos os parâmetros de entrada do DAE são processados, **SQLParamData** pode retornar qualquer código de retorno que **SQLExecute** e **SQLExecDirect** possa retornar. Os casos nesta tabela podem ser aplicados.<br /><br /> Se o código de retorno for SQL_PARAM_DATA_AVAILABLE, os parâmetros de saída em fluxo estarão disponíveis. Um aplicativo deve chamar **SQLParamData** novamente para recuperar o token para o parâmetro de saída transmitido, conforme descrito na primeira linha desta tabela.<br /><br /> Se o código de retorno for SQL_SUCCESS, haverá um conjunto de resultados a ser processado ou o processamento será concluído.<br /><br /> Se o código de retorno for SQL_SUCCESS_WITH_INFO, haverá mensagens de aviso a serem processadas.|  
  
 Após **SQLExecute**, **SQLExecDirect**ou **SQLMoreResults** retornar SQL_PARAM_DATA_AVAILABLE, um erro de sequência de função ocorrerá se um aplicativo chamar uma função que não está na seguinte lista:  
  
-   **SQLAllocHandle** / **SQLAllocHandleStd**  
  
-   **SQLDataSources** / **SQLDrivers**  
  
-   **SQLGetInfo** / **SQLGetFunctions**  
  
-   **SQLGetConnectAttr** / **SQLGetEnvAttr**SQLGetEnvAttr / **SQLGetDescField**SQLGetDescField / **SQLGetDescRec**  
  
-   **SQLNumParams**  
  
-   **SQLDescribeParam**  
  
-   **SQLNativeSql**  
  
-   **SQLParamData**  
  
-   **SQLMoreResults**  
  
-   **SQLGetDiagField** / **SQLGetDiagRec**  
  
-   **SQLCancel**  
  
-   **SQLCancelHandle** (com identificador de instrução)  
  
-   **SQLFreeStmt** (com Option = SQL_CLOSE, SQL_DROP ou SQL_UNBIND)  
  
-   **SQLCloseCursor**  
  
-   **SQLDisconnect**  
  
-   **SQLFreeHandle** (com HandleType = SQL_HANDLE_STMT)  
  
-   **SQLGetStmtAttr**  
  
 Os aplicativos ainda podem usar **SQLSetDescField** ou **SQLSetDescRec** para definir as informações de associação. O mapeamento de campo não será alterado. No entanto, os campos dentro do descritor podem retornar novos valores. Por exemplo, SQL_DESC_PARAMETER_TYPE pode retornar SQL_PARAM_INPUT_OUTPUT_STREAM ou SQL_PARAM_OUTPUT_STREAM.  
  
## <a name="usage-scenario-retrieve-an-image-in-parts-from-a-result-set"></a>Cenário de uso: recuperar uma imagem em partes de um conjunto de resultados  
 **SQLGetData** pode ser usado para obter dados em partes quando um procedimento armazenado retorna um conjunto de resultados que contém uma linha de metadados sobre uma imagem e a imagem é retornada em um parâmetro de saída grande.  
  
```  
// CREATE PROCEDURE SP_TestOutputPara  
//      @ID_of_picture   as int,  
//      @Picture         as varbinary(max) out  
// AS  
//     output the image data through streamed output parameter  
// GO  
BOOL displayPicture(SQLUINTEGER idOfPicture, SQLHSTMT hstmt) {  
   SQLLEN      lengthOfPicture;    // The actual length of the picture.  
   BYTE        smallBuffer[100];   // A very small buffer.  
   SQLRETURN   retcode, retcode2;  
  
   // Bind the first parameter (input parameter)  
   SQLBindParameter(  
         hstmt,  
         1,                         // The first parameter.   
         SQL_PARAM_INPUT,           // Input parameter: The ID_of_picture.  
         SQL_C_ULONG,               // The C Data Type.  
         SQL_INTEGER,               // The SQL Data Type.  
         0,                         // ColumnSize is ignored for integer.  
         0,                         // DecimalDigits is ignored for integer.  
         &idOfPicture,              // The Address of the buffer for the input parameter.  
         0,                         // BufferLength is ignored for integer.  
         NULL);                     // This is ignored for integer.  
  
   // Bind the streamed output parameter.  
   SQLBindParameter(  
         hstmt,   
         2,                         // The second parameter.  
         SQL_PARAM_OUTPUT_STREAM,   // A streamed output parameter.   
         SQL_C_BINARY,              // The C Data Type.    
         SQL_VARBINARY,             // The SQL Data Type.  
         0,                         // ColumnSize: The maximum size of varbinary(max).  
         0,                         // DecimalDigits is ignored for binary type.  
         (SQLPOINTER)2,             // ParameterValuePtr: An application-defined  
                                    // token (this will be returned from SQLParamData).  
                                    // In this example, we used the ordinal   
                                    // of the parameter.  
         0,                         // BufferLength is ignored for streamed output parameters.  
         &lengthOfPicture);         // StrLen_or_IndPtr: The status variable returned.   
  
   retcode = SQLPrepare(hstmt, L"{call SP_TestOutputPara(?, ?)}", SQL_NTS);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   retcode = SQLExecute(hstmt);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   // Assume that the retrieved picture exists.  Use SQLBindCol or SQLGetData to retrieve the result-set.  
  
   // Process the result set and move to the streamed output parameters.  
   retcode = SQLMoreResults( hstmt );  
  
   // SQLGetData retrieves and displays the picture in parts.  
   // The streamed output parameter is available.  
   while (retcode == SQL_PARAM_DATA_AVAILABLE) {  
      SQLPOINTER token;   // Output by SQLParamData.  
      SQLLEN cbLeft;      // #bytes remained  
      retcode = SQLParamData(hstmt, &token);   // returned token is 2 (according to the binding)  
      if ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
         // A do-while loop retrieves the picture in parts.  
         do {  
            retcode2 = SQLGetData(   
               hstmt,   
               (UWORD) token,          // the value of the token is the ordinal.   
               SQL_C_BINARY,           // The C-type.  
               smallBuffer,            // A small buffer.   
               sizeof(smallBuffer),    // The size of the buffer.  
               &cbLeft);               // How much data we can get.  
         }  
         while ( retcode2 == SQL_SUCCESS_WITH_INFO );  
      }  
   }  
  
   return TRUE;  
}  
```  
  
## <a name="usage-scenario-send-and-receive-a-large-object-as-a-streamed-inputoutput-parameter"></a>Cenário de uso: enviar e receber um objeto grande como um parâmetro de entrada/saída em fluxo  
 **SQLGetData** pode ser usado para obter e enviar dados em partes quando um procedimento armazenado passa um objeto grande como um parâmetro de entrada/saída, transmitindo o valor de e para o banco de dados. Você não precisa armazenar todos os dados na memória.  
  
```  
// CREATE PROCEDURE SP_TestInOut  
//       @picture as varbinary(max) out  
// AS  
//    output the image data through output parameter   
// go  
  
BOOL displaySimilarPicture(BYTE* image, ULONG lengthOfImage, SQLHSTMT hstmt) {  
   BYTE smallBuffer[100];   // A very small buffer.  
   SQLRETURN retcode, retcode2;  
   SQLLEN statusOfPicture;  
  
   // First bind the parameters, before preparing the statement that binds the output streamed parameter.  
   SQLBindParameter(  
      hstmt,   
      1,                                 // The first parameter.  
      SQL_PARAM_INPUT_OUTPUT_STREAM,     // I/O-streamed parameter: The Picture.  
      SQL_C_BINARY,                      // The C Data Type.  
      SQL_VARBINARY,                     // The SQL Data Type.  
      0,                                 // ColumnSize: The maximum size of varbinary(max).  
      0,                                 // DecimalDigits is ignored.   
      (SQLPOINTER)1,                     // An application defined token.   
      0,                                 // BufferLength is ignored for streamed I/O parameters.  
      &statusOfPicture);                 // The status variable.  
  
   statusOfPicture = SQL_DATA_AT_EXEC;   // Input data in parts (DAE parameter at input).  
  
   retcode = SQLPrepare(hstmt, L"{call SP_TestInOut(?) }", SQL_NTS);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   // Execute the statement.  
   retcode = SQLExecute(hstmt);  
   if ( retcode == SQL_ERROR )  
      return FALSE;  
  
   if ( retcode == SQL_NEED_DATA ) {  
      // Use SQLParamData to loop through DAE input parameters.  For  
      // each, use SQLPutData to send the data to database in parts.  
  
      // This example uses an I/O parameter with streamed output.  
      // Therefore, the last call to SQLParamData should return  
      // SQL_PARAM_DATA_AVAILABLE to indicate the end of the input phrase   
      // and report that a streamed output parameter is available.  
  
      // Assume retcode is set to the return value of the last call to  
      // SQLParamData, which is equal to SQL_PARAM_DATA_AVAILABLE.  
   }  
  
   // Start processing the streamed output parameters.  
   while ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
      SQLPOINTER token;   // Output by SQLParamData.  
      SQLLEN cbLeft;     // #bytes remained  
      retcode = SQLParamData(hstmt, &token);  
      if ( retcode == SQL_PARAM_DATA_AVAILABLE ) {  
         do {  
            retcode2 = SQLGetData(   
               hstmt,   
               (UWORD) token,          // the value of the token is the ordinal.   
               SQL_C_BINARY,           // The C-type.  
               smallBuffer,            // A small buffer.   
               sizeof(smallBuffer),    // The size of the buffer.  
               &cbLeft);               // How much data we can get.  
         }  
         while ( retcode2 == SQL_SUCCESS_WITH_INFO );  
      }  
   }   
  
   return TRUE;  
}  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md)

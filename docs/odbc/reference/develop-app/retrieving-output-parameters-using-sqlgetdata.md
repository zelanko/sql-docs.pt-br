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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ebb09b3118c2d16041d4ca60bf738d0fda561346
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199086"
---
# <a name="retrieving-output-parameters-using-sqlgetdata"></a>Recuperar parâmetros de saída usando SQLGetData
Antes do ODBC 3.8, um aplicativo só foi possível recuperar os parâmetros de saída de uma consulta com um buffer de saída associadas. No entanto, é difícil alocar um buffer muito grande, quando o tamanho do valor do parâmetro é muito grande (por exemplo, uma imagem grande). O ODBC 3.8 introduz uma nova maneira de recuperar parâmetros de saída em partes. Um aplicativo pode chamar **SQLGetData** várias vezes com um buffer pequeno para recuperar um valor de parâmetro grande. Isso é semelhante à recuperação de dados de coluna grande.  
  
 Para associar um parâmetro de saída ou parâmetro de entrada/saída a serem recuperados em partes, chame **SQLBindParameter** com o *InputOutputType* argumento definido como SQL_PARAM_OUTPUT_STREAM ou SQL_PARAM_INPUT_OUTPUT _STREAM. Com SQL_PARAM_INPUT_OUTPUT_STREAM, um aplicativo pode usar **SQLPutData** inserir dados no parâmetro e, em seguida, usar **SQLGetData** para recuperar o parâmetro de saída. Os dados de entrada devem estar na dados em execução (DAE) formam, usando **SQLPutData** em vez de associá-la para um buffer pré-alocadas.  
  
 Esse recurso pode ser usado por aplicativos ODBC 3.8 ou recompilado ODBC 3. x e os aplicativos ODBC 2. x e esses aplicativos devem ter um driver de ODBC 3.8 que dá suporte à recuperação de parâmetros de saída usando **SQLGetData** e o Driver ODBC 3.8 Gerenciador. Para obter informações sobre como habilitar um aplicativo mais antigo usar os novos recursos ODBC, consulte [matriz de compatibilidade](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
## <a name="usage-example"></a>Exemplo de uso  
 Por exemplo, considere a execução de um procedimento armazenado **{chamada sp_f(?,?)}** , em que ambos os parâmetros são associados como SQL_PARAM_OUTPUT_STREAM e o procedimento armazenado não retorna nenhum conjunto de resultados (neste tópico você encontrará um cenário mais complexo):  
  
1.  Para cada parâmetro, chame **SQLBindParameter** com *InputOutputType* definido como SQL_PARAM_OUTPUT_STREAM e *ParameterValuePtr* definido como um token, como um número de parâmetro , um ponteiro para dados ou um ponteiro para uma estrutura que o aplicativo usa para associar parâmetros de entrada. Este exemplo usará o ordinal do parâmetro como o token.  
  
2.  Execute a consulta com **SQLExecDirect** ou **SQLExecute**. SQL_PARAM_DATA_AVAILABLE será retornado, indicando que os parâmetros de saída transmitidos estão disponíveis para recuperação.  
  
3.  Chame **SQLParamData** para obter o parâmetro que está disponível para recuperação. **SQLParamData** retornará SQL_PARAM_DATA_AVAILABLE com o token do primeiro parâmetro disponível, que é definido no **SQLBindParameter** (etapa 1). O token é retornado no buffer que o *ValuePtrPtr* aponta.  
  
4.  Chame **SQLGetData** com o argumento *Col*_or\_*Param_Num* definido como o parâmetro ordinal para recuperar os dados do primeiro parâmetro disponível. Se **SQLGetData** retorna SQL_SUCCESS_WITH_INFO e SQLState 01004 (dados truncados) e o tipo é de tamanho variável no cliente e servidor, não há mais dados a serem recuperados do primeiro parâmetro disponível. Você pode continuar a chamar **SQLGetData** até que ele retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO com outro **SQLState**.  
  
5.  Repita as etapas 3 e 4 para recuperar o parâmetro atual.  
  
6.  Chame **SQLParamData** novamente. Se ele retornar qualquer coisa, exceto SQL_PARAM_DATA_AVAILABLE, há não mais em fluxo de dados de parâmetro para recuperar e o código de retorno será o código de retorno da próxima instrução que é executado.  
  
7.  Chame **SQLMoreResults** para processar o próximo conjunto de parâmetros até ele retornar SQL_NO_DATA. **SQLMoreResults** irá retornar SQL_NO_DATA neste exemplo, se o atributo da instrução SQL_ATTR_PARAMSET_SIZE foi definido como 1. Caso contrário, **SQLMoreResults** retornará SQL_PARAM_DATA_AVAILABLE para indicar que os parâmetros de saída transmitidos estão disponíveis para o próximo conjunto de parâmetros para recuperar.  
  
 Semelhante a um parâmetro de entrada DAE, o token usado no argumento *ParameterValuePtr* na **SQLBindParameter** (etapa 1) pode ser um ponteiro que aponta para uma estrutura de dados do aplicativo, que contém o ordinal do parâmetro e obter mais informações específicas do aplicativo, se necessário.  
  
 A ordem dos parâmetros de entrada/saída ou em fluxo de saída retornada é específico do driver e pode não sempre ser o mesmo que a ordem especificada na consulta.  
  
 Se o aplicativo não chama **SQLGetData** na etapa 4, o valor do parâmetro é descartado. Da mesma forma, se o aplicativo chamar **SQLParamData** antes que todos de um parâmetro de valor foi lido pela **SQLGetData**, o restante do valor será descartado e o aplicativo pode processar o próximo parâmetro.  
  
 Se o aplicativo chamar **SQLMoreResults** antes da saída em fluxo todos os parâmetros são processados (**SQLParamData** ainda retornará SQL_PARAM_DATA_AVAILABLE), todos os parâmetros restantes são descartados. Da mesma forma, se o aplicativo chamar **SQLMoreResults** antes que todos de um parâmetro de valor foi lido pela **SQLGetData**, o restante do valor e todos os parâmetros restantes é descartado e o aplicativo pode continuar a processar o próximo conjunto de parâmetros.  
  
 Observe que um aplicativo pode especificar o tipo de dados C em ambos **SQLBindParameter** e **SQLGetData**. O tipo de dados C especificado com **SQLGetData** substitui o tipo de dados C especificado em **SQLBindParameter**, a menos que o tipo de dados C especificado na **SQLGetData** é SQL_APD_TYPE.  
  
 Embora um parâmetro de saída transmitidos é mais útil quando o tipo de dados do parâmetro de saída é do tipo de BLOB, essa funcionalidade também pode ser usada com qualquer tipo de dados. Os tipos de dados com suporte pelos parâmetros de saída transmitidos são especificados no driver.  
  
 Se houver parâmetros SQL_PARAM_INPUT_OUTPUT_STREAM a ser processado **SQLExecute** ou **SQLExecDirect** retornará SQL_NEED_DATA pela primeira vez. Um aplicativo pode chamar **SQLParamData** e **SQLPutData** para enviar dados de parâmetro DAE. Quando todos os parâmetros de entrada DAE são processados, **SQLParamData** retorna SQL_PARAM_DATA_AVAILABLE para indicar os parâmetros de saída transmitidos estão disponíveis.  
  
 Quando há são transmitidos a parâmetros de saída e parâmetros de saída associada a ser processado, o driver determina a ordem de processamento de parâmetros de saída. Portanto, se um parâmetro de saída está associado a um buffer (o **SQLBindParameter** parâmetro *InputOutputType* está definido como SQL_PARAM_INPUT_OUTPUT ou SQL_PARAM_OUTPUT), o buffer não pode ser preenchido até  **SQLParamData** retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO. Um aplicativo deve ler um limite de buffer somente após **SQLParamData** retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO transmitidos depois que todos os parâmetros de saída são processadas.  
  
 A fonte de dados pode retornar que um aviso de conjunto de resultados e, além para o parâmetro de saída em fluxo. Em geral, avisos e conjuntos de resultados são processados separadamente de um parâmetro de saída transmitidos chamando **SQLMoreResults**. Avisos de processo e conjunto de resultados antes do parâmetro de saída em fluxo de processamento.  
  
 A tabela a seguir descreve os diferentes cenários de um único comando enviado para o servidor e como o aplicativo deve funcionar.  
  
|Cenário|Valor de retorno de SQLExecute ou SQLExecDirect|O que fazer em seguida|  
|--------------|---------------------------------------------------|---------------------|  
|Os dados incluem somente parâmetros de saída em fluxo|SQL_PARAM_DATA_AVAILABLE|Use **SQLParamData** e **SQLGetData** para recuperar parâmetros de saída em fluxo.|  
|Os dados incluem um conjunto de resultados e transmitidos parâmetros de saída|SQL_SUCCESS|Recuperar o conjunto de resultados com **SQLBindCol** e **SQLGetData**.<br /><br /> Chame **SQLMoreResults** para iniciar o processamento de parâmetros de saída em fluxo. Ele deverá retornar SQL_PARAM_DATA_AVAILABLE.<br /><br /> Use **SQLParamData** e **SQLGetData** para recuperar parâmetros de saída em fluxo.|  
|Os dados incluem uma mensagem de aviso e transmitidos a parâmetros de saída|SQL_SUCCESS_WITH_INFO|Use **SQLGetDiagRec** e **SQLGetDiagField** para processar as mensagens de aviso.<br /><br /> Chame **SQLMoreResults** para iniciar o processamento de parâmetros de saída em fluxo. Ele deverá retornar SQL_PARAM_DATA_AVAILABLE.<br /><br /> Use **SQLParamData** e **SQLGetData** para recuperar parâmetros de saída em fluxo.|  
|Os dados incluem uma mensagem de aviso, o conjunto de resultados e transmitidos a parâmetros de saída|SQL_SUCCESS_WITH_INFO|Use **SQLGetDiagRec** e **SQLGetDiagField** para processar as mensagens de aviso. Em seguida, chame **SQLMoreResults** para iniciar o processamento do resultado do conjunto.<br /><br /> Recuperar um conjunto de resultados com **SQLBindCol** e **SQLGetData**.<br /><br /> Chame **SQLMoreResults** para iniciar o processamento de parâmetros de saída em fluxo. **SQLMoreResults** deve retornar SQL_PARAM_DATA_AVAILABLE.<br /><br /> Use **SQLParamData** e **SQLGetData** para recuperar parâmetros de saída em fluxo.|  
|Parâmetro de consulta com parâmetros de entrada DAE, por exemplo, um em fluxo de entrada/saída (DAE)|SQL NEED_DATA|Chame **SQLParamData** e **SQLPutData** DAE de enviar dados de parâmetro de entrada.<br /><br /> Após o processamento, todos os parâmetros de entrada DAE **SQLParamData** pode retornar qualquer código de retorno que **SQLExecute** e **SQLExecDirect** pode retornar. Os casos nesta tabela, em seguida, podem ser aplicados.<br /><br /> Se o código de retorno for SQL_PARAM_DATA_AVAILABLE, parâmetros de saída transmitidos estão disponíveis. Um aplicativo deve chamar **SQLParamData** novamente para recuperar o token para o parâmetro de saída em fluxo, conforme descrito na primeira linha desta tabela.<br /><br /> Se o código de retorno seja SQL_SUCCESS, há um conjunto de resultados para processar ou o processamento é concluído.<br /><br /> Se o código de retorno for SQL_SUCCESS_WITH_INFO, há mensagens de aviso para processar.|  
  
 Após **SQLExecute**, **SQLExecDirect**, ou **SQLMoreResults** retorna SQL_PARAM_DATA_AVAILABLE, um erro de sequência de função ocorrerá se um aplicativo chama um função que não está na lista a seguir:  
  
-   **SQLAllocHandle** / **SQLAllocHandleStd**  
  
-   **SQLDataSources** / **SQLDrivers**  
  
-   **SQLGetInfo** / **SQLGetFunctions**  
  
-   **SQLGetConnectAttr** / **SQLGetEnvAttr** / **SQLGetDescField** / **SQLGetDescRec**  
  
-   **SQLNumParams**  
  
-   **SQLDescribeParam**  
  
-   **SQLNativeSql**  
  
-   **SQLParamData**  
  
-   **SQLMoreResults**  
  
-   **SQLGetDiagField** / **SQLGetDiagRec**  
  
-   **SQLCancel**  
  
-   **SQLCancelHandle** (com o identificador de instrução)  
  
-   **SQLFreeStmt** (com a opção = SQL_CLOSE, SQL_DROP ou SQL_UNBIND)  
  
-   **SQLCloseCursor**  
  
-   **SQLDisconnect**  
  
-   **SQLFreeHandle** (with HandleType = SQL_HANDLE_STMT)  
  
-   **SQLGetStmtAttr**  
  
 Os aplicativos ainda podem usar **SQLSetDescField** ou **SQLSetDescRec** para definir as informações de associação. Mapeamento de campo não será alterado. No entanto, os campos de descritor de podem retornar novos valores. Por exemplo, SQL_DESC_PARAMETER_TYPE pode retornar SQL_PARAM_INPUT_OUTPUT_STREAM ou SQL_PARAM_OUTPUT_STREAM.  
  
## <a name="usage-scenario-retrieve-an-image-in-parts-from-a-result-set"></a>Cenário de uso: Recuperar uma imagem em partes de um conjunto de resultados  
 **SQLGetData** pode ser usado para obter os dados em partes quando um procedimento armazenado retorna um conjunto de resultados que contém uma linha de metadados sobre uma imagem e a imagem é retornada em um parâmetro de saída grande.  
  
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
  
## <a name="usage-scenario-send-and-receive-a-large-object-as-a-streamed-inputoutput-parameter"></a>Cenário de uso: Enviar e receber um objeto grande como um parâmetro de entrada/saída em fluxo  
 **SQLGetData** pode ser usado para obter e enviar dados em partes quando um procedimento armazenado passa um objeto grande como um parâmetro de entrada/saída, o valor de e para o banco de dados de streaming. Não é necessário que armazenar todos os dados na memória.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md)

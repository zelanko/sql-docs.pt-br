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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294586"
---
# <a name="retrieving-output-parameters-using-sqlgetdata"></a>Recuperar parâmetros de saída usando SQLGetData
Antes do ODBC 3.8, um aplicativo só conseguia recuperar os parâmetros de saída de uma consulta com um buffer de saída vinculado. No entanto, é difícil alocar um buffer muito grande quando o tamanho do valor do parâmetro é muito grande (por exemplo, uma imagem grande). O ODBC 3.8 introduz uma nova maneira de recuperar parâmetros de saída em peças. Um aplicativo agora pode chamar **SQLGetData** com um pequeno buffer várias vezes para recuperar um grande valor de parâmetro. Isso é semelhante à recuperação de dados de colunas grandes.  
  
 Para vincular um parâmetro de saída ou parâmetro de entrada/saída a ser recuperado em partes, ligue para **SQLBindParameter** com o argumento *InputOutputType* definido para SQL_PARAM_OUTPUT_STREAM ou SQL_PARAM_INPUT_OUTPUT_STREAM. Com SQL_PARAM_INPUT_OUTPUT_STREAM, um aplicativo pode usar **SQLPutData** para inserir dados no parâmetro e, em seguida, usar **SQLGetData** para recuperar o parâmetro de saída. Os dados de entrada devem estar no formulário DAE (data-at-execution, execução de dados em execução), usando **SQLPutData** em vez de vinculá-los a um buffer pré-alocado.  
  
 Esse recurso pode ser usado por aplicativos ODBC 3.8 ou aplicativos ODBC 3.x e ODBC 2.x recompilados, e esses aplicativos devem ter um driver ODBC 3.8 que suporta recuperar parâmetros de saída usando **SQLGetData** e ODBC 3.8 Driver Manager. Para obter informações sobre como habilitar um aplicativo mais antigo para usar novos recursos ODBC, consulte [Matrix de compatibilidade](../../../odbc/reference/develop-app/compatibility-matrix.md).  
  
## <a name="usage-example"></a>Exemplo de uso  
 Por exemplo, considere a execução de um procedimento armazenado, **{CALL sp_f(?,?)}**, onde ambos os parâmetros estão vinculados como SQL_PARAM_OUTPUT_STREAM, e o procedimento armazenado não retorna nenhum conjunto de resultados (mais tarde neste tópico você encontrará um cenário mais complexo):  
  
1.  Para cada parâmetro, ligue para **SQLBindParameter** com *InputOutputType* definido como SQL_PARAM_OUTPUT_STREAM e *ParameterValuePtr* definido como um token, como um número de parâmetro, um ponteiro para dados ou um ponteiro para uma estrutura que o aplicativo usa para vincular parâmetros de entrada. Este exemplo usará o parâmetro ordinal como token.  
  
2.  Execute a consulta com **SQLExecDirect** ou **SQLExecute**. SQL_PARAM_DATA_AVAILABLE serão devolvidos, indicando que existem parâmetros de saída streamed disponíveis para recuperação.  
  
3.  Ligue para **o SQLParamData** para obter o parâmetro disponível para recuperação. **O SQLParamData** retornará SQL_PARAM_DATA_AVAILABLE com o token do primeiro parâmetro disponível, que está definido no **SQLBindParameter** (etapa 1). O token é devolvido no buffer que o *ValuePtrPtr* aponta.  
  
4.  Ligue para **o SQLGetData** com o argumento *de que*o Coronel _or\_*Param_Num* definido no parâmetro ordinal para recuperar os dados do primeiro parâmetro disponível. Se **o SQLGetData** retornar SQL_SUCCESS_WITH_INFO e o SQLState 01004 (dados truncados), e o tipo for comprimento variável no cliente e no servidor, haverá mais dados a serem recuperados do primeiro parâmetro disponível. Você pode continuar a ligar para **o SQLGetData** até que ele retorne SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO com um **SQLState**diferente .  
  
5.  Repita o passo 3 e o passo 4 para recuperar o parâmetro atual.  
  
6.  Ligue para **o SQLParamData** novamente. Se ele retornar qualquer coisa, exceto SQL_PARAM_DATA_AVAILABLE, não há mais dados de parâmetros transmitidos para recuperar, e o código de retorno será o código de retorno da próxima declaração que é executada.  
  
7.  Ligue para **o SQLMoreResults** para processar o próximo conjunto de parâmetros até que ele retorne SQL_NO_DATA. **O SQLMoreResults** retornará SQL_NO_DATA neste exemplo se o atributo de declaração SQL_ATTR_PARAMSET_SIZE foi definido como 1. Caso contrário, **o SQLMoreResults** retornará SQL_PARAM_DATA_AVAILABLE para indicar que existem parâmetros de saída em fluxo disponíveis para o próximo conjunto de parâmetros a serem recuperados.  
  
 Semelhante a um parâmetro de entrada da DAE, o token usado no argumento *ParameterValuePtr* no **SQLBindParameter** (etapa 1) pode ser um ponteiro que aponta para uma estrutura de dados do aplicativo, que contém a ordinal do parâmetro e informações mais específicas do aplicativo, se necessário.  
  
 A ordem dos parâmetros de saída ou entrada/saída retornados é específica do driver e pode nem sempre ser a mesma da ordem especificada na consulta.  
  
 Se o aplicativo não chamar **SQLGetData** na etapa 4, o valor do parâmetro será descartado. Da mesma forma, se o aplicativo chamar **SQLParamData** antes de todo o valor de um parâmetro ter sido lido pelo **SQLGetData,** o restante do valor é descartado e o aplicativo pode processar o próximo parâmetro.  
  
 Se o aplicativo chamar **SQLMoreResults** antes de todos os parâmetros de saída em fluxo serem processados (**SQLParamData** ainda retorna SQL_PARAM_DATA_AVAILABLE), todos os parâmetros restantes serão descartados. Da mesma forma, se o aplicativo chamar **SQLMoreResults** antes de todo o valor de parâmetro ter sido lido pelo **SQLGetData,** o restante do valor e todos os parâmetros restantes forem descartados, e o aplicativo pode continuar a processar o próximo parâmetro definido.  
  
 Observe que um aplicativo pode especificar o tipo de dados C tanto no **SQLBindParameter** quanto **no SQLGetData**. O tipo de dados C especificado com **o SQLGetData** substitui o tipo de dados C especificado no **SQLBindParameter,** a menos que o tipo de dados C especificado no **SQLGetData** seja SQL_APD_TYPE.  
  
 Embora um parâmetro de saída transmitida seja mais útil quando o tipo de dados do parâmetro de saída é do tipo BLOB, essa funcionalidade também pode ser usada com qualquer tipo de dados. Os tipos de dados suportados por parâmetros de saída streamed são especificados no driver.  
  
 Se houver SQL_PARAM_INPUT_OUTPUT_STREAM parâmetros a serem processados, **o SQLExecute** ou **o SQLExecDirect** retornarão SQL_NEED_DATA primeiro. Um aplicativo pode chamar **SQLParamData** e **SQLPutData** para enviar dados de parâmetros DAE. Quando todos os parâmetros de entrada do DAE são processados, **o SQLParamData** retorna SQL_PARAM_DATA_AVAILABLE para indicar que os parâmetros de saída em fluxo estão disponíveis.  
  
 Quando há parâmetros de saída em fluxo e parâmetros de saída vinculados a serem processados, o driver determina a ordem para processar parâmetros de saída. Assim, se um parâmetro de saída estiver vinculado a um buffer (o parâmetro **SQLBindParameter** *InputOutputType* está definido como SQL_PARAM_INPUT_OUTPUT ou SQL_PARAM_OUTPUT), o buffer pode não ser preenchido até que **o SQLParamData** retorne SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO. Um aplicativo deve ler um buffer vinculado somente após **o retorno do SQLParamData** SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO que é depois de todos os parâmetros de saída em fluxo serem processados.  
  
 A fonte de dados pode retornar um conjunto de avisos e resultados, além do parâmetro de saída transmitida. Em geral, os avisos e conjuntos de resultados são processados separadamente a partir de um parâmetro de saída em fluxo, **chamando-o de SQLMoreResults**. Os avisos de processo e o resultado definido antes de processar o parâmetro de saída em fluxo.  
  
 A tabela a seguir descreve diferentes cenários de um único comando enviado ao servidor e como o aplicativo deve funcionar.  
  
|Cenário|Valor de retorno de SQLExecute ou SQLExecDirect|O que fazer em seguida|  
|--------------|---------------------------------------------------|---------------------|  
|Os dados só incluem parâmetros de saída transmitida|SQL_PARAM_DATA_AVAILABLE|Use **SQLParamData** e **SQLGetData** para recuperar parâmetros de saída streamed.|  
|Os dados incluem um conjunto de resultados e parâmetros de saída em fluxo|SQL_SUCCESS|Recupere o conjunto de resultados com **SQLBindCol** e **SQLGetData**.<br /><br /> Ligue para **o SQLMoreResults** para iniciar o processamento de parâmetros de saída em fluxo. Deve voltar SQL_PARAM_DATA_AVAILABLE.<br /><br /> Use **SQLParamData** e **SQLGetData** para recuperar parâmetros de saída streamed.|  
|Os dados incluem uma mensagem de aviso e parâmetros de saída transmitidos|Sql_success_with_info|Use **SQLGetDiagRec** e **SQLGetDiagField** para processar mensagens de aviso.<br /><br /> Ligue para **o SQLMoreResults** para iniciar o processamento de parâmetros de saída em fluxo. Deve voltar SQL_PARAM_DATA_AVAILABLE.<br /><br /> Use **SQLParamData** e **SQLGetData** para recuperar parâmetros de saída streamed.|  
|Os dados incluem uma mensagem de aviso, conjunto de resultados e parâmetros de saída transmitidos|Sql_success_with_info|Use **SQLGetDiagRec** e **SQLGetDiagField** para processar mensagens de aviso. Em seguida, ligue para **sqlMoreResults** para começar a processar o conjunto de resultados.<br /><br /> Recupere um conjunto de resultados com **SQLBindCol** e **SQLGetData**.<br /><br /> Ligue para **o SQLMoreResults** para iniciar o processamento de parâmetros de saída em fluxo. **SQLMoreResults** deve retornar SQL_PARAM_DATA_AVAILABLE.<br /><br /> Use **SQLParamData** e **SQLGetData** para recuperar parâmetros de saída streamed.|  
|Consulta com parâmetros de entrada DAE, por exemplo, um parâmetro de entrada/saída (DAE) transmitido|SQL NEED_DATA|Ligue para **sqlparamData** e **SQLPutData** para enviar dados de parâmetros de entrada da DAE.<br /><br /> Depois que todos os parâmetros de entrada do DAE forem processados, **o SQLParamData** pode retornar qualquer código de retorno que **o SQLExecute** e **o SQLExecDirect** possam retornar. Os casos nesta tabela podem então ser aplicados.<br /><br /> Se o código de retorno for SQL_PARAM_DATA_AVAILABLE, os parâmetros de saída em streaming estão disponíveis. Um aplicativo deve chamar **SQLParamData** novamente para recuperar o token para o parâmetro de saída em fluxo, conforme descrito na primeira linha desta tabela.<br /><br /> Se o código de retorno for SQL_SUCCESS, ou há um conjunto de resultados para processar ou o processamento está concluído.<br /><br /> Se o código de retorno for SQL_SUCCESS_WITH_INFO, há mensagens de aviso para processar.|  
  
 Após **o retorno de SQLExecute,** **SQLExecDirect**ou **SQLMoreResults** SQL_PARAM_DATA_AVAILABLE, um erro de seqüência de funções resultará se um aplicativo chamar uma função que não esteja na lista a seguir:  
  
-   **SQLAllocHandle** / **SQLAllocHandleStd**  
  
-   **SQLDataSourcesS** / **SQLDrivers**  
  
-   **SQLGetInfo** / **SQLGetFunções**  
  
-   **SQLGetConnectAttr** / **SQLGetEnvAttr** / **SQLGetDescField** / **SQLGetDescRecRec**  
  
-   **SQLNumParams**  
  
-   **SQLDescribeParam**  
  
-   **SQLNativeSql**  
  
-   **SQLParamData**  
  
-   **SQLMoreResults**  
  
-   **SQLGetDiagField** / **SQLGetDiagRec**  
  
-   **SQLCancel**  
  
-   **SQLCancelHandle** (com alça de declaração)  
  
-   **SQLFreeStmt** (com opção = SQL_CLOSE, SQL_DROP ou SQL_UNBIND)  
  
-   **SQLCloseCursor**  
  
-   **Sqldisconnect**  
  
-   **SQLFreeHandle** (com HandleType = SQL_HANDLE_STMT)  
  
-   **SQLGetStmtAttr**  
  
 Os aplicativos ainda podem usar **SQLSetDescField** ou **SQLSetDescRec** para definir as informações de vinculação. O mapeamento de campo não será alterado. No entanto, campos dentro do descritor podem retornar novos valores. Por exemplo, SQL_DESC_PARAMETER_TYPE pode retornar SQL_PARAM_INPUT_OUTPUT_STREAM ou SQL_PARAM_OUTPUT_STREAM.  
  
## <a name="usage-scenario-retrieve-an-image-in-parts-from-a-result-set"></a>Cenário de uso: recuperar uma imagem em partes de um conjunto de resultados  
 **SQLGetData** pode ser usado para obter dados em partes quando um procedimento armazenado retorna um conjunto de resultados que contém uma linha de metadados sobre uma imagem e a imagem é devolvida em um grande parâmetro de saída.  
  
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
  
## <a name="usage-scenario-send-and-receive-a-large-object-as-a-streamed-inputoutput-parameter"></a>Cenário de uso: Enviar e Receber um Objeto Grande como um parâmetro de entrada/saída transmitido  
 **O SQLGetData** pode ser usado para obter e enviar dados em partes quando um procedimento armazenado passa um objeto grande como um parâmetro de entrada/saída, transmitindo o valor para e do banco de dados. Você não precisa armazenar todos os dados na memória.  
  
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

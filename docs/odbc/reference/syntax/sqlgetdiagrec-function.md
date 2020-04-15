---
title: Função SQLGetDiagRec | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDiagRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDiagRec
helpviewer_keywords:
- SQLGetDiagRec function [ODBC]
ms.assetid: ebdbac93-3d68-438f-8416-ef1f08e04269
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39069526e254903509ddfef00b7bd4844f3d9e10
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285376"
---
# <a name="sqlgetdiagrec-function"></a>Função SQLGetDiagRec
**Conformidade**  
 Versão introduzida: ODBC 3.0 Standards Compliance: ISO 92  
  
 **Resumo**  
 **O SQLGetDiagRec** retorna os valores atuais de vários campos de um registro de diagnóstico que contém informações de erro, aviso e status. Ao contrário **do SQLGetDiagField**, que retorna um campo de diagnóstico por chamada, **o SQLGetDiagRec** retorna vários campos comumente usados de um registro de diagnóstico, incluindo o SQLSTATE, o código de erro nativo e o texto da mensagem de diagnóstico.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
  
SQLRETURN SQLGetDiagRec(  
     SQLSMALLINT     HandleType,  
     SQLHANDLE       Handle,  
     SQLSMALLINT     RecNumber,  
     SQLCHAR *       SQLState,  
     SQLINTEGER *    NativeErrorPtr,  
     SQLCHAR *       MessageText,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   TextLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *Handletype*  
 [Entrada] Um identificador de tipo de alça que descreve o tipo de alça para a qual os diagnósticos são necessários. Deve ser uma destas opções:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN alça é usada apenas pelo Driver Manager e pelo motorista. Os aplicativos não devem usar este tipo de alça. Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [Developing Connection-Pool Awareness em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *Handle*  
 [Entrada] Uma alça para a estrutura de dados diagnósticos, do tipo indicado pelo *HandleType*. Se *o HandleType* estiver SQL_HANDLE_ENV, *o Handle* pode ser um cabo de ambiente compartilhado ou não compartilhado.  
  
 *RecNumber*  
 [Entrada] Indica o registro de status a partir do qual o aplicativo busca informações. Os registros de status são numerados a partir de 1.  
  
 *SQLState*  
 [Saída] Ponteiro para um buffer no qual retornar um código SQLSTATE de cinco caracteres (e terminando NULL) para o registro de diagnóstico *RecNumber*. Os dois primeiros caracteres indicam a classe; os próximos três indicam a subclasse. Essas informações estão contidas no campo de diagnóstico SQL_DIAG_SQLSTATE. Para obter mais informações, consulte [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md).  
  
 *NativeErrorPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o código de erro nativo, específico para a fonte de dados. Essas informações estão contidas no campo de diagnóstico SQL_DIAG_NATIVE.  
  
 *MessageText*  
 [Saída] Ponteiro para um buffer no qual retornar a seqüência de texto da mensagem de diagnóstico. Essas informações estão contidas no campo de diagnóstico SQL_DIAG_MESSAGE_TEXT. Para o formato da seqüência, consulte [Mensagens de diagnóstico](../../../odbc/reference/develop-app/diagnostic-messages.md).  
  
 Se *o MessageText* for NULL, *TextLengthPtr* ainda retornará o número total de caracteres (excluindo o caractere de rescisão nula para dados de caracteres) disponível para retornar no buffer apontado pelo *MessageText*.  
  
 *BufferLength*  
 [Entrada] Comprimento do buffer **MessageText* em caracteres. Não há comprimento máximo do texto da mensagem de diagnóstico.  
  
 *TextLengthPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de caracteres (excluindo o número de caracteres necessários para o caractere de rescisão nula) disponível para retornar no * \*MessageText*. Se o número de caracteres disponíveis para retornar for maior que *BufferLength,* o texto da mensagem de diagnóstico no * \*MessageText* será truncado para *BufferLength* menos o comprimento de um caractere de rescisão nula.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 **O SQLGetDiagRec** não publica registros de diagnóstico para si mesmo. Ele usa os seguintes valores de retorno para relatar o resultado de sua própria execução:  
  
-   SQL_SUCCESS: A função retornou com sucesso as informações de diagnóstico.  
  
-   SQL_SUCCESS_WITH_INFO: \*O buffer *MessageText* era muito pequeno para manter a mensagem de diagnóstico solicitada. Nenhum registro de diagnóstico foi gerado. Para determinar que ocorreu uma truncamento, o aplicativo deve comparar *BufferLength* com o número real de bytes disponíveis, que está escrito em **StringLengthPtr*.  
  
-   SQL_INVALID_HANDLE: A alça indicada por *HandleType* e *Handle* não era uma alça válida.  
  
-   SQL_ERROR: Ocorreu um dos seguintes:  
  
    -   *RecNumber* foi negativo ou 0.  
  
    -   *BufferLength* era menor que zero.  
  
    -   Ao usar a notificação assíncrona, a operação assíncrona na alça não foi concluída.  
  
-   SQL_NO_DATA: *RecNumber* foi maior do que o número de registros de diagnóstico que existiam para a alça especificada no *Handle.* A função também retorna SQL_NO_DATA para qualquer *RecNumber* positivo se não houver registros de diagnóstico para *Handle*.  
  
## <a name="comments"></a>Comentários  
 Um aplicativo normalmente chama **SQLGetDiagRec** quando uma chamada anterior para uma função ODBC retornou SQL_ERROR ou SQL_SUCCESS_WITH_INFO. No entanto, como qualquer função ODBC pode postar zero ou mais registros de diagnóstico cada vez que é chamada, um aplicativo pode chamar **SQLGetDiagRec** após qualquer chamada de função ODBC. Um aplicativo pode ligar para **o SQLGetDiagRec** várias vezes para retornar alguns ou todos os registros na estrutura de dados de diagnóstico. A ODBC não impõe limite ao número de registros diagnósticos que podem ser armazenados a qualquer momento.  
  
 **O SQLGetDiagRec** não pode ser usado para retornar campos do cabeçalho da estrutura de dados de diagnóstico. (O argumento *RecNumber* deve ser maior que 0.) O aplicativo deve chamar **SQLGetDiagField** para este fim.  
  
 **O SQLGetDiagRec** recupera apenas as informações de diagnóstico mais recentemente associadas à alça especificada no argumento *Lidar.* Se o aplicativo chamar outra função ODBC, exceto **SQLGetDiagRec,** **SQLGetDiagField**ou **SQLError,** quaisquer informações de diagnóstico das chamadas anteriores na mesma alça serão perdidas.  
  
 Um aplicativo pode escarná-los por looping, incrementando *o RecNumber,* desde que **o SQLGetDiagRec** retorne SQL_SUCCESS. As chamadas para **SQLGetDiagRec** não são destrutivas para os campos de cabeçalho e gravação. O aplicativo pode chamar **SQLGetDiagRec** novamente posteriormente para recuperar um campo de um registro, desde que nenhuma outra função, exceto **SQLGetDiagRec,** **SQLGetDiagField**ou **SQLError,** tenha sido chamada nesse ínterim. O aplicativo também pode recuperar uma contagem do número total de registros de diagnóstico disponíveis ligando para **SQLGetDiagField** para recuperar o valor do campo SQL_DIAG_NUMBER e, em seguida, chamando **SQLGetDiagRec** muitas vezes.  
  
 Para obter uma descrição dos campos da estrutura de dados diagnósticos, consulte [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md). Para obter mais informações, consulte [Usando SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) e [Implementando SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md).  
  
 Chamar uma API diferente da que está sendo executada de forma assíncrona gerará HY010 "Erro de seqüência de funções". No entanto, o registro de erro não pode ser recuperado antes que a operação assíncrona seja concluída.  
  
## <a name="handletype-argument"></a>Argumento handleType  
 Cada tipo de alça pode ter informações de diagnóstico associadas a ele. O argumento *HandleType* denota o tipo de alça do argumento *Lidar.*  
  
 Alguns campos de cabeçalho e registro não podem ser retornados para alças de ambiente, conexão, declaração e descritor. As alças para as quais um campo não é aplicável são indicadas nas seções "Campos de cabeçalho" e "Campos de registro" no [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
 Uma chamada para **o SQLGetDiagRec** retornará SQL_INVALID_HANDLE se *o HandleType* for SQL_HANDLE_SENV, o que denota uma alça de ambiente compartilhada. No entanto, se *o HandleType* for SQL_HANDLE_ENV, *o Handle* pode ser um cabo de ambiente compartilhado ou não compartilhado.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Obtenção de um campo de um registro de diagnóstico ou um campo do cabeçalho de diagnóstico|[Função SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API oDBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programa ODBC de exemplo](../../../odbc/reference/sample-odbc-program.md)

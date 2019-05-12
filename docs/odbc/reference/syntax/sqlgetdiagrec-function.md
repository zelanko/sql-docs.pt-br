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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6cb79375475e4827e1e1c4d3b76721f1614e864e
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/11/2019
ms.locfileid: "65538163"
---
# <a name="sqlgetdiagrec-function"></a>Função SQLGetDiagRec
**Conformidade com**  
 Versão introduzida: Conformidade com padrões 3.0 ODBC: ISO 92  
  
 **Resumo**  
 **SQLGetDiagRec** retorna os valores atuais de vários campos de um registro de diagnóstico que contém informações de erro, aviso e status. Diferentemente **SQLGetDiagField**, que retorna um campo de diagnóstico por chamada, **SQLGetDiagRec** retorna vários campos de um registro de diagnóstico, incluindo o SQLSTATE, o código de erro nativo comumente usados e o texto da mensagem de diagnóstico.  
  
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
 *HandleType*  
 [Entrada] Um identificador de tipo de identificador que descreve o tipo de identificador para o qual o diagnóstico é necessário. Deve ser uma destas opções:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 Identificador SQL_HANDLE_DBC_INFO_TOKEN é usado somente pelo Gerenciador de Driver e o driver. Aplicativos não devem usar esse tipo de identificador. Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desenvolvendo o reconhecimento de Pool de Conexão em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *Handle*  
 [Entrada] Um identificador para a estrutura de dados de diagnóstico, do tipo indicado por *HandleType*. Se *HandleType* é SQL_HANDLE_ENV, *manipular* pode ser compartilhado ou um identificador de ambiente não compartilhadas.  
  
 *RecNumber*  
 [Entrada] Indica que o registro de status do qual o aplicativo busca informações. Registros de status são numerados de 1.  
  
 *SQLState*  
 [Saída] Ponteiro para um buffer no qual retornar um código SQLSTATE de cinco caracteres (e nulo de terminação) para o registro de diagnóstico *RecNumber*. Os dois primeiros caracteres indicam a classe; os próximos três indicam a subclasse. Essas informações estão contidas no campo de diagnóstico SQL_DIAG_SQLSTATE. Para obter mais informações, consulte [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md).  
  
 *NativeErrorPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o código de erro nativo específico à fonte de dados. Essas informações estão contidas no campo de diagnóstico SQL_DIAG_NATIVE.  
  
 *MessageText*  
 [Saída] Ponteiro para um buffer no qual retornar a cadeia de caracteres de texto de mensagem de diagnóstico. Essas informações estão contidas no campo de diagnóstico SQL_DIAG_MESSAGE_TEXT. Para o formato da cadeia de caracteres, consulte [mensagens de diagnóstico](../../../odbc/reference/develop-app/diagnostic-messages.md).  
  
 Se *MessageText* for NULL, *TextLengthPtr* ainda retornará o número total de caracteres (exceto o caractere nulo de terminação para dados de caracteres) disponíveis para retornar no buffer apontado por *MessageText*.  
  
 *BufferLength*  
 [Entrada] Comprimento do **MessageText* buffer em caracteres. Não há nenhum tamanho máximo do texto da mensagem de diagnóstico.  
  
 *TextLengthPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de caracteres (exceto o número de caracteres necessários para o caractere nulo de terminação) disponíveis para retornar na  *\*MessageText*. Se o número de caracteres disponíveis para retornar for maior que *BufferLength*, o texto da mensagem de diagnóstico no  *\*MessageText* será truncado para *BufferLength* menos o comprimento de um caractere nulo de terminação.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 **SQLGetDiagRec** não envia os registros de diagnóstico para si mesmo. Ele usa os seguintes valores de retornados para relatar o resultado da execução do seu próprio:  
  
-   SQL_SUCCESS: A função retornado com êxito as informações de diagnóstico.  
  
-   SQL_SUCCESS_WITH_INFO: O \* *MessageText* buffer era muito pequeno para conter a mensagem de diagnóstico solicitada. Não há registros de diagnóstico foram gerados. Para determinar o que ocorreu um truncamento, o aplicativo deve comparar *BufferLength* o número real de bytes disponíveis, que é gravado em **StringLengthPtr*.  
  
-   SQL_INVALID_HANDLE: O identificador é indicado por *HandleType* e *manipular* não era um identificador válido.  
  
-   SQL_ERROR: Um dos seguintes ocorreu:  
  
    -   *RecNumber* era negativo ou 0.  
  
    -   *BufferLength* era menor que zero.  
  
    -   Ao usar a notificação assíncrona, a operação assíncrona no identificador não foi concluída.  
  
-   SQL_NO_DATA: *RecNumber* era maior que o número de registros de diagnóstico que existia para o identificador especificado na *manipular.* A função também retorna SQL_NO_DATA para qualquer positivo *RecNumber* se não há registros para diagnóstico *manipular*.  
  
## <a name="comments"></a>Comentários  
 Um aplicativo normalmente chama **SQLGetDiagRec** quando uma chamada anterior a uma função ODBC retornou SQL_ERROR ou SQL_SUCCESS_WITH_INFO. No entanto, porque qualquer função ODBC pode postar zero ou mais registros de diagnóstico a cada vez que é chamado, um aplicativo pode chamar **SQLGetDiagRec** após qualquer chamada de função ODBC. Um aplicativo pode chamar **SQLGetDiagRec** várias vezes para retornar alguns ou todos os registros na estrutura de dados de diagnóstico. ODBC não impõe limites ao número de registros de diagnóstico que podem ser armazenados em qualquer momento.  
  
 **SQLGetDiagRec** não pode ser usado para retornar campos do cabeçalho da estrutura de dados de diagnóstico. (O *RecNumber* argumento deve ser maior que 0.) O aplicativo deve chamar **SQLGetDiagField** para essa finalidade.  
  
 **SQLGetDiagRec** recupera apenas as informações de diagnóstico mais recentemente associadas com o identificador especificado na *manipular* argumento. Se o aplicativo chama outra função ODBC, exceto **SQLGetDiagRec**, **SQLGetDiagField**, ou **SQLError**, quaisquer informações de diagnóstico das chamadas anteriores sobre o mesmo identificador será perdido.  
  
 Um aplicativo pode examinar todos os registros de diagnóstico fazendo um loop, incrementar *RecNumber*, enquanto **SQLGetDiagRec** retorna SQL_SUCCESS. Chamadas para **SQLGetDiagRec** sejam não destrutivas campos de cabeçalho e o registro. O aplicativo pode chamar **SQLGetDiagRec** novamente mais tarde para recuperar um campo de um registro, desde como nenhuma outra função, exceto **SQLGetDiagRec**, **SQLGetDiagField**, ou **SQLError**, foi chamado nesse meio tempo. O aplicativo também pode recuperar uma contagem do número total de registros de diagnóstico disponíveis por meio da chamada **SQLGetDiagField** para recuperar o valor do campo SQL_DIAG_NUMBER e, em seguida, chamando **SQLGetDiagRec**tantas vezes.  
  
 Para obter uma descrição dos campos da estrutura de dados de diagnóstico, consulte [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md). Para obter mais informações, consulte [usando SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) e [implementando SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md).  
  
 Chamar uma API diferente daquele que está sendo executada de forma assíncrona gerará HY010 "Erro de sequência de função". No entanto, o registro de erro não pode ser recuperado antes que a operação assíncrona seja concluída.  
  
## <a name="handletype-argument"></a>Argumento HandleType  
 Cada tipo de identificador pode ter informações de diagnóstico associadas a ele. O *HandleType* argumento indica o tipo de identificador do *manipular* argumento.  
  
 Alguns campos de cabeçalho e o registro não podem ser retornados para o ambiente, conexão, instrução e descritor de identificadores. Esses identificadores para o qual um campo não é aplicável são indicadas nas seções "Campos do cabeçalho" e "Campos do Registro" em [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
 Uma chamada para **SQLGetDiagRec** retornará SQL_INVALID_HANDLE se *HandleType* é SQL_HANDLE_SENV, que denota um identificador de ambiente compartilhado. No entanto, se *HandleType* é SQL_HANDLE_ENV, *manipular* pode ser compartilhado ou um identificador de ambiente não compartilhadas.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Obtendo um campo de um registro de diagnóstico ou um campo do cabeçalho de diagnóstico|[Função SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programa ODBC de exemplo](../../../odbc/reference/sample-odbc-program.md)

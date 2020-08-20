---
description: Função SQLGetDiagRec
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
ms.openlocfilehash: 7f141891292fb80d53ba06e03329b66cbc8b826e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461009"
---
# <a name="sqlgetdiagrec-function"></a>Função SQLGetDiagRec
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,0: ISO 92  
  
 **Resumo**  
 **SQLGetDiagRec** retorna os valores atuais de vários campos de um registro de diagnóstico que contém informações de erro, aviso e status. Ao contrário de **SQLGetDiagField**, que retorna um campo de diagnóstico por chamada, **SQLGetDiagRec** retorna vários campos usados com frequência de um registro de diagnóstico, incluindo o SQLSTATE, o código de erro nativo e o texto da mensagem de diagnóstico.  
  
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
 Entrada Um identificador de tipo de identificador que descreve o tipo de identificador para o qual o diagnóstico é necessário. Deve ser uma destas opções:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 O identificador de SQL_HANDLE_DBC_INFO_TOKEN é usado somente pelo driver e pelo Gerenciador de driver. Os aplicativos não devem usar esse tipo de identificador. Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desenvolvendo o reconhecimento do pool de conexões em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *Handle*  
 Entrada Um identificador para a estrutura de dados de diagnóstico, do tipo indicado por *HandleType*. Se *HandleType* for SQL_HANDLE_ENV, o *identificador* poderá ser um identificador de ambiente compartilhado ou não compartilhado.  
  
 *RecNumber*  
 Entrada Indica o registro de status do qual o aplicativo busca informações. Os registros de status são numerados a partir de 1.  
  
 *SQLState*  
 Der Ponteiro para um buffer no qual retornar um código SQLSTATE de cinco caracteres (e terminando NULL) para o registro de diagnóstico *RecNumber*. Os dois primeiros caracteres indicam a classe; os próximos três indicam a subclasse. Essas informações estão contidas no campo diagnóstico de SQL_DIAG_SQLSTATE. Para obter mais informações, consulte [SQLstates](../../../odbc/reference/develop-app/sqlstates.md).  
  
 *NativeErrorPtr*  
 Der Ponteiro para um buffer no qual retornar o código de erro nativo, específico à fonte de dados. Essas informações estão contidas no campo diagnóstico de SQL_DIAG_NATIVE.  
  
 *MessageText*  
 Der Ponteiro para um buffer no qual retornar a cadeia de texto da mensagem de diagnóstico. Essas informações estão contidas no campo diagnóstico de SQL_DIAG_MESSAGE_TEXT. Para o formato da cadeia de caracteres, consulte [mensagens de diagnóstico](../../../odbc/reference/develop-app/diagnostic-messages.md).  
  
 Se *MessageText* for NULL, *TextLengthPtr* ainda retornará o número total de caracteres (excluindo o caractere de terminação nula para dados de caracteres) disponíveis para retornar no buffer apontado por *MessageText*.  
  
 *BufferLength*  
 Entrada Comprimento do buffer **MessageText* em caracteres. Não há nenhum comprimento máximo do texto da mensagem de diagnóstico.  
  
 *TextLengthPtr*  
 Der Ponteiro para um buffer no qual retornar o número total de caracteres (excluindo o número de caracteres necessários para o caractere de terminação nula) disponível para retornar em * \* MessageText*. Se o número de caracteres disponíveis para retornar for maior que *BufferLength*, o texto da mensagem de diagnóstico em * \* MessageText* será truncado para *BufferLength* menos o comprimento de um caractere de terminação nula.  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 **SQLGetDiagRec** não publica registros de diagnóstico para si mesmo. Ele usa os seguintes valores de retorno para relatar o resultado de sua própria execução:  
  
-   SQL_SUCCESS: a função retornou informações de diagnóstico com êxito.  
  
-   SQL_SUCCESS_WITH_INFO: o \* buffer *MessageText* era muito pequeno para manter a mensagem de diagnóstico solicitada. Nenhum registro de diagnóstico foi gerado. Para determinar que ocorreu um truncamento, o aplicativo deve comparar *BufferLength* com o número real de bytes disponíveis, que é gravado em **StringLengthPtr*.  
  
-   SQL_INVALID_HANDLE: o identificador indicado por *HandleType* e *identificador* não era um identificador válido.  
  
-   SQL_ERROR: uma das seguintes ocorrências:  
  
    -   *RecNumber* era negativo ou 0.  
  
    -   *BufferLength* era menor que zero.  
  
    -   Ao usar a notificação assíncrona, a operação assíncrona no identificador não foi concluída.  
  
-   SQL_NO_DATA: *RecNumber* foi maior que o número de registros de diagnóstico que existia para o identificador especificado no *identificador.* A função também retorna SQL_NO_DATA para qualquer *RecNumber* positivo se não houver nenhum registro de diagnóstico para o *identificador*.  
  
## <a name="comments"></a>Comentários  
 Um aplicativo normalmente chama **SQLGetDiagRec** quando uma chamada anterior a uma função ODBC retorna SQL_ERROR ou SQL_SUCCESS_WITH_INFO. No entanto, como qualquer função ODBC pode postar zero ou mais registros de diagnóstico cada vez que é chamado, um aplicativo pode chamar **SQLGetDiagRec** após qualquer chamada de função ODBC. Um aplicativo pode chamar **SQLGetDiagRec** várias vezes para retornar alguns ou todos os registros na estrutura de dados de diagnóstico. O ODBC impõe nenhum limite para o número de registros de diagnóstico que podem ser armazenados a qualquer momento.  
  
 **SQLGetDiagRec** não pode ser usado para retornar campos do cabeçalho da estrutura de dados de diagnóstico. (O argumento *RecNumber* deve ser maior que 0.) O aplicativo deve chamar **SQLGetDiagField** para essa finalidade.  
  
 **SQLGetDiagRec** recupera apenas as informações de diagnóstico mais recentemente associadas ao identificador especificado no argumento *Handle* . Se o aplicativo chamar outra função ODBC, exceto **SQLGetDiagRec**, **SQLGetDiagField**ou **SqlError**, todas as informações de diagnóstico das chamadas anteriores no mesmo identificador serão perdidas.  
  
 Um aplicativo pode verificar todos os registros de diagnóstico por loop, incrementando *RecNumber*, desde que **SQLGetDiagRec** retorne SQL_SUCCESS. As chamadas para **SQLGetDiagRec** não são destrutivas para os campos de cabeçalho e registro. O aplicativo pode chamar **SQLGetDiagRec** novamente mais tarde para recuperar um campo de um registro, desde que nenhuma outra função, exceto **SQLGetDiagRec**, **SQLGetDiagField**ou **SqlError**, tenha sido chamada no interim. O aplicativo também pode recuperar uma contagem do número total de registros de diagnóstico disponíveis chamando **SQLGetDiagField** para recuperar o valor do campo SQL_DIAG_NUMBER e, em seguida, chamando **SQLGetDiagRec** que muitas vezes.  
  
 Para obter uma descrição dos campos da estrutura de dados de diagnóstico, consulte [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md). Para obter mais informações, consulte [usando SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) e [implementando SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md).  
  
 Chamar uma API diferente daquela que está sendo executada de forma assíncrona gerará HY010 "erro de sequência de função". No entanto, o registro de erro não pode ser recuperado antes que a operação assíncrona seja concluída.  
  
## <a name="handletype-argument"></a>Argumento HandleType  
 Cada tipo de identificador pode ter informações de diagnóstico associadas a ele. O argumento *HandleType* denota o tipo de identificador do argumento *Handle* .  
  
 Alguns campos de cabeçalho e de registro não podem ser retornados para identificadores de ambiente, conexão, instrução e descritor. Esses identificadores para os quais um campo não é aplicável são indicados nas seções "campos de cabeçalho" e "campos de registro" em [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
 Uma chamada para **SQLGetDiagRec** retornará SQL_INVALID_HANDLE se *handletype* for SQL_HANDLE_SENV, que denota um identificador de ambiente compartilhado. No entanto, se *HandleType* for SQL_HANDLE_ENV, o *identificador* poderá ser um identificador de ambiente compartilhado ou não compartilhado.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Obtendo um campo de um registro de diagnóstico ou um campo do cabeçalho de diagnóstico|[Função SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência da API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programa ODBC de exemplo](../../../odbc/reference/sample-odbc-program.md)

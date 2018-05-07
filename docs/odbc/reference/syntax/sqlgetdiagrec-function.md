---
title: Função SQLGetDiagRec | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a926e8de729fe5d654f880128371bfc48dd39fdd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlgetdiagrec-function"></a>Função SQLGetDiagRec
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 3.0 ODBC: 92 ISO  
  
 **Resumo**  
 **SQLGetDiagRec** retorna os valores atuais de vários campos de um registro de diagnóstico que contém informações de erro, aviso e status. Ao contrário de **SQLGetDiagField**, que retorna um campo de diagnóstico por chamada, **SQLGetDiagRec** retorna vários campos de um registro de diagnóstico, incluindo o SQLSTATE, o código de erro nativo comumente usados e o texto da mensagem de diagnóstico.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
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
 [Entrada] Um identificador de tipo de identificador que descreve o tipo de identificador para o qual diagnósticos são necessários. Deve ser uma destas opções:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 Identificador SQL_HANDLE_DBC_INFO_TOKEN é usado somente pelo Gerenciador de Driver e do driver. Aplicativos não devem usar este tipo de identificador. Para obter mais informações sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desenvolvendo o reconhecimento do Pool de Conexão em um Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *Handle*  
 [Entrada] Um identificador para a estrutura de dados de diagnóstico, do tipo indicado pelo *HandleType*. Se *HandleType* é SQL_HANDLE_ENV, *tratar* pode ser um identificador de ambiente não compartilhado ou compartilhado.  
  
 *RecNumber*  
 [Entrada] Indica que o registro de status do qual o aplicativo busca de informações. Registros de status são numerados de 1.  
  
 *SQLState*  
 [Saída] Ponteiro para um buffer no qual retornar um código SQLSTATE de cinco caracteres (e terminação nula) para o registro de diagnóstico *RecNumber*. Os dois primeiros caracteres indicam a classe. as próximas três indicam a subclasse. Essa informação está contida no campo de diagnóstico SQL_DIAG_SQLSTATE. Para obter mais informações, consulte [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md).  
  
 *NativeErrorPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o código de erro nativo, específico para a fonte de dados. Essa informação está contida no campo de diagnóstico SQL_DIAG_NATIVE.  
  
 *MessageText*  
 [Saída] Ponteiro para um buffer no qual retornar a cadeia de caracteres de texto de mensagem de diagnóstico. Essa informação está contida no campo de diagnóstico SQL_DIAG_MESSAGE_TEXT. Para o formato da cadeia de caracteres, consulte [mensagens de diagnóstico](../../../odbc/reference/develop-app/diagnostic-messages.md).  
  
 Se *MessageText* for NULL, *TextLengthPtr* ainda retornará o número total de caracteres (excluindo o caractere null de terminação para dados de caractere) disponíveis para retornar o buffer apontado pelo *MessageText*.  
  
 *BufferLength*  
 [Entrada] Comprimento do **MessageText* buffer em caracteres. Não há nenhum tamanho máximo do texto da mensagem de diagnóstico.  
  
 *TextLengthPtr*  
 [Saída] Ponteiro para um buffer no qual retornar o número total de caracteres (excluindo o número de caracteres necessários para o caractere null de terminação) disponíveis para retornar em  *\*MessageText*. Se o número de caracteres disponíveis para retornar for maior do que *BufferLength*, o texto da mensagem de diagnóstico em  *\*MessageText* será truncado para *BufferLength* menos o comprimento de um caractere null de terminação.  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 **SQLGetDiagRec** não envia registros de diagnóstico para si mesmo. Ele usa os seguintes valores de retorno para relatar o resultado da execução do seu próprio:  
  
-   SQL_SUCCESS: A função retornou com êxito as informações de diagnósticas.  
  
-   SQL_SUCCESS_WITH_INFO: O \* *MessageText* buffer era muito pequeno para armazenar a mensagem de diagnóstica solicitada. Não há registros de diagnóstico foram gerados. Para determinar se ocorreu um truncamento, o aplicativo deve comparar *BufferLength* para o número real de bytes disponíveis, que está escrito em **StringLengthPtr*.  
  
-   SQL_INVALID_HANDLE: O identificador indicado por *HandleType* e *tratar* não era um identificador válido.  
  
-   SQL_ERROR: Uma das opções a seguir ocorreu:  
  
    -   *RecNumber* foi negativo ou 0.  
  
    -   *BufferLength* foi menor que zero.  
  
    -   Ao usar a notificação assíncrona, a operação assíncrona no identificador não foi concluída.  
  
-   SQL_NO_DATA: *RecNumber* era maior que o número de registros de diagnóstico que existiam para o identificador especificado no *tratar.* A função também retorna SQL_NO_DATA para qualquer positivo *RecNumber* se não houver nenhum registro de diagnóstico para *tratar*.  
  
## <a name="comments"></a>Comentários  
 Um aplicativo normalmente chama **SQLGetDiagRec** quando uma chamada anterior para uma função ODBC retornou SQL_ERROR ou SQL_SUCCESS_WITH_INFO. No entanto, como uma função ODBC pode lançar zero ou mais registros de diagnóstico cada vez que ele é chamado, um aplicativo pode chamar **SQLGetDiagRec** após qualquer chamada de função ODBC. Um aplicativo pode chamar **SQLGetDiagRec** várias vezes para retornar alguns ou todos os registros na estrutura de dados de diagnóstico. ODBC não impõe limites para o número de registros de diagnóstico que podem ser armazenados em qualquer momento.  
  
 **SQLGetDiagRec** não pode ser usado para retornar campos do cabeçalho da estrutura de dados de diagnóstico. (O *RecNumber* argumento deve ser maior que 0.) O aplicativo deve chamar **SQLGetDiagField** para essa finalidade.  
  
 **SQLGetDiagRec** recupera apenas as informações de diagnósticas mais recentemente associadas com o identificador especificado no *tratar* argumento. Se o aplicativo chamar outra função ODBC, exceto **SQLGetDiagRec**, **SQLGetDiagField**, ou **SQLError**, quaisquer informações de diagnóstico das chamadas anteriores sobre o Identificador do mesmo é perdida.  
  
 Um aplicativo pode verificar todos os registros de diagnósticos por looping, incrementando *RecNumber*, contanto que **SQLGetDiagRec** retorna SQL_SUCCESS. Chamadas para **SQLGetDiagRec** são destrutivos nos campos de cabeçalho e o registro. O aplicativo pode chamar **SQLGetDiagRec** novamente mais tarde para recuperar um campo de um registro desde como nenhuma outra função, exceto **SQLGetDiagRec**, **SQLGetDiagField**, ou **SQLError**, foi chamado nesse meio tempo. O aplicativo também pode recuperar uma contagem do número total de registros de diagnóstico disponíveis ao chamar **SQLGetDiagField** para recuperar o valor do campo SQL_DIAG_NUMBER e, em seguida, chamar **SQLGetDiagRec**que muitas vezes.  
  
 Para obter uma descrição dos campos da estrutura de dados de diagnóstico, consulte [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md). Para obter mais informações, consulte [usando SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) e [SQLGetDiagRec implementando e SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md).  
  
 Chamar uma API diferente daquele que está sendo executada de forma assíncrona gerará HY010 "Erro de sequência de função". No entanto, o registro de erro não pode ser recuperado antes que a operação assíncrona é concluída.  
  
## <a name="handletype-argument"></a>Argumento HandleType  
 Cada tipo de identificador pode ter informações de diagnóstico associadas a ele. O *HandleType* argumento indica o tipo de identificador do *tratar* argumento.  
  
 Alguns campos de cabeçalho e o registro não podem ser retornados para o ambiente, a conexão, a instrução e descritor de identificadores. Os identificadores de um campo não é aplicável para o qual são indicadas nas seções "Campos de cabeçalho" e "Campos do Registro" em [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
 Uma chamada para **SQLGetDiagRec** retornará SQL_INVALID_HANDLE se *HandleType* é SQL_HANDLE_SENV, que indica um identificador de ambiente compartilhado. No entanto, se *HandleType* é SQL_HANDLE_ENV, *tratar* pode ser um identificador de ambiente não compartilhado ou compartilhado.  
  
## <a name="related-functions"></a>Funções relacionadas  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Obter um campo de um registro de diagnóstico ou um campo do cabeçalho do diagnóstico|[Função SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Arquivos de cabeçalho ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programa ODBC de exemplo](../../../odbc/reference/sample-odbc-program.md)

---
title: Enviando dados Long | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- sending long data [ODBC]
ms.assetid: ea989084-a8e6-4737-892e-9ec99dd49caf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc7a140d7de8548f02fde6ab309823bbe1c9c656
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62465915"
---
# <a name="sending-long-data"></a>Enviar dados Long
Definem DBMSs *dados long* como qualquer caractere ou dados binários ao longo de um determinado tamanho, como 254 caracteres. Pode não ser possível armazenar todo o item de dados longos em memória, como quando o item representa um documento de texto longo ou um bitmap. Como esses dados não podem ser armazenados em um único buffer, a fonte de dados envia para o driver em partes com **SQLPutData** quando a instrução é executada. Os parâmetros para o qual os dados são enviados em tempo de execução são conhecidos como *parâmetros de dados em execução*.  
  
> [!NOTE]  
>  Um aplicativo, na verdade, pode enviar qualquer tipo de dados em tempo de execução com **SQLPutData**, embora somente os caracteres e dados binários podem ser enviados em partes. No entanto, se os dados são pequenos o suficiente para caber em um único buffer, há geralmente não há motivo para usar **SQLPutData**. É muito mais fácil associar o buffer e permitir que o driver recupera os dados do buffer.  
  
 Para enviar dados em tempo de execução, o aplicativo executa as seguintes ações:  
  
1.  Transmite um valor de 32 bits que identifica o parâmetro na *ParameterValuePtr* argumento **SQLBindParameter** em vez de passar o endereço de um buffer. Esse valor não será analisado pelo driver. Ele será retornado para o aplicativo mais tarde, portanto, ele deve significar algo para o aplicativo. Por exemplo, ele pode ser o número do parâmetro ou o identificador de um arquivo que contém dados.  
  
2.  Passa o endereço de um buffer de comprimento/indicador na *StrLen_or_IndPtr* argumento de **SQLBindParameter**.  
  
3.  Armazena SQL_DATA_AT_EXEC ou o resultado do SQL_LEN_DATA_AT_EXEC (*comprimento*) macro no buffer de comprimento/indicador. Esses valores indicam para o driver que serão enviados com os dados para o parâmetro **SQLPutData**. SQL_LEN_DATA_AT_EXEC (*comprimento*) é usado ao enviar dados longos para uma fonte de dados que precisa saber quantos bytes de dados long serão enviados para que ele pode alocar antecipadamente espaço. Para determinar se uma fonte de dados solicita este valor, o aplicativo chama **SQLGetInfo** com a opção SQL_NEED_LONG_DATA_LEN. Todos os drivers devem dar suporte a esta macro; Se a fonte de dados não requer o comprimento em bytes, o driver pode ignorá-lo.  
  
4.  Chamadas **SQLExecute** ou **SQLExecDirect**. O driver detecta que um buffer de comprimento/indicador contém o valor SQL_DATA_AT_EXEC ou o resultado do SQL_LEN_DATA_AT_EXEC (*comprimento*) macro e retorna SQL_NEED_DATA como o valor de retorno da função.  
  
5.  Chamadas **SQLParamData** em resposta ao SQL_NEED_DATA o valor de retorno. Se precisam ser enviada, dados longos **SQLParamData** retornará SQL_NEED_DATA. No buffer apontado pela *ValuePtrPtr* argumento, o driver retorna o valor que identifica o parâmetro de dados em execução. Se houver mais de um parâmetro de dados em execução, o aplicativo deve usar esse valor para determinar qual parâmetro para enviar dados para; o driver não é necessário para solicitar dados para parâmetros de dados em execução em uma ordem específica.  
  
6.  Chamadas **SQLPutData** para enviar os dados de parâmetro para o driver. Se os dados de parâmetro não couberem em um único buffer, pois geralmente é o caso de dados longo, o aplicativo chama **SQLPutData** repetidamente para enviar os dados em partes; cabe a fonte de dados e o driver para remontar os dados. Se o aplicativo passa os dados de cadeia de caracteres terminada em nulo, a driver ou fonte de dados deve remover o caractere de terminação null como parte do processo de remontagem.  
  
7.  Chamadas **SQLParamData** novamente para indicar que ele enviou todos os dados para o parâmetro. Se houver quaisquer parâmetros de dados em execução para o qual os dados não foram enviados, o driver retorna SQL_NEED_DATA e o valor que identifica o próximo parâmetro; o aplicativo retorna para a etapa 6. Se os dados foram enviados para todos os parâmetros de dados em execução, a instrução é executada. **SQLParamData** retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO e pode retorna qualquer valor de retorno ou diagnóstico que **SQLExecute** ou **SQLExecDirect** pode retornar.  
  
 Após **SQLExecute** ou **SQLExecDirect** retornará SQL_NEED_DATA e antes de dados seja completamente enviados para o último parâmetro de dados em execução, a instrução está em um estado de dados necessário. Enquanto uma instrução está em um estado de dados necessário, o aplicativo pode chamar apenas **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**, ou **SQLGetDiagRec**; todas as outras funções retornam SQLSTATE HY010 (erro de sequência de função). Chamando **SQLCancel** cancela a execução da instrução e o retorna ao estado anterior. Para obter mais informações, consulte [apêndice b: Tabelas de transição de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Para obter um exemplo de envio de dados em tempo de execução, consulte o [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md) descrição da função.

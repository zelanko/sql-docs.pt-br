---
description: Enviar dados Long
title: Enviando dados longos | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f6a0ec1a7e8dc703d3e7a3ed5332d20e6539eafe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476458"
---
# <a name="sending-long-data"></a>Enviar dados Long
DBMSs definem *dados longos* como qualquer caractere ou dados binários em um determinado tamanho, como 254 caracteres. Talvez não seja possível armazenar um item inteiro de dados longos na memória, como quando o item representa um documento de texto longo ou um bitmap. Como esses dados não podem ser armazenados em um único buffer, a fonte de dados o envia para o driver em partes com **SQLPutData** quando a instrução é executada. Os parâmetros para os quais os dados são enviados no momento da execução são conhecidos como *parâmetros de dados em execução*.  
  
> [!NOTE]  
>  Um aplicativo pode realmente enviar qualquer tipo de dados no momento da execução com **SQLPutData**, embora apenas dados de caractere e binário possam ser enviados em partes. No entanto, se os dados forem pequenos o suficiente para caber em um único buffer, geralmente não há motivo para usar **SQLPutData**. É muito mais fácil associar o buffer e permitir que o driver recupere os dados do buffer.  
  
 Para enviar dados no momento da execução, o aplicativo executa as seguintes ações:  
  
1.  Passa um valor de 32 bits que identifica o parâmetro no argumento *ParameterValuePtr* em **SQLBindParameter** em vez de passar o endereço de um buffer. Esse valor não é analisado pelo driver. Ele será retornado para o aplicativo mais tarde, portanto, ele deve significar algo ao aplicativo. Por exemplo, pode ser o número do parâmetro ou o identificador de um arquivo que contém dados.  
  
2.  Passa o endereço de um buffer de comprimento/indicador no argumento *StrLen_or_IndPtr* de **SQLBindParameter**.  
  
3.  Armazena SQL_DATA_AT_EXEC ou o resultado da macro SQL_LEN_DATA_AT_EXEC (*comprimento*) no buffer de comprimento/indicador. Ambos os valores indicam ao driver que os dados para o parâmetro serão enviados com **SQLPutData**. SQL_LEN_DATA_AT_EXEC (*Length*) é usado ao enviar dados longos para uma fonte de dados que precisa saber quantos bytes de dados longos serão enviados para que possa alocar espaço. Para determinar se uma fonte de dados requer esse valor, o aplicativo chama **SQLGetInfo** com a opção SQL_NEED_LONG_DATA_LEN. Todos os drivers devem dar suporte a essa macro; se a fonte de dados não exigir o comprimento do byte, o driver poderá ignorá-lo.  
  
4.  Chama **SQLExecute** ou **SQLExecDirect**. O driver descobre que um buffer de comprimento/indicador contém o valor SQL_DATA_AT_EXEC ou o resultado da macro SQL_LEN_DATA_AT_EXEC (*comprimento*) e retorna SQL_NEED_DATA como o valor de retorno da função.  
  
5.  Chama **SQLParamData** em resposta ao valor de retorno de SQL_NEED_DATA. Se for necessário enviar dados longos, **SQLParamData** retornará SQL_NEED_DATA. No buffer apontado pelo argumento *ValuePtrPtr* , o driver retorna o valor que identifica o parâmetro de dados em execução. Se houver mais de um parâmetro de dados em execução, o aplicativo deverá usar esse valor para determinar para qual parâmetro enviar dados; o driver não precisa solicitar dados para parâmetros de dados em execução em qualquer ordem específica.  
  
6.  Chama **SQLPutData** para enviar os dados de parâmetro para o driver. Se os dados do parâmetro não couberem em um único buffer, como geralmente é o caso com dados longos, o aplicativo chamará **SQLPutData** repetidamente para enviar os dados em partes; cabe ao driver e à fonte de dados remontar os dados. Se o aplicativo passar dados de cadeia de caracteres terminados em nulo, o driver ou a fonte de dados deverá remover o caractere de terminação nula como parte do processo de remontagem.  
  
7.  Chama **SQLParamData** novamente para indicar que ele enviou todos os dados para o parâmetro. Se houver parâmetros de dados em execução para os quais os dados não foram enviados, o driver retornará SQL_NEED_DATA e o valor que identificará o próximo parâmetro; o aplicativo retorna para a etapa 6. Se os dados forem enviados para todos os parâmetros de dados em execução, a instrução será executada. **SQLParamData** retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO e pode retornar qualquer valor de retorno ou diagnóstico que **SQLExecute** ou **SQLExecDirect** possa retornar.  
  
 Após **SQLExecute** ou **SQLExecDirect** retornar SQL_NEED_DATA e antes que os dados sejam completamente enviados para o último parâmetro de dados em execução, a instrução estará em um estado de dados necessário. Embora uma instrução esteja em um estado de dados necessário, o aplicativo pode chamar somente **SQLPutData**, **SQLParamData**, **SQLCancel**, **SQLGetDiagField**ou **SQLGetDiagRec**; todas as outras funções retornam SQLSTATE HY010 (erro de sequência de função). Chamar **SQLCancel** cancela a execução da instrução e a retorna ao estado anterior. Para obter mais informações, consulte o [Apêndice B: tabelas de transição de estado ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Para obter um exemplo de envio de dados em tempo de execução, consulte a descrição da função [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md) .

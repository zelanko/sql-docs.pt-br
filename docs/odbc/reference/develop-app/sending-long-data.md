---
title: Envio de Dados Longos | Microsoft Docs
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
ms.openlocfilehash: aeeeb716aa2f9a72338f3aeb586dffce86f84069
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304177"
---
# <a name="sending-long-data"></a>Enviar dados Long
DBMSs *definem dados longos* como qualquer caractere ou dados binários em um determinado tamanho, como 254 caracteres. Pode não ser possível armazenar um item inteiro de dados longos na memória, como quando o item representa um documento de texto longo ou um bitmap. Como esses dados não podem ser armazenados em um único buffer, a fonte de dados envia-os ao driver em partes com **SQLPutData** quando a declaração é executada. Os parâmetros para os quais os dados são enviados no momento da execução são conhecidos como *parâmetros de data-at-execution*.  
  
> [!NOTE]  
>  Um aplicativo pode realmente enviar qualquer tipo de dados no momento de execução com **SQLPutData**, embora apenas dados de caracteres e binários possam ser enviados em partes. No entanto, se os dados são pequenos o suficiente para caber em um único buffer, geralmente não há razão para usar **SQLPutData**. É muito mais fácil vincular o buffer e deixar o driver recuperar os dados do buffer.  
  
 Para enviar dados no momento da execução, o aplicativo executa as seguintes ações:  
  
1.  Passa um valor de 32 bits que identifica o parâmetro no argumento *ParameterValuePtr* no **SQLBindParameter** em vez de passar o endereço de um buffer. Esse valor não é analisado pelo motorista. Ele será devolvido ao aplicativo mais tarde, então deve significar algo para a aplicação. Por exemplo, pode ser o número do parâmetro ou a alça de um arquivo contendo dados.  
  
2.  Passa o endereço de um buffer de comprimento/indicador no *argumento StrLen_or_IndPtr* do **SQLBindParameter**.  
  
3.  Armazena SQL_DATA_AT_EXEC ou o resultado da macro*SQL_LEN_DATA_AT_EXEC(comprimento)* no buffer de comprimento/indicador. Ambos os valores indicam ao driver que os dados do parâmetro serão enviados com **SQLPutData**. *SQL_LEN_DATA_AT_EXEC(comprimento)* é usado ao enviar dados longos para uma fonte de dados que precisa saber quantos bytes de dados longos serão enviados para que ele possa prealocar espaço. Para determinar se uma fonte de dados requer esse valor, o aplicativo chama **SQLGetInfo** com a opção SQL_NEED_LONG_DATA_LEN. Todos os drivers devem suportar essa macro; se a fonte de dados não exigir o comprimento do byte, o driver pode ignorá-lo.  
  
4.  Chamadas **SQLExecute** ou **SQLExecDirect**. O driver descobre que um buffer de comprimento/indicador contém o valor SQL_DATA_AT_EXEC ou o resultado da macro de SQL_LEN_DATA_AT_EXEC*comprimento*e retorna SQL_NEED_DATA como o valor de retorno da função.  
  
5.  Chama **SQLParamData** em resposta ao valor de retorno SQL_NEED_DATA. Se os dados longos precisarem ser enviados, **o SQLParamData** retorna SQL_NEED_DATA. No buffer apontado pelo argumento *ValuePtrPtr,* o driver retorna o valor que identifica o parâmetro data-at-execution. Se houver mais de um parâmetro de dados em execução, o aplicativo deve usar esse valor para determinar para qual parâmetro enviar dados; o driver não é obrigado a solicitar dados para parâmetros de data-at-execution em qualquer ordem específica.  
  
6.  Chama **sqlPutData** para enviar os dados do parâmetro para o driver. Se os dados de parâmetros não se encaixam em um único buffer, como é frequentemente o caso com dados longos, o aplicativo chama **SQLPutData** repetidamente para enviar os dados em partes; cabe ao driver e à fonte de dados remontar os dados. Se o aplicativo passar dados de seqüência de caracteres com término nulo, o driver ou a fonte de dados devem remover o caractere de rescisão nula como parte do processo de remontagem.  
  
7.  Chama **o SQLParamData** novamente para indicar que enviou todos os dados para o parâmetro. Se houver parâmetros de execução de dados para os quais os dados não foram enviados, o driver retorna SQL_NEED_DATA e o valor que identifica o próximo parâmetro; o aplicativo retorna à etapa 6. Se os dados forem enviados para todos os parâmetros de execução de dados, a declaração será executada. **SQLParamData** retorna SQL_SUCCESS ou SQL_SUCCESS_WITH_INFO e pode retornar qualquer valor de retorno ou diagnóstico que **o SQLExecute** ou **o SQLExecDirect** possam retornar.  
  
 Depois **que SQLExecute** ou **SQLExecDirect** retornar SQL_NEED_DATA e antes que os dados sejam completamente enviados para o último parâmetro de dados em execução, a declaração está em um estado de Dados de Necessidade. Enquanto uma declaração estiver em um estado de Dados de Necessidade, o aplicativo pode chamar apenas **SQLPutData,** **SQLParamData,** **SQLCancel,** **SQLGetDiagField**ou **SQLGetDiagRec;** todas as outras funções retornam SQLSTATE HY010 (erro de seqüência de função). Chamar **o SQLCancel** cancela a execução da declaração e a devolve ao seu estado anterior. Para obter mais informações, consulte [o apêndice B: Tabelas de transição do estado oDBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
 Para obter um exemplo de envio de dados no momento da execução, consulte a descrição da função [SQLPutData.](../../../odbc/reference/syntax/sqlputdata-function.md)

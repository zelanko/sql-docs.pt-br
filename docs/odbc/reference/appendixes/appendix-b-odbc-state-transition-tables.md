---
title: 'Apêndice B: tabelas de transição de estado ODBC | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC]
- transitioning states [ODBC], about state transitions
- state transitions [ODBC], about state transitions
ms.assetid: 15088dbe-896f-4296-b397-02bb3d0ac0fb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7ceb128aec3a4cbe5ef7180483eb2a033ae57138
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67996245"
---
# <a name="appendix-b-odbc-state-transition-tables"></a>Apêndice B: Tabelas de transição de estado ODBC
As tabelas neste apêndice mostram como as funções ODBC causam transições do ambiente, da conexão, da instrução e dos Estados do descritor. O estado do ambiente, da conexão, da instrução ou do descritor geralmente determina quando as funções que usam o tipo de identificador correspondente (ambiente, conexão, instrução ou descritor) podem ser chamadas. Os Estados de ambiente, conexão, instrução e descritor se sobrepõem aproximadamente conforme mostrado nas ilustrações a seguir. Por exemplo, a sobreposição exata dos Estados de conexão C5 e C6 e os Estados de instrução S1 a S12 são dependentes da fonte de dados, pois as transações começam em momentos diferentes em diferentes fontes de dados e o estado do descritor D1i (descritor implicitamente alocado) depende no estado da instrução à qual o descritor está associado, enquanto o estado D1E (descritor explicitamente alocado) é independente do estado de qualquer instrução. Para obter uma descrição de cada Estado, consulte [transições de ambiente](../../../odbc/reference/appendixes/environment-transitions.md), [transições de conexão](../../../odbc/reference/appendixes/connection-transitions.md), [transições de instrução](../../../odbc/reference/appendixes/statement-transitions.md)e [transições de descritor](../../../odbc/reference/appendixes/descriptor-transitions.md), mais adiante neste apêndice.  
  
 Os Estados de ambiente e conexão se sobrepõem da seguinte maneira:  
  
 ![Os estados de ambiente e de conexão se sobrepõem](../../../odbc/reference/appendixes/media/app01.gif "app01")  
  
 Os Estados de conexão e instrução se sobrepõem da seguinte maneira:  
  
 ![Os estados de conexão e de instrução se sobrepõem](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 Os Estados da instrução e do descritor se sobrepõem da seguinte maneira:  
  
 ![Os estados de instrução e descrição se sobrepõem](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 Os Estados de conexão e descritor se sobrepõem da seguinte maneira:  
  
 ![Os estados de conexão e de descrição se sobrepõem](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 Cada entrada em uma tabela de transição pode ser um dos seguintes valores:  
  
-   **--**-O estado é inalterado após a execução da função.  
  
-   **Oriental**  

     **_n_** , **C_n_**, **S_n_** ou **D_n_** -o ambiente, a conexão, a instrução ou o estado do descritor se move para o estado especificado.  
 
-   **(IH)** -um identificador inválido foi passado para a função. Se o identificador era um identificador nulo ou era um identificador válido do tipo errado, por exemplo, um identificador de conexão foi passado quando um identificador de instrução era necessário-a função retorna SQL_INVALID_HANDLE; caso contrário, o comportamento será indefinido e provavelmente fatal. Esse erro é mostrado somente quando é o único resultado possível de chamar a função no estado especificado. Esse erro não altera o estado e é sempre detectado pelo Gerenciador de driver, conforme indicado pelos parênteses.  
  
-   **Ns** -estado seguinte. A transição de instrução é igual a se a instrução não tivesse passado pelos Estados assíncronos. Por exemplo, suponha que uma instrução que cria um conjunto de resultados Insira o estado S11 do Estado S1 porque **SQLExecDirect** retornou SQL_STILL_EXECUTING. A notação NS no estado S11 significa que as transições para a instrução são as mesmas para uma instrução no Estado S1 que cria um conjunto de resultados. Se **SQLExecDirect** retornar um erro, a instrução permanecerá no Estado S1; Se tiver sucesso, a instrução será movida para o estado S5; Se precisar de dados, a instrução será movida para o estado S8; e se ele ainda estiver em execução, ele permanecerá no estado S11.  

-   **_Xxxxx_** ou **(*xxxxx*)** -um SQLSTATE que está relacionado à tabela de transição; Sqlstates detectados pelo Gerenciador de driver são colocados entre parênteses. A função retornou SQL_ERROR e o SQLSTATE especificado, mas o estado não é alterado. Por exemplo, se **SQLExecute** for chamado antes de **SQLPrepare**, ele retornará SQLSTATE HY010 (erro de sequência de função).  

> [!NOTE]  
>  As tabelas não mostram erros não relacionados às tabelas de transição que não alteram o estado. Por exemplo, quando **SQLAllocHandle** é chamado no estado do ambiente E1 e retorna SQLSTATE HY001 (erro de alocação de memória), o ambiente permanece no estado E1; Isso não é mostrado na tabela de transição de ambiente para **SQLAllocHandle**.  
  
 Se o ambiente, a conexão, a instrução ou o descritor puder passar para mais de um estado, cada Estado possível será mostrado e uma ou mais notas de rodapé explicará as condições sob as quais cada transição ocorre. As seguintes notas de rodapé podem aparecer em qualquer tabela.  
  
|Rodapé|Significado|  
|--------------|-------------|  
|b|Antes ou depois. O cursor foi posicionado antes do início do conjunto de resultados ou após o final do conjunto de resultados.|  
|c|Função atual. A função atual estava sendo executada de forma assíncrona.|  
|d|Dados necessários. A função retornou SQL_NEED_DATA.|  
|e|Erro. A função retornou SQL_ERROR.|  
|i|Linha inválida. O cursor foi posicionado em uma linha no conjunto de resultados e a linha tinha sido excluída ou ocorreu um erro em uma operação na linha. Se a matriz de status de linha existir, o valor na matriz de status de linha para a linha foi SQL_ROW_DELETED ou SQL_ROW_ERROR. (A matriz de status de linha é apontada pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR.)|  
|NF|Não encontrado. A função retornou SQL_NO_DATA. Isso não se aplica quando **SQLExecDirect**, **SQLExecute**ou **SQLParamData** retorna SQL_NO_DATA depois de executar uma atualização pesquisada ou uma instrução DELETE.|  
|np|Não preparado. A instrução não foi preparada.|  
|NR|Nenhum resultado. A instrução não irá ou não criar um conjunto de resultados.|  
|o|Outra função. Outra função estava sendo executada de forma assíncrona.|  
|p|Preparado. A instrução foi preparada.|  
|r|Da. A instrução fará ou criará um conjunto de resultados (possivelmente vazio).|  
|s|Sucesso. A função retornou SQL_SUCCESS_WITH_INFO ou SQL_SUCCESS.|  
|v|Linha válida. O cursor foi posicionado em uma linha no conjunto de resultados e a linha foi inserida com êxito, atualizada com êxito ou outra operação na linha foi concluída com êxito. Se a matriz de status de linha existir, o valor na matriz de status de linha para a linha foi SQL_ROW_ADDED, SQL_ROW_SUCCESS ou SQL_ROW_UPDATED. (A matriz de status de linha é apontada pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR.)|  
|x|Em execução. A função retornou SQL_STILL_EXECUTING.|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 Neste exemplo, a linha na tabela de transição de estado do ambiente para **SQLFreeHandle** quando *handletype* é SQL_HANDLE_ENV é a seguinte.  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Reserva|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|Ih|E0|(HY010)|  
  
 Se **SQLFreeHandle** for chamado no estado do ambiente E0 com *HandleType* definido como SQL_HANDLE_ENV, o gerenciador de driver retornará SQL_INVALID_HANDLE. Se for chamado no estado E1 com *HandleType* definido como SQL_HANDLE_ENV, o ambiente se moverá para o estado E0 se a função for bem-sucedida e permanecerá no estado E1 se a função falhar. Se for chamado no estado E2 com *HandleType* definido como SQL_HANDLE_ENV, o Gerenciador de driver sempre retornará SQL_ERROR e SQLSTATE HY010 (erro de sequência de função) e o ambiente permanecerá no estado E2.  
  
 Para entender as tabelas de transição de estado, é necessário entender o item (ambiente, conexão, instrução ou descritor) ao qual se referem. Suponha que uma função aceite o identificador de um item do tipo X. A tabela de transição de estado X para essa função descreve como chamar a função, com o identificador de um item do tipo X, afeta esse item. Por exemplo, **SQLDisconnect** aceita um identificador de conexão. A tabela de transição de estado de conexão para **SQLDisconnect** descreve como o **SQLDisconnect** afeta o estado da conexão para a qual ele é chamado.  
  
 Suponha que uma função aceite o identificador de um item do tipo Y, em que Y não é igual a X. A tabela de transição de estado X para essa função descreve como chamar a função, com um identificador do tipo X que está associado ao item do tipo Y, afeta o item do tipo Y. Por exemplo, a instrução de tabela de transição de estado para **SQLDisconnect** descreve como o **SQLDisconnect** afeta o estado de uma instrução quando chamado com o identificador da conexão com a qual a instrução está associada.  
  
 Este apêndice contém os tópicos a seguir.  
  
-   [Transições de ambiente](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [Transições de conexão](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [Transições de instrução](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [Transições de descritor](../../../odbc/reference/appendixes/descriptor-transitions.md)

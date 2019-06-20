---
title: 'Apêndice B: Tabelas de transição de estado ODBC | Microsoft Docs'
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
manager: craigg
ms.openlocfilehash: 82c19931073aa96eb045f574e8670068f3d3c659
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63026868"
---
# <a name="appendix-b-odbc-state-transition-tables"></a>Apêndice B: Tabelas de transição de estado ODBC
As tabelas neste apêndice mostram como funções ODBC causam transições do ambiente, conexão, instrução e estados do descritor. O estado do ambiente, conexão, instrução ou descritor geralmente determina quando as funções que usam o tipo correspondente do identificador (ambiente, conexão, instrução ou descritor) podem ser chamadas. Os estados de ambiente, conexão, instrução e descritor se sobrepor aproximadamente conforme mostrado nas ilustrações a seguir. Por exemplo, a sobreposição exata da conexão declara C5 e C6 e estados de instrução que S1 por meio de S12 é dependente da fonte, dados uma vez que as transações começam em momentos diferentes em diferentes fontes de dados, e depende do estado de descritor D1i (implicitamente alocados descritor) sobre o estado da instrução ao qual o descritor está associado, enquanto o estado D1e (descritor alocado explicitamente) é independente do estado de qualquer instrução. Para obter uma descrição de cada estado, consulte [transições de ambiente](../../../odbc/reference/appendixes/environment-transitions.md), [transições de Conexão](../../../odbc/reference/appendixes/connection-transitions.md), [transições de instrução](../../../odbc/reference/appendixes/statement-transitions.md), e [transições de descritor ](../../../odbc/reference/appendixes/descriptor-transitions.md), mais adiante neste apêndice.  
  
 Os estados de ambiente e conexão se sobrepõem da seguinte maneira:  
  
 ![Estados de ambiente e conexão se sobrepõem](../../../odbc/reference/appendixes/media/app01.gif "app01")  
  
 Os estados de conexão e instrução se sobrepõem da seguinte maneira:  
  
 ![Estados de Conexão e instrução se sobrepõem](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 Os estados de instrução e descrição se sobrepõem da seguinte maneira:  
  
 ![Estados de instrução e descrição se sobrepõem](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 Os estados de conexão e o descritor se sobrepõem da seguinte maneira:  
  
 ![Estados de Conexão e o descritor se sobrepõem](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 Cada entrada em uma tabela de transição pode ser um dos seguintes valores:  
  
-   **--** -O estado permanece inalterado após a execução da função.  
  
-   **E**  

     **_n_**  , **C_n_** , **S_n_** , ou **D_n_** -o estado do ambiente, conexão, instrução ou descritor se move para o estado especificado.  
 
-   **(IH)**  -Um identificador inválido foi passado para a função. Se o identificador era um identificador nulo ou era um identificador válido do tipo errado - por exemplo, um identificador de conexão foi passado quando um identificador de instrução era necessário – a função retorne SQL_INVALID_HANDLE; Caso contrário, o comportamento é indefinido e provavelmente fatal. Esse erro é mostrado somente quando ele é o resultado só é possível chamar a função no estado especificado. Esse erro não altera o estado e sempre é detectado pelo Gerenciador de Driver, conforme indicado pelos parênteses.  
  
-   **NS** -próximo estado. A transição de instrução é o mesmo como se a instrução não fui por meio dos Estados assíncronos. Por exemplo, suponha que uma instrução que cria um conjunto de resultados entra em estado S11 de estado S1 porque **SQLExecDirect** retornado SQL_STILL_EXECUTING. A notação de NS no estado S11 significa que as transições para a instrução são os mesmos para uma instrução no estado S1 que cria um conjunto de resultados. Se **SQLExecDirect** retornará um erro, a instrução permanece no estado S1; se for bem-sucedida, a instrução move para o estado S5; se precisar de dados, a instrução move para o estado S8; e se ele ainda está em execução, ele permanecerá no estado S11.  

-   **_XXXXX_**  ou **(*XXXXX*)** - uma SQLSTATE está relacionada à tabela de transição; SQLSTATEs detectadas pelo Gerenciador de Driver são colocados entre parênteses. A função retornado SQL_ERROR e o SQLSTATE especificado, mas não altera o estado. Por exemplo, se **SQLExecute** é chamado antes **SQLPrepare**, ele retornará SQLSTATE HY010 (erro de sequência de função).  

> [!NOTE]  
>  As tabelas não mostram erros não relacionados com as tabelas de transição que não alteram o estado. Por exemplo, quando **SQLAllocHandle** é chamado no estado do ambiente E1 e retornará SQLSTATE HY001 (erro de alocação de memória), o ambiente permanece no estado E1; isso não é mostrado na tabela de transição de ambiente para  **Falha de SQLAllocHandle**.  
  
 Se o ambiente, a conexão, a instrução ou o descritor pode mover para mais de um estado, cada estado possível é mostrado e um ou mais rodapés explicam as condições sob as quais cada transição ocorre. As seguintes notas de rodapé podem aparecer em qualquer tabela.  
  
|Nota de rodapé|Significado|  
|--------------|-------------|  
|b|Antes ou depois. O cursor é posicionado antes do início do conjunto de resultados ou após o final do conjunto de resultados.|  
|c|Função atual. A função atual estava em execução de forma assíncrona.|  
|d|Precisa de dados. A função retornou SQL_NEED_DATA.|  
|e|Erro. A função retornou SQL_ERROR.|  
|i|Linha inválida. O cursor é posicionado em uma linha no resultado do conjunto e a linha tinham sido excluídos ou ocorreu um erro em uma operação na linha. Se a matriz de status de linha existia, o valor na matriz de status de linha para a linha era SQL_ROW_DELETED ou SQL_ROW_ERROR. (A matriz de status de linha é apontada pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR.)|  
|nf|Não foi encontrado. A função retornar SQL_NO_DATA. Isso não se aplica quando **SQLExecDirect**, **SQLExecute**, ou **SQLParamData** retorna SQL_NO_DATA após a execução de um pesquisada instrução update ou delete.|  
|np|Não preparado. A instrução não foi preparada.|  
|nr|Nenhum resultado. A instrução não irá ou não tiver criado um conjunto de resultados.|  
|o|Outra função. Outra função estava em execução de forma assíncrona.|  
|p|Preparado. A instrução foi preparada.|  
|r|Resultados. A instrução será ou criar um conjunto de resultados (possivelmente vazia).|  
|s|Sucesso. A função retornou SQL_SUCCESS_WITH_INFO ou SQL_SUCCESS.|  
|v|Linha válida. O cursor é posicionado em uma linha no conjunto de resultados e a linha tivesse sido inserida com êxito, atualizada com êxito, ou outra operação na linha foi concluída com êxito. Se a matriz de status de linha existia, o valor na matriz de status de linha para a linha era SQL_ROW_ADDED, SQL_ROW_SUCCESS ou SQL_ROW_UPDATED. (A matriz de status de linha é apontada pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR.)|  
|x|Em execução. A função retornou SQL_STILL_EXECUTING.|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 Neste exemplo, a linha em que a transição de estado do ambiente de tabela para **SQLFreeHandle** quando *HandleType* é SQL_HANDLE_ENV é da seguinte maneira.  
  
|E0<br /><br /> Não alocado|E1<br /><br /> alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH)|E0|(HY010)|  
  
 Se **SQLFreeHandle** é chamado no estado do ambiente E0 com *HandleType* definido como SQL_HANDLE_ENV, o Gerenciador de Driver retorne SQL_INVALID_HANDLE. Se for chamado no estado E1 com *HandleType* definido como SQL_HANDLE_ENV, o ambiente se move para o estado E0 se a função for bem-sucedida e permanecerá no estado E1 se a função falhar. Se for chamado no estado E2 com *HandleType* definido como SQL_HANDLE_ENV, o Gerenciador de Driver sempre retornará SQL_ERROR e SQLSTATE HY010 (erro de sequência de função) e o ambiente permanece no estado E2.  
  
 Para entender as tabelas de transição de estado, é necessário entender qual item (ambiente, conexão, instrução ou descritor) referem-se. Suponha que uma função aceita o identificador de um item do tipo X. A tabela de transição de estado de X para a função descreve afeta a função, com o identificador de um item do tipo X, como chamada esse item. Por exemplo, **SQLDisconnect** aceita um identificador de conexão. A tabela de transição de estado de conexão para **SQLDisconnect** descreve como **SQLDisconnect** afeta o estado da conexão para o qual ele é chamado.  
  
 Suponha que uma função aceita o identificador de um item do tipo Y, onde Y não é igual a X. A tabela de transição de estado de X para a função descreve como chamar a função, com um identificador de tipo X que está associado com o item do tipo Y, afetar o item do tipo Y. Por exemplo, a instrução transição tabela de estado para **SQLDisconnect** descreve como **SQLDisconnect** afeta o estado de uma instrução quando chamado com o identificador da conexão com o qual o instrução está associada.  
  
 Este apêndice contém os tópicos a seguir.  
  
-   [Transições de ambiente](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [Transições de conexão](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [Transições de instrução](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [Transições de descritor](../../../odbc/reference/appendixes/descriptor-transitions.md)

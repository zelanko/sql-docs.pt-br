---
title: 'Apêndice b: tabelas de transição de estado ODBC | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC]
- transitioning states [ODBC], about state transitions
- state transitions [ODBC], about state transitions
ms.assetid: 15088dbe-896f-4296-b397-02bb3d0ac0fb
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a0d114dd574faf2909fa200f7c24ab0ccaa07804
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913891"
---
# <a name="appendix-b-odbc-state-transition-tables"></a>Apêndice b: tabelas de transição de estado de ODBC
As tabelas neste apêndice mostram como funções ODBC causam transições do ambiente, conexão, instrução e estados do descritor. O estado do ambiente, conexão, instrução ou descritor geralmente determina quando as funções que usam o tipo de identificador (ambiente, conexão, instrução ou descritor) correspondente podem ser chamadas. Os estados de ambiente, conexão, instrução e descritor se sobrepor aproximadamente conforme mostrado nas ilustrações a seguir. Por exemplo, a sobreposição exata de conexão estados C5 e C6 e estados de instrução que S1 por meio de /s12 é – dependente, da fonte de dados, pois transações começam em momentos diferentes com diferentes fontes de dados, e depende do estado de descritor D1i (descritor alocado implicitamente) sobre o estado da instrução ao qual o descritor está associado, ao estado D1e (explicitamente alocados descritor) é independente do estado de qualquer instrução. Para obter uma descrição de cada estado, consulte [ambiente transições](../../../odbc/reference/appendixes/environment-transitions.md), [Conexão transições](../../../odbc/reference/appendixes/connection-transitions.md), [transições de instrução](../../../odbc/reference/appendixes/statement-transitions.md), e [transições do descritor ](../../../odbc/reference/appendixes/descriptor-transitions.md), mais adiante neste apêndice.  
  
 Os estados de ambiente e conexão sobreponham da seguinte maneira:  
  
 ![Sobreposição de estados de ambiente e conexão](../../../odbc/reference/appendixes/media/app01.gif "app01")  
  
 Os estados de conexão e instrução se sobrepõem da seguinte maneira:  
  
 ![Sobreposição de estados de Conexão e instrução](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 Os estados de instrução e descrição se sobrepõem da seguinte maneira:  
  
 ![Sobreposição de estados de instrução e descritor](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 Os estados de conexão e descritor sobreponham da seguinte maneira:  
  
 ![Sobreposição de estados de Conexão e o descritor de](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 Cada entrada em uma tabela de transição pode ser um dos seguintes valores:  
  
-   **--** – O estado é alterado depois de executar a função.  
  
-   **E**  
     ***n*** , **C*n * **S*n * **, ou **D * n***  — o estado do ambiente, conexão, instrução ou descritor move para o estado especificado.  
  
-   **(IH)**  — Um identificador inválido foi passado para a função. Se o identificador de um identificador nulo ou um identificador válido do tipo errado — por exemplo, um identificador de conexão foi passado quando um identificador de instrução era necessário, a função retorna SQL_INVALID_HANDLE; Caso contrário, o comportamento é indefinido e provavelmente fatal. Esse erro é mostrado apenas quando ele é o resultado só é possível chamar a função no estado especificado. Esse erro não altera o estado e sempre é detectado pelo Gerenciador de Driver, conforme indicado por parênteses.  
  
-   **NS** — próximo estado. A transição de instrução é o mesmo como se a instrução não tenham ido pelos estados assíncronos. Por exemplo, suponha que uma instrução que cria um conjunto de resultados entra em estado de S11 de estado S1 porque **SQLExecDirect** retornou SQL_STILL_EXECUTING. A notação de NS no estado S11 significa que as transições de instrução são iguais às de uma instrução no estado S1 que cria um conjunto de resultados. Se **SQLExecDirect** retorna um erro, a instrução permanece no estado S1; se for bem-sucedida, a instrução move para o estado S5; se precisar de dados, a instrução move para o estado S8; e se ele ainda está em execução, ele permanecerá no estado S11.  
  
-   ***XXXXX*** ou **(*XXXXX*)** — um SQLSTATE que está relacionada à tabela de transição; SQLSTATEs detectados pelo Gerenciador de Driver são colocados entre parênteses. A função retornou SQL_ERROR e o SQLSTATE especificado, mas não altera o estado. Por exemplo, se **SQLExecute** é chamado antes de **SQLPrepare**, ele retornará SQLSTATE HY010 (erro de sequência de função).  
  
> [!NOTE]  
>  As tabelas não mostram erros não relacionados para as tabelas de transição que não alteram o estado. Por exemplo, quando **SQLAllocHandle** é chamado no estado do ambiente E1 e retornará SQLSTATE HY001 (erro de alocação de memória), o ambiente permanece no estado E1; isso não é mostrado na tabela de transição de ambiente para  **SQLAllocHandle**.  
  
 Se o ambiente, conexão, instrução ou descritor pode mover a mais de um estado, cada estado possível é mostrado e um ou mais rodapés explicam as condições sob as quais cada transição ocorre. As seguintes notas de rodapé podem aparecer em qualquer tabela.  
  
|Nota de rodapé|Significado|  
|--------------|-------------|  
|b|Antes ou depois. O cursor é posicionado antes do início do conjunto de resultados ou após o final do conjunto de resultados.|  
|c|Função atual. A função atual foi execução assíncrona.|  
|d|Precisa de dados. A função retornou SQL_NEED_DATA.|  
|e|Erro. A função retornou SQL_ERROR.|  
|i|Linha inválida. O cursor é posicionado em uma linha no resultado do conjunto e ou a linha foi excluídos ou ocorreu um erro em uma operação na linha. Se a matriz de status de linha existia, o valor na matriz de status de linha para a linha foi SQL_ROW_DELETED ou SQL_ROW_ERROR. (A matriz de status de linha é apontada pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR.)|  
|NF|Não foi encontrado. A função retornar SQL_NO_DATA. Isso não se aplica quando **SQLExecDirect**, **SQLExecute**, ou **SQLParamData** retorna SQL_NO_DATA depois de executar uma pesquisa instrução update ou delete.|  
|np|Não preparado. Não foi possível preparar a instrução.|  
|nr|Nenhum resultado. A instrução não será ou não criou um conjunto de resultados.|  
|o|Outra função. Outra função estava sendo executado de forma assíncrona.|  
|p|Preparado. A instrução foi preparada.|  
|r|Resultados. A instrução será ou criar um conjunto de resultados (possivelmente vazia).|  
|s|Sucesso. A função retornou SQL_SUCCESS_WITH_INFO ou SQL_SUCCESS.|  
|v|Linha válida. O cursor é posicionado em uma linha no conjunto de resultados e a linha tivesse sido inserida com êxito, atualizada com êxito, ou outra operação na linha tinha sido concluída com êxito. Se a matriz de status de linha existia, o valor na matriz de status de linha para a linha foi SQL_ROW_ADDED, SQL_ROW_SUCCESS ou SQL_ROW_UPDATED. (A matriz de status de linha é apontada pelo atributo de instrução SQL_ATTR_ROW_STATUS_PTR.)|  
|x|Em execução. A função retornou SQL_STILL_EXECUTING.|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 Neste exemplo, a linha de transição de estado do ambiente de tabela para **SQLFreeHandle** quando *HandleType* é SQL_HANDLE_ENV é da seguinte maneira.  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH)|E0|(HY010)|  
  
 Se **SQLFreeHandle** é chamado no estado do ambiente E0 com *HandleType* definido como SQL_HANDLE_ENV, o Gerenciador de Driver retorne SQL_INVALID_HANDLE. Se for chamado no estado E1 com *HandleType* definido como SQL_HANDLE_ENV, o ambiente move para o estado E0 se a função tiver êxito e permanece em estado E1 se a função falhará. Se for chamado no estado E2 com *HandleType* definido como SQL_HANDLE_ENV, o Gerenciador de Driver sempre retornará SQL_ERROR e SQLSTATE HY010 (erro de sequência de função) e o ambiente permanece no estado E2.  
  
 Para entender as tabelas de transição de estado, é necessário entender qual item (ambiente, conexão, instrução ou descritor) se referem. Suponha que uma função aceita o identificador de um item do tipo X. A tabela de transição de estado de X para essa função descreve como chamar a função, com o identificador de um item do tipo X, afeta esse item. Por exemplo, **SQLDisconnect** aceita um identificador de conexão. A tabela de transição de estado de conexão **SQLDisconnect** descreve como **SQLDisconnect** afeta o estado da conexão para o qual ele é chamado.  
  
 Suponha que uma função aceita o identificador de um item do tipo Y, onde Y não é igual a X. A tabela de transição de estado de X para essa função descreve como chamar a função, com um identificador do tipo X que é associado ao item do tipo Y, afeta o item do tipo Y. Por exemplo, a instrução transição tabela de estado **SQLDisconnect** descreve como **SQLDisconnect** afeta o estado de uma instrução quando chamado com o identificador da conexão com a qual o instrução está associada.  
  
 Este apêndice contém os tópicos a seguir.  
  
-   [Transições de ambiente](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [Transições de conexão](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [Transições de instrução](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [Transições de descritor](../../../odbc/reference/appendixes/descriptor-transitions.md)

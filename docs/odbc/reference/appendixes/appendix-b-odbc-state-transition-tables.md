---
title: 'Apêndice B: Tabelas de Transição do Estado ODBC | Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: db20c492ababbe6bf8f065fce88067c643f2694d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302880"
---
# <a name="appendix-b-odbc-state-transition-tables"></a>Apêndice B: Tabelas de transição de estado ODBC
As tabelas deste apêndice mostram como as funções do ODBC causam transições dos estados ambientais, de conexão, de declaração e de descritores. O estado do ambiente, conexão, instrução ou descritor geralmente dita quando funções que usam o tipo correspondente de alça (ambiente, conexão, declaração ou descritor) podem ser chamadas. Os estados de ambiente, conexão, declaração e descritor se sobrepõem aproximadamente como mostrado nas ilustrações a seguir. Por exemplo, a sobreposição exata dos estados de conexão C5 e C6 e afirma que S1 por S12 é dependente da fonte de dados, uma vez que as transações começam em diferentes momentos em diferentes fontes de dados, e o estado descritor D1i (descritor implícito) depende do estado da declaração com o qual o descritor está associado, enquanto o D1e estadual (descritor explicitamente alocado) é independente do estado de qualquer declaração. Para obter uma descrição de cada estado, consulte [Transições do Ambiente,](../../../odbc/reference/appendixes/environment-transitions.md) [Transições de Conexão,](../../../odbc/reference/appendixes/connection-transitions.md) [Transições de Declaração](../../../odbc/reference/appendixes/statement-transitions.md)e [Transições de Descritor,](../../../odbc/reference/appendixes/descriptor-transitions.md)mais tarde neste apêndice.  
  
 Os estados de ambiente e conexão se sobrepõem da seguinte forma:  
  
 ![Os estados de ambiente e de conexão se sobrepõem](../../../odbc/reference/appendixes/media/app01.gif "app01")  
  
 Os estados de conexão e declaração se sobrepõem da seguinte forma:  
  
 ![Os estados de conexão e de instrução se sobrepõem](../../../odbc/reference/appendixes/media/app02.gif "app02")  
  
 A declaração e os estados descritores se sobrepõem da seguinte forma:  
  
 ![Os estados de instrução e descrição se sobrepõem](../../../odbc/reference/appendixes/media/app03.gif "app03")  
  
 Os estados de conexão e descritor se sobrepõem da seguinte forma:  
  
 ![Os estados de conexão e de descrição se sobrepõem](../../../odbc/reference/appendixes/media/app04.gif "app04")  
  
 Cada entrada em uma tabela de transição pode ser um dos seguintes valores:  
  
-   **--**- O estado fica inalterado após a execução da função.  
  
-   **E**  

     **_n_** , **C_n_**, **S_n_** ou **D_n_** - O ambiente, conexão, declaração ou estado descritor passa para o estado especificado.  
 
-   **(IH)** - Uma alça inválida foi passada para a função. Se a alça era uma alça nula ou era uma alça válida do tipo errado - por exemplo, uma alça de conexão foi passada quando uma alça de declaração foi necessária - a função retorna SQL_INVALID_HANDLE; caso contrário, o comportamento é indefinido e provavelmente fatal. Este erro é mostrado somente quando é o único resultado possível de chamar a função no estado especificado. Esse erro não altera o estado e é sempre detectado pelo Driver Manager, conforme indicado pelos parênteses.  
  
-   **NS** - Próximo Estado. A transição da declaração é a mesma que se a declaração não tivesse passado pelos estados assíncronos. Por exemplo, suponha que uma declaração que crie um conjunto de resultados entra no estado S11 do estado S1 porque **o SQLExecDirect** retornou SQL_STILL_EXECUTING. A notação NS no estado S11 significa que as transições para a declaração são as mesmas de uma declaração no estado S1 que cria um conjunto de resultados. Se **o SQLExecDirect** retornar um erro, a declaração permanece no estado S1; se for bem sucedido, a declaração passa para o estado S5; se precisar de dados, a declaração passa para o estado S8; e se ainda estiver executando, permanece no estado S11.  

-   **_XXXXX_** ou **(*XXXXX*)** - Um SQLSTATE que está relacionado à tabela de transição; Os SQLSTATEs detectados pelo Driver Manager são fechados entre parênteses. A função retornou SQL_ERROR e o SQLSTATE especificado, mas o estado não muda. Por exemplo, se **sQLExecute** for chamado antes **do SQLPrepare,** ele retorna SQLSTATE HY010 (erro de seqüência de funções).  

> [!NOTE]  
>  As tabelas não mostram erros não relacionados às tabelas de transição que não alteram o estado. Por exemplo, quando **o SQLAllocHandle** é chamado no estado ambiente E1 e retorna SQLSTATE HY001 (erro de alocação de memória), o ambiente permanece no estado E1; isso não é mostrado na tabela de transição de ambiente para **SQLAllocHandle**.  
  
 Se o ambiente, conexão, declaração ou descritor puderem se mover para mais de um estado, cada estado possível é mostrado e uma ou mais notas de rodapé explicam as condições em que cada transição ocorre. As seguintes notas de rodapé podem aparecer em qualquer tabela.  
  
|Nota|Significado|  
|--------------|-------------|  
|b|Antes ou depois. O cursor foi posicionado antes do início do conjunto de resultados ou após o término do conjunto de resultados.|  
|c|Função atual. A função atual estava sendo executada assíncronamente.|  
|d|Preciso de dados. A função retornou SQL_NEED_DATA.|  
|e|Erro. A função retornou SQL_ERROR.|  
|i|Linha inválida. O cursor foi posicionado em uma linha no conjunto de resultados e ou a linha foi excluída ou um erro ocorreu em uma operação na linha. Se a matriz de status da linha existisse, o valor na matriz de status da linha para a linha seria SQL_ROW_DELETED ou SQL_ROW_ERROR. (A matriz de status da linha é apontada pelo atributo de declaração SQL_ATTR_ROW_STATUS_PTR.)|  
|nf|Não encontrado. A função retornou SQL_NO_DATA. Isso não se aplica quando **SQLExecDirect,** **SQLExecute**ou **SQLParamData** retornar SQL_NO_DATA após a execução de uma declaração de atualização ou exclusão pesquisada.|  
|np|Não está preparado. A declaração não foi preparada.|  
|nr|Sem resultados. A declaração não criará ou não um conjunto de resultados.|  
|o|Outra função. Outra função era executar assíncronamente.|  
|p|Preparado. A declaração foi preparada.|  
|r|Resultados. A declaração irá ou criou um conjunto de resultados (possivelmente vazio).|  
|s|Sucesso. A função retornou SQL_SUCCESS_WITH_INFO ou SQL_SUCCESS.|  
|v|Linha válida. O cursor foi posicionado em uma linha no conjunto de resultados, e a linha foi inserida com sucesso, atualizada com sucesso ou outra operação na linha foi concluída com sucesso. Se a matriz de status da linha existisse, o valor na matriz de status da linha para a linha seria SQL_ROW_ADDED, SQL_ROW_SUCCESS ou SQL_ROW_UPDATED. (A matriz de status da linha é apontada pelo atributo de declaração SQL_ATTR_ROW_STATUS_PTR.)|  
|x|Em execução. A função voltou SQL_STILL_EXECUTING.|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 Neste exemplo, a tabela de transição do estado do ambiente para **SQLFreeHandle** quando *handleType* é SQL_HANDLE_ENV é a seguinte.  
  
|E0<br /><br /> Não alocado|E1<br /><br /> Alocado|E2<br /><br /> Conexão|  
|------------------------|----------------------|-----------------------|  
|(IH)|E0|(HY010)|  
  
 Se **o SQLFreeHandle** for chamado no estado de ambiente E0 com *handleType* definido para SQL_HANDLE_ENV, o Gerenciador de driver retorna SQL_INVALID_HANDLE. Se for chamado no estado E1 com *handleType* definido para SQL_HANDLE_ENV, o ambiente se move para o estado E0 se a função for bem sucedida e permanecer no estado E1 se a função falhar. Se for chamado no estado E2 com *handleType* definido para SQL_HANDLE_ENV, o Driver Manager sempre retorna SQL_ERROR e SQLSTATE HY010 (erro de seqüência de função) e o ambiente permanece no estado E2.  
  
 Para entender as tabelas de transição de estado, é necessário entender a qual item (ambiente, conexão, declaração ou descritor) eles se referem. Suponha que uma função aceite a alça de um item do tipo X. A tabela de transição do estado X para essa função descreve como chamar a função, com o punho de um item do tipo X, afeta esse item. Por exemplo, **o SQLDisconnect** aceita uma alça de conexão. A tabela de transição de estado de conexão para **SQLDisconnect** descreve como o **SQLDisconnect** afeta o estado da conexão para a qual é chamada.  
  
 Suponha que uma função aceite a alça de um item do tipo Y, onde Y não é igual a X. A tabela de transição do estado X para essa função descreve como chamar a função, com uma alça do tipo X que está associada ao item do tipo Y, afeta o item do tipo Y. Por exemplo, a tabela de transição de estado de declaração para **SQLDisconnect** descreve como o **SQLDisconnect** afeta o estado de uma declaração quando chamado com a alça da conexão com a qual a declaração está associada.  
  
 Este apêndice contém os seguintes tópicos.  
  
-   [Transições de ambiente](../../../odbc/reference/appendixes/environment-transitions.md)  
  
-   [Transições de conexão](../../../odbc/reference/appendixes/connection-transitions.md)  
  
-   [Transições de instrução](../../../odbc/reference/appendixes/statement-transitions.md)  
  
-   [Transições de descritor](../../../odbc/reference/appendixes/descriptor-transitions.md)

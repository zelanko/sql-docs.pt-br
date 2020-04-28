---
title: Função SQLRateConnection | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLRateConnection function [ODBC]
ms.assetid: e8da2ffb-d6ef-4ca7-824f-57afd29585d8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d29033460a7f89fc4a8b1c371a4d32bdf94a2a05
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288876"
---
# <a name="sqlrateconnection-function"></a>Função SQLRateConnection
**Conformidade**  
 Versão introduzida: conformidade de padrões do ODBC 3,81: ODBC  
  
 **Resumo**  
 **SQLRateConnection** determina se um driver pode reutilizar uma conexão existente no pool de conexões.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
  
SQLRETURN  SQLRateConnection(  
                SQLHDBC_INFO_TOKEN   hRequest,  
                SQLHDBC              hCandidateConnection,  
                BOOL                 fRequiredTransactionEnlistment,  
                TRANSID              transId,  
                DWORD *              pRating );  
```  
  
## <a name="arguments"></a>Argumentos  
 *hRequest*  
 Entrada Um identificador de token que representa a nova solicitação de conexão de aplicativo.  
  
 *hCandidateConnection*  
 Entrada A conexão existente no pool de conexões. A conexão deve estar em um estado aberto.  
  
 *fRequiredTransactionEnlistment*  
 Entrada Se for TRUE, reutilizar o *hCandidateConnection* da conexão existente para a nova solicitação de conexão (*hRequest*) exigirá uma inscrição adicional.  
  
 *transid*  
 Entrada Se *fRequiredTransactionEnlistment* for true, *transid* representará a transação do DTC que a solicitação irá inscrever. Se *fRequiredTransactionEnlistment* for false, *transid* será ignorado.  
  
 *pRating*  
 Der a classificação de reutilização do *hCandidateConnection*para o *hRequest*. Essa classificação estará entre 0 e 100 (inclusivo).  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 O Gerenciador de driver não processará as informações de diagnóstico retornadas dessa função.  
  
## <a name="remarks"></a>Comentários  
 **SQLRateConnection** produz uma pontuação entre 0 e 100 (inclusivo) indicando quão bem uma conexão existente corresponde à solicitação.  
  
|Pontuação|Significado (quando SQL_SUCCESS é retornado)|  
|-----------|-----------------------------------------------|  
|0|*hCandidateConnection* não deve ser reutilizado para o *hRequest*.|  
|Quaisquer valores entre 1 e 98 (inclusivo)|Quanto maior a pontuação, mais próximo que *hCandidateConnection* corresponde a *hRequest*.|  
|99|Há apenas incompatibilidades em atributos insignificantes.  O Gerenciador de driver deve parar o loop de classificação.|  
|100|Correspondência perfeita.  O Gerenciador de driver deve parar o loop de classificação.|  
|Qualquer outro valor maior que 100|*hCandidateConnection* é marcado como Dead e não será reutilizado mesmo em uma solicitação de conexão futura.|  
  
 O Gerenciador de driver marcará uma conexão como inativa se o código de retorno for algo diferente de SQL_SUCCESS (incluindo SQL_SUCCESS_WITH_INFO) ou a classificação for maior que 100. Essa conexão inativa não será reutilizada (mesmo em solicitações de conexão futuras) e eventualmente expirará após o CPTimeout passar. O Gerenciador de driver continuará a encontrar outra conexão do pool a ser avaliada.  
  
 Se o Gerenciador de driver reutilizou uma conexão cuja Pontuação é estritamente menor que 100 (incluindo 99), o Gerenciador de driver chamará SQLSetConnectAttr (SQL_ATTR_DBC_INFO_TOKEN) para redefinir a conexão de volta para o estado solicitado pelo aplicativo. O driver não deve redefinir a conexão nesta chamada de função.  
  
 Se *fRequiredTransactionEnlistment* for true, reutilizar *hCandidateConnection* precisará de uma inscrição extra (*transid* ! = NULL) ou de canalistação (*transid* = = NULL). Isso indica o custo de reutilizar uma conexão e se o driver deve inscrever/desinscrever a conexão se ela for reutilizar a conexão. Se *fRequireTransactionEnlistment* for false, o driver deverá ignorar o valor de *transid*.  
  
 O Gerenciador de driver garante que o identificador HENV pai de *hRequest* e *hCandidateConnection* sejam os mesmos. O Gerenciador de driver garante que a ID do pool associada a *hRequest* e *hCandidateConnection* sejam iguais.  
  
 Os aplicativos não devem chamar essa função diretamente. Um driver ODBC que dá suporte ao pool de conexões com reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi. h para o desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)

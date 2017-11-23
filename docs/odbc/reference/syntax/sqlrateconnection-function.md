---
title: "Função SQLRateConnection | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLRateConnection function [ODBC]
ms.assetid: e8da2ffb-d6ef-4ca7-824f-57afd29585d8
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e63a6312a6f4b637d13282e25311204ea3879fd5
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sqlrateconnection-function"></a>Função SQLRateConnection
**Conformidade**  
 Versão introduzidas: Conformidade de padrões 3.81 ODBC: ODBC  
  
 **Resumo**  
 **SQLRateConnection** determina se um driver pode reutilizar uma conexão existente no pool de conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SQLRETURN  SQLRateConnection(  
                SQLHDBC_INFO_TOKEN   hRequest,  
                SQLHDBC              hCandidateConnection,  
                BOOL                 fRequiredTransactionEnlistment,  
                TRANSID              transId,  
                DWORD *              pRating );  
```  
  
## <a name="arguments"></a>Argumentos  
 *hRequest*  
 [Entrada] Um identificador de token que representa a nova solicitação de conexão do aplicativo.  
  
 *hCandidateConnection*  
 [Entrada] A conexão existente no pool de conexão. A conexão deve estar em um estado aberto.  
  
 *fRequiredTransactionEnlistment*  
 [Entrada] Se for TRUE, a reutilização da conexão existente *hCandidateConnection* para a nova solicitação de conexão (*hRequest*) requer uma inscrição adicional.  
  
 *ID de transação*  
 [Entrada] Se *fRequiredTransactionEnlistment* for TRUE, *ID de transação* representa a transação de DTC listará a solicitação. Se *fRequiredTransactionEnlistment* é FALSE, *ID de transação* será ignorado.  
  
 *pRating*  
 [Saída] *hCandidateConnection*da reutilização de classificação para o *hRequest*. Essa classificação será entre 0 e 100 (inclusive).  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>diagnóstico  
 O Gerenciador de Driver não processa informações de diagnóstico retornadas por essa função.  
  
## <a name="remarks"></a>Comentários  
 **SQLRateConnection** produz uma pontuação entre 0 e 100 (inclusive) que indica quanto uma conexão existente corresponde à solicitação.  
  
|Pontuação|Significado (quando SQL_SUCCESS é retornado)|  
|-----------|-----------------------------------------------|  
|0|*hCandidateConnection* não deve ser reutilizado para o *hRequest*.|  
|Quaisquer valores entre 1 e 98 (inclusivo)|Quanto maior a pontuação, mais próximo que *hCandidateConnection* corresponde ao *hRequest*.|  
|99|Há diferenças apenas em atributos insignificantes.  O Gerenciador de Driver deve interromper o loop de classificação.|  
|100|Correspondência perfeita.  O Gerenciador de Driver deve interromper o loop de classificação.|  
|Qualquer valor maior que 100|*hCandidateConnection* está marcado como inativo e ele não serão reutilizadas mesmo em uma solicitação de conexão futura.|  
  
 O Gerenciador de Driver marcará uma conexão como inativo, se o código de retorno for algo diferente de SQL_SUCCESS (incluindo SQL_SUCCESS_WITH_INFO) ou a classificação é maior que 100. Essa conexão inativa não será reutilizada (mesmo em solicitações de conexão futura) e será eventualmente esgotado após CPTimeout passa. O Gerenciador de Driver continuará encontrar outra conexão do pool de taxa.  
  
 Se o Gerenciador de Driver reutilizado uma conexão cuja pontuação é estritamente menor que 100 (incluindo 99), o Gerenciador de Driver chamará SQLSetConnectAttr(SQL_ATTR_DBC_INFO_TOKEN) para redefinir a conexão volta para o estado solicitado pelo aplicativo. O driver não deve redefinir a conexão na chamada de função.  
  
 Se *fRequiredTransactionEnlistment* é TRUE, reutilizando *hCandidateConnection* precisa de uma inscrição adicional (*ID de transação* ! = NULL) ou unenlistment ( *ID de transação* = = NULL). Isso indica o custo de reutilizar uma conexão e se o driver deve inscrever / inscrição a conexão se ela for reutilizar a conexão. Se *fRequireTransactionEnlistment* é FALSE, o driver deve ignorar o valor de *ID de transação*.  
  
 O Gerenciador de Driver garante que o pai HENV tratar de *hRequest* e *hCandidateConnection* são os mesmos. O Gerenciador de Driver garante que a ID do pool associado *hRequest* e *hCandidateConnection* são os mesmos.  
  
 Aplicativos não devem chamar esta função diretamente. Um driver ODBC que oferece suporte ao pooling de conexão com reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de Conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)


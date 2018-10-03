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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9f3d0058e798fe9bdbcbfcbc1ed3adea8e405a98
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47776379"
---
# <a name="sqlrateconnection-function"></a>Função SQLRateConnection
**Conformidade com**  
 Versão introduziu: Conformidade de padrões 3.81 ODBC: ODBC  
  
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
 [Entrada] Se *fRequiredTransactionEnlistment* for TRUE, *ID de transação* representa a transação do DTC que a solicitação se inscreverá. Se *fRequiredTransactionEnlistment* é FALSE, o *ID de transação* será ignorado.  
  
 *pRating*  
 [Saída] *hCandidateConnection*classificação de reutilização para o *hRequest*. Essa classificação será entre 0 e 100 (inclusive).  
  
## <a name="returns"></a>Retorna  
 SQL_SUCCESS, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 O Gerenciador de Driver não processará as informações de diagnóstico retornadas desta função.  
  
## <a name="remarks"></a>Comentários  
 **SQLRateConnection** produz uma pontuação entre 0 e 100 (inclusive) que indica quão bem uma conexão existente corresponde à solicitação.  
  
|Pontuação|Significado (quando SQL_SUCCESS é retornado)|  
|-----------|-----------------------------------------------|  
|0|*hCandidateConnection* não deve ser reutilizada para o *hRequest*.|  
|Os valores entre 1 e 98 (inclusivo)|Quanto maior a pontuação, quanto mais próximo que *hCandidateConnection* neodpovídá *hRequest*.|  
|99|Há incompatibilidades somente nos atributos insignificantes.  O Gerenciador de Driver deve interromper o loop de classificação.|  
|100|Correspondência perfeita.  O Gerenciador de Driver deve interromper o loop de classificação.|  
|Qualquer valor maior que 100|*hCandidateConnection* está marcado como inativo e ele não serão reutilizados até mesmo em uma solicitação de conexão futura.|  
  
 O Gerenciador de Driver marcará uma conexão como inativa, se o código de retorno for algo diferente de SQL_SUCCESS (incluindo SQL_SUCCESS_WITH_INFO) ou a classificação é maior que 100. Essa conexão inativo não será reutilizado (mesmo em solicitações de conexão futura) e será eventualmente esgotado depois CPTimeout passa. O Gerenciador de Driver continuará encontrar outra conexão no pool de à taxa.  
  
 Se o Gerenciador de Driver reutilizado uma conexão cuja pontuação for estritamente menor que 100 (incluindo 99), o Gerenciador de Driver chamará SQLSetConnectAttr(SQL_ATTR_DBC_INFO_TOKEN) para redefinir a conexão volta para o estado solicitado pelo aplicativo. O driver não deve redefinir a conexão nessa chamada de função.  
  
 Se *fRequiredTransactionEnlistment* for TRUE, reutilizando *hCandidateConnection* precisa de uma inscrição extra (*ID de transação* ! = NULL) ou unenlistment ( *ID de transação* = = NULL). Isso indica que o custo de reutilizar uma conexão e se o driver deve se inscrever / inscrição a conexão se vai reutilizar a conexão. Se *fRequireTransactionEnlistment* é FALSE, o driver deve ignorar o valor de *ID de transação*.  
  
 O Gerenciador de Driver garante que o pai HENV tratar dos *hRequest* e *hCandidateConnection* são os mesmos. O Gerenciador de Driver garante que a ID do pool associado *hRequest* e *hCandidateConnection* são os mesmos.  
  
 Aplicativos não devem chamar essa função diretamente. Um driver ODBC que dá suporte ao pool de conexão de reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de Conexão de reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)

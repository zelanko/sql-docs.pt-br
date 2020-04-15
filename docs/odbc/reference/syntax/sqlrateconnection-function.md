---
title: Função sqlrateconnection | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288876"
---
# <a name="sqlrateconnection-function"></a>Função SQLRateConnection
**Conformidade**  
 Versão introduzida: ODBC 3.81 Normas De conformidade: ODBC  
  
 **Resumo**  
 **O SQLRateConnection** determina se um driver pode reutilizar uma conexão existente no pool de conexão.  
  
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
 *hSolicitar*  
 [Entrada] Uma alça de token representando a nova solicitação de conexão do aplicativo.  
  
 *hCandidateConnection*  
 [Entrada] A conexão existente no pool de conexão. A conexão deve estar em estado aberto.  
  
 *fRequiredTransactionalista*  
 [Entrada] Se TRUE, reutilizar o *hCandidateConnection* da conexão existente para a nova solicitação de conexão *(hRequest)* requer um alistamento adicional.  
  
 *transId*  
 [Entrada] Se *fRequiredTransactionAlista* for TRUE, o *transId* representa a transação DTC que a solicitação irá solicitar. Se *fRequiredTransactionAlista* for FALSO, *o transId* será ignorado.  
  
 *pRating*  
 [Saída] a classificação de reutilização do *hCandidateConnection*para o *hRequest*. Esta classificação será entre 0 e 100 (inclusive).  
  
## <a name="returns"></a>Retornos  
 SQL_SUCCESS, SQL_ERROR ou SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 O Driver Manager não processará informações de diagnóstico retornadas desta função.  
  
## <a name="remarks"></a>Comentários  
 **O SQLRateConnection** produz uma pontuação entre 0 e 100 (inclusive) indicando o quão bem uma conexão existente corresponde à solicitação.  
  
|Pontuação|Significado (quando SQL_SUCCESS é devolvida)|  
|-----------|-----------------------------------------------|  
|0|*hCandidateConnection* não deve ser reutilizado para o *hRequest*.|  
|Quaisquer valores entre 1 e 98 (inclusive)|Quanto maior a pontuação, mais perto *de hCandidateConnection* coincidir com *hRequest*.|  
|99|Só há incompatibilidades em atributos insignificantes.  O Driver Manager deve parar o ciclo de classificação.|  
|100|Combinação perfeita.  O Driver Manager deve parar o ciclo de classificação.|  
|Qualquer outro valor maior que 100|*hCandidateConnection* é marcado como morto e não será reutilizado mesmo em uma futura solicitação de conexão.|  
  
 O Driver Manager marcará uma conexão como morta se o código de retorno for algo diferente de SQL_SUCCESS (incluindo SQL_SUCCESS_WITH_INFO) ou a classificação for superior a 100. Essa conexão morta não será reutilizada (mesmo em futuras solicitações de conexão) e eventualmente será cronometrada após a passagem do CPTimeout. O Driver Manager continuará a encontrar outra conexão do pool para classificar.  
  
 Se o Driver Manager reutilizar uma conexão cuja pontuação é estritamente menor que 100 (incluindo 99), o Driver Manager ligará para sqlsetconnectattr(SQL_ATTR_DBC_INFO_TOKEN) para redefinir a conexão de volta ao estado solicitado pelo aplicativo. O driver não deve reiniciar a conexão nesta chamada de função.  
  
 Se *fRequiredTransactionAlista* for TRUE, a reutilização *do hCandidateConnection* precisa de um alistamento extra *(transId* != NULL) ou unenlistment *(transId* == NULL). Isso indica o custo de reutilização de uma conexão e se o motorista deve alistar/desalistar a conexão se ele vai reutilizar a conexão. Se *fRequireTransactionAlista* for FALSO, o driver deve ignorar o valor do *transId*.  
  
 O Driver Manager garante que a alça HENV pai de *hRequest* e *hCandidateConnection* são as mesmas. O Driver Manager garante que o ID do pool associado ao *hRequest* e *hCandidateConnection* são os mesmos.  
  
 Os aplicativos não devem chamar essa função diretamente. Um driver ODBC que suporta pooling de conexão com reconhecimento de driver deve implementar essa função.  
  
 Inclua sqlspi.h para desenvolvimento de driver ODBC.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)

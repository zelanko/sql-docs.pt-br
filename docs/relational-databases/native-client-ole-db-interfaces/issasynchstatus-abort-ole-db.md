---
title: 'Issasynchstatus:: Abort (OLE DB) | Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ISSAsynchStatus::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
ms.assetid: 2a4bd312-839a-45a8-a299-fc8609be9a2a
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: cf05d99617114059dac55794b68ca7bf2222ca4e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="issasynchstatusabort-ole-db"></a>ISSAsynchStatus::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Cancela uma operação que está sendo executada de forma assíncrona.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT Abort(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hChapter*[in]  
 O identificador do capítulo que contém a operação a ser anulada. Se o objeto que está sendo chamado não for um objeto de conjunto de linhas ou se a operação não se aplicar a um capítulo, o chamador deverá definir *hChapter* como DB_NULL_HCHAPTER.  
  
 *eOperation*[in]  
 A operação a ser anulada. O valor desse argumento deveria ser o seguinte:  
  
 DBASYNCHOP_OPEN – a solicitação de cancelamento se aplica à abertura ou população assíncrona de um conjunto de linhas ou à inicialização assíncrona de um objeto de fonte de dados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 A solicitação para cancelar a operação assíncrona foi processada. Isso não garante que a operação seja cancelada. Para determinar se a operação foi cancelada, o consumidor deve chamar [ISSAsynchStatus::GetStatus](../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-getstatus-ole-db.md) e verificar DB_E_CANCELED; no entanto, esse valor pode não ser retornado na chamada seguinte.  
  
 DB_E_CANTCANCEL  
 A operação assíncrona não pode ser cancelada.  
  
 DB_E_CANCELED  
 A solicitação para anular a operação assíncrona foi cancelada durante notificações. A operação ainda está sendo executada de forma assíncrona.  
  
 E_FAIL  
 Ocorreu um erro específico de provedor.  
  
 E_INVALIDARG  
 O parâmetro *hChapter* não é DB_NULL_HCHAPTER ou *eOperation* não é DBASYNCH_OPEN.  
  
 E_UNEXPECTED  
 **ISSAsynchStatus::Abort** foi chamado em um objeto de fonte de dados no qual **IDBInitialize::Initialize** não foi chamado ou não foi concluído.  
  
 **ISSAsynchStatus::Abort** foi chamado em um objeto de fonte de dados no qual **IDBInitialize::Initialize** foi chamado, mas, subsequentemente, foi cancelado antes da inicialização ou seu tempo limite foi atingido. O objeto de fonte de dados permanece não inicializado.  
  
 **ISSAsynchStatus::Abort** foi chamado em um conjunto de linhas no qual **ITransaction::Commit** ou **ITransaction::Abort** foi chamado anteriormente, e o conjunto de linhas não sobreviveu à operação de confirmação ou anulação e está em um estado zumbi.  
  
 **ISSAsynchStatus::Abort** foi chamado em um conjunto de linhas cancelado de forma assíncrona em sua fase de inicialização. O conjunto de linhas está em um estado zumbi.  
  
## <a name="remarks"></a>Remarks  
 Anular a inicialização de um conjunto de linhas ou objeto de fonte de dados pode deixar o conjunto de linhas ou o objeto de fonte de dados em um estado zumbi, de modo que todos os métodos diferentes de **IUnknown** retornam E_UNEXPECTED. Quando isso acontece, a única ação possível para o consumidor é liberar o conjunto de linhas ou objeto de fonte de dados.  
  
 Chamar **ISSAsynchStatus::Abort** e atribuir um valor a *eOperation* diferente de DBASYNCHOP_OPEN retorna S_OK. Isso não significa que a operação tenha sido concluída ou cancelada.  
  
## <a name="see-also"></a>Consulte também  
 [Executando operações assíncronas](../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
  
  

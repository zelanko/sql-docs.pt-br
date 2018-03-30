---
title: 'Issasynchstatus:: Abort (OLE DB) | Microsoft Docs'
description: ISSAsynchStatus::Abort (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
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
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5f4070ab6a99a809fa0486dfd9462431e5608d25
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2018
---
# <a name="issasynchstatusabort-ole-db"></a>ISSAsynchStatus::Abort (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Cancela uma operação que está sendo executada de forma assíncrona.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT Abort(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hChapter*[in]  
 O identificador do capítulo que contém a operação a ser anulada. Se o objeto que está sendo chamado não é um objeto de conjunto de linhas ou a operação não se aplica a um capítulo, o chamador deverá definir *hChapter* como DB_NULL_HCHAPTER.  
  
 *eOperation*[in]  
 A operação a ser anulada. O valor a seguir deve ser usado:  
  
 DBASYNCHOP_OPEN – a solicitação de cancelamento se aplica à abertura ou população assíncrona de um conjunto de linhas ou à inicialização assíncrona de um objeto de fonte de dados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 A solicitação para cancelar a operação assíncrona foi processada. Ele não garante que a operação foi cancelada. Para determinar se a operação foi cancelada, o consumidor deve chamar [ISSAsynchStatus::GetStatus](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md) e verificar DB_E_CANCELED; no entanto, esse valor pode não ser retornado na chamada seguinte.  
  
 DB_E_CANTCANCEL  
 A operação assíncrona não pode ser cancelada.  
  
 DB_E_CANCELED  
 A solicitação para anular a operação assíncrona foi cancelada durante notificações. A operação ainda está sendo executada de forma assíncrona.  
  
 E_FAIL  
 Ocorreu um erro específico de provedor.  
  
 E_INVALIDARG  
 O *hChapter* parâmetro não é DB_NULL_HCHAPTER ou *eOperation* não é DBASYNCH_OPEN.  
  
 E_UNEXPECTED  
 **Issasynchstatus:: Abort** foi chamado em um objeto de fonte de dados no qual **IDBInitialize:: Initialize** ainda não foi chamado ou não foi concluída.  
  
 **ISSAsynchStatus::Abort** foi chamado em um objeto de fonte de dados no qual **IDBInitialize::Initialize** foi chamado, mas, subsequentemente, foi cancelado antes da inicialização ou seu tempo limite foi atingido. O objeto de fonte de dados permanece não inicializado.  
  
 **Issasynchstatus:: Abort** foi chamado em um conjunto de linhas no qual **ITransaction:: Commit** ou **ITransaction:: Abort** foi chamado anteriormente, e o conjunto de linhas não sobrevivem a confirmação ou anulação e está em um estado zumbi.  
  
 **ISSAsynchStatus::Abort** foi chamado em um conjunto de linhas cancelado de forma assíncrona em sua fase de inicialização. O conjunto de linhas está em um estado zumbi.  
  
## <a name="remarks"></a>Remarks  
 Anular a inicialização de um conjunto de linhas ou objeto de fonte de dados pode deixar o conjunto de linhas ou o objeto de fonte de dados em um estado zumbi, de modo que todos os métodos diferentes de **IUnknown** retornam E_UNEXPECTED. Quando isso acontece, a única ação possível para o consumidor é liberar o conjunto de linhas ou objeto de fonte de dados.  
  
 Chamar **ISSAsynchStatus::Abort** e atribuir um valor a *eOperation* diferente de DBASYNCHOP_OPEN retorna S_OK. Isso não significa que a operação foi concluída ou cancelada.  
  
## <a name="see-also"></a>Consulte também  
 [Executando operações assíncronas](../../oledb/features/performing-asynchronous-operations.md)  
  
  

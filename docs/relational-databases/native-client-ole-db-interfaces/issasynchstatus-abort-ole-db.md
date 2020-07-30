---
title: 'ISSAsynchStatus:: Abort (provedor de OLE DB de cliente nativo) | Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apiname:
- ISSAsynchStatus::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
ms.assetid: 2a4bd312-839a-45a8-a299-fc8609be9a2a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a713f210c04032d9b24d90c59ad1088b1a1cd0d8
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246917"
---
# <a name="issasynchstatusabort-native-client-ole-db-provider"></a>ISSAsynchStatus:: Abort (provedor de OLE DB de cliente nativo)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

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
  
 **ISSAsynchStatus:: Abort** foi chamado em um objeto de fonte de dados no qual **IDBInitialize:: Initialize** foi chamado, mas subsequentemente cancelado antes da inicialização ou atingiu o tempo limite. O objeto de fonte de dados ainda não foi inicializado.  
  
 **ISSAsynchStatus::Abort** foi chamado em um conjunto de linhas no qual **ITransaction::Commit** ou **ITransaction::Abort** foi chamado anteriormente, e o conjunto de linhas não sobreviveu à operação de confirmação ou anulação e está em um estado zumbi.  
  
 **ISSAsynchStatus::Abort** foi chamado em um conjunto de linhas cancelado de forma assíncrona em sua fase de inicialização. O conjunto de linhas está em um estado zumbi.  
  
## <a name="remarks"></a>Comentários  
 Anular a inicialização de um conjunto de linhas ou objeto de fonte de dados pode deixar o conjunto de linhas ou o objeto de fonte de dados em um estado zumbi, de modo que todos os métodos diferentes de **IUnknown** retornam E_UNEXPECTED. Quando isso acontece, a única ação possível para o consumidor é liberar o conjunto de linhas ou objeto de fonte de dados.  
  
 Chamar **ISSAsynchStatus::Abort** e atribuir um valor a *eOperation* diferente de DBASYNCHOP_OPEN retorna S_OK. Isso não significa que a operação tenha sido concluída ou cancelada.  
  
## <a name="see-also"></a>Consulte Também  
 [Executando operações assíncronas](../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
  
  

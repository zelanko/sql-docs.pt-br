---
title: IServerVirtualDeviceSet2::SignalAbort
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IServerVirtualDeviceSet2::SignalAbort.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: b61a972d7b379ff40440124c875d8d49a7af1835
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70847167"
---
# <a name="iservervirtualdeviceset2signalabort-vdi"></a>IServerVirtualDeviceSet2::SignalAbort (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A função **SignalAbort** sinaliza que um encerramento anormal deve ocorrer.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IServerVirtualDeviceSet2::SignalAbort ();
```

## <a name="return-value"></a>Valor retornado

Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor igual a NOERROR indica que a chamada de método teve êxito. Um valor diferente de zero indica que ocorreu um erro.

## <a name="remarks"></a>Comentários

A qualquer momento, o servidor pode optar por anular a operação BACKUP ou RESTORE.

Essa rotina sinaliza que todas as operações devem ser interrompidas. A interface geral entra em um estado de anulação. Nenhum outro comando é aceito nos dispositivos. O agente de conclusão retorna ERROR_OPERATION_ABORTED para cada solicitação pendente e retorna ao chamador. Todas as conclusões registradas no cliente são ignoradas.

O servidor garante que não haja nenhum uso adicional necessário dos buffers ou dos dispositivos retornados da interface de dispositivo virtual. Em seguida, o servidor executa a limpeza de encerramento anormal, que deve incluir uma chamada à função IServerVirtualDeviceSet2::Close.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
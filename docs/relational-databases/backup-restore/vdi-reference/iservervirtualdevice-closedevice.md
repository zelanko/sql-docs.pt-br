---
title: IServerVirtualDevice::CloseDevice
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IServerVirtualDevice::CloseDevice.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 61d877fddb32f6455303a006e8955b1042ce7aa6
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128903"
---
# <a name="iservervirtualdeviceclosedevice-vdi"></a>IServerVirtualDevice::CloseDevice (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

A função **CloseDevice** fecha um dispositivo virtual que foi aberto com IServerVirtualDeviceSet2::OpenDevice

## <a name="syntax"></a>Sintaxe

```c
HRESULT IServerVirtualDevice::CloseDevice ();
```

## <a name="return-value"></a>Valor retornado

|Valor retornado | Explicação |
|---|---|
| VD_E_CLOSE | O dispositivo já está fechado. |
| VD_E_ABORT | A interface está no estado de anulação. |

## <a name="remarks"></a>Comentários

CloseDevice não é necessário depois que SignalAbort é usado para forçar o encerramento anormal. Se CloseDevice for invocado depois que SignalAbort for usado, nenhuma ação será executada.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
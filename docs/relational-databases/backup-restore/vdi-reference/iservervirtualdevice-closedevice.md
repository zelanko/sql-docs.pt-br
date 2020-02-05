---
title: IServerVirtualDevice::CloseDevice
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IServerVirtualDevice::CloseDevice.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: c73649e2a4301e94f8e68504222cc0122061f25f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70847427"
---
# <a name="iservervirtualdeviceclosedevice-vdi"></a>IServerVirtualDevice::CloseDevice (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

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
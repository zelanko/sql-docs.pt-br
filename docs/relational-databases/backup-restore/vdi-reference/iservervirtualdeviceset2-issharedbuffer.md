---
title: IServerVirtualDeviceSet2::IsSharedBuffer
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IServerVirtualDeviceSet2::IsSharedBuffer.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: cd3e7abfd1d250a170e0de4ebc1b392bc5857468
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847357"
---
# <a name="iservervirtualdeviceset2issharedbuffer-vdi"></a>IServerVirtualDeviceSet2::IsSharedBuffer (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A função **IsSharedBuffer** determina se o endereço de buffer fornecido refere-se a um dos buffers compartilhados disponibilizados pelo método AllocateBuffer.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IServerVirtualDeviceSet2::IsSharedBuffer (
   LPVOID   lpBuffer
);
```

## <a name="parameters"></a>Parâmetros

*lpBuffer* Esse é um endereço de um buffer.

## <a name="return-value"></a>Valor retornado

|Valor retornado | Explicação |
|---|---|
| TRUE | O buffer é um buffer compartilhado. |
| FALSE | O buffer não faz parte do conjunto de dispositivos virtuais. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
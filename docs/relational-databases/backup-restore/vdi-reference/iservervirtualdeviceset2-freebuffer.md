---
title: IServerVirtualDeviceSet2::FreeBuffer
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IServerVirtualDeviceSet2::FreeBuffer.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1e7ac18a3a16d860b3fda7cfc26b0ab6733be4d0
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85895267"
---
# <a name="iservervirtualdeviceset2freebuffer-vdi"></a>IServerVirtualDeviceSet2::FreeBuffer (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

A função **FreeBuffer** obtém um buffer de memória compartilhada do conjunto de dispositivos virtuais.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IServerVirtualDeviceSet2::FreeBuffer (
   LPVOID   pBuffer,
   UINT32   dwSize
);
```

## <a name="parameters"></a>parâmetros

*pBuffer* Isso retorna um buffer retornado por IServerVirtualDeviceSet2::AllocateBuffer.

*dwSize* Esse é o tamanho do buffer em bytes. Isso não inclui nenhuma zona de prefixo solicitada pelo cliente. Qualquer zona desse tipo fica oculta do servidor e haverá espaço disponível antes de o endereço do buffer ser retornado.

## <a name="return-value"></a>Valor retornado

|Valor retornado | Explicação |
|---|---|
| NOERROR | O buffer é retornado. |
| VD_E_INVALID | Um parâmetro era inválido. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
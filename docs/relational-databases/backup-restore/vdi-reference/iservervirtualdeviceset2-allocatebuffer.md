---
title: IServerVirtualDeviceSet2::AllocateBuffer
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IServerVirtualDeviceSet2::AllocateBuffer.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 8c28009fae8b52264b541ca3eb4281ab9abccf63
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "70847487"
---
# <a name="iservervirtualdeviceset2allocatebuffer-vdi"></a>IServerVirtualDeviceSet2::AllocateBuffer (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A função **AllocateBuffer** obtém um buffer de memória compartilhada do conjunto de dispositivos virtuais.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IServerVirtualDeviceSet2::AllocateBuffer (
   LPVOID*      ppBuffer,
   UINT32      dwSize,
   UINT32      dwAlignment
);
```

## <a name="parameters"></a>parâmetros

*ppBuffer* Isso retorna um ponteiro para o início do buffer.

*dwSize* Esse é o tamanho do buffer em bytes. Isso não inclui nenhuma zona de prefixo solicitada pelo cliente. Qualquer zona desse tipo fica oculta do servidor e haverá espaço disponível antes de o endereço do buffer ser retornado.

*dwAlignment* Isso especifica o limite de alinhamento do buffer. Por exemplo, com um valor de 4096, o buffer fica alinhado em um limite de 4096 bytes. Isso significa que o endereço retornado teria 12 bits de ordem inferior definidos como zero. Esse parâmetro deve ser uma potência de 2.

## <a name="return-value"></a>Valor retornado

|Valor retornado | Explicação |
|---|---|
| NOERROR | O buffer é retornado. |
| VD_E_MEMORY | Uma condição fora de memória ocorreu. |
| VD_E_INVALID | Um parâmetro era inválido. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
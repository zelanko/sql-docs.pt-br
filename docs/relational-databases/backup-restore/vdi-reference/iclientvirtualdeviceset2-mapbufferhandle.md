---
title: IClientVirtualDeviceSet2::MapBufferHandle
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IClientVirtualDeviceSet2::MapBufferHandle.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 23bb125d8744cf51f6b72187b6a251e27fb84f05
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896893"
---
# <a name="iclientvirtualdeviceset2mapbufferhandle-vdi"></a>IClientVirtualDeviceSet2::MapBufferHandle (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

A função **MapBufferHandle** é usada para obter um endereço de buffer válido de um identificador de buffer obtido de algum outro processo.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IClientVirtualDeviceSet2::MapBufferHandle (
   DWORD      dwBuffer,
   BYTE**      ppBuffer
);
```

## <a name="parameters"></a>parâmetros

*dwBuffer* Este é o identificador retornado por IClientVirtualDeviceSet2::GetBufferHandle.

*ppBuffer* Esse é o endereço do buffer válido no processo atual.

## <a name="return-value"></a>Valor retornado

|Valor retornado | Explicação |
|---|---|
| NOERROR | A função foi bem-sucedida. |
| VD_E_PROTOCOL | O conjunto de dispositivos virtuais não está aberto no momento. |
| VD_E_INVALID | O ppBuffer é um identificador inválido. |

## <a name="remarks"></a>Comentários

Deve-se tomar cuidado para comunicar os identificadores corretamente. Os identificadores são locais para um único conjunto de dispositivos virtuais. Os processos de parceiros que compartilham um identificador precisam garantir que os identificadores de buffer sejam usados somente dentro do escopo do conjunto de dispositivos virtuais do qual o buffer foi originalmente obtido.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
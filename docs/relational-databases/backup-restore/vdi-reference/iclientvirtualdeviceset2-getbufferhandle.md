---
title: IClientVirtualDeviceSet2::GetBufferHandle
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IClientVirtualDeviceSet2::GetBufferHandle.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 844ddad21eaf3fb579d6a0981f2a042238e92372
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70847327"
---
# <a name="iclientvirtualdeviceset2getbufferhandle-vdi"></a>IClientVirtualDeviceSet2::GetBufferHandle (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Alguns aplicativos podem exigir mais de um processo para operar nos buffers retornados por **IClientVirtualDevice2::GetCommand**. Nesses casos, o processo que recebe o comando pode usar **GetBufferHandle** para obter um identificador independente de processo que identifica o buffer. Esse identificador pode então ser comunicado a qualquer outro processo que também tenha o mesmo conjunto de dispositivos virtuais aberto. Esse processo usará IClientVirtualDeviceSet2::MapBufferHandle para obter o endereço do buffer. O endereço provavelmente será um endereço diferente do que em seu parceiro, pois cada processo pode estar mapeando buffers em endereços diferentes.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IClientVirtualDeviceSet2::GetBufferHandle (
   BYTE*         pBuffer,
   DWORD*      pBufferHandle
);
```

## <a name="parameters"></a>parâmetros

*pBuffer* Esse é o endereço de um buffer obtido de um comando de Leitura ou Gravação.

*pBufferHandle* Um identificador exclusivo para o buffer é retornado.

## <a name="return-value"></a>Valor retornado

|Valor retornado | Explicação |
|---|---|
| NOERROR | A função foi bem-sucedida. |
| VD_E_PROTOCOL | O conjunto de dispositivos virtuais não está aberto no momento. |
| VD_E_INVALID | O pBuffer não é um endereço válido. |

## <a name="remarks"></a>Comentários

O processo que invoca a função GetBufferHandle é responsável por invocar IClientVirtualDevice2::CompleteCommand quando a transferência de dados é concluída.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
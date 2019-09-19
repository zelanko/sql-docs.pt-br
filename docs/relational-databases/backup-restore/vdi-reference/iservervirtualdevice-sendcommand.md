---
title: IServerVirtualDevice::SendCommand
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IServerVirtualDevice::SendCommand.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: c75cd206557547f55d47eec0a7aec52cc0069b71
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847507"
---
# <a name="iservervirtualdevicesendcommand-vdi"></a>IServerVirtualDevice::SendCommand (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A função **SendCommand** envia um comando para o cliente usando um objeto de dispositivo virtual retornado de IServerVirtualDeviceSet2::OpenDevice.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IServerVirtualDevice::SendCommand (
   VDS_Command*   pCmd
);
```

## <a name="parameters"></a>Parâmetros

*pCmd* Esse é um ponteiro para um bloco de solicitação de comando. Para obter mais informações, confira Comandos. O campo completionFunction deve ser definido para apontar para o endereço de uma função com a seguinte assinatura:

```c
void callbackFunction ( VDS_Command *pCmd);
```

Esse retorno de chamada é feito pelo agente de conclusão quando o cliente indica que um comando foi concluído. O SQL Server define o campo completionContext do pCmd. Sua finalidade é fornecer contexto para a função de retorno de chamada.

## <a name="return-value"></a>Valor retornado

|Valor retornado | Explicação |
|---|---|
| NOERROR | O comando foi enfileirado com êxito para o cliente. |
| VD_E_QUEUE_FULL | A fila do dispositivo está cheia. |
| VD_E_IO_ERROR | O dispositivo está em um estado IO-ERROR. |
| VD_E_PROTOCOL | O dispositivo não está ativo. |

## <a name="remarks"></a>Remarks

Quando ocorre um erro ao tentar enviar o comando, a função de retorno de chamada é invocada e o completionCode no buffer de comando é definido da seguinte maneira:

| completionCode | Erro |
|---|---|
| VD_E_QUEUE_FULL | ERROR_NO_SYSTEM_RESOURCES |
| VD_E_IO_ERROR   | ERROR_IO_DEVICE |
| VD_E_PROTOCOL   | ERROR_INVALID_HANDLE |
| VD_E_ABORT      | ERROR_OPERATION_ABORTED |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
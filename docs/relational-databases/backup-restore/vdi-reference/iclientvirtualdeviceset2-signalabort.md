---
title: IClientVirtualDeviceSet2::SignalAbort
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IClientVirtualDeviceSet2::SignalAbort.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 0a0d53421f0928b1ebf0ba557afbd29dd8680993
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847537"
---
# <a name="iclientvirtualdeviceset2signalabort-vdi"></a>IClientVirtualDeviceSet2::SignalAbort (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A função **SignalAbort** é usada para sinalizar que um encerramento anormal deverá ocorrer.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IClientVirtualDeviceSet2::SignalAbort ();
```

## <a name="return-value"></a>Valor retornado

Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor igual a NOERROR indica que a chamada de método teve êxito. Um valor diferente de zero indica que ocorreu um erro.

## <a name="remarks"></a>Remarks

A qualquer momento, o cliente pode optar por anular a operação BACKUP ou RESTORE. Essa rotina sinaliza que todas as operações devem ser interrompidas. O estado do conjunto geral de dispositivos virtuais entra em um estado de anulação. Nenhum outro comando é retornado nos dispositivos. Todos os comandos não concluídos são concluídos automaticamente, retornando ERROR_OPERATION_ABORTED como um código de conclusão. O cliente deverá chamar IClientVirtualDeviceSet2::Close depois de encerrar com segurança qualquer uso pendente de buffers fornecidos ao cliente. Para obter mais informações, confira Encerramento Anormal.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
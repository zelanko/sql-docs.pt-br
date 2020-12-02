---
title: IClientVirtualDeviceSet2::SignalAbort
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IClientVirtualDeviceSet2::SignalAbort.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: d36a08586a6903a6e85bb4bad4d6344a54938cd2
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125386"
---
# <a name="iclientvirtualdeviceset2signalabort-vdi"></a>IClientVirtualDeviceSet2::SignalAbort (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

A função **SignalAbort** é usada para sinalizar que um encerramento anormal deverá ocorrer.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IClientVirtualDeviceSet2::SignalAbort ();
```

## <a name="return-value"></a>Valor retornado

Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor igual a NOERROR indica que a chamada de método teve êxito. Um valor diferente de zero indica que ocorreu um erro.

## <a name="remarks"></a>Comentários

A qualquer momento, o cliente pode optar por anular a operação BACKUP ou RESTORE. Essa rotina sinaliza que todas as operações devem ser interrompidas. O estado do conjunto geral de dispositivos virtuais entra em um estado de anulação. Nenhum outro comando é retornado nos dispositivos. Todos os comandos não concluídos são concluídos automaticamente, retornando ERROR_OPERATION_ABORTED como um código de conclusão. O cliente deverá chamar IClientVirtualDeviceSet2::Close depois de encerrar com segurança qualquer uso pendente de buffers fornecidos ao cliente. Para obter mais informações, confira Encerramento Anormal.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
---
title: IServerVirtualDeviceSet2::ExecuteCompletionAgent
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IServerVirtualDeviceSet2::ExecuteCompletionAgent.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: ce53793d624c0a56fda48805c5c2fc8fc178e42c
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128883"
---
# <a name="iservervirtualdeviceset2executecompletionagent-vdi"></a>IServerVirtualDeviceSet2::ExecuteCompletionAgent (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

A função **ExecuteCompletionAgent** é usada para implementar o loop principal do agente de conclusão.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IServerVirtualDeviceSet2::ExecuteCompletionAgent ();
```

## <a name="return-value"></a>Valor retornado

Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor igual a NOERROR indica que a chamada de método teve êxito. Um valor diferente de zero indica que ocorreu um erro.

## <a name="remarks"></a>Comentários

O agente de conclusão fornece um mecanismo pelo qual o SQL Server pode se sincronizar com as conclusões de comando do dispositivo virtual. Ele precisa estar ativo antes que qualquer comando possa ser emitido e deve permanecer ativo até todos os dispositivos serem fechados.

Como o SQL Server pode precisar executar uma inicialização de thread especial, essa interface não inicia um novo thread de controle. Em vez disso, o SQL Server configura um thread e, em seguida, passa o controle para essa rotina. O thread precisa ser bloqueável em mecanismos de IPC (comunicação entre processos) do Windows NT e ter a capacidade de chamar qualquer uma das funções de retorno de chamada fornecidas com os comandos enviados por meio de IServerVirtualDevice::SendCommand.

Essa função não será retornada enquanto IServerVirtualDeviceSet2::Close ou SignalAbort não for invocado.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
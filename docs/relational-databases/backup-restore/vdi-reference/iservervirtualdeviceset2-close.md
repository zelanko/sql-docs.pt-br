---
title: IServerVirtualDeviceSet2::Close
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IServerVirtualDeviceSet2::Close.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 2847ef10bd52d69375fa4f13f1d003eb4159961f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "70847467"
---
# <a name="iservervirtualdeviceset2close-vdi"></a>IServerVirtualDeviceSet2::Close (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A função **Close** fecha um conjunto de dispositivo virtual aberto por IServerVirtualDeviceSet2::Open. Isso resulta na liberação de todos os recursos associados ao dispositivo virtual. O identificador IServerVirtualDeviceSet2 não será útil depois que essa função for retornada e ela deverá ser retornada para COM.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IServerVirtualDeviceSet2::Close ();
```

## <a name="return-value"></a>Valor retornado

|Valor retornado | Explicação |
|---|---|
| VD_E_PROTOCOL | Os dispositivos ainda estavam abertos. |

## <a name="remarks"></a>Comentários

Fechar o conjunto de dispositivos virtuais antes de fechar os dispositivos não deve ser executado. Se essa situação ocorrer, VD_E_PROTOCOL será retornado. Essa ação resulta em Close liberando imediatamente seu mapeamento de memória compartilhada. O servidor estará sujeito a violações de acesso se continuar esperando a propriedade de recursos retornados da interface do dispositivo virtual. A interface executa o processamento SignalAbort.

O agente de conclusão, se estiver em execução, concluirá os comandos pendentes antes de ser retornado ao seu chamador. Os comandos pendentes são concluídos com ERROR_OPERATION_ABORTED. Ou seja, a função de retorno de chamada é invocada para cada comando desse tipo.

Em todos os casos, incluindo quando erros são retornados, a Close libera todos os recursos da interface do dispositivo virtual. Os buffers e outros ponteiros de interface retornados do VDI tornam-se inválidos.

É importante verificar se o agente de conclusão foi encerrado antes que a biblioteca COM seja descarregada. Se a biblioteca for descarregada antes do retorno do agente de conclusão ao seu chamador, o processo poderá causar uma violação de instrução.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
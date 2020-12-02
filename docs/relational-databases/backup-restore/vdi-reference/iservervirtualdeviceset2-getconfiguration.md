---
title: IServerVirtualDeviceSet2::GetConfiguration
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IServerVirtualDeviceSet2::GetConfiguration.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: a70217da1fad6461ee5d20cdc6228f3984c367ff
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128869"
---
# <a name="iservervirtualdeviceset2getconfiguration-vdi"></a>IServerVirtualDeviceSet2::GetConfiguration (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

A função **GetConfiguration** obtém a configuração solicitada pelo cliente.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IServerVirtualDeviceSet2::GetConfiguration (
   VDConfig*   pCfg
);
```

## <a name="parameters"></a>parâmetros

*pCfg* Essa é a configuração especificada pelo cliente usando IClientVirtualDeviceSet2::Create.

## <a name="return-value"></a>Valor retornado

Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor igual a NOERROR indica que a chamada de método teve êxito. Um valor diferente de zero indica que ocorreu um erro.

## <a name="remarks"></a>Comentários

Espera-se que o servidor inspecione e responda às configurações fornecidas pelo cliente. Para obter mais informações, confira Configuração. O servidor poderá usar SignalAbort se determinar que ele não funciona corretamente com a configuração fornecida.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
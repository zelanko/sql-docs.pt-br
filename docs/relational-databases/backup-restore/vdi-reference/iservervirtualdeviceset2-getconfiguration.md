---
title: IServerVirtualDeviceSet2::GetConfiguration
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IServerVirtualDeviceSet2::GetConfiguration.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1d62a2042221bebf04e19a46a21ba81caa7c877b
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847247"
---
# <a name="iservervirtualdeviceset2getconfiguration-vdi"></a>IServerVirtualDeviceSet2::GetConfiguration (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A função **GetConfiguration** obtém a configuração solicitada pelo cliente.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IServerVirtualDeviceSet2::GetConfiguration (
   VDConfig*   pCfg
);
```

## <a name="parameters"></a>Parâmetros

*pCfg* Essa é a configuração especificada pelo cliente usando IClientVirtualDeviceSet2::Create.

## <a name="return-value"></a>Valor retornado

Retorna um *HRESULT* indicando êxito ou falha da chamada do método. Um valor igual a NOERROR indica que a chamada de método teve êxito. Um valor diferente de zero indica que ocorreu um erro.

## <a name="remarks"></a>Remarks

Espera-se que o servidor inspecione e responda às configurações fornecidas pelo cliente. Para obter mais informações, confira Configuração. O servidor poderá usar SignalAbort se determinar que ele não funciona corretamente com a configuração fornecida.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
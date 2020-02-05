---
title: IClientVirtualDeviceSet2::GetConfiguration
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IClientVirtualDeviceSet2::GetConfiguration.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 5d7d42d081b0494feeb5c2b221575e0d5df1143a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70847447"
---
# <a name="iclientvirtualdeviceset2getconfiguration-vdi"></a>IClientVirtualDeviceSet2::GetConfiguration (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A função **GetConfiguration** é usada para aguardar o servidor configurar o conjunto de dispositivos virtuais.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IClientVirtualDeviceSet2::GetConfiguration (
   DWORD         dwTimeOut,
   VDConfig*      pCfg
);
```

## <a name="parameters"></a>parâmetros

*DwTimeOut* Esse é o tempo limite em milissegundos. Use INFINITE para evitar o tempo limite.

*pCfg* Após a execução bem-sucedida, isso conterá a configuração selecionada pelo servidor. Para obter mais informações, confira Configuração.

## <a name="return-value"></a>Valor retornado

|Valor retornado | Explicação |
|---|---|
| NOERROR | A configuração foi retornada. |
| VD_E_ABORT | SignalAbort foi invocado. |
| VD_E_TIMEOUT | A função atingiu o tempo limite. |

## <a name="remarks"></a>Comentários

Essa função é bloqueada em um estado Passível de Alerta. Após a invocação bem-sucedida, os dispositivos do conjunto de dispositivos virtuais poderão ser abertos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
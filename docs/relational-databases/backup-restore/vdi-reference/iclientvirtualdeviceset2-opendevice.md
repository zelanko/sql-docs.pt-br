---
title: IClientVirtualDeviceSet2::OpenDevice
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IClientVirtualDeviceSet2::OpenDevice.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: aff46d7240cf504b02e75d91b75d0ba746a24752
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70847567"
---
# <a name="iclientvirtualdeviceset2opendevice-vdi"></a>IClientVirtualDeviceSet2::OpenDevice (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A função **OpenDevice** abre um dos dispositivos no conjunto de dispositivos virtuais.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IClientVirtualDeviceSet2::OpenDevice (
   LPCWSTR                  lpName,
   IClientVirtualDevice**   ppVirtualDevice

);
```

## <a name="parameters"></a>parâmetros

*lpName* Isso identifica o dispositivo virtual.

*ppVirtualDevice* Quando a função é bem-sucedida, um ponteiro de interface para o dispositivo virtual é retornado. Essa interface é usada para o GetCommand e CompleteCommand.

## <a name="return-value"></a>Valor retornado

|Valor retornado | Explicação |
|---|---|
| NOERROR | A função foi bem-sucedida. |
| VD_E_ABORT | A anulação foi solicitada. |
| VD_E_OPEN |Todos os dispositivos estão abertos. |
| VD_E_PROTOCOL | O conjunto não está no estado de inicialização ou esse dispositivo específico já está aberto. |
| VD_E_INVALID | O nome do dispositivo é inválido. Não é um dos nomes considerados integrantes do conjunto. |

## <a name="remarks"></a>Comentários

VD_E_OPEN pode ser retornado sem problemas. O cliente pode chamar OpenDevice por meio de um loop até que esse código seja retornado.
Se mais de um dispositivo estiver configurado, por exemplo, n dispositivos, o conjunto de dispositivos virtuais retornará n interfaces de dispositivo exclusivas. O primeiro dispositivo tem o mesmo nome que o conjunto de dispositivos virtuais. Outros dispositivos são nomeados conforme especificado com as cláusulas VIRTUAL_DEVICE da instrução BACKUP/RESTORE.

A função GetConfiguration pode ser usada para aguardar até que os dispositivos possam ser abertos.

Se essa função não for bem-sucedida, um valor nulo será retornado por meio do ppVirtualDevice.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
---
title: IServerVirtualDeviceSet2::OpenDevice
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IServerVirtualDeviceSet2::OpenDevice.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: af24aff4bbb8f0eefa14363453e962c0a90d610e
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847207"
---
# <a name="iservervirtualdeviceset2opendevice-vdi"></a>IServerVirtualDeviceSet2::OpenDevice (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A função **OpenDevice** obtém interfaces de dispositivo virtual do conjunto de dispositivos virtuais.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IServerVirtualDeviceSet2::OpenDevice (
   LPCWSTR                     lpName,
   IServerVirtualDevice**      ppVirtualDevice
);
```

## <a name="parameters"></a>Parâmetros

*lpName* Isso é fornecido pela primeira cláusula VIRTUAL_DEVICE= do comando BACKUP ou RESTORE. Esse nome é usado como a chave para obter acesso ao conjunto de dispositivos virtuais criado pelo cliente.

*ppVirtualDevice* Isso é usado para retornar uma interface de dispositivo virtual.

## <a name="return-value"></a>Valor retornado

|Valor retornado | Explicação |
|---|---|
| NOERROR | A função foi bem-sucedida. |
| VD_E_OPEN |Todos os dispositivos foram abertos. |

## <a name="remarks"></a>Remarks

Cada chamada retorna o próximo dispositivo não aberto. A função pode ser chamada apenas pelo número de vezes igual ao número de dispositivos especificados na configuração do conjunto de dispositivos virtuais.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
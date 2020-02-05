---
title: IServerVirtualDeviceSet2::Open
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IServerVirtualDeviceSet2::Open.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 552394db26a1b236a4d6997f6dbfba77d12086ee
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70847217"
---
# <a name="iservervirtualdeviceset2open-vdi"></a>IServerVirtualDeviceSet2::Open (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A função **Open** abre o conjunto de dispositivos virtuais no servidor e precisa ser a primeira chamada feita usando o identificador de interface fornecido pelo COM.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IServerVirtualDeviceSet2::Open (
   LPCWSTR      lpInstanceName,
   LPCWSTR      lpName
);
```

## <a name="parameters"></a>parâmetros

*lpInstanceName* Essa cadeia de caracteres identifica a Instância do SQL Server à qual o comando SQL será enviado. NULL pode ser passado para identificar a instância padrão no computador atual.

*lpName* Isso é fornecido pela primeira cláusula VIRTUAL_DEVICE= do comando BACKUP ou RESTORE. Esse nome é usado como a chave para obter acesso ao conjunto de dispositivos virtuais criado pelo cliente.

## <a name="return-value"></a>Valor retornado

|Valor retornado | Explicação |
|---|---|
| NOERROR | A função foi bem-sucedida. |
| VD_E_INVALID | O nome fornecido não identificou um conjunto de dispositivos virtuais que é acessível ao servidor. |

## <a name="remarks"></a>Comentários

Depois que essa função for invocada com êxito, o servidor poderá continuar para configurar o conjunto de dispositivos virtuais usando GetConfiguration e SetConfiguration.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
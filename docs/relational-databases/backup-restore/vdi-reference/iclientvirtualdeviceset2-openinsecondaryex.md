---
title: IClientVirtualDeviceSet2::OpenInSecondaryEx
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IClientVirtualDeviceSet2::OpenInSecondaryEx.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: cd89359ecbcc920fe03ed4b2bc7d90fd01592476
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70847557"
---
# <a name="iclientvirtualdeviceset2openinsecondaryex-vdi"></a>IClientVirtualDeviceSet2::OpenInSecondaryEx (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A função **OpenInSecondaryEx** abre o dispositivo virtual definido em um cliente secundário. O cliente primário já deve ter usado CreateEx e GetConfiguration para configurar o conjunto de dispositivos virtuais.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IClientVirtualDeviceSet2::OpenInSecondaryEx (
   LPCWSTR      lpInstanceName,
   LPCWSTR      lpSetName
);
```

## <a name="parameters"></a>parâmetros

*lpInstanceName* Essa cadeia de caracteres identifica a Instância do SQL Server à qual o comando SQL será enviado.

*lpSetName* Isso identifica o conjunto. Esse nome diferencia maiúsculas de minúsculas e precisa corresponder ao nome usado pelo cliente primário quando ele invoca IClientVirtualDeviceSet2::Create.

## <a name="return-value"></a>Valor retornado

|Valor retornado | Explicação |
|---|---|
| NOERROR | A função foi bem-sucedida. |
| VD_E_PROTOCOL | O conjunto de dispositivos virtuais foi aberto ou não está pronto para aceitar solicitações abertas de clientes secundários. |
| VD_E_ABORT | A operação está sendo anulada. |

## <a name="remarks"></a>Comentários

Ao usar um modelo de processo múltiplo, o cliente primário é responsável por detectar o encerramento normal e anormal de clientes secundários.

O nome da instância precisa identificar a instância para a qual o T-SQL é emitido. NULL identifica a instância padrão. Nenhum "machineName\" é aceito.

OpenInSecondaryEx substitui o IClientVirtualDeviceSet::OpenInSecondary original que foi definido na interface do SQL Server versão 7.0 original. O novo desenvolvimento deveria usar OpenInSecondaryEx.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
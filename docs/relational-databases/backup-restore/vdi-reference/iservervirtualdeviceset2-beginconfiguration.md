---
title: IServerVirtualDeviceSet2::BeginConfiguration
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IServerVirtualDeviceSet2::BeginConfiguration.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: d188c79a558fcfe03b713a973cf0681822e24ba5
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85887620"
---
# <a name="iservervirtualdeviceset2beginconfiguration-vdi"></a>IServerVirtualDeviceSet2::BeginConfiguration (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

O servidor invoca a função **BeginConfiguration** para iniciar a configuração do conjunto de dispositivos virtuais.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IServerVirtualDeviceSet2::BeginConfiguration (
   DWORD   dwFeatures,
   DWORD   dwAlignment,
   DWORD   dwBlockSize,
   DWORD   dwMaxTransferSize,
   DWORD   dwTimeout
);
```

## <a name="parameters"></a>parâmetros

*dwFeatures* A máscara de recursos modificada. VDF_WriteMedia e/ou VDF_ReadMedia.

*dwAlignment* O alinhamento final. Se for 0, o padrão será dwBlockSize. Deve ser uma potência de 2, >= dwBlockSize e <= 64 KB.

*dwBlockSize* A unidade mínima de transferência, em bytes. Deve ser uma potência de 2, >=512 e <= 64 KB.

*dwMaxTransferSize* A maior transferência que será tentada. Deve ser um múltiplo de 64 KB.

*dwTimeout* Milissegundos para aguardar até que o cliente primário conclua a declaração das áreas do buffer que serão fornecidas.

## <a name="return-value"></a>Valor retornado

|Valor retornado | Explicação |
|---|---|
| NOERROR | O conjunto de dispositivos virtuais está no estado Configurável. |
| VD_E_ABORT | O SignalAbort foi invocado. |
| VD_E_PROTOCOL | O conjunto de dispositivos virtuais não está no estado Conectado. |

## <a name="remarks"></a>Comentários

Depois que a função for invocada, o conjunto de dispositivos virtuais será movido para o estado Configurável, no qual o layout do buffer será decidido.
Depois que a configuração básica for definida (de acordo com os parâmetros), esses valores permanecerão fixos durante a vida útil do conjunto de dispositivos virtuais. A propriedade de alinhamento do conjunto de dispositivos virtuais é usada para controlar o alinhamento de buffers de dados. Esse valor define um valor de alinhamento mínimo que pode ser substituído de acordo com o buffer.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
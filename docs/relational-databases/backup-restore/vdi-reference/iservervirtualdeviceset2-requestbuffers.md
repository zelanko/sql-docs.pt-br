---
title: IServerVirtualDeviceSet2::RequestBuffers
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IServerVirtualDeviceSet2::RequestBuffers.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1b941f251c9093f10abbced8c3522f1719a1580e
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847177"
---
# <a name="iservervirtualdeviceset2requestbuffers-vdi"></a>IServerVirtualDeviceSet2::RequestBuffers (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A função **RequestBuffers** informa à VDI de que o servidor precisará de determinado número de buffers com um requisito de tamanho e alinhamento especificado.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IServerVirtualDeviceSet2::RequestBuffers (
   DWORD   dwSize,
   DWORD   dwAlignment,
   DWORD   dwCount
);
```

## <a name="parameters"></a>Parâmetros

*dwSize* Identifica o tamanho de cada buffer. Esse tamanho deve incluir apenas a região necessária para os dados. A VDI cuida dos requisitos de alinhamento e prefixo.

*dwAlignment* O alinhamento necessário para esses buffers. Um valor mais restritivo do que o valor de alinhamento básico especificado com 'BeginConfiguration' pode ser usado. Se o valor for 0, ele usará como padrão o valor de alinhamento básico.

*dwCount* O número de buffers que serão solicitados por 'AllocateBuffer' com o tamanho e o alinhamento especificados.

## <a name="return-value"></a>Valor retornado

|Valor retornado | Explicação |
|---|---|
| NOERROR | A função foi bem-sucedida. |
| VD_E_ABORT | A anulação foi solicitada. |
| VD_E_PROTOCOL | O conjunto não está em um estado no qual as alocações de buffer possam ser declaradas (confira a matriz de transição de estado). |
| VD_E_MEMORY | A memória solicitada não pôde ser obtida. |

## <a name="remarks"></a>Remarks

Esse método deve ser usado antes que os buffers sejam alocados com AllocateBuffer. Conjuntos de buffers com um tamanho e um alinhamento especificados são solicitados com RequestBuffers e, em seguida, buffers individuais são alocados com AllocateBuffer.

Durante a fase de configuração, as chamadas a RequestBuffers são somadas para que, na chamada a EndConfiguration, uma única área de buffer possa ser usada (alocada nesse momento). Após a conclusão da configuração, todas as chamadas de RequestBuffers resultarão na alocação imediata de mais espaço do buffer.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
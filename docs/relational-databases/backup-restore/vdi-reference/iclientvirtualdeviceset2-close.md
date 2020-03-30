---
title: IClientVirtualDeviceSet2::Close
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IClientVirtualDeviceSet2::Close.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 5f87b375773b9c81b29b3b5cac11ea97121c45df
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "70847377"
---
# <a name="iclientvirtualdeviceset2close-vdi"></a>IClientVirtualDeviceSet2::Close (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A função **Close** fecha o conjunto de dispositivos virtuais criado por IClientVirtualDeviceSet2::Create. Isso resulta na liberação de todos os recursos associados ao conjunto de dispositivos virtuais.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IClientVirtualDeviceSet2::Close ();
```

## <a name="return-value"></a>Valor retornado

|Valor retornado | Explicação |
|---|---|
| NOERROR | Isso é retornado quando o conjunto de dispositivos virtuais é fechado com êxito. |
| VD_E_PROTOCOL | Nenhuma ação foi executada porque o conjunto de dispositivos virtuais não estava aberto. |
| VD_E_OPEN | Os dispositivos ainda estavam abertos. |

## <a name="remarks"></a>Comentários

A invocação de Close é uma declaração do cliente de que todos os recursos usados pelo conjunto de dispositivos virtuais devem ser liberados. O cliente precisa garantir que todas as atividades que envolvem buffers de dados e dispositivos virtuais sejam encerradas antes da invocação de Close. Todas as interfaces de dispositivos virtuais retornadas por OpenDevice são invalidadas por Close.

O cliente tem permissão para emitir uma chamada Create na interface do conjunto de dispositivos virtuais depois que a chamada Close é retornada. Essa chamada criará um novo conjunto de dispositivos virtuais para uma operação BACKUP ou RESTORE seguinte.

Se Close for chamado quando um ou mais dispositivos virtuais ainda estiverem abertos, VD_E_OPEN será retornado. Nesse caso, SignalAbort é disparado internamente, para garantir um desligamento adequado, se possível. Os recursos de VDI são liberados. O cliente deve aguardar uma indicação de VD_E_CLOSE em cada dispositivo antes de invocar IClientVirtualDeviceSet2::Close. Se o cliente souber que o conjunto de dispositivos virtuais já está em um estado Encerrado de Modo Anormal, ele não deverá esperar uma indicação VD_E_CLOSE de GetCommand e poderá invocar IClientVirtualDeviceSet2::Close assim que a atividade nos buffers compartilhados for encerrada.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
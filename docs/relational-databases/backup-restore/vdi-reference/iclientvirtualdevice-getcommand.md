---
title: IClientVirtualDevice::GetCommand
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IClientVirtualDevice::GetCommand.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 7665d541663097452fa9aaeba4f30dcd95c75232
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896932"
---
# <a name="iclientvirtualdevicegetcommand-vdi"></a>IClientVirtualDevice::GetCommand (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

A função **GetCommand** é usada para obter o próximo comando enfileirado para um dispositivo. Quando solicitada, essa função aguarda o próximo comando.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IClientVirtualDevice::GetCommand (
   DWORD               dwTimeOut,
   VDC_Command**      const ppCmd
);
```

## <a name="parameters"></a>parâmetros

*ppCmd* Quando um comando é retornado com êxito, o parâmetro retorna o endereço de um comando a ser executado. A memória retornada é somente leitura. Quando o comando é concluído, esse ponteiro é passado para a rotina CompleteCommand. Para obter mais informações sobre cada comando, confira Comandos.

*dwTimeOut* Este é o tempo de espera, em milissegundos. Use INFINITE para aguardar indefinidamente. Use 0 para sondar um comando. VD_E_TIMEOUT será retornado se nenhum comando estiver disponível no momento. Se o tempo limite esgotar, o cliente decidirá a próxima ação.

## <a name="return-value"></a>Valor retornado

|Valor retornado | Explicação |
|---|---|
| NOERROR | Foi efetuado fetch de um comando. |
| VD_E_CLOSE | O dispositivo foi fechado pelo servidor. |
| VD_E_TIMEOUT | Nenhum comando estava disponível e o tempo limite expirou. |
| VD_E_ABORT | O cliente ou o servidor usou o SignalAbort para forçar um desligamento. |

## <a name="remarks"></a>Comentários

Quando VD_E_CLOSE é retornado, o SQL Server fecha o dispositivo. Isso faz parte do desligamento normal. Depois que todos os dispositivos forem fechados, o cliente invocará IClientVirtualDeviceSet2::Close para fechar o conjunto de dispositivos virtuais.

Quando essa rotina precisa ser bloqueada para aguardar um comando, o thread é deixado em uma condição Passível de Alerta.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
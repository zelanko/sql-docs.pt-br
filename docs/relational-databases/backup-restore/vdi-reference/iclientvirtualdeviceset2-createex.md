---
title: IClientVirtualDeviceSet2::CreateEx
titlesuffix: SQL Server VDI reference
description: Este artigo fornece referência para o comando IClientVirtualDeviceSet2::CreateEx.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 90165738dfcea8818353d602f72390bb08eea792
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "70847347"
---
# <a name="iclientvirtualdeviceset2createex-vdi"></a>IClientVirtualDeviceSet2::CreateEx (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

A função **CreateEx** cria o conjunto de dispositivos virtuais.

## <a name="syntax"></a>Sintaxe

```c
HRESULT IClientVirtualDeviceSet2::CreateEx (
   LPCWSTR         lpInstanceName,
   LPCWSTR         lpName,
   VDConfig*      pCfg
);
```

## <a name="parameters"></a>parâmetros

*lpInstanceName* Essa cadeia de caracteres identifica a Instância do SQL Server à qual o comando SQL será enviado.

*lpName* Isso identifica o conjunto de dispositivos virtuais. As regras para nomes usados por CreateFileMapping() precisam ser seguidas. Qualquer caractere, exceto barra invertida (\) pode ser usado). Essa é uma cadeia de caracteres Unicode de caractere largo. É recomendável prefixar a cadeia de caracteres com o nome do produto ou da empresa do usuário e o nome do banco de dados.

*pCfg* Essa é a configuração do conjunto de dispositivos virtuais. Para obter mais informações, confira Configuração.

## <a name="return-value"></a>Valor retornado

|Valor retornado | Explicação |
|---|---|
| NOERROR | A função foi bem-sucedida. |
| VD_E_NOTSUPPORTED | Um ou mais campos na configuração eram inválidos ou não tinham suporte. |
| VD_E_PROTOCOL | O conjunto de dispositivos virtuais foi criado. |

## <a name="remarks"></a>Comentários

O método CreateEx deve ser chamado apenas uma vez por operação BACKUP ou RESTORE. Depois de invocar o método Close, o cliente pode reutilizar a interface para criar outro conjunto de dispositivos virtuais.

O nome da instância precisa identificar a instância para a qual o Transact-SQL é emitido. NULL identifica a instância padrão. Nenhum "machineName\" é aceito.

As chamadas CreateEx (e Create) modificarão a DACL de segurança no identificador de processo no processo do cliente. Por isso, qualquer outra modificação do identificador de processo precisa ser serializada com a invocação de CreateEx. CreateEx será serializado com outras chamadas a CreateEx, mas não pode ser serializada com processamento externo. O acesso é concedido à conta que executa o serviço SQL Server.

O método CreateEx substitui o método Create definido no IClientVirtualDeviceSet original. O método Create original foi preterido e não deve ser usado em desenvolvimento futuro. O método Create original implementa uma forma de suporte de nome da instância com a variável de ambiente _VIRTUAL_SERVER_NAME_. Se essa variável for definida no ambiente, o método Create chamará CreateEx internamente, passando o valor de _VIRTUAL_SERVER_NAME_ como o nome da instância.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações, confira a [Visão geral da referência da interface de dispositivo virtual do SQL Server](reference-virtual-device-interface.md).
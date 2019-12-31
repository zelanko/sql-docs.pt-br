---
title: Configurando o TLS 1,2
description: Recomendação para configurar o TLS 1,2 no APS
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 10/29/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 988cac765a596b541d128b0b6190f6f228d95ee7
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401248"
---
# <a name="configure-tls-12-in-aps"></a>Configurar o TLS 1,2 no APS

Para proteger os APS para usar apenas o TLS 1,2, você terá que desabilitar explicitamente outro protocolo em todos os hosts físicos e virtuais. A desabilitação de protocolos requer alterações de configuração do registro. As alterações de registro exigem uma reinicialização dos hosts virtuais e físicos.

> [!WARNING]
> Esta seção, método ou tarefa contêm as etapas que indicam como modificar o Registro. No entanto, problemas sérios podem ocorrer se você modificar o registro incorretamente, o que pode causar perda de dados e exigir a reinstalação do sistema operacional. É altamente recomendável fazer backup do registro antes de modificá-lo. Em seguida, restaure o Registro se ocorrer algum problema. Para obter mais informações sobre como fazer backup e restaurar o registro, clique no número de artigo a seguir para exibir o artigo na base de dados de conhecimento Microsoft:<br>
[322756](https://support.microsoft.com/help/322756) como fazer backup e restaurar o registro no Windows

**Desativar**
```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0]
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1]
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server]
"Enabled"=dword:00000000
"DisabledByDefault"=dword:00000001
```

Além disso, defina as seguintes chaves em seus computadores cliente onde as ferramentas como os adaptadores de destino do APS SSIS estão instaladas.
```
[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319]
"SystemDefaultTlsVersions"=dword:00000001
"SchUseStrongCrypto"=dword:00000001 
```




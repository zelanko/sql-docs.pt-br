---
title: referência de mssqlctl
titleSuffix: SQL Server 2019 big data clusters
description: Artigo de referência para comandos mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: be1ece46bd171370a91273c832bf89a0bf426cd3
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018362"
---
# <a name="mssqlctl"></a>mssqlctl

O artigo a seguir fornece referência para o **mssqlctl** ferramenta para clusters de big data de 2019 do SQL Server (versão prévia).

## <a id="commands"></a> Comandos

|||
|---|---|
| [app](reference-mssqlctl-app.md) | Criar, excluir, executar e gerenciar aplicativos. |
| [cluster](reference-mssqlctl-cluster.md) | Selecionar, gerenciar e operar clusters. |
| [login](#login) | Faça logon no cluster. |
| [logout](#logout) | Faça logoff do cluster. |
| [storage](reference-mssqlctl-storage.md) | Gerencie o armazenamento de cluster. |

## <a id="login"></a> logon de mssqlctl

Faça logon no cluster.

```
mssqlctl login
   --endpoint
   --password
   --username
```

### <a name="parameters"></a>Parâmetros

| Parâmetro | Descrição |
|---|---|
|**--endpoint -e**| Cluster de host e a porta (ex) `http://host:port"`. |
|**-senha -p**| Credenciais de senha. |
|**--username -u**| Conta do usuário. |

### <a name="examples"></a>Exemplos

Faça logon interativamente.

```
mssqlctl login
```

Faça logon com nome de usuário e senha.

```
mssqlctl login -u johndoe@contoso.com -p VerySecret
```

Faça logon com nome de usuário, senha e ponto de extremidade do cluster.

```
mssqlctl login -u johndoe@contoso.com -p VerySecret --endpoint https://host.com:12800
```

## <a id="logout"></a> mssqlctl logout

Faça logoff do cluster.

```
mssqlctl logout
   --username
```

### <a name="parameters"></a>Parâmetros

| Parâmetros | Descrição |
|---|---|
| **--username -u** | Usuário da conta, se estiverem ausentes, a conta do Active Directory atual de logout. |

### <a name="examples"></a>Exemplos

Fazer logoff deste usuário.

```
mssqlctl logout --username admin
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre como instalar o **mssqlctl** ferramenta, consulte [instalar mssqlctl para gerenciar os clusters do SQL Server 2019 grandes dados](deploy-install-mssqlctl.md).
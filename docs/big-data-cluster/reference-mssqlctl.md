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
ms.openlocfilehash: d15b4149fe336b173452030ec67fb7f229e6ae3d
ms.sourcegitcommit: d7ed341b2c635dcdd6b0f5f4751bb919a75a6dfe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/06/2019
ms.locfileid: "57527279"
---
# <a name="mssqlctl"></a>mssqlctl

O artigo a seguir fornece referência para o **mssqlctl** ferramenta para [clusters de big data de 2019 do SQL Server (visualização)](big-data-cluster-overview.md). Para obter mais informações sobre como instalar o **mssqlctl** ferramenta, consulte [instalar mssqlctl para gerenciar os clusters do SQL Server 2019 grandes dados](deploy-install-mssqlctl.md).

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
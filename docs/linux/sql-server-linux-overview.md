---
title: Visão geral do SQL Server no Linux | Microsoft Docs
description: Este artigo descreve como o SQL Server é executado no Linux e fornece informações sobre como obter mais informações.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 9dcc6a90-0add-42c2-815b-862e4e2a21ac
ms.openlocfilehash: 1f89e4f093c2216c90f133bdf38298272ea57f18
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66713243"
---
# <a name="sql-server-on-linux"></a>SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

::: moniker range="= sql-server-2017 || = sqlallproducts-allversions"
Começando com o SQL Server 2017, o SQL Server é executado no Linux. É o mesmo mecanismo de banco de dados do SQL Server, com muitos recursos e serviços, independentemente de seu sistema operacional semelhante.
::: moniker-end

::: moniker range=">= sql-server-ver15 || >= sql-server-linux-ver15"
Visualização do SQL Server 2019 é executado no Linux. É o mesmo mecanismo de banco de dados do SQL Server, com muitos recursos e serviços, independentemente de seu sistema operacional semelhante. Para obter mais informações sobre esta versão, consulte [quais são as novidades na visualização de 2019 do SQL Server para Linux](../sql-server/what-s-new-in-sql-server-ver15.md#sql-server-on-linux).
::: moniker-end

::: moniker range="= sql-server-2017"
> [!TIP]
> [Visualização do SQL Server 2019](sql-server-linux-overview.md?view=sql-server-ver15) foi lançado! Para descobrir as novidades do Linux na versão mais recente, consulte [quais são as novidades na visualização de 2019 do SQL Server para Linux](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux).
::: moniker-end

::: moniker range="= sql-server-linux-2017"
> [!TIP]
> [Visualização do SQL Server 2019](sql-server-linux-overview.md?view=sql-server-linux-ver15) foi lançado! Para descobrir as novidades do Linux na versão mais recente, consulte [quais são as novidades na visualização de 2019 do SQL Server para Linux](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-linux-ver15#sql-server-on-linux).
::: moniker-end

::: moniker range="= sqlallproducts-allversions"
> [!TIP]
> Visualização de 2019 do SQL Server foi lançada! Para descobrir as novidades do Linux na versão mais recente, consulte [quais são as novidades na visualização de 2019 do SQL Server para Linux](../sql-server/what-s-new-in-sql-server-ver15.md#sql-server-on-linux).
::: moniker-end

## <a name="install"></a>Instalar

Para começar, instale o SQL Server no Linux usando um dos seguintes inícios rápidos:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-docker.md)
- [Provisionar uma VM SQL no Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

> [!NOTE]
> Docker em si é executado em várias plataformas, que significa que você pode executar a imagem do Docker no Linux, Mac e Windows.

## <a name="connect"></a>Conectar

Após a instalação, conecte-se à instância do SQL Server no computador Linux. Você pode se conectar localmente ou remotamente e com uma variedade de ferramentas e drivers. Os inícios rápidos demonstram como usar o [sqlcmd](sql-server-linux-setup-tools.md) ferramenta de linha de comando. Outras ferramentas incluem o seguinte:

| Ferramenta | Tutorial |
|-----|-----|
| Visual Studio Code (VS Code) | [Usar o VS Code com o SQL Server no Linux](sql-server-linux-develop-use-vscode.md) |
| SQL Server Management Studio (SSMS) | [Use o SSMS no Windows para se conectar ao SQL Server no Linux](sql-server-linux-manage-ssms.md) |
| SQL Server Data Tools (SSDT) | [Use o SSDT com o SQL Server no Linux](sql-server-linux-develop-use-ssdt.md) |

## <a name="explore"></a>Explorar

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

SQL Server 2017 tem o mesmo mecanismo de banco de dados subjacente em todas as plataformas com suporte, incluindo Linux. Portanto, muitos recursos e recursos existentes funcionam da mesma forma no Linux. Esta área da documentação expõe alguns desses recursos de uma perspectiva de Linux. Ele também chama as áreas que têm requisitos exclusivos no Linux.

Se você já estiver familiarizado com o SQL Server, examine os [notas de versão](sql-server-linux-release-notes.md) para diretrizes gerais e problemas conhecidos desta versão. Em seguida, examine [o que há de novo para o SQL Server no Linux](sql-server-linux-whats-new.md) , bem como [novidades do SQL Server 2017 geral](../sql-server/what-s-new-in-sql-server-2017.md).

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15"

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] tem o mesmo mecanismo de banco de dados subjacente em todas as plataformas com suporte, incluindo Linux. Portanto, muitos recursos e recursos existentes funcionam da mesma forma no Linux. Esta área da documentação expõe alguns desses recursos de uma perspectiva de Linux. Ele também chama as áreas que têm requisitos exclusivos no Linux.

Se você já estiver familiarizado com o SQL Server no Linux, examine os [notas de versão](sql-server-linux-release-notes-2019.md) para diretrizes gerais e problemas conhecidos desta versão. Em seguida, examine [o que há de novo para visualização de 2019 do SQL Server no Linux](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15).

::: moniker-end

<!--SQL Server All Versions-->
::: moniker range="=sqlallproducts-allversions"

SQL Server 2017 e [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] têm o mesmo mecanismo de banco de dados subjacente em todas as plataformas com suporte, incluindo Linux. Portanto, muitos recursos e recursos existentes funcionam da mesma forma no Linux. Esta área da documentação expõe alguns desses recursos de uma perspectiva de Linux. Ele também chama as áreas que têm requisitos exclusivos no Linux.

Se você já estiver familiarizado com o SQL Server no Linux, examine as notas de versão:

- [Notas de versão do SQL Server 2017](sql-server-linux-release-notes.md)
- [Notas de versão de preview do SQL Server de 2019](sql-server-linux-release-notes-2019.md)

Em seguida, examine o que há de novo:

- [Quais são as novidades do SQL Server 2017](sql-server-linux-whats-new.md)
- [O que há de novo para visualização de 2019 do SQL Server no Linux](../sql-server/what-s-new-in-sql-server-ver15.md#sql-server-on-linux)

::: moniker-end

> [!TIP]
> Para obter respostas para perguntas frequentes, consulte o [SQL Server nas perguntas frequentes sobre o Linux](sql-server-linux-faq.md).

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

---
title: Visão geral do SQL Server em Linux
description: Este artigo descreve como o SQL Server é executado no Linux e fornece informações sobre como saber mais a respeito.
author: VanMSFT
ms.author: vanto
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 9dcc6a90-0add-42c2-815b-862e4e2a21ac
ms.openlocfilehash: 31904a43dba642c73620a66bcf4abaa066b5ef82
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "73531280"
---
# <a name="sql-server-on-linux"></a>SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

::: moniker range="= sql-server-2017 || = sqlallproducts-allversions"
Do SQL Server 2017 em diante, o SQL Server é executado no Linux. É o mesmo mecanismo de banco de dados do SQL Server, com muitos recursos e serviços semelhantes, independentemente do sistema operacional.
::: moniker-end

::: moniker range=">= sql-server-ver15 || >= sql-server-linux-ver15"
O SQL Server 2019 é executado no Linux. É o mesmo mecanismo de banco de dados do SQL Server, com muitos recursos e serviços semelhantes, independentemente do sistema operacional. Para saber mais sobre essa versão, confira [Novidades no SQL Server 2019 para Linux](sql-server-linux-whats-new-2019.md).
::: moniker-end

::: moniker range="= sql-server-2017"
> [!TIP]
> O [SQL Server 2019](sql-server-linux-overview.md?view=sql-server-ver15) está disponível. Para conhecer as novidades da versão mais recente para Linux, confira [Novidades no SQL Server 2019 para Linux](sql-server-linux-whats-new-2019.md?view=sql-server-ver15).
::: moniker-end

::: moniker range="= sql-server-linux-2017"
> [!TIP]
> O [SQL Server 2019](sql-server-linux-overview.md?view=sql-server-linux-ver15) está disponível. Para conhecer as novidades da versão mais recente para Linux, confira [Novidades no SQL Server 2019 para Linux](sql-server-linux-whats-new-2019.md?view=sql-server-linux-ver15).
::: moniker-end

::: moniker range="= sqlallproducts-allversions"
> [!TIP]
> O SQL Server 2019 está disponível. Para conhecer as novidades da versão mais recente para Linux, confira [Novidades no SQL Server 2019 para Linux](sql-server-linux-whats-new-2019.md).
::: moniker-end

## <a name="install"></a>Instalar

Para começar, instale o SQL Server em Linux usando um dos seguintes inícios rápidos:

- [Instalação no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalação no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-docker.md)
- [Provisionar uma VM SQL no Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

> [!NOTE]
> O Docker é executado em várias plataformas, o que significa que você pode executar a imagem do Docker no Linux, no Mac e no Windows.

## <a name="connect"></a>Conectar

Após a instalação, conecte-se à instância do SQL Server no computador Linux. Você pode se conectar localmente ou remotamente e com uma variedade de ferramentas e drivers. Os inícios rápidos demonstram como usar a ferramenta de linha de comando [sqlcmd](sql-server-linux-setup-tools.md). Outras ferramentas incluem as seguintes:

| Ferramenta | Tutorial |
|-----|-----|
| VS Code (Visual Studio Code) | [Usar o VS Code com o SQL Server em Linux](sql-server-linux-develop-use-vscode.md) |
| SQL Server Management Studio (SSMS) | [Usar o SSMS no Windows para se conectar ao SQL Server em Linux](sql-server-linux-manage-ssms.md) |
| SQL Server Data Tools (SSDT) | [Usar o SSDT com o SQL Server em Linux](sql-server-linux-develop-use-ssdt.md) |

## <a name="explore"></a>Explorar

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

O SQL Server 2017 tem o mesmo mecanismo de banco de dados subjacente em todas as plataformas compatíveis, incluindo o Linux. Portanto, muitos recursos e funcionalidades existentes funcionam da mesma maneira no Linux. Esta área da documentação expõe alguns desses recursos sob uma perspectiva voltada para o Linux. Ela também chama áreas que têm requisitos exclusivos no Linux.

Se você já estiver familiarizado com o SQL Server, examine as [Notas sobre a versão](sql-server-linux-release-notes.md) para ver as diretrizes gerais e os problemas conhecidos desta versão. Em seguida, veja as [novidades do SQL Server em Linux](sql-server-linux-whats-new.md), bem como as [novidades do SQL Server 2017 em geral](../sql-server/what-s-new-in-sql-server-2017.md).

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15"

O [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] tem o mesmo mecanismo de banco de dados subjacente em todas as plataformas compatíveis, incluindo o Linux. Portanto, muitos recursos e funcionalidades existentes funcionam da mesma maneira no Linux. Esta área da documentação expõe alguns desses recursos sob uma perspectiva voltada para o Linux. Ela também chama áreas que têm requisitos exclusivos no Linux.

Se você já estiver familiarizado com o SQL Server em Linux, examine as [Notas sobre a versão](sql-server-linux-release-notes-2019.md) para ver as diretrizes gerais e os problemas conhecidos desta versão. Em seguida, confira as [novidades no SQL Server 2019 em Linux](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15).

::: moniker-end

<!--SQL Server All Versions-->
::: moniker range="=sqlallproducts-allversions"

O SQL Server 2017 e o [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] têm o mesmo mecanismo de banco de dados subjacente em todas as plataformas compatíveis, incluindo o Linux. Portanto, muitos recursos e funcionalidades existentes funcionam da mesma maneira no Linux. Esta área da documentação expõe alguns desses recursos sob uma perspectiva voltada para o Linux. Ela também chama áreas que têm requisitos exclusivos no Linux.

Se você já estiver familiarizado com o SQL Server em Linux, examine as notas sobre a versão:

- [Notas de versão do SQL Server 2017](sql-server-linux-release-notes.md)
- [Notas sobre a versão do SQL Server 2019](sql-server-linux-release-notes-2019.md)

Em seguida, veja o que há de novo:

- [Novidades do SQL Server 2017](sql-server-linux-whats-new.md)
- [Novidades do SQL Server 2019 em Linux](../sql-server/what-s-new-in-sql-server-ver15.md#sql-server-on-linux)

::: moniker-end

> [!TIP]
> Para obter respostas a perguntas frequentes, confira as [Perguntas frequentes sobre o SQL Server em Linux](sql-server-linux-faq.md).

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

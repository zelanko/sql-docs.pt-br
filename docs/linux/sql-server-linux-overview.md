---
title: Visão geral do SQL Server no Linux | Microsoft Docs
description: Este artigo descreve como o SQL Server é executado no Linux e fornece informações sobre como obter mais informações.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 06/20/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 9dcc6a90-0add-42c2-815b-862e4e2a21ac
ms.openlocfilehash: 16ea8b69f1d55e5b338931f0531bdf8a2e037707
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38020134"
---
# <a name="sql-server-on-linux"></a>SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

O SQL Server 2017 agora é executado no Linux. Ele tem o mesmo mecanismo de banco de dados do SQL Server, com uma variedade maior de recursos e serviços, independentemente do sistema operacional que esteja sendo executado na máquina.

## <a name="install"></a>Instalar

Para começar, instale o SQL Server no Linux usando um dos seguintes inícios rápidos:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-docker.md)
- [Provisionar uma VM SQL no Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

> [!NOTE]
> Docker em si é executado em várias plataformas, que significa que você pode executar a imagem do Docker no Linux, Mac e Windows.

## <a name="connect"></a>Connect

Após a instalação, conecte-se à instância do SQL Server no computador Linux. Você pode se conectar localmente ou remotamente e com uma variedade de ferramentas e drivers. Os inícios rápidos demonstram como usar o [sqlcmd](sql-server-linux-setup-tools.md) ferramenta de linha de comando. Outras ferramentas incluem o seguinte:

| Ferramenta | Tutorial |
|-----|-----|
| Visual Studio Code (VS Code) | [Usar o VS Code com o SQL Server no Linux](sql-server-linux-develop-use-vscode.md) |
| SQL Server Management Studio (SSMS) | [Use o SSMS no Windows para se conectar ao SQL Server no Linux](sql-server-linux-manage-ssms.md) |
| SQL Server Data Tools (SSDT) | [Use o SSDT com o SQL Server no Linux](sql-server-linux-develop-use-ssdt.md) |

## <a name="explore"></a>Explorar

SQL Server 2017 tem o mesmo mecanismo de banco de dados subjacente em todas as plataformas com suporte, incluindo Linux. Muitos recursos e recursos existentes funcionam da mesma forma no Linux. Esta área da documentação expõe alguns desses recursos de uma perspectiva de Linux. Ele também chama as áreas que têm requisitos exclusivos no Linux.

Se você já estiver familiarizado com o SQL Server, examine os [notas de versão](sql-server-linux-release-notes.md) para diretrizes gerais e problemas conhecidos desta versão. Em seguida, examine [o que há de novo para o SQL Server no Linux](sql-server-linux-whats-new.md) , bem como [novidades do SQL Server 2017 geral](../sql-server/what-s-new-in-sql-server-2017.md). 

> [!TIP]
> Para obter respostas para perguntas frequentes, consulte o [SQL Server nas perguntas frequentes sobre o Linux](sql-server-linux-faq.md).

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
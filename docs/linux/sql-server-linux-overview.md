---
title: Visão geral do SQL Server no Linux | Microsoft Docs
description: Este artigo descreve como o SQL Server é executado no Linux e fornece informações sobre como saber mais.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/24/2018
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 9dcc6a90-0add-42c2-815b-862e4e2a21ac
ms.openlocfilehash: 2c67e5d1563ef2420f45ec4b1d0093de888dd157
ms.sourcegitcommit: a9da0abd3e17fbcd6339980d7331d0418cdada53
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/24/2018
ms.locfileid: "34473840"
---
# <a name="sql-server-on-linux"></a>SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

O SQL Server 2017 agora é executado no Linux. Ele tem o mesmo mecanismo de banco de dados do SQL Server, com uma variedade maior de recursos e serviços, independentemente do sistema operacional que esteja sendo executado na máquina.

## <a name="install"></a>Instalar

Para começar, instale o SQL Server no Linux usando um dos tutoriais a seguir:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-docker.md)
- [Provisionar uma VM SQL no Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

> [!NOTE]
> Docker em si é executado em várias plataformas, que significa que você pode executar a imagem do Docker no Windows, Mac e Linux.

## <a name="connect"></a>Connect

Após a instalação, conecte-se à instância do SQL Server no computador Linux. Você pode se conectar localmente ou remotamente e com uma variedade de ferramentas e drivers. Os tutoriais demonstram como usar o [sqlcmd](sql-server-linux-setup-tools.md) ferramenta de linha de comando. Outras ferramentas incluem o seguinte:

| Ferramenta | Tutorial |
|-----|-----|
| Código do Visual Studio (VS código) | [Use o código do VS com o SQL Server no Linux](sql-server-linux-develop-use-vscode.md) |
| SQL Server Management Studio (SSMS) | [Use o SSMS no Windows para se conectar ao SQL Server no Linux](sql-server-linux-manage-ssms.md) |
| SQL Server Data Tools (SSDT) | [Use o SSDT com o SQL Server no Linux](sql-server-linux-develop-use-ssdt.md) |

## <a name="explore"></a>Explorar

SQL Server 2017 tem o mesmo mecanismo de banco de dados subjacente em todas as plataformas com suporte, inclusive Linux. Muitos recursos e recursos existentes funcionam da mesma forma no Linux. Esta área da documentação expõe alguns desses recursos de uma perspectiva de Linux. Ele também chama áreas que tem requisitos exclusivos no Linux.

Se você já estiver familiarizado com o SQL Server, examine o [notas de versão](sql-server-linux-release-notes.md) para diretrizes gerais e problemas conhecidos desta versão. Em seguida, examinar [novidades do SQL Server no Linux](sql-server-linux-whats-new.md) , bem como [novidades do SQL Server 2017 geral](../sql-server/what-s-new-in-sql-server-2017.md). 

> [!TIP]
> Para obter respostas para perguntas frequentes, consulte o [SQL Server nas perguntas frequentes sobre o Linux](sql-server-linux-faq.md).

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
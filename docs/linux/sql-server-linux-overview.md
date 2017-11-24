---
title: "Visão geral do SQL Server no Linux | Microsoft Docs"
description: "Este tópico descreve como o SQL Server é executado no Linux e fornece informações sobre como saber mais."
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 9dcc6a90-0add-42c2-815b-862e4e2a21ac
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 80c1228faeaaa4012afc0fd27992a2f5cf389f6e
ms.openlocfilehash: 48e2d1ae54100f7ea83bdd677bf4a98859825b67
ms.contentlocale: pt-br
ms.lasthandoff: 10/05/2017

---
# <a name="sql-server-on-linux"></a>SQL Server no Linux

O SQL Server 2017 agora é executado no Linux. Ele tem o mesmo mecanismo de banco de dados do SQL Server, com uma variedade maior de recursos e serviços, independentemente do sistema operacional que esteja sendo executado na máquina.

## <a name="install"></a>Instalar

Para começar, instale o SQL Server no Linux usando um dos seguintes tutoriais de início rápido:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-docker.md)
- [Provisionar uma VM SQL no Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

> [!NOTE]
> Docker em si é executado em várias plataformas, que significa que você pode executar a imagem do Docker no Windows, Mac e Linux.

## <a name="connect"></a>Connect

Após a instalação, conecte-se à instância do SQL Server no computador que esteja executando o Linux. É possivel se conectar localmente ou remotamente e com uma variedade de ferramentas e drivers. Os tutoriais de início rápido demonstram como usar o [sqlcmd](sql-server-linux-setup-tools.md) ferramenta de linha de comando. Outras ferramentas incluem o seguinte:

| Ferramenta | Tutorial |
|-----|-----|
| Código do Visual Studio (VS código) | [Use o código do VS com o SQL Server no Linux](sql-server-linux-develop-use-vscode.md) |
| SQL Server Management Studio (SSMS) | [Use o SSMS no Windows para se conectar ao SQL Server no Linux](sql-server-linux-develop-use-ssms.md) |
| SQL Server Data Tools (SSDT) | [Use o SSDT com o SQL Server no Linux](sql-server-linux-develop-use-ssdt.md) |

## <a name="explore"></a>Explorar

SQL Server 2017 tem o mesmo mecanismo de banco de dados subjacente em todas as plataformas com suporte, inclusive Linux. Muitos recursos e recursos existentes funcionam da mesma forma no Linux. Esta área da documentação expõe alguns desses recursos de uma perspectiva de Linux. Ele também chama áreas que tem requisitos exclusivos no Linux.

Se você já estiver familiarizado com o SQL Server, examine o [notas de versão](sql-server-linux-release-notes.md) para diretrizes gerais e problemas conhecidos desta versão. Em seguida, examinar [novidades do SQL Server no Linux](sql-server-linux-whats-new.md) , bem como [novidades do SQL Server 2017 geral](../sql-server/what-s-new-in-sql-server-2017.md).

##  <a name="infotipmediageneralinfotippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](./media/general/info_tip.png) Entre em contato com a equipe de engenharia do SQL Server

- [DBA pilha Exchange](https://dba.stackexchange.com/questions/tagged/sql-server): faça perguntas de administração de banco de dados
- [Estouro de pilha](http://stackoverflow.com/questions/tagged/sql-server): faça perguntas de desenvolvimento
- [Fóruns do MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver): questões técnicas
- [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback): relatório de bugs e o recurso de solicitação
- [Reddit](https://www.reddit.com/r/SQLServer/): discutir do SQL Server


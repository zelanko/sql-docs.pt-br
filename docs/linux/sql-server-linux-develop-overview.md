---
title: Desenvolver aplicativos para o SQL Server no Linux | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 758cb738-b018-465b-9ab0-59a24b892e66
ms.openlocfilehash: 4d3ef46dfbacb1c4cbfe67df555b79fb10ade86d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705820"
---
# <a name="how-to-get-started-developing-applications-for-sql-server-on-linux"></a>Como começar a desenvolver aplicativos para o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Você pode criar aplicativos que se conectam ao usam o SQL Server no Linux, de uma variedade de linguagens de programação, como c#, Java, Node. js, PHP, Python, Ruby e C++. Você também pode usar estruturas web populares e estruturas de objeto ORM (mapeamento relacional).

> [!VIDEO https://channel9.msdn.com/events/Connect/2017/T153/player]

> [!TIP]
> Essas mesmas opções de desenvolvimento também habilitar destino do SQL Server em outras plataformas. Aplicativos podem direcionar o SQL Server em execução no local ou na nuvem, no Linux, Windows ou Docker no macOS. Ou você pode direcionar o banco de dados SQL e Azure SQL Data Warehouse.

## <a name="try-the-tutorials"></a>Experimente os tutoriais

A melhor maneira de começar e criar aplicativos com o SQL Server é experimentá-lo por conta própria.

- Navegue até [tutoriais de Introdução](https://aka.ms/sqldev).
- Selecione seu idioma e plataforma de desenvolvimento.
- Experimente os exemplos de código.

> [!TIP]
> Se você quiser desenvolver para o SQL Server no Docker, examine os **macOS** tutoriais.

## <a name="create-new-applications"></a>Criar novos aplicativos

Se você estiver criando um novo aplicativo, dê uma olhada em uma lista da [bibliotecas de conectividade](sql-server-linux-develop-connectivity-libraries.md) para obter um resumo dos conectores e estruturas populares disponíveis para várias linguagens de programação.

## <a name="use-existing-applications"></a>Usar aplicativos existentes

Se você tiver um aplicativo de banco de dados existente, você pode simplesmente alterar sua cadeia de caracteres de conexão para o destino do SQL Server no Linux. Certifique-se de ler sobre as [problemas conhecidos](sql-server-linux-release-notes.md) no SQL Server no Linux.

## <a name="use-existing-sql-tools-on-windows-with-sql-server-on-linux"></a>Usar ferramentas existentes do SQL no Windows com o SQL Server no Linux

Ferramentas que são executados no momento no Windows, como o SSMS, SSDT e o PowerShell, também funcionam com o SQL Server no Linux. Embora eles não são executados nativamente no Linux, você ainda pode gerenciar as instâncias remotas do SQL Server no Linux. 

Consulte os tópicos a seguir para obter mais informações:

- [SSMS (SQL Server Management Studio)](sql-server-linux-manage-ssms.md)
- [SSDT (SQL Server Data Tools)](sql-server-linux-develop-use-ssdt.md)
- [SQL PowerShell](sql-server-linux-manage-powershell.md)

> [!Note]
> Certifique-se de que você está usando as versões mais recentes dessas ferramentas para a melhor experiência.

## <a name="use-new-sql-tools-for-linux"></a>Usar novas ferramentas SQL para Linux

Você pode usar o novo [extensão mssql](https://aka.ms/mssql-marketplace) para [Visual Studio Code](https://code.visualstudio.com) no Linux, macOS e Windows. Para obter uma explicação passo a passo, consulte o tutorial a seguir:

- [Usar o Visual Studio Code](sql-server-linux-develop-use-vscode.md)

Você também pode usar as novas ferramentas de linha de comando que são nativas para Linux. Essas ferramentas incluem o seguinte:

- [sqlcmd](../tools/sqlcmd-utility.md)
- [bcp](sql-server-linux-migrate-bcp.md)
- [mssql-conf](sql-server-linux-configure-mssql-conf.md)

## <a name="next-steps"></a>Próximas etapas

Para começar, instale o SQL Server no Linux usando um dos seguintes inícios rápidos:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)

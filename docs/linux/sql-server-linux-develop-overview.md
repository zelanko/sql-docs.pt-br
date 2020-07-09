---
title: Desenvolver aplicativos para SQL Server em Linux
description: Você pode criar aplicativos que se conectam e usam o SQL Server em Linux com uma variedade de linguagens de programação e estruturas da Web populares.
author: VanMSFT
ms.author: vanto
ms.date: 11/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 758cb738-b018-465b-9ab0-59a24b892e66
ms.openlocfilehash: 09bdea851ed3b9efeca1c69a09c12108706bbb22
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896506"
---
# <a name="how-to-get-started-developing-applications-for-sql-server-on-linux"></a>Como começar a desenvolver aplicativos para SQL Server em Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

Você pode criar aplicativos que se conectam e usam o SQL Server em Linux de uma variedade de linguagens de programação, como C#, Java, Node.js, PHP, Python, Ruby e C++. Você também pode usar estruturas da Web populares e estruturas de ORM (mapeamento relacional de objeto).

> [!VIDEO https://channel9.msdn.com/events/Connect/2017/T153/player]

> [!TIP]
> Essas mesmas opções de desenvolvimento também permitem que você tenha o SQL Server como destino em outras plataformas. Os aplicativos podem ter o SQL Server como destino em execução local ou na nuvem em Linux, Windows ou Docker em macOS. Outra opção é ter o Banco de Dados SQL do Azure e o SQL Data Warehouse do Azure como destinos.

## <a name="try-the-tutorials"></a>Experimente os tutoriais

A melhor maneira de começar e criar aplicativos com o SQL Server é experimentá-lo por conta própria.

- Navegue até [Tutoriais de Introdução](https://aka.ms/sqldev).
- Selecione seu idioma e a plataforma de desenvolvimento.
- Experimente os exemplos de código.

> [!TIP]
> Se você quiser desenvolver para SQL Server no Docker, dê uma olhada nos tutoriais do **macOS**.

## <a name="create-new-applications"></a>Criar novos aplicativos

Se você estiver criando um novo aplicativo, dê uma olhada em uma lista das [Bibliotecas de conectividade](sql-server-linux-develop-connectivity-libraries.md) para obter um resumo dos conectores e das estruturas populares disponíveis para várias linguagens de programação.

## <a name="use-existing-applications"></a>Usar aplicativos existentes

Se você tiver um aplicativo de banco de dados existente, poderá simplesmente alterar sua cadeia de conexão para ter como destino o SQL Server em Linux. Leia sobre os [Problemas Conhecidos](sql-server-linux-release-notes.md) em SQL Server em Linux.

## <a name="use-existing-sql-tools-on-windows-with-sql-server-on-linux"></a>Usar as ferramentas SQL existentes no Windows com SQL Server em Linux

As ferramentas que atualmente são executadas no Windows, como SSMS, SSDT e PowerShell, também funcionam com SQL Server em Linux. Embora não sejam executadas nativamente no Linux, você ainda pode gerenciar instâncias remotas do SQL Server no Linux. 

Para obter mais informações, confira os tópicos a seguir:

- [SQL Server Management Studio (SSMS)](sql-server-linux-manage-ssms.md)
- [SSDT (SQL Server Data Tools)](sql-server-linux-develop-use-ssdt.md)
- [SQL PowerShell](sql-server-linux-manage-powershell.md)

> [!Note]
> Verifique se você está usando as versões mais recentes dessas ferramentas para obter a melhor experiência.

## <a name="use-new-sql-tools-for-linux"></a>Usar novas ferramentas SQL para Linux

Você pode usar a nova [extensão mssql](https://aka.ms/mssql-marketplace) para [Visual Studio Code](https://code.visualstudio.com) em Linux, macOS e Windows. Para obter instruções passo a passo, confira o seguinte tutorial:

- [Usar o Visual Studio Code](sql-server-linux-develop-use-vscode.md)

Você também pode usar as novas ferramentas de linha de comando nativas para Linux. Essas ferramentas incluem as seguintes:

- [sqlcmd](../tools/sqlcmd-utility.md)
- [bcp](sql-server-linux-migrate-bcp.md)
- [mssql-conf](sql-server-linux-configure-mssql-conf.md)

## <a name="next-steps"></a>Próximas etapas

Para começar, instale o SQL Server em Linux usando um dos seguintes inícios rápidos:

- [Instalação no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalação no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)

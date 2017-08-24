---
title: Desenvolver aplicativos para o SQL Server no Linux | Microsoft Docs
description: 
author: sanagama
ms.author: sanagama
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 758cb738-b018-465b-9ab0-59a24b892e66
ms.custom: H1Hack27Feb2017
ms.translationtype: MT
ms.sourcegitcommit: ea75391663eb4d509c10fb785fcf321558ff0b6e
ms.openlocfilehash: 7fcd3350796d88d02011f0d45e666851d69cfd78
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="how-to-get-started-developing-applications-for-sql-server-on-linux"></a>Como começar a desenvolver aplicativos para o SQL Server no Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

Você pode criar aplicativos que se conectam ao 2017 RC2 do SQL Server no Linux de uma variedade de linguagens de programação, como c#, Java, Node.js, PHP, Python, Ruby e C++. Você também pode usar as estruturas de sites populares e estruturas de mapeamento relacional objeto (ORM).

> [!TIP]
> Essas mesmas opções de desenvolvimento também habilitar destino do SQL Server em outras plataformas. Aplicativos podem direcionar o SQL Server em execução no local ou na nuvem, no Docker, Windows ou Linux em macOS. Ou você pode direcionar o banco de dados do SQL Azure e o Azure SQL Data Warehouse.

## <a name="try-the-tutorials"></a>Experimente os tutoriais

É a melhor maneira de começar e criar aplicativos com o SQL Server para testá-lo por conta própria.

- Navegue até [tutoriais de Introdução](http://aka.ms/sqldev).
- Selecione seu idioma e plataforma de desenvolvimento.
- Experimente os exemplos de código.

> [!TIP]
> Se você quiser desenvolver para o SQL Server de 2017 RC2 no Docker, examine o **macOS** tutoriais.

## <a name="create-new-applications"></a>Criar novos aplicativos

Se você estiver criando um novo aplicativo, dê uma olhada em uma lista da [bibliotecas de conectividade](sql-server-linux-develop-connectivity-libraries.md) para obter um resumo dos conectores e estruturas populares disponíveis para várias linguagens de programação.

## <a name="use-existing-applications"></a>Usar aplicativos existentes

Se você tiver um aplicativo de banco de dados existente, você pode simplesmente alterar sua cadeia de caracteres de conexão para SQL Server 2017 RC2 no Linux de destino. Certifique-se de ler sobre o [problemas conhecidos](sql-server-linux-release-notes.md) no SQL Server de 2017 RC2 no Linux.

## <a name="use-existing-sql-tools-on-windows-with-sql-server-on-linux"></a>Usar as ferramentas existentes do SQL no Windows com o SQL Server no Linux

Ferramentas que são executados no momento no Windows, como o SSMS, o SSDT e o PowerShell, também funcionam com o SQL Server de 2017 RC2 no Linux. Embora eles não forem executados nativamente no Linux, você ainda pode gerenciar instâncias remotas do SQL Server no Linux. 

Consulte os tópicos a seguir para obter mais informações:

- [SSMS (SQL Server Management Studio)](sql-server-linux-develop-use-ssms.md)
- [SSDT (SQL Server Data Tools)](sql-server-linux-develop-use-ssdt.md)
- [PowerShell SQL](sql-server-linux-manage-powershell.md)

> [!Note] 
> Certifique-se de que você está usando as versões mais recentes dessas ferramentas para a melhor experiência.

## <a name="use-new-sql-tools-for-linux"></a>Usar novas ferramentas SQL para Linux

Você pode usar o novo [mssql extensão](https://aka.ms/mssql-marketplace) para [código do Visual Studio](https://code.visualstudio.com) no Windows, Linux e macOS. Para obter instruções passo a passo, consulte o tutorial a seguir:

- [Use o código do Visual Studio](sql-server-linux-develop-use-vscode.md)

Você também pode usar novas ferramentas de linha de comando que são nativas para Linux. Essas ferramentas incluem o seguinte:

- [Sqlcmd](../tools/sqlcmd-utility.md)
- [bcp](sql-server-linux-migrate-bcp.md)
- [MSSQL conf](sql-server-linux-configure-mssql-conf.md)

## <a name="next-steps"></a>Próximas etapas

Para começar, instale o SQL Server no Linux usando um dos seguintes tutoriais de início rápido:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)


---
title: Desenvolver aplicativos para o SQL Server no Linux | Microsoft Docs
description: 
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/17/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.technology: database-engine
ms.assetid: 758cb738-b018-465b-9ab0-59a24b892e66
ms.workload: On Demand
ms.openlocfilehash: 9bfd1b4f30593fa6ae4d17ec92bfa0047ea751bc
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2018
---
# <a name="how-to-get-started-developing-applications-for-sql-server-on-linux"></a>Como começar a desenvolver aplicativos para o SQL Server no Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Você pode criar aplicativos que se conectam ao 2017 do SQL Server no Linux de uma variedade de linguagens de programação, como c#, Java, Node.js, PHP, Python, Ruby e C++. Você também pode usar as estruturas de sites populares e estruturas de mapeamento relacional objeto (ORM).

> [!VIDEO https://channel9.msdn.com/events/Connect/2017/T153/player]

> [!TIP]
> Essas mesmas opções de desenvolvimento também habilitar destino do SQL Server em outras plataformas. Aplicativos podem direcionar o SQL Server em execução no local ou na nuvem, no Docker, Windows ou Linux em macOS. Ou você pode direcionar o banco de dados do SQL Azure e o Azure SQL Data Warehouse.

## <a name="try-the-tutorials"></a>Experimente os tutoriais

É a melhor maneira de começar e criar aplicativos com o SQL Server para testá-lo por conta própria.

- Navegue até [tutoriais de Introdução](http://aka.ms/sqldev).
- Selecione seu idioma e plataforma de desenvolvimento.
- Experimente os exemplos de código.

> [!TIP]
> Se você quiser desenvolver para o SQL Server 2017 no Docker, examine o **macOS** tutoriais.

## <a name="create-new-applications"></a>Criar novos aplicativos

Se você estiver criando um novo aplicativo, dê uma olhada em uma lista da [bibliotecas de conectividade](sql-server-linux-develop-connectivity-libraries.md) para obter um resumo dos conectores e estruturas populares disponíveis para várias linguagens de programação.

## <a name="use-existing-applications"></a>Usar aplicativos existentes

Se você tiver um aplicativo de banco de dados existente, você pode simplesmente alterar sua cadeia de caracteres de conexão para destino 2017 do SQL Server no Linux. Certifique-se de ler sobre o [problemas conhecidos](sql-server-linux-release-notes.md) em 2017 do SQL Server no Linux.

## <a name="use-existing-sql-tools-on-windows-with-sql-server-on-linux"></a>Usar as ferramentas existentes do SQL no Windows com o SQL Server no Linux

Ferramentas que são executados no momento no Windows, como o SSMS, o SSDT e o PowerShell, também funcionam com 2017 do SQL Server no Linux. Embora eles não forem executados nativamente no Linux, você ainda pode gerenciar instâncias remotas do SQL Server no Linux. 

Consulte os tópicos a seguir para obter mais informações:

- [SSMS (SQL Server Management Studio)](sql-server-linux-develop-use-ssms.md)
- [SSDT (SQL Server Data Tools)](sql-server-linux-develop-use-ssdt.md)
- [SQL PowerShell](sql-server-linux-manage-powershell.md)

> [!Note] 
> Certifique-se de que você está usando as versões mais recentes dessas ferramentas para a melhor experiência.

## <a name="use-new-sql-tools-for-linux"></a>Usar novas ferramentas SQL para Linux

Você pode usar o novo [mssql extensão](https://aka.ms/mssql-marketplace) para [código do Visual Studio](https://code.visualstudio.com) no Windows, Linux e macOS. Para obter instruções passo a passo, consulte o tutorial a seguir:

- [Usar o Visual Studio Code](sql-server-linux-develop-use-vscode.md)

Você também pode usar novas ferramentas de linha de comando que são nativas para Linux. Essas ferramentas incluem o seguinte:

- [sqlcmd](../tools/sqlcmd-utility.md)
- [bcp](sql-server-linux-migrate-bcp.md)
- [mssql-conf](sql-server-linux-configure-mssql-conf.md)

## <a name="next-steps"></a>Próximas etapas

Para começar, instale o SQL Server no Linux usando um dos tutoriais a seguir:

- [Instalar no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-ubuntu.md)

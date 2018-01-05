---
title: "Baixe e instale o Studio de operações do Microsoft SQL (visualização) | Microsoft Docs"
description: "Baixar e instalar o Microsoft SQL operações Studio (visualização) para Windows, macOS ou Linux"
ms.custom: tools|sos
ms.date: 12/19/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3a34a03b447e26f072b6c8064cd115333600fef4
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="download-and-install-sql-operations-studio-preview"></a>Baixe e instale o Studio de operações do SQL (visualização)

[!INCLUDE[name-sos](../includes/name-sos.md)]executa no Linux, Windows e macOS.

Baixe e instale a versão mais recente, o *visualização pública dezembro*:

|Plataforma|Download|Data de lançamento|
|:---|:---|:---|
|Windows|[Instalador](https://go.microsoft.com/fwlink/?linkid=865305)<br>[arquivos. zip](https://go.microsoft.com/fwlink/?linkid=865304)|19 de dezembro de 2017 |
|MacOS|[arquivos. zip](https://go.microsoft.com/fwlink/?linkid=865306)|19 de dezembro de 2017 |
|Linux|[. DEB](https://go.microsoft.com/fwlink/?linkid=865308)<br>[. rpm](https://go.microsoft.com/fwlink/?linkid=865309)<br>[. gz](https://go.microsoft.com/fwlink/?linkid=865307)|19 de dezembro de 2017|

Para obter detalhes sobre a versão mais recente, consulte o [notas de versão](release-notes.md).

## <a name="get-sql-operations-studio-preview-for-windows"></a>Obter o Studio de operações do SQL (visualização) para Windows

Esta versão do [!INCLUDE[name-sos](../includes/name-sos-short.md)] inclui uma experiência de instalação padrão do Windows e. zip: 

**Instalador**

1. Baixe e execute o [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] installer para Windows](https://go.microsoft.com/fwlink/?linkid=865305).
1. Iniciar o [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] aplicativo.


**arquivo. zip**

1. Baixar [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] . zip para o Windows](https://go.microsoft.com/fwlink/?linkid=865304).
2. Navegue até o arquivo baixado e extraia-o.
3. Execute `\sqlops-windows\sqlops.exe`


## <a name="get-sql-operations-studio-preview-for-macos"></a>Obter o Studio de operações do SQL (visualização) para macOS

1. Baixar [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] para macOS](https://go.microsoft.com/fwlink/?linkid=865306).
2. Para expandir o conteúdo do zip, clique duas vezes nele.
3. Para fazer [!INCLUDE[name-sos](../includes/name-sos-short.md)] disponíveis no *Launchpad*, arraste *sqlops.app* para o *aplicativos* pasta.


## <a name="get-sql-operations-studio-preview-for-linux"></a>Obter o Studio de operações do SQL (visualização) para Linux

1. Baixar [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] para Linux](https://go.microsoft.com/fwlink/?linkid=865307).
1. Para extrair o arquivo e inicialização [!INCLUDE[name-sos](../includes/name-sos-short.md)], abra uma nova janela do Terminal e digite os seguintes comandos:

   ```bash
   cd ~
   cp ~/Downloads/sqlops-linux-<version string>.tar.gz ~
   tar -xvf ~/sqlops-linux-<version string>.tar.gz
   echo 'export PATH="$PATH:~/sqlops-linux-x64"' >> ~/.bashrc
   source ~/.bashrc
   sqlops
   ```

   > [!NOTE]
   > No Ubuntu e Redhat, você pode ter dependências ausentes. Use os comandos a seguir para instalar essas dependências, dependendo de sua versão do Linux:
   
   **Ubuntu:** 
   ```bash
   sudo apt-get install libxss1

   sudo apt-get install libgconf-2-4

   sudo apt-get install libunwind8
   ```

   **RedHat:** 
   ```bash
   yum install libXScrnSaver
   ```

## <a name="uninstall-sql-operations-studio-preview"></a>Desinstalar o Studio de operações do SQL (visualização)

Se você instalou [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] usando o Windows installer, desinstale da mesma maneira que você remova qualquer aplicativo do Windows.

Se você instalou [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] . zip ou outro arquivo, em seguida, simplesmente excluir os arquivos.

## <a name="supported-operating-systems"></a>Sistemas operacionais com suporte

[!INCLUDE[name-sos](../includes/name-sos-short.md)]executa no Linux, Windows e macOS e é suportado nas seguintes plataformas:

### <a name="windows"></a>Windows
- Windows 10 (64 bits)
- Windows 8.1 (64 bits)
- Windows 8 (64 bits)
- Requer o Windows 7 (SP1) (64 bits) - [KB2533623](https://www.microsoft.com/en-us/download/details.aspx?id=26767)
- Windows Server 2016
- Windows Server 2012 R2 (64 bits)
- Windows Server 2012 (64 bits)
- Windows Server 2008 R2 (64 bits)

### <a name="macos"></a>MacOS
- macOS 10.13 Serra alta
- macOS 10.12 Serra

### <a name="linux"></a>Linux
- 7.4 do Red Hat Enterprise Linux
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04



## <a name="next-steps"></a>Next Steps

Consulte um dos seguintes guias de início rápido para começar:
- [Conectar e consultar o SQL Server](quickstart-sql-server.md)
- [Conectar e consultar o banco de dados SQL do Azure](quickstart-sql-database.md)
- [Conectar e consultar o depósito de dados do Azure](quickstart-sql-dw.md)

Contribuir com [!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://GitHub.com/Microsoft/sqlopsstudio](https://github.com/Microsoft/sqlopsstudio) 

[Declaração de privacidade do Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839) e [coleta de dados de uso](usage-data-collection.md).

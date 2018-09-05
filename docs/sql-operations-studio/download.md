---
title: Baixe e instale o Microsoft SQL Operations Studio (versão prévia) | Microsoft Docs
description: Baixar e instalar o Microsoft SQL Operations Studio (versão prévia) para Windows, macOS ou Linux
ms.custom: tools|sos
ms.date: 08/30/2018
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 30eea457bdba7ac671829bb02f01152235babaf3
ms.sourcegitcommit: 2a47e66cd6a05789827266f1efa5fea7ab2a84e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/31/2018
ms.locfileid: "43348647"
---
# <a name="download-and-install-sql-operations-studio-preview"></a>Baixe e instale o SQL Operations Studio (versão prévia)

[!INCLUDE[name-sos](../includes/name-sos.md)] é executado no Windows, macOS e Linux.

Baixe e instale a versão mais recente, o *agosto Public Preview*:

|Plataforma|Download|Data de liberação| Versão |
|:---|:---|:---|:---|
|Windows|[Instalador](https://go.microsoft.com/fwlink/?linkid=2013365)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2013712)|30 de agosto de 2018 |0.32.8|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2013715)|30 de agosto de 2018 |0.32.8|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2013833)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2013830)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2013718)|30 de agosto de 2018 |0.32.8|

Para obter detalhes sobre a versão mais recente, consulte o [notas de versão](release-notes.md).

## <a name="get-sql-operations-studio-preview-for-windows"></a>Obtenha o SQL Operations Studio (versão prévia) para Windows

Esta versão do [!INCLUDE[name-sos](../includes/name-sos-short.md)] inclui uma experiência padrão do Windows installer e. zip: 

**Instalador**

1. Baixe e execute o [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] installer para Windows](https://go.microsoft.com/fwlink/?linkid=2013365).
1. Iniciar o [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] aplicativo.


**arquivo. zip**

1. Baixe [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] . zip para Windows](https://go.microsoft.com/fwlink/?linkid=2013712).
2. Navegue até o arquivo baixado e extraí-lo.
3. Execute `\sqlops-windows\sqlops.exe`


## <a name="get-sql-operations-studio-preview-for-macos"></a>Obtenha o SQL Operations Studio (versão prévia) para macOS

1. Baixe [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] para macOS](https://go.microsoft.com/fwlink/?linkid=2013715).
2. Para expandir o conteúdo do zip, clique duas vezes nele.
3. Para tornar [!INCLUDE[name-sos](../includes/name-sos-short.md)] disponíveis na *Launchpad*, arraste *sqlops.app* para o *aplicativos* pasta.


## <a name="get-sql-operations-studio-preview-for-linux"></a>Obtenha o SQL Operations Studio (versão prévia) para Linux

1. Baixar [!INCLUDE[name-sos](../includes/name-sos-short.md)] para Linux usando um dos instaladores ou gz arquivo morto:
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2013833)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2013830)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2013718)
1. Para extrair o arquivo e inicialização [!INCLUDE[name-sos](../includes/name-sos-short.md)], abra uma nova janela do Terminal e digite os seguintes comandos:

   **Instalação do Debian:**
   ```bash
   cd ~
   sudo dpkg -i ./Downloads/sqlops-linux-<version string>.deb

   sqlops
   ```

   **Instalação do RPM:**
   ```bash
   cd ~
   yum install ./Downloads/sqlops-linux-<version string>.rpm

   sqlops
   ```

   **gz instalação:**
   ```bash 
   cd ~ 
   cp ~/Downloads/sqlops-linux-<version string>.tar.gz ~ 
   tar -xvf ~/sqlops-linux-<version string>.tar.gz 
   echo 'export PATH="$PATH:~/sqlops-linux-x64"' >> ~/.bashrc
   source ~/.bashrc 
   sqlops 
   ``` 

   > [!NOTE]
   > No Ubuntu, Redhat e Debian, você pode ter dependências ausentes. Use os comandos a seguir para instalar essas dependências, dependendo de sua versão do Linux:
   

   **Debian:** 
   ```bash
   sudo apt-get install libunwind8
   ```

   **Red Hat:** 
   ```bash
   yum install libXScrnSaver
   ```

   **Ubuntu:** 
   ```bash
   sudo apt-get install libxss1

   sudo apt-get install libgconf-2-4

   sudo apt-get install libunwind8
   ```


## <a name="uninstall-sql-operations-studio-preview"></a>Desinstalar o SQL Operations Studio (versão prévia)

Se você instalou o [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] usando o instalador do Windows, desinstale da mesma maneira que você remova qualquer aplicativo do Windows.

Se você instalou o [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] com um. zip ou outro arquivo, em seguida, simplesmente excluir os arquivos.

## <a name="supported-operating-systems"></a>Sistemas operacionais com suporte

[!INCLUDE[name-sos](../includes/name-sos-short.md)] é executado no Windows, macOS e Linux e é suportado nas seguintes plataformas:

### <a name="windows"></a>Windows
- Windows 10 (64 bits)
- Windows 8.1 (64 bits)
- Windows 8 (64 bits)
- Requer o Windows 7 (SP1) (64 bits) - [KB2533623](https://www.microsoft.com/en-us/download/details.aspx?id=26767)
- Windows Server 2016
- Windows Server 2012 R2 (64 bits)
- Windows Server 2012 (64 bits)
- Windows Server 2008 R2 (64 bits)

### <a name="macos"></a>macOS
- macOS 10.13 High Sierra
- macOS 10.12 Sierra

### <a name="linux"></a>Linux
- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="check-for-updates"></a>Verificar atualizações
Para verificar se há atualizações mais recentes, clique no ícone de engrenagem na parte inferior esquerda da janela e clique **verificar se há atualizações**

## <a name="next-steps"></a>Próximas etapas

Consulte um dos seguintes inícios rápidos para começar:
- [Conectar-se e consultar o SQL Server](quickstart-sql-server.md)
- [Conectar-se e consultar o banco de dados SQL do Azure](quickstart-sql-database.md)
- [Conectar-se e consultar o Data Warehouse do Azure](quickstart-sql-dw.md)

Contribuir com [!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/sqlopsstudio](https://github.com/Microsoft/sqlopsstudio) 

[Declaração de privacidade da Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839) e [coleta de dados de uso](usage-data-collection.md).

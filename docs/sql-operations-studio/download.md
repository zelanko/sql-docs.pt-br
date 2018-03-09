---
title: "Baixe e instale o Studio de operações do Microsoft SQL (visualização) | Microsoft Docs"
description: "Baixar e instalar o Microsoft SQL operações Studio (visualização) para Windows, macOS ou Linux"
ms.custom: tools|sos
ms.date: 03/05/2018
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
ms.openlocfilehash: 1cb41e1824fc157932e2cb08292608bb97e46712
ms.sourcegitcommit: ab25b08a312d35489a2c4a6a0d29a04bbd90f64d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/08/2018
---
# <a name="download-and-install-sql-operations-studio-preview"></a>Baixe e instale o Studio de operações do SQL (visualização)

[!INCLUDE[name-sos](../includes/name-sos.md)] executa no Linux, Windows e macOS.

Baixe e instale a versão mais recente, o *visualização pública fevereiro*:

|Plataforma|Download|Data de lançamento| Versão |
|:---|:---|:---|:---|
|Windows|[Instalador](https://go.microsoft.com/fwlink/?linkid=867998)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=867997)|15 de fevereiro de 2018 |0.26.7|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=867999)|15 de fevereiro de 2018 |0.26.7|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=868002)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=868001)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=868000)|15 de fevereiro de 2018|0.26.7|

Para obter detalhes sobre a versão mais recente, consulte o [notas de versão](release-notes.md).

## <a name="get-sql-operations-studio-preview-for-windows"></a>Obter o Studio de operações do SQL (visualização) para Windows

Esta versão do [!INCLUDE[name-sos](../includes/name-sos-short.md)] inclui uma experiência de instalação padrão do Windows e. zip: 

**Instalador**

1. Baixe e execute o [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] installer para Windows](https://go.microsoft.com/fwlink/?linkid=867998).
1. Iniciar o [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] aplicativo.


**arquivo. zip**

1. Baixar [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] . zip para o Windows](https://go.microsoft.com/fwlink/?linkid=867997).
2. Navegue até o arquivo baixado e extraia-o.
3. Execute `\sqlops-windows\sqlops.exe`


## <a name="get-sql-operations-studio-preview-for-macos"></a>Obter o Studio de operações do SQL (visualização) para macOS

1. Baixar [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] para macOS](https://go.microsoft.com/fwlink/?linkid=867999).
2. Para expandir o conteúdo do zip, clique duas vezes nele.
3. Para fazer [!INCLUDE[name-sos](../includes/name-sos-short.md)] disponíveis no *Launchpad*, arraste *sqlops.app* para o *aplicativos* pasta.


## <a name="get-sql-operations-studio-preview-for-linux"></a>Obter o Studio de operações do SQL (visualização) para Linux

1. Baixar [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] para Linux](https://go.microsoft.com/fwlink/?linkid=868000).
1. Para extrair o arquivo e inicialização [!INCLUDE[name-sos](../includes/name-sos-short.md)], abra uma nova janela do Terminal e digite os seguintes comandos:

   ```bash
   cd ~
   sudo dpkg -i ./Downloads/sqlops-linux-<version string>.deb

   sqlops
   ```

   > [!NOTE]
   > No Debian, Redhat e Ubuntu, você pode ter dependências ausentes. Use os comandos a seguir para instalar essas dependências, dependendo de sua versão do Linux:
   

   **Debian:** 
   ```bash
   sudo apt-get install libuwind8
   ```

   **Redhat:** 
   ```bash
   yum install libXScrnSaver
   ```

   **Ubuntu:** 
   ```bash
   sudo apt-get install libxss1

   sudo apt-get install libgconf-2-4

   sudo apt-get install libunwind8
   ```


## <a name="uninstall-sql-operations-studio-preview"></a>Desinstalar o Studio de operações do SQL (visualização)

Se você instalou [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] usando o Windows installer, desinstale da mesma maneira que você remova qualquer aplicativo do Windows.

Se você instalou [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] . zip ou outro arquivo, em seguida, simplesmente excluir os arquivos.

## <a name="supported-operating-systems"></a>Sistemas operacionais com suporte

[!INCLUDE[name-sos](../includes/name-sos-short.md)] executa no Linux, Windows e macOS e é suportado nas seguintes plataformas:

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
- macOS 10.13 Serra alta
- macOS 10.12 Sierra

### <a name="linux"></a>Linux
- Red Hat Enterprise Linux 7.4
- Red Hat Enterprise Linux 7.3
- SUSE Linux Enterprise Server v12 SP2
- Ubuntu 16.04

## <a name="check-for-updates"></a>Verificar atualizações
Para verificar as atualizações mais recentes, clique no ícone de engrenagem na parte inferior esquerda da janela e clique **verificar se há atualizações**

## <a name="next-steps"></a>Próximas etapas

Consulte um dos seguintes guias de início rápido para começar:
- [Conectar e consultar o SQL Server](quickstart-sql-server.md)
- [Conectar e consultar o banco de dados SQL do Azure](quickstart-sql-database.md)
- [Conectar e consultar o depósito de dados do Azure](quickstart-sql-dw.md)

Contribuir com [!INCLUDE[name-sos](../includes/name-sos-short.md)]:
- [https://github.com/Microsoft/sqlopsstudio](https://github.com/Microsoft/sqlopsstudio) 

[Declaração de privacidade do Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839) e [coleta de dados de uso](usage-data-collection.md).

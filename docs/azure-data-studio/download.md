---
title: Baixe e instale o
titleSuffix: Azure Data Studio
description: Download e instalação do Azure Data Studio no Windows, macOS ou Linux
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: jroth
ms.custom: seodec18
ms.date: 07/10/2019
ms.reviewer: alayu; sstein
ms.openlocfilehash: 75122c146a33e5e44b61cbfd894c6997c2a4601f
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792944"
---
# <a name="download-and-install-azure-data-studio"></a>Baixe e instale o Azure Data Studio

[!INCLUDE[name-sos](../includes/name-sos.md)] pode ser executado no Windows, macOS e Linux.


Baixe e instale a versão mais recente, o *versão de julho do*:

> [!NOTE]
> Se você estiver atualizando do SQL Operations Studio e deseja manter as configurações, os atalhos de teclado ou os trechos de código, consulte [mover as configurações do usuário](#move-user-settings).

|Plataforma|Download|Data de liberação| Versão |
|:---|:---|:---|:---|
|Windows|[Instalador do usuário (recomendado)](https://go.microsoft.com/fwlink/?linkid=2098449)<br>[Instalador do sistema](https://go.microsoft.com/fwlink/?linkid=2098450)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2098500)|10 de julho de 2019 |1.9.0|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2098501)|10 de julho de 2019 |1.9.0|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2098279)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2098280)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2098197)|10 de julho de 2019 |1.9.0|

Para obter detalhes sobre a versão mais recente, consulte as [notas de versão](release-notes.md).

## <a name="get-azure-data-studio-for-windows"></a>Obter o Azure Data Studio para o Windows

Esta versão do [!INCLUDE[name-sos](../includes/name-sos-short.md)] inclui uma experiência padrão do Windows installer e um arquivo. zip.

O *instalador do usuário* é recomendado porque ele não requer privilégios de administrador, que simplifica a instalações e atualizações. O instalador do usuário não requer privilégios de administrador que o local está na sua pasta de AppData Local (LOCALAPPDATA) do usuário. O instalador do usuário também fornece uma experiência mais suave de atualização em segundo plano. Para obter mais informações, consulte [configuração do usuário para Windows](https://code.visualstudio.com/updates/v1_26#_user-setup-for-windows).


**Instalador de usuário** (recomendado)

1. Baixe e execute o [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] *usuário* instalador para Windows](https://go.microsoft.com/fwlink/?linkid=2098449).
2. Inicie o aplicativo [!INCLUDE[name-sos-short](../includes/name-sos-short.md)].

**Instalador do sistema**

1. Baixe e execute o [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] *sistema* instalador para Windows](https://go.microsoft.com/fwlink/?linkid=2098450 ).
2. Inicie o aplicativo [!INCLUDE[name-sos-short](../includes/name-sos-short.md)].


**arquivo zip**

1. Baixe o [arquivo .zip do [!INCLUDE[name-sos](../includes/name-sos-short.md)] para o Windows](https://go.microsoft.com/fwlink/?linkid=2098500).
2. Navegue até o arquivo baixado e o extraia.
3. Execute `\azuredatastudio-windows\azuredatastudio.exe`


## <a name="get-azure-data-studio-for-macos"></a>Obtenha o Azure Data Studio para macOS

1. Baixe [ [!INCLUDE[name-sos](../includes/name-sos-short.md)] para macOS](https://go.microsoft.com/fwlink/?linkid=2098501).
2. Para expandir o conteúdo do zip, clique duas vezes nele.
3. Para tornar [!INCLUDE[name-sos](../includes/name-sos-short.md)] disponíveis na *Launchpad*, arraste */aplicativos de dados do Azure* para o *aplicativos* pasta.


## <a name="get-azure-data-studio-for-linux"></a>Obtenha o Azure Data Studio para Linux

1. Baixe o [!INCLUDE[name-sos](../includes/name-sos-short.md)] para Linux usando um dos instaladores ou o arquivo morto gz:
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2098279)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2098280)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2098197)
1. Para extrair o arquivo e inicializá-lo [!INCLUDE[name-sos](../includes/name-sos-short.md)], abra uma nova janela do Terminal e digite os seguintes comandos:

   **Instalação do Debian:**
   ```bash
   cd ~
   sudo dpkg -i ./Downloads/azuredatastudio-linux-<version string>.deb

   azuredatastudio
   ```

   **Instalação do RPM:**
   ```bash
   cd ~
   yum install ./Downloads/azuredatastudio-linux-<version string>.rpm

   azuredatastudio
   ```

   **instalação gz:**
   ```bash 
   cd ~ 
   cp ~/Downloads/azuredatastudio-linux-<version string>.tar.gz ~ 
   tar -xvf ~/azuredatastudio-linux-<version string>.tar.gz 
   echo 'export PATH="$PATH:~/azuredatastudio-linux-x64"' >> ~/.bashrc
   source ~/.bashrc 
   azuredatastudio 
   ``` 

   > [!NOTE]
   > No Debian, Redhat e Ubuntu, você pode ter dependências ausentes. Use os seguintes comandos para instalar estas dependências, de acordo com sua versão do Linux:
   

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
## <a name="download-insiders-build-of-azure-data-studio"></a>Baixe o build Insiders do Studio de dados do Azure
Em geral, os usuários devem baixar a versão estável do Studio de dados do Azure acima. No entanto, se você quiser experimentar nossos recursos beta e fornecer comentários, você pode baixar um [build Insiders do Studio de dados do Azure.](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)

## <a name="uninstall-azure-data-studio"></a>Desinstalar o Azure Data Studio

Se você instalou o [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] usando o instalador do Windows, desinstale da mesma maneira que você remove qualquer aplicativo do Windows.

Se você instalou o [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] com um. zip ou outro arquivo, basta excluir os arquivos.

## <a name="supported-operating-systems"></a>Sistemas operacionais com suporte

[!INCLUDE[name-sos](../includes/name-sos-short.md)] pode ser executado no Windows, macOS e Linux e é suportado nas seguintes plataformas:

### <a name="windows"></a>Windows
- Windows 10 (64 bits)
- Windows 8.1 (64 bits)
- Windows 8 (64 bits)
- Requer o Windows 7 (SP1) (64 bits) - [KB2533623](https://www.microsoft.com/download/details.aspx?id=26767)
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

## <a name="recommended-system-requirements"></a>Requisitos de sistema recomendados
Para obter uma experiência ideal, use os requisitos de sistema recomendados.
[Requerem atualização aqui quantificar memória]

|             | Núcleos de CPU | Memória/RAM |
|:-----------|:---------|:----------|
| Recomendado |     4     |      8 GB    |
|   Mínimo   |     2     |      4 GB     |
|             |           |            |

## <a name="check-for-updates"></a>Verificar atualizações
Para verificar se há atualizações mais recentes, clique no ícone de engrenagem na parte inferior esquerda da janela e clique em **verificar se há atualizações**

## <a name="supported-sql-offerings"></a>Ofertas de SQL com suporte

* Esta versão do Azure Data Studio funciona com todas as [versões com suporte do SQL Server 2014 - [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)] ](https://support.microsoft.com/lifecycle?C2=1044) e fornece suporte para trabalhar com os recursos de nuvem mais recentes no Banco de Dados SQL do Azure e no SQL Data Warehouse do Azure. O Azure Data Studio também fornece suporte de versão prévia para instância gerenciada do SQL Server.

## <a name="upgrade-from-sql-operations-studio"></a>Atualização do SQL Operations Studio

Se você ainda estiver usando o SQL Operations Studio, você precisará atualizar para o estúdio de dados do Azure. SQL Operations Studio era o nome de visualização e a versão de visualização do estúdio de dados do Azure. Em setembro de 2018, estamos [alterou o nome para o Azure Data Studio](https://cloudblogs.microsoft.com/sqlserver/2018/09/25/azure-data-studio-for-sql-server/) e lançou a versão de GA (disponibilidade geral). Porque o SQL Operations Studio é não mais que está sendo atualizado ou tem suporte, pedimos que todos os usuários do SQL Operations Studio para baixar a versão mais recente do Studio de dados do Azure para obter os recursos mais recentes, atualizações de segurança e correções.
 
Ao atualizar da versão prévia antiga para o Studio de dados mais recente do Azure, você perderá as suas configurações atuais e extensões. Para mover suas configurações, siga as instruções a seguir *mover as configurações do usuário* seção:


## <a name="move-user-settings"></a>Mover as configurações do usuário

Se você quiser mover suas configurações personalizadas, os atalhos de teclado ou trechos de código, siga as etapas abaixo. É importante fazer isso se você estiver atualizando da versão do SQL Operations Studio para Azure Data Studio.

*Se você já tiver o Azure Data Studio, ou nunca tiver sido instalado ou personalizado do SQL Operations Studio, você pode ignorar esta seção.*


1. Abra as configurações clicando a engrenagem no canto inferior esquerdo e clicando em **configurações.**

   ![open-settings](./media/download/open-settings.png)

2. Clique com botão direito na guia **as configurações de usuário** na parte superior e clique em **Revelar no Explorer**

   ![reveal-in-explorer](./media/download/reveal-in-explorer.png)

3. Copie todos os arquivos nessa pasta e salve em uma forma fácil de encontrar o local em sua unidade local, como sua pasta Documentos.

   ![copy-settings](./media/download/copy-settings.png)

4. Na nova versão do Azure Data Studio, siga as etapas 1 e 2, em seguida, para a etapa 3 cole o conteúdo salvo na pasta. Manualmente, você pode copiar sobre as configurações, associações de teclas ou trechos de código em seus respectivos locais.

5. Se substituir uma instalação existente, exclua o diretório de instalação antigo antes da instalação para evitar erros de conexão com sua conta do Azure para o Gerenciador de recursos.

## <a name="next-steps"></a>Próximas etapas

Consulte um dos seguintes inícios rápidos para começar:
- [Conectar-se e consultar o SQL Server](quickstart-sql-server.md)
- [Conectar-se e consultar o banco de dados SQL do Azure](quickstart-sql-database.md)
- [Conectar-se e consultar o Data Warehouse do Azure](quickstart-sql-dw.md)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

[Declaração de privacidade da Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839) e [coleta de dados de uso](usage-data-collection.md).
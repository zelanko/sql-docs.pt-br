---
title: Fazer o download e instalar
titleSuffix: Azure Data Studio
description: Baixar e instalar o Azure Data Studio para Windows, macOS ou Linux
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.custom: seodec18
ms.date: 12/26/2019
ms.reviewer: alayu; sstein
ms.openlocfilehash: c5c75b2fda96d970b243161636d791029e311330
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76516487"
---
# <a name="download-and-install-azure-data-studio"></a>Baixar e instalar o Azure Data Studio

O [!INCLUDE[name-sos](../includes/name-sos.md)] é executado no Windows, no macOS e no Linux.


Baixe e instale a versão mais recente:

> [!NOTE]
> Se você estiver fazendo a atualização do SQL Operations Studio e quiser manter as configurações, os atalhos de teclado ou os snippets de código, confira [Mover as configurações de usuário](#move-user-settings).

|Plataforma|Baixar|Data de liberação| Versão |
|:---|:---|:---|:---|
|Windows|[Instalador do usuário (recomendado)](https://go.microsoft.com/fwlink/?linkid=2113530)<br>[Instalador do sistema](https://go.microsoft.com/fwlink/?linkid=2113628)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2113529)|26 de dezembro de 2019|1.14.1|
|macOS|[.zip](https://go.microsoft.com/fwlink/?linkid=2113528)|26 de dezembro de 2019|1.14.1|
|Linux|[.deb](https://go.microsoft.com/fwlink/?linkid=2113344)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2113718)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2113627)|26 de dezembro de 2019|1.14.1|

Para obter detalhes sobre a versão mais recente, confira as [notas sobre a versão](release-notes.md).

## <a name="get-azure-data-studio-for-windows"></a>Obter o Azure Data Studio para Windows

Esta versão do [!INCLUDE[name-sos](../includes/name-sos-short.md)] inclui uma experiência padrão do Windows Installer e um arquivo .zip.

O *instalador do usuário* é recomendado porque não exige privilégios de administrador, o que simplifica as instalações e as atualizações. O instalador do usuário não exige privilégios de administrador, pois a localização está na pasta AppData Local (LOCALAPPDATA) do usuário. O instalador do usuário também fornece uma experiência de atualização em segundo plano mais tranquila. Para obter mais informações, confira [Configuração de usuário para Windows](https://code.visualstudio.com/updates/v1_26#_user-setup-for-windows).

**Instalador do usuário** (recomendado)

1. Baixe e execute o [instalador do [!INCLUDE[name-sos](../includes/name-sos-short.md)]usuário*do* para Windows](https://go.microsoft.com/fwlink/?linkid=2113530).
2. Inicie o aplicativo [!INCLUDE[name-sos-short](../includes/name-sos-short.md)].

**Instalador do sistema**

1. Baixe e execute o [instalador do [!INCLUDE[name-sos](../includes/name-sos-short.md)]sistema*do* para Windows](https://go.microsoft.com/fwlink/?linkid=2113628).
2. Inicie o aplicativo [!INCLUDE[name-sos-short](../includes/name-sos-short.md)].

**arquivo zip**

1. Baixe o [.zip do [!INCLUDE[name-sos](../includes/name-sos-short.md)] para Windows](https://go.microsoft.com/fwlink/?linkid=2113529).
2. Procure o arquivo baixado e extraia-o.
3. Execute `\azuredatastudio-windows\azuredatastudio.exe`

## <a name="get-azure-data-studio-for-macos"></a>Obter o Azure Data Studio para macOS

1. Baixe o [[!INCLUDE[name-sos](../includes/name-sos-short.md)] para macOS](https://go.microsoft.com/fwlink/?linkid=2113528).
2. Para expandir o conteúdo do zip, clique duas vezes nele.
3. Para disponibilizar o [!INCLUDE[name-sos](../includes/name-sos-short.md)] no *Launchpad*, arraste *Azure Data Studio.app* para a pasta *Aplicativos*.

## <a name="get-azure-data-studio-for-linux"></a>Obter o Azure Data Studio para Linux

1. Baixe o [!INCLUDE[name-sos](../includes/name-sos-short.md)] para Linux usando um dos instaladores ou os arquivos tar.gz:
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2113344)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2113718)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2113627)
1. Para extrair o arquivo e iniciar o [!INCLUDE[name-sos](../includes/name-sos-short.md)], abra uma nova janela do terminal e digite os seguintes comandos:

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

   **Instalação do tar.gz:**
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
## <a name="download-insiders-build-of-azure-data-studio"></a>Baixar o build do Insiders do Azure Data Studio
Em geral, os usuários devem baixar a versão estável do Azure Data Studio acima. No entanto, caso deseje experimentar nossos recursos beta e nos enviar comentários, baixe um [build do Insiders do Azure Data Studio.](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-master)

## <a name="uninstall-azure-data-studio"></a>Desinstalar o Azure Data Studio

Caso tenha instalado o [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] usando o Windows Installer, desinstale-o da mesma forma que você remove aplicativos do Windows.

Caso tenha instalado o [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] com um arquivo .zip ou outros arquivos, basta excluir os arquivos.

## <a name="supported-operating-systems"></a>Sistemas operacionais com suporte

O [!INCLUDE[name-sos](../includes/name-sos-short.md)] é executado no Windows, no macOS e no Linux e é compatível com as seguintes plataformas:

### <a name="windows"></a>Windows
- Windows 10 (64 bits)
- Windows 8.1 (64 bits)
- Windows 8 (64 bits)
- Windows 7 (SP1) (64 bits) – exige o [KB2533623](https://www.microsoft.com/download/details.aspx?id=26767)
- Windows Server 2019
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

## <a name="recommended-system-requirements"></a>Requisitos do sistema recomendados

|             | Núcleos de CPU | Memória/RAM |
|:-----------|:---------|:----------|
| Recomendadas |     4     |      8 GB    |
|   Mínimo   |     2     |      4 GB     |
|             |           |            |

## <a name="check-for-updates"></a>Verificar atualizações

Para verificar se há atualizações mais recentes, clique no ícone de engrenagem na parte inferior esquerda da janela e clique em **Verificar se há atualizações**

## <a name="supported-sql-offerings"></a>Ofertas de SQL com suporte

* Esta versão do Azure Data Studio funciona com todas as [versões compatíveis com o SQL Server 2014 – [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044) e fornece o maior nível de suporte para trabalhar com os recursos de nuvem mais recentes no Banco de Dados SQL do Azure e no SQL Data Warehouse do Azure. O Azure Data Studio também fornece suporte de versão prévia para a Instância Gerenciada SQL do Azure.

## <a name="upgrade-from-sql-operations-studio"></a>Atualização do SQL Operations Studio

Caso você ainda esteja usando o SQL Operations Studio, precisará fazer a atualização para o Azure Data Studio. O SQL Operations Studio era o nome da versão prévia e a versão prévia do Azure Data Studio. Em setembro de 2018, [alteramos o nome para Azure Data Studio](https://cloudblogs.microsoft.com/sqlserver/2018/09/25/azure-data-studio-for-sql-server/) e liberamos a versão GA (Disponibilidade Geral). Como o SQL Operations Studio deixou de ser atualizado ou ter suporte, solicitamos que todos os usuários do SQL Operations Studio baixem a última versão do Azure Data Studio para obter os recursos, as atualizações de segurança e as correções mais recentes.

Ao fazer a atualização da versão prévia antiga para o Azure Data Studio mais recente, você perderá as configurações e as extensões atuais. Para mover as configurações, siga as instruções da seguinte seção *Mover as configurações de usuário*:

## <a name="move-user-settings"></a>Mover as configurações de usuário

Caso deseje mover as configurações personalizadas, os atalhos de teclado ou os snippets de código, siga as etapas abaixo. Isso é importante se você está atualizando da versão do SQL Operations Studio para o Azure Data Studio.

*Caso já tenha o Azure Data Studio ou nunca tenha instalado ou personalizado o SQL Operations Studio, ignore esta seção.*


1. Abra as Configurações clicando na engrenagem na parte inferior esquerda e clicando em **Configurações.**

   ![abrir configurações](./media/download/open-settings.png)

2. Clique com o botão direito do mouse na guia **Configurações de Usuário** na parte superior e clique em **Revelar no Explorer**

   ![revelar no Explorer](./media/download/reveal-in-explorer.png)

3. Copie todos os arquivos dessa pasta e salve em uma localização fácil de localizar na unidade local, como a pasta Documentos.

   ![copiar configurações](./media/download/copy-settings.png)

4. Na nova versão do Azure Data Studio, siga as etapas 1 e 2 e, em seguida, para a etapa 3, cole o conteúdo salvo na pasta. Você também pode copiar manualmente as configurações, as associações de teclas ou os snippets de código em suas respectivas localizações.

5. Se estiver substituindo uma instalação existente, exclua o diretório de instalação antigo antes da instalação para evitar erros de conexão com sua conta do Azure no gerenciador de recursos.

## <a name="next-steps"></a>Próximas etapas

Confira um dos seguintes inícios rápidos para começar:

- [Conectar-se ao SQL Server e consultá-lo](quickstart-sql-server.md)
- [Conectar-se a um Banco de Dados SQL do Azure e consultá-lo](quickstart-sql-database.md)
- [Conectar-se ao Data Warehouse do Azure e consultá-lo](quickstart-sql-dw.md)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

[Política de privacidade da Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839) e [coleta de dados de uso](usage-data-collection.md).

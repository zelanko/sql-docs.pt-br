---
title: Baixar e instalar o Azure Data Studio
description: Baixar e instalar o Azure Data Studio para Windows, macOS ou Linux
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan
ms.custom: seodec18
ms.date: 6/15/2020
ms.openlocfilehash: 249dfc97acea8228eef1234a41f1510e8b223788
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85774681"
---
# <a name="download-and-install-azure-data-studio"></a>Baixar e instalar o Azure Data Studio

O Azure Data Studio é executado no Windows, macOS e Linux.

Baixe e instale a versão mais recente:

> [!NOTE]
> Se você estiver fazendo a atualização do SQL Operations Studio e quiser manter as configurações, os atalhos de teclado ou os snippets de código, confira [Mover as configurações de usuário](#move-user-settings).

|Plataforma|Baixar|Data de liberação| Versão |
|:---|:---|:---|:---|
| Windows | [Instalador do usuário (recomendado)](https://go.microsoft.com/fwlink/?linkid=2132348)<br>[Instalador do sistema](https://go.microsoft.com/fwlink/?linkid=2132347)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2132518) | 15 de junho de 2020 | 1.19.0 |
| macOS | [.zip](https://go.microsoft.com/fwlink/?linkid=2132519) | 15 de junho de 2020 | 1.19.0 |
| Linux | [.deb](https://go.microsoft.com/fwlink/?linkid=2132350)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2132351)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2132349) | 15 de junho de 2020| 1.19.0 |

Para obter detalhes sobre a versão mais recente, confira as [notas sobre a versão](release-notes.md).

## <a name="get-azure-data-studio-for-windows"></a>Obter o Azure Data Studio para Windows

Esta versão do Azure Data Studio inclui uma experiência padrão do Windows Installer e um arquivo .zip.

O *instalador do usuário* é recomendado porque não exige privilégios de administrador, o que simplifica as instalações e atualizações. O instalador do usuário não exige privilégios de administrador, pois a localização está na pasta AppData Local (LOCALAPPDATA) do usuário. O instalador do usuário também fornece uma experiência de atualização em segundo plano mais tranquila. Para obter mais informações, confira [Configuração de usuário para Windows](https://code.visualstudio.com/updates/v1_26#_user-setup-for-windows).

**Instalador do usuário** (recomendado)

1. Baixe e execute o [instalador do *usuário* do [!INCLUDE[name-sos](../includes/name-sos-short.md)] para Windows](https://go.microsoft.com/fwlink/?linkid=2132348).
2. Inicie o aplicativo [!INCLUDE[name-sos-short](../includes/name-sos-short.md)].

**Instalador do sistema**

1. Baixe e execute o [instalador do *sistema* do [!INCLUDE[name-sos](../includes/name-sos-short.md)] para Windows](https://go.microsoft.com/fwlink/?linkid=2132347).
2. Inicie o aplicativo [!INCLUDE[name-sos-short](../includes/name-sos-short.md)].

**arquivo zip**

1. Baixe o [.zip do [!INCLUDE[name-sos](../includes/name-sos-short.md)] para Windows](https://go.microsoft.com/fwlink/?linkid=2132518).
2. Procure o arquivo baixado e extraia-o.
3. Execute `\azuredatastudio-windows\azuredatastudio.exe`

## <a name="get-azure-data-studio-for-macos"></a>Obter o Azure Data Studio para macOS

1. Baixe o [[!INCLUDE[name-sos](../includes/name-sos-short.md)] para macOS](https://go.microsoft.com/fwlink/?linkid=2132519).
2. Para expandir o conteúdo do zip, clique duas vezes nele.
3. Para disponibilizar o Azure Data Studio no *Launchpad*, arraste *Azure Data Studio.app* para a pasta *Aplicativos*.

## <a name="get-azure-data-studio-for-linux"></a>Obter o Azure Data Studio para Linux

1. Baixe o [!INCLUDE[name-sos](../includes/name-sos-short.md)] para Linux usando um dos instaladores ou os arquivos tar.gz:
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2132350)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2132351)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2132349)
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

Em geral, os usuários devem baixar a versão estável do Azure Data Studio acima. No entanto, caso deseje experimentar nossos recursos beta e nos enviar comentários, baixe um [build do Insiders do Azure Data Studio.](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-main)

## <a name="uninstall-azure-data-studio"></a>Desinstalar o Azure Data Studio

Caso tenha instalado o [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] usando o Windows Installer, desinstale-o da mesma forma como você remove aplicativos do Windows.

Caso tenha instalado o [!INCLUDE[name-sos-short](../includes/name-sos-short.md)] com um arquivo .zip ou outros arquivos, basta excluir os arquivos.

## <a name="supported-operating-systems"></a>Sistemas operacionais com suporte

O Azure Data Studio é executado no Windows, macOS e Linux e tem suporte nas seguintes plataformas:

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

- macOS 10.15 Catalina
- macOS 10.14 Mojave
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

- Esta versão do Azure Data Studio funciona com todas as [versões compatíveis com o SQL Server 2014 – [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044) e fornece o maior nível de suporte para trabalhar com os recursos de nuvem mais recentes no Banco de Dados SQL do Azure e no SQL Data Warehouse do Azure. O Azure Data Studio também fornece suporte de versão prévia para a Instância Gerenciada SQL do Azure.

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

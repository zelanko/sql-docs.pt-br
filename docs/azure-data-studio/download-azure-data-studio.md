---
title: Baixar e instalar o Azure Data Studio
description: Baixe e instale o Azure Data Studio para Windows, macOS ou Linux. Este artigo fornece datas de lançamento, números de versão, requisitos do sistema e links de download.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: overview
author: yualan
ms.author: alayu
ms.reviewer: maghan
ms.custom: seodec18
ms.date: 10/20/2020
ms.openlocfilehash: b3363e9b5b8872d3a78d7c5c0fa7f70a80c8d6f9
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257357"
---
# <a name="download-and-install-azure-data-studio"></a>Baixar e instalar o Azure Data Studio

O Azure Data Studio é executado no Windows, macOS e Linux.

Baixe e instale a versão mais recente:

> [!NOTE]
> Se você estiver fazendo a atualização do SQL Operations Studio e quiser manter as configurações, os atalhos de teclado ou os snippets de código, confira [Mover as configurações de usuário](#move-user-settings).

|Plataforma|Baixar|Data de liberação| Versão |
|--------|--------|------------|---------|
| Windows | [Instalador do usuário (recomendado)](https://go.microsoft.com/fwlink/?linkid=2145989)<br>[Instalador do sistema](https://go.microsoft.com/fwlink/?linkid=2145990)<br>[.zip](https://go.microsoft.com/fwlink/?linkid=2145864) | 14 de outubro de 2020 | 1.23.0 |
| macOS | [.zip](https://go.microsoft.com/fwlink/?linkid=2145865) | 14 de outubro de 2020 | 1.23.0 |
| Linux | [.deb](https://go.microsoft.com/fwlink/?linkid=2146016)<br>[.rpm](https://go.microsoft.com/fwlink/?linkid=2146015)<br>[.tar.gz](https://go.microsoft.com/fwlink/?linkid=2145866) | 14 de outubro de 2020 | 1.23.0 |

Para obter detalhes sobre a versão mais recente, confira as [notas sobre a versão](./release-notes-azure-data-studio.md).

## <a name="get-azure-data-studio-for-windows"></a>Obter o Azure Data Studio para Windows

[!INCLUDE [ssms-ads-install](../includes/ssms-azure-data-studio-install.md)]

Esta versão do Azure Data Studio inclui uma experiência padrão do Windows Installer e um arquivo .zip.

Recomendamos o *instalador do usuário* porque ele não exige privilégios de administrador, que simplificam as instalações e atualizações. O instalador do usuário não exige privilégios de administrador, pois a localização está na pasta AppData Local (LOCALAPPDATA) do usuário. O instalador do usuário também fornece uma experiência de atualização em segundo plano mais tranquila. Para obter mais informações, confira [Configuração de usuário para Windows](https://code.visualstudio.com/updates/v1_26#_user-setup-for-windows).

**Instalador do usuário** (recomendado)

1. Baixe e execute o [instalador do *usuário* do Azure Data Studio para Windows](https://go.microsoft.com/fwlink/?linkid=2145989).
2. Iniciar o aplicativo Azure Data Studio.

**Instalador do sistema**

1. Baixe e execute o [instalador do *sistema* do Azure Data Studio para Windows](https://go.microsoft.com/fwlink/?linkid=2145990).
2. Iniciar o aplicativo Azure Data Studio.

**arquivo zip**

1. Baixe o [.zip do Azure Data Studio para Windows](https://go.microsoft.com/fwlink/?linkid=2145864).
2. Procure o arquivo baixado e extraia-o.
3. Execute `\azuredatastudio-windows\azuredatastudio.exe`

## <a name="get-azure-data-studio-for-macos"></a>Obter o Azure Data Studio para macOS

1. Baixe o [Azure Data Studio para macOS](https://go.microsoft.com/fwlink/?linkid=2145865).
2. Para expandir o conteúdo do zip, clique duas vezes nele.
3. Para disponibilizar o Azure Data Studio no *Launchpad*, arraste *Azure Data Studio.app* para a pasta *Aplicativos*.

## <a name="get-azure-data-studio-for-linux"></a>Obter o Azure Data Studio para Linux

1. Baixe o Azure Data Studio para Linux usando um dos instaladores ou o arquivo tar.gz:
    - [.deb](https://go.microsoft.com/fwlink/?linkid=2146016)
    - [.rpm](https://go.microsoft.com/fwlink/?linkid=2146015)
    - [.tar.gz](https://go.microsoft.com/fwlink/?linkid=2145866)
1. Para extrair o arquivo e iniciar o Azure Data Studio, abra uma nova janela do Terminal e digite os seguintes comandos:

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

Em geral, os usuários devem baixar a versão estável do Azure Data Studio acima. No entanto, caso deseje experimentar os recursos beta e nos enviar comentários, baixe uma [Compilação interna do Azure Data Studio](https://github.com/microsoft/azuredatastudio#try-out-the-latest-insiders-build-from-main).

## <a name="supported-operating-systems"></a>Sistemas operacionais com suporte

O Azure Data Studio é executado no Windows, macOS e Linux e tem suporte nas seguintes plataformas:

### <a name="windows"></a>Windows

- Windows 10 (64 bits)
- Windows 8.1 (64 bits)
- Windows 8 (64 bits)
- Windows 7 (SP1)
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

| Recomendado/Mínimo | Núcleos de CPU | Memória/RAM |
|---------------------|-----------|------------|
| Recomendadas         |     4     |   8 GB     |
|   Mínimo           |     2     |   4 GB     |

## <a name="check-for-updates"></a>Verificar atualizações

Para verificar se há atualizações mais recentes, selecione o ícone de engrenagem na parte inferior esquerda da janela e selecione **Verificar se há Atualizações**.

Atualizações de ambiente offline podem ser aplicadas [instalando a versão mais recente](#download-and-install-azure-data-studio) diretamente em uma versão já instalada. Não é necessário desinstalar as versões anteriores do Azure Data Studio. O instalador atualiza um aplicativo atualmente instalado, se presente.

## <a name="supported-sql-offerings"></a>Ofertas de SQL com suporte

- Esta versão do Azure Data Studio funciona com todas as versões [compatíveis do SQL Server 2014 – [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044) e fornece suporte para trabalhar com os recursos de nuvem mais recentes no Banco de Dados SQL do Azure e no Azure Synapse Analytics. O Azure Data Studio também fornece suporte de versão prévia para a Instância Gerenciada SQL do Azure.

## <a name="move-user-settings"></a>Mover as configurações de usuário

Caso deseje mover as configurações personalizadas, os atalhos de teclado ou os snippets de código, siga as etapas abaixo. Isso é importante se você está fazendo a atualização da versão do SQL Operations Studio para o Azure Data Studio.

*Caso já tenha o Azure Data Studio ou nunca tenha instalado ou personalizado o SQL Operations Studio, ignore esta seção.*

1. Abra as Configurações selecionando a engrenagem na parte inferior esquerda e selecionando **Configurações.**

   ![configurações de edição no Azure Data Studio](./media/download/open-settings.png)

2. Clique com o botão direito do mouse na guia **Configurações de Usuário** na parte superior e selecione **Revelar no Explorer**

   ![inicie o explorador, que levará você ao sistema de arquivos local](./media/download/reveal-in-explorer.png)

3. Copie todos os arquivos dessa pasta e salve em uma localização fácil de localizar na unidade local, como a pasta Documentos.

   ![use os arquivos e copie para seu local](./media/download/copy-settings.png)

4. Na nova versão do Azure Data Studio, siga as etapas 1 e 2 e, em seguida, para a etapa 3, cole o conteúdo salvo na pasta. Você também pode copiar manualmente as configurações, as associações de teclas ou os snippets de código nas respectivas localizações.

5. Se estiver substituindo uma instalação existente, exclua o diretório de instalação antigo antes da instalação para evitar erros de conexão com sua conta do Azure no gerenciador de recursos.

## <a name="unattended-install-for-windows"></a>Instalação autônoma no Windows

Você também pode instalar o Azure Data Studio usando um script de prompt de comando.

Se você deseja instalar o Azure Data Studio em segundo plano sem prompts de GUI e estiver na plataforma Windows, siga as etapas abaixo.

1. Inicialize o prompt de comando com permissões elevadas.

2. Digite o comando abaixo no prompt de comando.

    ```console
    <path where the azuredatastudio-windows-user-setup-x.xx.x.exe file is located> /VERYSILENT /MERGETASKS=!runcode>
    ```

    Exemplo:

    ```console
    %systemdrive%\azuredatastudio-windows-user-setup-1.23.0.exe /VERYSILENT /MERGETASKS=!runcode
    ```

    > [!Note]
    > O exemplo também funciona com o arquivo do instalador do sistema.
    > 
    > ```console
    > <path where the azuredatastudio-windows-setup-x.xx.x.exe file is located> /VERYSILENT /MERGETASKS=!runcode>
    > ```

    Você também pode passar */SILENT* em vez de */VERYSILENT* para ver a interface do usuário da configuração.

3. Se tudo correr bem, você poderá ver o Azure Data Studio instalado.

## <a name="uninstall-azure-data-studio"></a>Desinstalar o Azure Data Studio

Caso tenha instalado o Azure Data Studio usando o Windows Installer, desinstale-o da mesma forma como você remove aplicativos do Windows.

Se você instalou o Azure Data Studio com um arquivo .zip ou outros arquivos, exclua os arquivos.

## <a name="next-steps"></a>Próximas etapas

Confira um dos seguintes inícios rápidos para começar:

- [Conectar-se ao SQL Server e consultá-lo](quickstart-sql-server.md)
- [Conectar-se a um Banco de Dados SQL do Azure e consultá-lo](quickstart-sql-database.md)
- [Conectar-se ao Data Warehouse do Azure e consultá-lo](quickstart-sql-dw.md)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]

[Política de privacidade da Microsoft](https://go.microsoft.com/fwlink/?LinkId=521839) e [coleta de dados de uso](usage-data-collection.md).

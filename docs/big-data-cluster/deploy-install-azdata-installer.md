---
title: Instalar o azdata com Windows Installer
titleSuffix: SQL Server big data clusters
description: Saiba como instalar a ferramenta azdata para instalar e gerenciar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)] o (versão prévia) com o instalador.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 08/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a8dd5d2c7d0210880a82d774185a3f2a915608ec
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70158141"
---
# <a name="install-azdata-to-manage-includebig-data-clusters-2019includesssbigdataclusters-ss-novermd-with-windows-installer"></a>Instalar `azdata` para gerenciar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] com o Windows Installer

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Este artigo descreve como instalar `azdata` o para SQL Server 2019 de clusters de Big data versão release candidate no Windows. Antes que a instalação do Windows estivesse disponível, a `azdata` instalação `pip`do é necessária.

>Para Linux (Ubuntu), consulte [instalar `azdata` com o instalador](./deploy-install-azdata-linux-package.md).

Neste momento, não há gerenciadores de pacotes para instalar `azdata` em outros sistemas operacionais ou distribuições. Para essas plataformas, consulte [instalar `azdata` sem o Gerenciador de pacotes](./deploy-install-azdata.md).

## <a name="install-azdata-with-the-microsoft-windows-installer"></a>Instalar `azdata` com o Microsoft Windows Installer

Para instalar `azdata` o com o Microsoft Windows Installer,

1. Remova `azdata` se ele foi instalado usando `pip`. Se `azdata` o tiver sido instalado usando Windows Installer, vá para a próxima etapa.
1. Instale `azdata` o usando o Windows Installer.

### <a name="uninstall-if-previous-installation-done-with-pip"></a>Desinstalar se a instalação anterior foi feita com`pip`

Se você tiver versões anteriores do **mssqlctl** instaladas, remova-as. O comando a seguir remove a versão CTP 3,1 do **mssqlctl**.

   ```bash
   pip3 uninstall -r https://private-repo.microsoft.com/python/ctp3.1/mssqlctl/requirements.txt
   ```

Se você tiver versões anteriores do `azdata` instaladas, será importante desinstalá-la primeiro antes de instalar a versão mais recente.

   Para o CTP 3,2, execute o comando a seguir.

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-ctp3.2/requirements.txt
   ```

Depois de removido [, `azdata` instale no Windows](#install-azdata-windows).

>[!NOTE]
>Se a instalação anterior tiver sido feita usando o MSI, não será necessário desinstalar nenhuma versão atual antes de usar o instalador MSI.

### <a id="install-azdata-windows"></a>Instalar com o Windows Installer

Use o Windows Installer para instalar ou atualizar `azdata` no Windows.

[Baixe o `azdata` Windows Installer](http://aka.ms/azdata-msi).

Quando o instalador perguntar se pode fazer alterações no seu computador, clique em `Yes`.

### <a name="uninstall-azdata-with-windows-installer"></a>Desinstalar `azdata` com o Windows Installer

Para desinstalar `azdata` o com o Windows Installer, siga as instruções para o sistema operacional apropriado.

| Plataforma      | Instruções                                           |
| ------------- |--------------------------------------------------------|
| Windows 10    | Iniciar > Configurações > aplicativos                                |
| Windows 8     | Iniciar > painel de controle > programas > desinstalar um programa |

O programa a ser desinstalado **`Azdata CLI`** é chamado. Selecione este aplicativo e clique no `Uninstall` botão.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters Big Data, consulte [o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]que são?](big-data-cluster-overview.md).

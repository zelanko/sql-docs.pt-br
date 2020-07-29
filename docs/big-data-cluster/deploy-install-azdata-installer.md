---
title: Instalar o azdata com o Windows Installer
titleSuffix: SQL Server big data clusters
description: Saiba como instalar a ferramenta azdata para instalar e gerenciar Clusters de Big Data do SQL Server com o instalador.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 72b1caab9f457ad9ba2c21792ff4927d954cb3f4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85784277"
---
# <a name="install-azdata-to-manage-big-data-clusters-2019-with-windows-installer"></a>Instalar o `azdata` para gerenciar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] com o Windows Installer

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este artigo descreve como instalar `azdata` para Clusters de Big Data do SQL Server 2019 no Windows. Antes que a instalação do Windows estivesse disponível, a instalação do `azdata` exigiu `pip`.

>Para Linux (Ubuntu), confira [Instalar o `azdata` com o instalador](./deploy-install-azdata-linux-package.md).

Neste momento, não há gerenciadores de pacotes para instalar `azdata` em outros sistemas operacionais ou distribuições. Para essas plataformas, confira [Instalar o `azdata` sem o gerenciador de pacotes](./deploy-install-azdata.md).

## <a name="install-azdata-with-the-microsoft-windows-installer"></a>Instalar o `azdata` com o Microsoft Windows Installer

Para instalar o `azdata` com o Microsoft Windows Installer,

1. remova `azdata` se ele tiver sido instalado usando `pip`. Se o `azdata` tiver sido instalado usando Windows Installer, vá para a próxima etapa.
1. Instale o `azdata` usando o Windows Installer.

### <a name="uninstall-if-previous-installation-done-with-pip"></a>Desinstalar se a instalação anterior tiver sido feita com `pip`

Caso você tenha versões anteriores de `azdata` instaladas, será importante desinstalá-las primeiro antes de instalar a última versão.

   Para remover a versão Release Candidate do `azdata`, execute o comando a seguir.

   ```bash
   pip3 uninstall -r https://azdatacli.blob.core.windows.net/python/azdata/2019-rc1/requirements.txt
   ```

Depois de removida, [instale o `azdata` no Windows](#install-azdata-windows).

>[!NOTE]
>Se a instalação anterior tiver sido feita usando o MSI, não será necessário desinstalar nenhuma versão atual antes de usar o instalador do MSI.

### <a name="install-with-windows-installer"></a><a id="install-azdata-windows"></a>Instalar com o Windows Installer

Use o Windows Installer para instalar ou atualizar o `azdata` no Windows.

[Baixe o Windows Installer do `azdata`](https://aka.ms/azdata-msi).

Quando o instalador perguntar se ele pode fazer alterações ao seu computador, clique em `Yes`.

### <a name="uninstall-azdata-with-windows-installer"></a>Desinstalar o `azdata` com o Windows Installer

Para desinstalar o `azdata` com o Windows Installer, siga as instruções para o sistema operacional adequado.

| Plataforma      | Instruções                                           |
| ------------- |--------------------------------------------------------|
| Windows 10| Iniciar > Configurações > Aplicativos                                |
| Windows 8     | Iniciar > Painel de Controle > Programas > Desinstalar um programa |

O programa a ser desinstalado chama-se `Azdata CLI`. Selecione este aplicativo e clique no botão `Uninstall`.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md)
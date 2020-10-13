---
title: Instalar o azdata com o Windows Installer
titleSuffix: ''
description: Saiba como instalar a ferramenta azdata com o instalador.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b36b69206f6a50c3c24a5ed059f52a7f2edd6c68
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91784741"
---
# <a name="install-azdata-with-windows-installer"></a>Instalar o `azdata` com o Windows Installer

[!INCLUDE [azdata](../../includes/applies-to-version/azdata.md)]

Este artigo descreve como instalar o `azdata` no Windows com um instalador. Use o `azdata` para gerenciar os Clusters de Big Data do SQL Server ou os serviços de dados habilitados para Azure Arc.

## <a name="steps-to-install-azdata-with-the-microsoft-windows-installer"></a>Etapas para instalar o `azdata` com o Microsoft Windows Installer

Para instalar o `azdata` com o Microsoft Windows Installer,

1. remova `azdata` se ele tiver sido instalado usando `pip`. Se o `azdata` tiver sido instalado usando Windows Installer, vá para a próxima etapa.
1. Instale o `azdata` usando o [Windows Installer](https://aka.ms/azdata-msi).

### <a name="uninstall-azdata-with-windows-installer"></a>Desinstalar o `azdata` com o Windows Installer

Para desinstalar o `azdata` com o Windows Installer, siga as instruções para o sistema operacional adequado.

| Plataforma      | Instruções                                           |
| ------------- |--------------------------------------------------------|
| Windows 10| Iniciar > Configurações > Aplicativos                                |
| Windows 8     | Iniciar > Painel de Controle > Programas > Desinstalar um programa |

O programa a ser desinstalado chama-se `Azdata CLI`. Selecione este aplicativo e clique no botão `Uninstall`.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../../includes/ssbigdataclusters-ver15.md)]?](../../big-data-cluster/big-data-cluster-overview.md)

Usar o azdata com [serviços de dados habilitados o Azure Arc](/azure/azure-arc/data/)

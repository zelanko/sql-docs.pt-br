---
title: Abrir e salvar arquivos com pacotes SSIS implantados no Azure | Microsoft Docs
description: Saiba como abrir e salvar arquivos localmente e no Azure quando você migra para o SSIS no Azure, por lift-and-shift, pacotes SSIS que usam sistemas de arquivos locais
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c4f9d5e91db382d59dc156ed919c1af06cc56b77
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35410468"
---
# <a name="open-and-save-files-on-premises-and-in-azure-with-ssis-packages-deployed-in-azure"></a>Abrir e salvar arquivos localmente e no Azure com pacotes SSIS implantados no Azure

Este artigo descreve como abrir e salvar arquivos localmente e no Azure quando você migra para o SSIS no Azure, por lift-and-shift, pacotes SSIS que usam sistemas de arquivos locais.

> [!IMPORTANT]
> Atualmente, o SSISDB (Catálogo do SSIS) dá suporte a apenas um único conjunto de credenciais de acesso. Como resultado, você não pode usar conjuntos de credenciais diferentes em um único conjunto para se conectar a vários compartilhamentos de arquivos locais e a compartilhamentos de Arquivos do Azure.

## <a name="save-temporary-files"></a>Salvar arquivos temporários
Se você precisar armazenar e processar arquivos temporários durante a execução de um único pacote, os pacotes poderão usar o diretório de trabalho atual (`.`) ou a pasta temporária (`%TEMP%`) de seus nós do Azure SSIS Integration Runtime.

## <a name="use-on-premises-file-shares"></a>Usar compartilhamentos de arquivos local
Para continuar a usar os **compartilhamentos de arquivos locais** quando você migrar por lift-and-shift pacotes que usem sistemas de arquivos locais no SSIS no Azure, faça o seguinte:
1.  Transfira arquivos de sistemas de arquivos locais para compartilhamentos de arquivos locais.
2.  Una os compartilhamentos de arquivos locais a uma Rede Virtual do Azure.
3.  Una o Azure-SSIS IR à mesma rede virtual. Para obter mais informações, consulte [Unir um Azure-SSIS Integration Runtime a uma rede virtual](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network).
4.  Conecte o Azure-SSIS IR aos compartilhamentos de arquivos locais dentro da mesma rede virtual, configurando credenciais de acesso que usam a Autenticação do Windows. Para obter mais informações, confira [Conectar-se a dados e a compartilhamentos de arquivos com a Autenticação do Windows](ssis-azure-connect-with-windows-auth.md).
5.  Atualize caminhos de arquivos locais em seus pacotes para caminhos UNC apontando para compartilhamentos de arquivos locais. Por exemplo, atualize `C:\abc.txt` para `\\<on-prem-server-name>\<share-name>\abc.txt`.

## <a name="use-azure-file-shares"></a>Usar compartilhamentos de arquivos do Azure
Para usar **Arquivos do Azure** quando você migrar por lift-and-shift pacotes que usem sistemas de arquivos locais no SSIS no Azure, faça o seguinte:
1.  Transfira arquivos de sistemas de arquivos locais para Arquivos do Azure. Para obter mais informações, consulte [Arquivos do Azure](https://azure.microsoft.com/services/storage/files/).
2.  Conecte o Azure-SSIS IR aos Arquivos do Azure, configurando credenciais de acesso que usam a autenticação do Windows. Para obter mais informações, confira [Conectar-se a dados e a compartilhamentos de arquivos com a Autenticação do Windows](ssis-azure-connect-with-windows-auth.md).
3.  Atualize caminhos de arquivos locais em seus pacotes para caminhos UNC apontando para Arquivos do Azure. Por exemplo, atualize `C:\abc.txt` para `\\<storage-account-name>.file.core.windows.net\<share-name>\abc.txt`.

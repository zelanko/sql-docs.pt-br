---
title: Conectar-se a arquivos e compartilhamentos de arquivos local e no Azure | Microsoft Docs
description: Este artigo descreve como usar o sistema de arquivos e compartilhamentos de arquivos, localmente e no Azure, com o SSIS
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6472263658ed831aade7d0951b10a712dfee312d
ms.sourcegitcommit: 0cc2cb281e467a13a76174e0d9afbdcf4ccddc29
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/15/2018
---
# <a name="connect-to-files-and-file-shares-on-premises-and-in-azure-with-ssis"></a>Conectar-se a arquivos e compartilhamentos de arquivos local e no Azure com o SSIS
Este artigo descreve como atualizar seus pacotes do SSIS (SQL Server Integration Services) quando você compara e desloca pacotes que usam sistemas de arquivos locais no SSIS no Azure.

> [!IMPORTANT]
> Atualmente, o SSISDB (banco de dados do catálogo do SSIS) dá suporte a apenas um único conjunto de credenciais de acesso. Portanto, o Azure SSIS IR (Integration Runtime) não pode usar credenciais diferentes para se conectar a vários compartilhamentos de arquivos locais e compartilhamentos de arquivos do Azure.

## <a name="store-temporary-files"></a>Armazenar arquivos temporários
Se você precisar armazenar e processar arquivos temporários durante a execução de um único pacote, os pacotes poderão usar o diretório de trabalho atual (`.`) ou a pasta temporária (`%TEMP%`) de seus nós do Azure SSIS Integration Runtime.

## <a name="store-files-across-multiple-package-executions"></a>Armazenar arquivos entre várias execuções de pacote
Se você precisar armazenar e processar arquivos permanentes e mantê-los entre várias execuções de pacote, você poderá usar o compartilhamentos de arquivos locais ou arquivos do Azure

### <a name="use-on-premises-file-shares"></a>Usar compartilhamentos de arquivos local
Para continuar a usar os **compartilhamentos de arquivos locais** quando você migrar por lift-and-shift pacotes que usem sistemas de arquivos locais no SSIS no Azure, faça o seguinte:
1.  Transfira arquivos de sistemas de arquivos locais para compartilhamentos de arquivos locais.
2.  Una os compartilhamentos de arquivos locais a uma VNet (rede virtual) do Azure.
3.  Una o Azure-SSIS IR à mesma VNet. Para obter mais informações, consulte [Unir um Azure-SSIS Integration Runtime a uma rede virtual](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network).
4.  Conecte o Azure-SSIS IR aos compartilhamentos de arquivos locais dentro da mesma VNet, configurando credenciais de acesso que usam a autenticação do Windows. Para obter mais informações, consulte [Conectar-se às fontes de dados e compartilhamentos de arquivo do Azure locais com a Autenticação do Windows](ssis-azure-connect-with-windows-auth.md).
5.  Atualize caminhos de arquivos locais em seus pacotes para caminhos UNC apontando para compartilhamentos de arquivos locais. Por exemplo, atualize `C:\abc.txt` para `\\<on-prem-server-name>\<share-name>\abc.txt`.

### <a name="use-azure-file-shares"></a>Usar compartilhamentos de arquivos do Azure
Para usar **Arquivos do Azure** quando você migrar por lift-and-shift pacotes que usem sistemas de arquivos locais no SSIS no Azure, faça o seguinte:
1.  Transfira arquivos de sistemas de arquivos locais para Arquivos do Azure. Para obter mais informações, consulte [Arquivos do Azure](https://azure.microsoft.com/services/storage/files/).
2.  Conecte o Azure-SSIS IR aos Arquivos do Azure, configurando credenciais de acesso que usam a autenticação do Windows. Para obter mais informações, consulte [Conectar-se às fontes de dados e compartilhamentos de arquivo do Azure locais com a Autenticação do Windows](ssis-azure-connect-with-windows-auth.md).
3.  Atualize caminhos de arquivos locais em seus pacotes para caminhos UNC apontando para Arquivos do Azure. Por exemplo, atualize `C:\abc.txt` para `\\<storage-account-name>.file.core.windows.net\<share-name>\abc.txt`.

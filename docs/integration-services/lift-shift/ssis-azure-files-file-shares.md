---
title: Armazenar e recuperar arquivos em compartilhamentos de arquivos local e no Azure | Microsoft Docs
description: Este artigo descreve como usar o sistema de arquivos e compartilhamentos de arquivos, localmente e no Azure, com o SSIS
ms.date: 11/10/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f4980f39deea4d70817da3650dccbff7997ba83d
ms.sourcegitcommit: 06bb91d138a4d6395c7603a2d8f99c69a20642d3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2017
---
# <a name="store-and-retrieve-files-on-file-shares-on-premises-and-in-azure-with-ssis"></a>Armazenar e recuperar arquivos em compartilhamentos de arquivos local e no Azure com o SSIS
Este artigo descreve como atualizar seus pacotes do SSIS (SQL Server Integration Services) quando você compara e desloca pacotes que usam sistemas de arquivos locais no SSIS no Azure.

> [!IMPORTANT]
> Atualmente, o SSISDB (banco de dados do catálogo do SSIS) dá suporte a apenas um único conjunto de credenciais de acesso. Portanto, o Azure SSIS IR (Integration Runtime) não pode usar credenciais diferentes para se conectar a vários compartilhamentos de arquivos locais e compartilhamentos de arquivos do Azure.

## <a name="store-temporary-files"></a>Armazenar arquivos temporários
Se você precisar armazenar e processar arquivos temporários durante a execução de um único pacote, os pacotes poderão usar a pasta temporária `(.)/temp` ou `%TEMP%` de seus nós do Azure SSIS Integration Runtime.

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

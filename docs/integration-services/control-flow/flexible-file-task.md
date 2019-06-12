---
title: Tarefa de Arquivo Flexível | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPEXTFILETASK.F1
- SQL14.DTS.DESIGNER.AFPEXTFILETASK.F1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2d01304a36f7676f53ffef3f6c6e3c600cb87cb6
ms.sourcegitcommit: fc0eb955b41c9c508a1fe550eb5421c05fbf11b4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66411093"
---
# <a name="flexible-file-task"></a>Tarefa Arquivo Flexível

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

A Tarefa de Arquivo Flexível permite que os usuários realizem operações de arquivo em vários serviços de armazenamento compatíveis.
Os serviços de armazenamento compatíveis no momento são

- Sistema de Arquivos Local
- [Armazenamento de Blobs do Azure](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-introduction)

A Tarefa de Arquivo Flexível é um componente do [Feature Pack do SSIS (SQL Server Integration Services) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Para adicionar uma Tarefa de Arquivo Flexível a um pacote, arraste-a da Caixa de Ferramentas do SSIS para a tela do designer. Em seguida, clique duas vezes na tarefa ou clique com o botão direito do mouse na tarefa e selecione **Editar** para abrir a caixa de diálogo **Editor de Tarefa de Arquivo Flexível**.

A propriedade **Operation** especifica a operação de arquivo a ser executada.
Somente a operação **Copy** é compatível no momento.

Para a operação **Copy**, as seguintes propriedades estão disponíveis.

- **SourceConnectionType:** especifica o tipo do gerenciador de conexões de origem.
- **SourceConnection:** especifica o gerenciador de conexões de origem.
- **SourceFolderPath:** especifica o caminho da pasta de origem.
- **SourceFileName:** especifica o nome do arquivo de origem. Se deixada em branco, a pasta de origem será copiada.
- **SearchRecursively:** especifica se as subpastas devem ser copiadas de maneira recursiva.
- **DestinationConnectionType:** especifica o tipo do gerenciador de conexões de destino.
- **DestinationConnection:** especifica o gerenciador de conexões de destino.
- **DestinationFolderPath:** especifica o caminho da pasta de destino.
- **DestinationFileName:** especifica o nome do arquivo de destino.

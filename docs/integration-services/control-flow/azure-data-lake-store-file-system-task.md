---
title: "Tarefa de sistema de arquivos do repositório Azure Data Lake | Microsoft Docs"
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-server-2016
ms.reviewer: douglasl
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSTASK.F1
- SQL14.DTS.DESIGNER.AFPADLSTASK.F1
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 29b296b2ae7e04871e81a9c236cb990bdd19562b
ms.openlocfilehash: cbc72958f992e0b5cae12cdfc8c0996378f9708c
ms.contentlocale: pt-br
ms.lasthandoff: 10/11/2017

---
# <a name="azure-data-lake-store-file-system-task"></a>Tarefa de sistema de arquivos do repositório Azure Data Lake

A tarefa de sistema de arquivos do Azure Data Lake repositório permite que os usuários a executar várias operações de sistema de arquivos em [Azure Data Lake ADLS (repositório)](https://azure.microsoft.com/services/data-lake-store/).

A tarefa de sistema de arquivos do Azure Data Lake repositório é um componente do [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

## <a name="configure-the-azure-data-lake-store-file-system-task"></a>Configurar a tarefa de sistema de arquivos do repositório Azure Data Lake

Para adicionar uma tarefa de sistema de arquivos do Azure Data Lake repositório para um pacote, arraste-o na caixa de ferramentas do SSIS para a tela do designer. Em seguida, clique duas vezes em tarefa, ou a tarefa e selecione **editar**para abrir o **Editor da tarefa do sistema do arquivo armazenamento do Azure Data Lake** caixa de diálogo.

O **operação** propriedade especifica a operação do sistema de arquivos para executar. Selecione uma das seguintes operações:

- **CopyToADLS:** carregar arquivos para ADLS.
- **CopyFromADLS:** baixar arquivos do ADLS.

## <a name="configure-the-properties-for-the-operation"></a>Configurar as propriedades para a operação
Para qualquer operação, você precisa especificar um Gerenciador de conexão do Azure Data Lake.

Aqui estão as propriedades específicas para cada operação:

### <a name="copytoadls"></a>CopyToADLS
- **LocalDirectory:** Especifica o diretório local de origem que contém os arquivos a serem carregados.
- **FileNamePattern:** Especifica um filtro de nome de arquivo para arquivos de origem. Somente os arquivos cujo nome corresponde ao padrão especificado são carregados. Curingas `*` e `?` têm suporte.
- **SearchRecursively:** Especifica se a pesquisa recursivamente dentro do diretório de origem para os arquivos carregar.
- **AzureDataLakeDirectory:** Especifica o diretório de destino do ADLS para carregar arquivos.
- **FileExpiry:** Especifica uma data de expiração para os arquivos carregados ADLS. Essa propriedade deixe em branco para indicar que os arquivos nunca expirarem.

### <a name="copyfromadls"></a>CopyFromADLS
- **AzureDataLakeDirectory:** Especifica o diretório de origem do ADLS que contém os arquivos para baixar.
- **SearchRecursively:** Especifica se deseja pesquisar dentro do diretório de origem de arquivos para baixar de forma recursiva.
- **LocalDirectory:** Especifica o diretório de destino para armazenar arquivos baixados.

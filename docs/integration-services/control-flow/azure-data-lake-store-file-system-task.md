---
title: "Tarefa de sistema de arquivos do repositório Azure Data Lake | Microsoft Docs"
ms.custom: 
ms.date: 08/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
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
ms.sourcegitcommit: 303d3b74da3fe370d19b7602c0e11e67b63191e7
ms.openlocfilehash: ce2355de312faed9ab66991d6d0dd344ff315a55
ms.contentlocale: pt-br
ms.lasthandoff: 08/29/2017

---
# <a name="azure-data-lake-store-file-system-task"></a>Tarefa de sistema de arquivos do repositório Azure Data Lake

O **tarefa de sistema de arquivos de armazenamento do Azure Data Lake** permite que os usuários executar várias operações de sistema de arquivos em [Azure Data Lake ADLS (repositório)](https://azure.microsoft.com/services/data-lake-store/).

O **tarefa de sistema de arquivos de armazenamento do Azure Data Lake** é um componente do [SQL Server Integration Services (SSIS) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Para adicionar uma tarefa de sistema de arquivos do Azure Data Lake repositório para um pacote, arraste-o na caixa de ferramentas do SSIS para a tela do designer. Em seguida, clique duas vezes em tarefa, ou a tarefa e selecione **editar**, para abrir a caixa de diálogo do editor de tarefa.

O **operação** propriedade especifica a operação do sistema de arquivos para executar. As seguintes operações têm suporte.

* **CopyToADLS:** carregar arquivos para ADLS.
* **CopyFromADLS:** baixar arquivos do ADLS.

Para qualquer operação, você precisa especificar um Gerenciador de conexão do Azure Data Lake.

Aqui estão as descrições das propriedades específicas para cada operação.

## <a name="copytoadls"></a>CopyToADLS
* **LocalDirectory:** Especifica o diretório de origem que contém os arquivos a serem carregados.
* **FileNamePattern:** Especifica um filtro de nome de arquivo para arquivos de origem. Somente os arquivos cujo nome corresponde ao padrão especificado serão carregados. Curingas `*` e `?` têm suporte.
* **SearchRecursively:** Especifica se a pesquisa recursivamente dentro do diretório de origem para os arquivos carregar.
* **AzureDataLakeDirectory:** Especifica o diretório de destino do ADLS para carregar arquivos.
* **FileExpiry:** Especifica uma data de expiração para os arquivos carregados ADLS ou deixam essa propriedade em branco para indicar que os arquivos nunca expirarem.

## <a name="copyfromadls"></a>CopyFromADLS
* **AzureDataLakeDirectory:** Especifica o diretório de origem do ADLS que contém os arquivos para baixar.
* **SearchRecursively:** Especifica se deseja pesquisar dentro do diretório de origem de arquivos para baixar de forma recursiva.
* **LocalDirectory:** Especifica o diretório de destino para armazenar arquivos baixados.

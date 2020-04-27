---
title: Tarefa do sistema de arquivos do Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSTASK.F1
- SQL11.DTS.DESIGNER.AFPADLSTASK.F1
ms.assetid: 02b9edd7-6ef9-463e-abbf-e1830bcae875
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 69a521cb72e68141f5706f5187a0288a3f44f241
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66061382"
---
# <a name="azure-data-lake-store-file-system-task"></a>Tarefa do sistema de arquivos do Azure Data Lake Store

A **tarefa sistema de arquivos Azure data Lake Store** permite que os usuários executem várias operações de sistema de arquivos em [Azure data Lake Store (ADLS)](https://azure.microsoft.com/services/data-lake-store/).

Para adicionar uma tarefa do sistema de arquivos do Azure Data Lake Store para um pacote, arraste-o da Caixa de Ferramentas do SSIS para a tela do designer. Em seguida, clique duas vezes na tarefa ou clique com o botão direito do mouse na tarefa e selecione **Editar**para abrir a caixa de diálogo editor da tarefa.

A propriedade **Operation** especifica a operação do sistema de arquivos a ser executada. As operações a seguir têm suporte.

* **CopyToADLS:** carregar arquivos para o ADLS.
* **CopyFromADLS:** baixar arquivos do ADLS.

Para qualquer operação, você precisa especificar um gerenciador de conexões do Azure Data Lake.

Aqui estão as descrições das propriedades específicas de cada operação.

## <a name="copytoadls"></a>CopyToADLS

* **LocalDirectory:** Especifica o diretório de origem que contém os arquivos a serem carregados.
* **FileNamePattern:** especifica um filtro de nome de arquivo para arquivos de origem. Somente os arquivos cujo nome corresponde ao padrão especificado serão carregados. Curingas `*` e `?` são compatíveis.
* **SearchRecursively:** especifica se deve-se pesquisar recursivamente dentro do diretório de origem por arquivos a serem carregados.
* **AzureDataLakeDirectory:** especifica o diretório de destino do ADLS para o qual carregar arquivos.
* **Fileexpirey:** Especifica uma data e hora de expiração para os arquivos carregados em ADLS, ou deixe essa propriedade em branco para indicar que os arquivos nunca expiram.

## <a name="copyfromadls"></a>CopyFromADLS

* **AzureDataLakeDirectory:** especifica o diretório de origem do ADLS que contém os arquivos a serem baixados.
* **SearchRecursively:** especifica se deve-se pesquisar recursivamente dentro do diretório de origem por arquivos a serem baixados.
* **LocalDirectory:** especifica o diretório de destino no qual armazenar arquivos baixados.

---
title: Tarefa do sistema de arquivos do Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSTASK.F1
- SQL11.DTS.DESIGNER.AFPADLSTASK.F1
ms.assetid: 02b9edd7-6ef9-463e-abbf-e1830bcae875
caps.latest.revision: 3
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.openlocfilehash: 240780efd1b12596b0ebb6156ad98c508f0e8051
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36005918"
---
# <a name="azure-data-lake-store-file-system-task"></a>Tarefa do sistema de arquivos do Azure Data Lake Store
O **tarefa de sistema de arquivos de armazenamento do Azure Data Lake** permite que os usuários executar várias operações de sistema de arquivos em [Azure Data Lake ADLS (repositório)](https://azure.microsoft.com/en-us/services/data-lake-store/).

Para adicionar uma tarefa do sistema de arquivos do Azure Data Lake Store para um pacote, arraste-o da Caixa de Ferramentas do SSIS para a tela do designer. Em seguida, clique duas vezes em tarefa, ou a tarefa e selecione **editar**, para abrir a caixa de diálogo do editor de tarefa.

A propriedade **Operation** especifica a operação do sistema de arquivos a ser executada. As seguintes operações têm suporte.

* **CopyToADLS:** carregar arquivos para o ADLS.
* **CopyFromADLS:** baixar arquivos do ADLS.

Para qualquer operação, você precisa especificar um gerenciador de conexões do Azure Data Lake.

Aqui estão as descrições das propriedades específicas para cada operação.

## <a name="copytoadls"></a>CopyToADLS
* **LocalDirectory:** Especifica o diretório de origem que contém os arquivos a serem carregados.
* **FileNamePattern:** especifica um filtro de nome de arquivo para arquivos de origem. Somente os arquivos cujo nome corresponde ao padrão especificado serão carregados. Curingas `*` e `?` são compatíveis.
* **SearchRecursively:** especifica se deve-se pesquisar recursivamente dentro do diretório de origem por arquivos a serem carregados.
* **AzureDataLakeDirectory:** especifica o diretório de destino do ADLS para o qual carregar arquivos.
* **FileExpiry:** Especifica uma data de expiração para os arquivos carregados ADLS ou deixam essa propriedade em branco para indicar que os arquivos nunca expirarem.

## <a name="copyfromadls"></a>CopyFromADLS
* **AzureDataLakeDirectory:** especifica o diretório de origem do ADLS que contém os arquivos a serem baixados.
* **SearchRecursively:** especifica se deve-se pesquisar recursivamente dentro do diretório de origem por arquivos a serem baixados.
* **LocalDirectory:** especifica o diretório de destino no qual armazenar arquivos baixados.

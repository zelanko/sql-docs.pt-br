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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66061382"
---
# <a name="azure-data-lake-store-file-system-task"></a>Tarefa do sistema de arquivos do Azure Data Lake Store

O **tarefa de sistema de arquivos do Azure Data Lake Store** permite aos usuários executar várias operações de sistema de arquivos na [Azure Data Lake Store (ADLS)](https://azure.microsoft.com/services/data-lake-store/).

Para adicionar uma tarefa do sistema de arquivos do Azure Data Lake Store para um pacote, arraste-o da Caixa de Ferramentas do SSIS para a tela do designer. Clique duas vezes na tarefa, ou a tarefa com o botão direito e selecione **editar**, para abrir a caixa de diálogo do editor de tarefa.

A propriedade **Operation** especifica a operação do sistema de arquivos a ser executada. As seguintes operações têm suporte.

* **CopyToADLS:** carrega os arquivos para o ADLS.
* **CopyFromADLS:** baixa os arquivos do ADLS.

Para qualquer operação, você precisa especificar um gerenciador de conexões do Azure Data Lake.

Aqui estão as descrições das propriedades específicas para cada operação.

## <a name="copytoadls"></a>CopyToADLS

* **LocalDirectory:** Especifica o diretório de origem que contém os arquivos a serem carregados.
* **FileNamePattern:** especifica um filtro de nome de arquivo para arquivos de origem. Somente os arquivos cujo nome corresponde ao padrão especificado serão carregados. Curingas `*` e `?` são compatíveis.
* **SearchRecursively:** especifica se deve-se pesquisar recursivamente dentro do diretório de origem por arquivos a ser carregados.
* **AzureDataLakeDirectory:** especifica o diretório de destino do ADLS para o qual carregar arquivos.
* **FileExpiry:** Especifica uma data de expiração para os arquivos carregados para o ADLS ou deixe essa propriedade em branco para indicar que os arquivos nunca expiram.

## <a name="copyfromadls"></a>CopyFromADLS

* **AzureDataLakeDirectory:** especifica o diretório de origem do ADLS que contém os arquivos a ser baixados.
* **SearchRecursively:** especifica se deve-se pesquisar recursivamente dentro do diretório de origem por arquivos a ser baixados.
* **LocalDirectory:** especifica o diretório de destino no qual armazenar arquivos baixados.

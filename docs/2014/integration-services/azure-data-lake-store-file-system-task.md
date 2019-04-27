---
title: Tarefa do sistema de arquivos do Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSTASK.F1
- SQL11.DTS.DESIGNER.AFPADLSTASK.F1
ms.assetid: 02b9edd7-6ef9-463e-abbf-e1830bcae875
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: aeabdcfa1fd36adf9bd4291623c56fbfecf0520e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62771872"
---
# <a name="azure-data-lake-store-file-system-task"></a>Tarefa do sistema de arquivos do Azure Data Lake Store

O **tarefa de sistema de arquivos do Azure Data Lake Store** permite aos usuários executar várias operações de sistema de arquivos na [Azure Data Lake Store (ADLS)](https://azure.microsoft.com/services/data-lake-store/).

Para adicionar uma tarefa do sistema de arquivos do Azure Data Lake Store para um pacote, arraste-o da Caixa de Ferramentas do SSIS para a tela do designer. Clique duas vezes na tarefa, ou a tarefa com o botão direito e selecione **editar**, para abrir a caixa de diálogo do editor de tarefa.

A propriedade **Operation** especifica a operação do sistema de arquivos a ser executada. As seguintes operações têm suporte.

* **CopyToADLS:** Carregar arquivos para o ADLS.
* **CopyFromADLS:** Baixe arquivos do ADLS.

Para qualquer operação, você precisa especificar um gerenciador de conexões do Azure Data Lake.

Aqui estão as descrições das propriedades específicas para cada operação.

## <a name="copytoadls"></a>CopyToADLS

* **LocalDirectory:** Especifica o diretório de origem que contém os arquivos a serem carregados.
* **FileNamePattern:** Especifica um filtro de nome de arquivo para arquivos de origem. Somente os arquivos cujo nome corresponde ao padrão especificado serão carregados. Curingas `*` e `?` são compatíveis.
* **SearchRecursively:** Especifica se deve pesquisar recursivamente dentro do diretório de origem por arquivos a serem carregados.
* **AzureDataLakeDirectory:** Especifica o diretório de destino para carregar arquivos para o ADLS.
* **FileExpiry:** Especifica uma data de expiração para os arquivos carregados para o ADLS ou deixe essa propriedade em branco para indicar que os arquivos nunca expiram.

## <a name="copyfromadls"></a>CopyFromADLS

* **AzureDataLakeDirectory:** Especifica o diretório de origem do ADLS que contém os arquivos para baixar.
* **SearchRecursively:** Especifica se deve pesquisar recursivamente dentro do diretório de origem por arquivos a serem baixados.
* **LocalDirectory:** Especifica o diretório de destino para armazenar arquivos baixados.

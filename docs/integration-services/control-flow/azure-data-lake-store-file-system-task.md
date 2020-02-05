---
title: Tarefa do sistema de arquivos do Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: maghan
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSTASK.F1
- SQL14.DTS.DESIGNER.AFPADLSTASK.F1
author: Lingxi-Li
ms.author: lingxl
ms.openlocfilehash: cab5a97beb9f1bfe4d47844e2d0acdb49b28b924
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67947343"
---
# <a name="azure-data-lake-store-file-system-task"></a>Tarefa do sistema de arquivos do Azure Data Lake Store

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



A Tarefa do Sistema de Arquivos do Azure Data Lake Store permite aos usuários executar várias operações de sistema de arquivos no [Azure Data Lake Store (ADLS)](https://azure.microsoft.com/services/data-lake-store/).

A Tarefa de Sistema de Arquivos do Azure Data Lake Store é um componente do [Feature Pack do SSIS (SQL Server Integration Services) para o Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

## <a name="configure-the-azure-data-lake-store-file-system-task"></a>Configurar a tarefa do sistema de arquivos do Azure Data Lake Store

Para adicionar uma tarefa do sistema de arquivos do Azure Data Lake Store para um pacote, arraste-o da Caixa de Ferramentas do SSIS para a tela do designer. Em seguida, clique duas vezes na tarefa ou clique com o botão direito do mouse na tarefa e selecione **Editar** para abrir a caixa de diálogo **Editor de Tarefa do Sistema de Arquivos do Azure Data Lake Store**.

A propriedade **Operation** especifica a operação do sistema de arquivos a ser executada. Selecione uma das operações a seguir:

- **CopyToADLS:** carregar arquivos para o ADLS.
- **CopyFromADLS:** baixar arquivos do ADLS.

## <a name="configure-the-properties-for-the-operation"></a>Configurar as propriedades para a operação
Para qualquer operação, você precisa especificar um gerenciador de conexões do Azure Data Lake.

Aqui estão as propriedades específicas para cada operação:

### <a name="copytoadls"></a>CopyToADLS
- **LocalDirectory:** especifica o diretório de origem local que contém os arquivos a serem carregados.
- **FileNamePattern:** especifica um filtro de nome de arquivo para arquivos de origem. Somente os arquivos cujo nome corresponde ao padrão especificado são carregados. Curingas `*` e `?` são compatíveis.
- **SearchRecursively:** especifica se deve-se pesquisar recursivamente dentro do diretório de origem por arquivos a serem carregados.
- **AzureDataLakeDirectory:** especifica o diretório de destino do ADLS para o qual carregar arquivos.
- **FileExpiry:** especifica uma data de expiração para os arquivos carregados para o ADLS. Deixe essa propriedade em branco para indicar que os arquivos nunca expiram.

### <a name="copyfromadls"></a>CopyFromADLS
- **AzureDataLakeDirectory:** especifica o diretório de origem do ADLS que contém os arquivos a serem baixados.
- **SearchRecursively:** especifica se deve-se pesquisar recursivamente dentro do diretório de origem por arquivos a serem baixados.
- **LocalDirectory:** especifica o diretório de destino no qual armazenar arquivos baixados.

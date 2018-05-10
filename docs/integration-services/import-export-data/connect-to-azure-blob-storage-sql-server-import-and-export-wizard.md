---
title: Conectar-se ao Armazenamento de Blobs do Azure (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: import-export-data
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e2e482b8-5f90-48c5-93fb-b412ed52659f
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 550e8323ef2a8997c72d28c58c4452097ed8ecc0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="connect-to-azure-blob-storage-sql-server-import-and-export-wizard"></a>Conectar-se ao Armazenamento de Blobs do Azure (Assistente de Importação e Exportação do SQL Server)
Este tópico mostra como se conectar a uma fonte de dados do **Armazenamento de Blobs do Azure** (arquivo de texto) por meio da página **Escolher uma Fonte de Dados** ou **Escolher um Destino** do Assistente de Importação e Exportação do SQL Server.

>   [!NOTE]
> Para usar o Destino ou Origem de Blobs do Azure, você precisa instalar o Feature Pack do Azure para SQL Server Integration Services.
> - Para baixar o Feature Pack, veja [Feature Pack do Microsoft SQL Server 2016 Integration Services para o Azure](https://www.microsoft.com/download/details.aspx?id=49492).
>
> - Para obter mais informações, consulte [Feature Pack do Azure para o Integration Services &#40;SSIS&#41;](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

A captura de tela a seguir mostra as opções a configurar para uma conexão ao Armazenamento de Blobs do Azure.

![Conexão do armazenamento de blobs do Azure](../../integration-services/import-export-data/media/azure-blob-storage-connection.png)

## <a name="options-to-specify"></a>Opções a serem especificadas

> [!NOTE]
> As opções de conexão para este provedor de dados serão as mesmas se o Armazenamento de Blobs do Azure for sua origem ou seu destino. Ou seja, as opções exibidas nas páginas **Escolher uma Fonte de Dados** e **Escolher um Destino** do assistente são as mesmas.

 **Usar conta do Azure**  
 Especifique se uma conta online deverá ser usada.
  
 **Nome da conta de armazenamento**  
 Insira o nome da conta de armazenamento do Azure.  
  
**Chave de conta**  
Insira a chave para a conta de armazenamento do Azure.  
  
 **Usar HTTPS**  
 Especifique se deseja usar HTTP ou HTTPS para se conectar à conta de armazenamento.  
  
 **Usar conta de desenvolvedor local**  
 Especifique se deseja usar o emulador de armazenamento no computador local.  
  
 **Nome do contêiner de Blob**  
 Selecione na lista de contêineres de armazenamento disponíveis na conta de armazenamento especificada.  
  
 **Formato de arquivo do Blob**  
 Selecione o formato de arquivo de texto ou Avro.  
  
 **Caractere delimitador de coluna**  
 Se você selecionou o formato Texto, especifique o caractere delimitador de coluna.  
  
 **Use a primeira linha como nomes de colunas**  
 Especifique se a primeira linha de dados contém nomes de coluna.  

## <a name="see-also"></a>Confira também
[Escolher uma Fonte de Dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Escolher um Destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)


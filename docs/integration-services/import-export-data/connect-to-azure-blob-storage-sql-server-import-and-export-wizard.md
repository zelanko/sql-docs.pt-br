---
title: "Conectar ao armazenamento de BLOBs do Azure (SQL Server Assistente de importação e exportação) | Microsoft Docs"
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e2e482b8-5f90-48c5-93fb-b412ed52659f
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 36b992b5141799d4e168b2e990643e6a515a8d69
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="connect-to-azure-blob-storage-sql-server-import-and-export-wizard"></a>Conectar ao armazenamento de BLOBs do Azure (Assistente de exportação e importação do SQL Server)
Este tópico mostra como se conectar a um **armazenamento de BLOBs do Azure** da fonte de dados do **escolher uma fonte de dados** ou **escolha um destino** página do Assistente para exportação e importação do SQL Server.

>   [!NOTE]
> Para usar a fonte de BLOBs do Azure ou o destino, você precisa instalar o Azure Feature Pack para SQL Server Integration Services.
> - Para baixar o pacote de recursos, consulte [Microsoft SQL Server 2016 Integration Services Feature Pack para Azure](https://www.microsoft.com/download/details.aspx?id=49492).
>
> - Para obter mais informações, consulte [Feature Pack do Azure para o Integration Services &#40;SSIS&#41;](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

A captura de tela a seguir mostra as opções para configurar para uma conexão para o armazenamento de BLOBs do Azure.

![Conexão do armazenamento de blobs do Azure](../../integration-services/import-export-data/media/azure-blob-storage-connection.png)

## <a name="options-to-specify"></a>Opções para especificar

> [!NOTE]
> As opções de conexão para este provedor de dados são os mesmos se o armazenamento de BLOBs do Azure é a fonte ou destino. Ou seja, as opções exibidas são os mesmos em ambos os **escolher uma fonte de dados** e o **escolha um destino** páginas do assistente.

 **Usar conta do Azure**  
 Especifique se uma conta online deverá ser usada.
  
 **Nome da conta de armazenamento**  
 Digite o nome da conta de armazenamento do Azure.  
  
**Chave de conta**  
Insira a chave da conta de armazenamento do Azure.  
  
 **Usar HTTPS**  
 Especifique se deseja usar HTTP ou HTTPS para se conectar à conta de armazenamento.  
  
 **Usar conta de desenvolvedor local**  
 Especifique se deseja usar o emulador de armazenamento no computador local.  
  
 **Nome do contêiner de Blob**  
 Selecione na lista de contêineres de armazenamento disponíveis na conta de armazenamento especificada.  
  
 **Formato de arquivo do Blob**  
 Selecione o formato de arquivo de texto ou Avro.  
  
 **Caractere delimitador de coluna**  
 Se você selecionou o formato de texto, digite o caractere delimitador de coluna.  
  
 **Use a primeira linha como nomes de colunas**  
 Especifique se a primeira linha de dados contém nomes de coluna.  

## <a name="see-also"></a>Consulte também
[Escolha uma fonte de dados](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Escolha um destino](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)



---
title: Tarefa de Upload do DW no SQL Azure | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPDWUPTASK.F1
- SQL11.DTS.DESIGNER.AFPDWUPTASK.F1
ms.assetid: 112cf764-f85a-4c1a-b732-d299d717c0d4
caps.latest.revision: 5
author: yualan
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dfdaa7d851e4d29f476e50ddeaacf0fae943c410
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37250529"
---
# <a name="azure-sql-dw-upload-task"></a>Tarefa de Upload do SQL DW do Azure
A **Tarefa de Upload do SQL DW do Azure** permite que um pacote do SSIS carregue dados locais em uma tabela no SQL Data Warehouse (DW) do Azure. O formato de arquivo de dados de origem com suporte atualmente é texto delimitado em codificação UTF8. O processo de carregamento segue a abordagem PolyBase eficiente. Especificamente, os dados serão primeiro carregados no Armazenamento de Blobs do Azure e, em seguida, no SQL DW do Azure. Portanto, é necessário uma conta de Armazenamento de Blobs do Azure para usar essa tarefa.

Para adicionar uma **Tarefa de Upload do SQL DW do Azure**, arraste-a da Caixa de Ferramentas do SSIS e solte-a na tela do designer, e clique duas vezes ou clique com o botão direito do mouse em **Editar** para ver a caixa de diálogo editor da tarefa.

Na página **Geral** , defina as propriedades a seguir.

Campo|Description
-----|-----------
LocalDirectory|Especifica o diretório local que contém os arquivos de dados a serem carregados.
Recursivamente|Especifica se os subdiretórios devem ser pesquisados recursivamente.
FileName|Especifica um filtro de nome para selecionar arquivos com o padrão de nome determinado. Por ex.: MySheet\*.xsl\* incluirá arquivos como MySheet001.xsl e MySheetABC.xslx.
RowDelimiter|Especifica os caracteres que marcam o final de cada linha.
ColumnDelimiter|Especifica um ou mais caracteres que marcam o final de cada coluna. Por ex.: &#124; (barra vertical) \t (tabulação), ' (aspa simples), "(aspas duplas) e 0x5c (barra invertida).
IsFirstRowHeader|Especifica se a primeira linha em cada arquivo de dados contém nomes de coluna em vez de dados reais.
AzureStorageConnection|Especifica um gerenciador de conexões do Armazenamento do Azure.
BlobContainer|Especifica o nome do contêiner de blob no qual os dados locais serão carregados e retransmitidos ao DW do Azure através do PolyBase. Um novo contêiner será criado, caso não exista.
BlobDirectory|Especifica o diretório de blob (estrutura hierárquica virtual) no qual os dados locais serão carregados e retransmitidos ao DW do Azure através do PolyBase.
RetainFiles|Especifica se os arquivos carregados no Armazenamento do Azure serão mantidos.
CompressionType|Especifica o formato de compactação a ser usado ao carregar arquivos no Armazenamento do Azure. A origem local não é afetada.
CompressionLevel|Especifica o nível de compactação a ser usado para o formato de compactação.
AzureDwConnection|Especifica um Gerenciador de conexões ADO.NET para o SQL DW do Azure.
TableName|Especifica o nome da tabela de destino. Escolha um nome de tabela existente ou crie uma nova tabela escolhendo **\<Nova Tabela...>**.
TableDistribution|Especifica o método de distribuição para a nova tabela. Aplica-se caso um novo nome de tabela para **TableName**seja especificado.
HashColumnName|Especifica a coluna usada para a distribuição da tabela de hash. Aplica-se caso **HASH** for especificado para **TableDistribution**.

Você verá uma página **Mapeamentos** diferente caso esteja carregando para uma tabela nova ou para uma tabela existente. No primeiro caso, configure quais colunas de origem serão mapeadas e os nomes correspondentes na tabela de destino a ser criada. No último caso, configure as relações de mapeamento entre colunas de origem e de destino.

Na página **Colunas** , configure as propriedades de tipo de dados para cada coluna de origem.

A página **T-SQL** mostra o T-SQL usado para carregar os dados do Armazenamento de Blobs do Azure para o SQL DW do Azure. O T-SQL é gerado automaticamente de configurações nas outras páginas e será executado como parte da execução da tarefa. Você pode optar por editar manualmente o T-SQL gerado para atender às suas necessidades específicas clicando no botão **Editar** . Depois, você pode reverter para aquele que foi gerado automaticamente, clicando no botão **Redefinir** .

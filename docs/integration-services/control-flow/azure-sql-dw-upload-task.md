---
title: Tarefa de Upload do DW no SQL Azure | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPDWUPTASK.F1
- sql14.dts.designer.afpdwuptask.f1
ms.assetid: eef82c89-228a-4dc7-9bd0-ea00f57692f5
author: Lingxi-Li
ms.author: lingxl
ms.openlocfilehash: 52b4f561f29d78c170b334a4ea97486a30ba41c4
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918892"
---
# <a name="azure-sql-dw-upload-task"></a>Tarefa de Upload do SQL DW do Azure

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]



A **Tarefa de Upload do Azure SQL DW** habilita um pacote do SSIS a copiar dados de tabela para o Azure SQL Data Warehouse (DW) do sistema de arquivos ou do Armazenamento de Blobs do Azure.
A tarefa aproveita o PolyBase para melhorar o desempenho, conforme descrito no artigo [Padrões de carregamento e estratégias do Azure SQL Data Warehouse](https://blogs.msdn.microsoft.com/sqlcat/2017/05/17/azure-sql-data-warehouse-loading-patterns-and-strategies/).
O formato de arquivo de dados de origem com suporte atualmente é texto delimitado em codificação UTF8.
Ao copiar do sistema de arquivos, primeiro os dados serão carregados no Armazenamento de Blobs do Azure para o preparo e, depois, para o Azure SQL DW. Portanto, é necessário uma conta de Armazenamento de Blobs do Azure.

A **Tarefa de Upload de DW SQL do Azure** é um componente do [Feature Pack do SSIS (SQL Server Integration Services) para o Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Para adicionar uma **Tarefa de Upload do SQL DW do Azure**, arraste-a da Caixa de Ferramentas do SSIS e solte-a na tela do designer, e clique duas vezes ou clique com o botão direito do mouse em **Editar** para ver a caixa de diálogo editor da tarefa.

Na página **Geral** , defina as propriedades a seguir.

**SourceType** especifica o tipo de armazenamento de dados de origem. Selecione um dos seguintes tipos:

* **FileSystem:** dados de origem residem no sistema de arquivos local.
* **BlobStorage:** Dados de origem residem no Armazenamento de Blobs do Azure.

A seguir, as propriedades para cada tipo de fonte.

### <a name="filesystem"></a>FileSystem

Campo|DESCRIÇÃO
-----|-----------
LocalDirectory|Especifica o diretório local que contém os arquivos de dados a serem carregados.
Recursivamente|Especifica se os subdiretórios devem ser pesquisados recursivamente.
FileName|Especifica um filtro de nome para selecionar arquivos com o padrão de nome determinado. Por ex.: MySheet*.xsl\* incluirá arquivos como MySheet001.xsl e MySheetABC.xslx.
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
TableName|Especifica o nome da tabela de destino. Escolha o nome de uma tabela existente ou crie uma selecionando **\<New Table ...>** .
TableDistribution|Especifica o método de distribuição para a nova tabela. Aplica-se caso um novo nome de tabela para **TableName**seja especificado.
HashColumnName|Especifica a coluna usada para a distribuição da tabela de hash. Aplica-se caso **HASH** for especificado para **TableDistribution**.

### <a name="blobstorage"></a>BlobStorage

Campo|DESCRIÇÃO
-----|-----------
AzureStorageConnection|Especifica um gerenciador de conexões do Armazenamento do Azure.
BlobContainer|Especifica o nome do contêiner de blob em que os dados de origem residem.
BlobDirectory|Especifica o diretório de blobs (estrutura hierárquica virtual) em que os dados de origem residem.
RowDelimiter|Especifica os caracteres que marcam o final de cada linha.
ColumnDelimiter|Especifica um ou mais caracteres que marcam o final de cada coluna. Por ex.: &#124; (barra vertical) \t (tabulação), ' (aspa simples), "(aspas duplas) e 0x5c (barra invertida).
CompressionType|Especifica o formato de compactação usado para dados de origem.
AzureDwConnection|Especifica um Gerenciador de conexões ADO.NET para o SQL DW do Azure.
TableName|Especifica o nome da tabela de destino. Escolha o nome de uma tabela existente ou crie uma selecionando **\<New Table ...>** .
TableDistribution|Especifica o método de distribuição para a nova tabela. Aplica-se caso um novo nome de tabela para **TableName**seja especificado.
HashColumnName|Especifica a coluna usada para a distribuição da tabela de hash. Aplica-se caso **HASH** for especificado para **TableDistribution**.

Você verá uma página **Mapeamentos** diferente caso esteja copiando para uma tabela nova ou para uma tabela existente.
No primeiro caso, configure quais colunas de origem serão mapeadas e os nomes correspondentes na tabela de destino a ser criada.
No último caso, configure as relações de mapeamento entre colunas de origem e de destino.

Na página **Colunas** , configure as propriedades de tipo de dados para cada coluna de origem.

A página **T-SQL** mostra o T-SQL usado para carregar os dados do Armazenamento de Blobs do Azure para o SQL DW do Azure.
O T-SQL é gerado automaticamente de configurações nas outras páginas e será executado como parte da execução da tarefa.
Você pode optar por editar manualmente o T-SQL gerado para atender às suas necessidades específicas clicando no botão **Editar** .
Depois, você pode reverter para aquele que foi gerado automaticamente, clicando no botão **Redefinir** .

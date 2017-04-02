---
title: "Tarefa de Upload do SQL DW do Azure | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "SQL13.DTS.DESIGNER.AFPDWUPTASK.F1"
  - "sql14.dts.designer.afpdwuptask.f1"
ms.assetid: eef82c89-228a-4dc7-9bd0-ea00f57692f5
caps.latest.revision: 5
author: "Lingxi-Li"
ms.author: "lingxl"
manager: "jhubbard"
caps.handback.revision: 3
---
# Tarefa de Upload do SQL DW do Azure
A **Tarefa de Upload do SQL DW do Azure** permite que um pacote do SSIS carregue dados locais em uma tabela no SQL Data Warehouse (DW) do Azure. O formato de arquivo de dados de origem com suporte atualmente é texto delimitado em codificação UTF8. O processo de carregamento segue a abordagem PolyBase eficiente conforme descrito no artigo [Azure SQL Data Warehouse Loading Patterns and Strategies](https://blogs.msdn.microsoft.com/sqlcat/2016/02/06/azure-sql-data-warehouse-loading-patterns-and-strategies/) (Padrões e estratégias de carregamento do SQL Data Warehouse do Azure). Especificamente, os dados serão primeiro carregados no Armazenamento de Blobs do Azure e, em seguida, no SQL DW do Azure. Portanto, é necessário uma conta de Armazenamento de Blobs do Azure para usar essa tarefa.

A **Tarefa de Upload do SQL DW do Azure** é um componente do SSIS (SQL Server Integration Services) Feature Pack para Azure para SQL Server 2016. Baixe o Feature Pack [daqui](http://go.microsoft.com/fwlink/?LinkID=626967).

Para adicionar uma **Tarefa de Upload do SQL DW do Azure**, arraste-a da Caixa de Ferramentas do SSIS e solte-a na tela do designer, e clique duas vezes ou clique com o botão direito do mouse em **Editar** para ver a caixa de diálogo editor da tarefa.

Na página **Geral**, defina as propriedades a seguir.

Campo|Description
-----|-----------
LocalDirectory|Especifica o diretório local que contém os arquivos de dados a serem carregados.
Recursivamente|Especifica se os subdiretórios devem ser pesquisados recursivamente.
FileName|Especifica um filtro de nome para selecionar arquivos com o padrão de nome determinado. Por ex.: MySheet*.xsl\* incluirá arquivos como MySheet001.xsl e MySheetABC.xslx.
RowDelimiter|Especifica os caracteres que marcam o final de cada linha.
ColumnDelimiter|Especifica um ou mais caracteres que marcam o final de cada coluna. Por ex.: &#124; para a barra vertical, \t para tabulação e &#124;\t para uma sequência de barra vertical e tabulação.
IsFirstRowHeader|Especifica se a primeira linha em cada arquivo de dados contém nomes de coluna em vez de dados reais.
AzureStorageConnection|Especifica um gerenciador de conexões do Armazenamento do Azure.
BlobContainer|Especifica o nome do contêiner de blob no qual os dados locais serão carregados e retransmitidos ao DW do Azure através do PolyBase. Um novo contêiner será criado, caso não exista.
BlobDirectory|Especifica o diretório de blob (estrutura hierárquica virtual) no qual os dados locais serão carregados e retransmitidos ao DW do Azure através do PolyBase.
RetainFiles|Especifica se os arquivos carregados no Armazenamento do Azure serão mantidos.
CompressionType|Especifica o formato de compactação a ser usado ao carregar arquivos no Armazenamento do Azure. A origem local não é afetada.
CompressionLevel|Especifica o nível de compactação a ser usado para o formato de compactação.
AzureDwConnection|Especifica um Gerenciador de conexões ADO.NET para o SQL DW do Azure.
TableName|Especifica o nome da tabela de destino. Escolha um nome de tabela existente, ou crie uma nova tabela escolhendo **\<Nova Tabela...>**.
TableDistribution|Especifica o método de distribuição para a nova tabela. Aplica-se caso um novo nome de tabela para **TableName** seja especificado.
HashColumnName|Especifica a coluna usada para a distribuição da tabela de hash. Aplica-se caso **HASH** for especificado para **TableDistribution**.

Você verá uma página **Mapeamentos** diferente caso esteja carregando para uma tabela nova ou para uma tabela existente. No primeiro caso, configure quais colunas de origem serão mapeadas e os nomes correspondentes na tabela de destino a ser criada. No último caso, configure as relações de mapeamento entre colunas de origem e de destino.

Na página **Colunas**, configure as propriedades de tipo de dados para cada coluna de origem.

A página **T-SQL** mostra o T-SQL usado para carregar os dados do Armazenamento de Blobs do Azure para o SQL DW do Azure. O T-SQL é gerado automaticamente de configurações nas outras páginas e será executado como parte da execução da tarefa. Você pode optar por editar manualmente o T-SQL gerado para atender às suas necessidades específicas clicando no botão **Editar**. Depois, você pode reverter para aquele que foi gerado automaticamente, clicando no botão **Redefinir**.

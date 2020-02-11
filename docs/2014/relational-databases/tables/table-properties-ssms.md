---
title: Propriedades da tabela | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql12.swb.tableproperties.storage.f1
- sql12.SWB.SELECTCOLUMNS.F1
- sql12.swb.tableproperties.filetable.f1
- sql12.swb.tableproperties.general.f1
- sql12.swb.tableproperties.changetracking.f1
ms.assetid: ad8a2fd4-f092-4c0f-be85-54ce8b9d725a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b07f157294700b3b3b7958ce4cdc6f1589bff864
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68196716"
---
# <a name="table-properties"></a>Propriedades da tabela
  Este tópico descreve as propriedades de tabela que são exibidas na caixa de diálogo Propriedades da Tabela no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações sobre como exibir essas propriedades, veja [Exibir a definição da tabela](view-the-table-definition.md).  
  
 **Neste tópico**  
  
1.  [Página Geral](#GeneralPage)  
  
2.  [Página Controle de Alterações](#ChangeTracking)  
  
3.  [Página Tabela de Arquivos](#FileTable)  
  
4.  [Página Armazenamento](#Storage)  
  
##  <a name="GeneralPage"></a> Página Geral  
 **Backup de banco de dados**  
 O nome do banco de dados que contém esta tabela.  
  
 **Servidor**  
 O nome da instância do servidor atual.  
  
 **Usuário**  
 Nome do usuário desta conexão.  
  
 **Data da Criação**  
 A data e a hora em que a tabela foi criada.  
  
 **Nome**  
 O nome da tabela.  
  
 **Esquema**  
 O esquema que possui a tabela.  
  
 **Objeto do sistema**  
 Indica que esta é uma tabela do sistema, usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conter informações internas. Os usuários não devem alterar ou fazer referência diretamente a tabelas do sistema.  
  
 **ANSI NULLs**  
 Indica se o objeto foi criado com a opção ANSI NULLs definida como ON. Para obter mais informações, veja [SET ANSI_NULLS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql)  
  
 **Identificador entre aspas**  
 Indica se o objeto foi criado com a opção de identificador entre aspas definida como ON. Para obter mais informações, veja [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql)  
  
 **Escalonamento de Bloqueios**  
 Indica a granularidade do escalonamento de bloqueios da tabela. Para obter mais informações sobre bloqueio no Mecanismo de Banco de Dados, consulte [Bloqueio de transação do SQL Server e guia de controle de versão de linha](https://msdn.microsoft.com/library/jj856598.aspx). Os valores possíveis são:  
  
 AUTO  
 Essa opção permite que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] selecione a granularidade do escalonamento de bloqueios apropriado ao esquema da tabela.  
  
-   Se a tabela estiver particionada, o escalonamento de bloqueios será permitido para a granularidade HoBT (pilha ou árvore B). Depois de ser escalonado para o nível de HoBT, o bloqueio não será escalonado posteriormente para a granularidade TABLE.  
  
-   Se a tabela não estiver particionada, o escalonamento de bloqueios será feito para a granularidade TABLE.  
  
 TABLE  
 O escalonamento de bloqueios será feito na granularidade em nível de tabela independentemente de a tabela estar particionada ou não. TABLE é o valor padrão.  
  
 DISABLE  
 Impede o escalonamento de bloqueios na maioria dos casos. Os bloqueios em nível de tabela não são totalmente desautorizados. Por exemplo, quando você está verificando uma tabela que não tem nenhum índice clusterizado no nível de isolamento serializável, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve usar um bloqueio de tabela para proteger a integridade dos dados.  
  
 **A tabela é replicada**  
 Indica quando a tabela é replicada em outro banco de dados usando a replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os valores possíveis são `True` ou `False`.  
  
##  <a name="ChangeTracking"></a>Página de Controle de Alterações  
 **Controle de alterações**  
 Indica se o controle de alterações está habilitado para a tabela. O valor padrão é `False`.  
  
 Essa opção só estará disponível quando o controle de alterações estiver habilitado para o banco de dados.  
  
 Para habilitar o controle de alterações, a tabela deve ter uma chave primária e é necessário ter permissão para alterar a tabela. Você também pode configurar o controle de alterações usando [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql).  
  
 **Rastrear colunas atualizadas**  
 Indica se o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] rastreia as colunas que foram atualizadas.  
  
 Para obter mais informações sobre o controle de alterações, veja [Sobre o controle de alterações &#40;SQL Server&#41;](../track-changes/about-change-tracking-sql-server.md).  
  
##  <a name="FileTable"></a>Página filetable  
 Exibe as propriedades da tabela relacionada a FileTables. Para obter mais informações, veja [FileTables &#40;SQL Server&#41;](../blob/filetables-sql-server.md).  
  
 **Ordenação da colunas de nome FileTable**  
 A ordenação aplicada à coluna **Name** em uma FileTable. A coluna **Name** contém nomes de arquivos e diretórios.  
  
 **Nome do diretório filetable**  
 A pasta raiz da FileTable.  
  
 **Namespace filetable habilitado**  
 Quando `True`, este valor indica que a tabela é uma FileTable. Se você alterar esse valor para `False`, estará alterando a FileTable para uma tabela de usuário comum. Se você desejar reverter novamente a tabela para FileTable, ela precisará passar em uma verificação de consistência da FileTable para que a conversão seja bem-sucedida.  
  
##  <a name="Storage"></a>Página armazenamento  
 Exibe as propriedades relacionadas ao armazenamento da tabela selecionada.  
  
### <a name="compression"></a>Compactação  
 **Tipo de compactação**  
 O tipo de compactação da tabela. Essa propriedade está disponível somente para tabelas que não são particionadas. Para saber mais, veja [Data Compression](../data-compression/data-compression.md).  
  
 **Partições que usam compactação de página**  
 Os números de partição que estão usando compactação de página. Essa propriedade está disponível somente para tabelas particionadas.  
  
 **Partições não compactadas**  
 Os números das partições que não são compactadas. Essa propriedade está disponível somente para tabelas particionadas.  
  
 **Partições que usam compactação de linha**  
 Os números das partições que estão usando compactação de linha. Essa propriedade está disponível somente para tabelas particionadas.  
  
### <a name="filegroup"></a>Grupo de arquivos  
 **Grupo de arquivos de texto**  
 O nome do grupo de arquivos que contém os dados de texto para a tabela.  
  
 **Arquivos**  
 O nome do grupo de arquivos que contém a tabela.  
  
 **A tabela está particionada**  
 Os valores possíveis são `True` e `False`.  
  
 **Grupo de arquivos FILESTREAM**  
 Especifique o nome do grupo de arquivos de dados FILESTREAM se a tabela tiver uma coluna `varbinary(max)` com um atributo FILESTREAM. O valor padrão é o grupo de arquivos de dados padrão FILESTREAM.  
  
 Se a tabela não contiver dados FILESTREAM, o campo ficará em branco.  
  
### <a name="general"></a>Geral  
 **O formato de armazenamento vardecimal está habilitado**  
 Quando `True`, esse valor somente leitura indica que `decimal` os tipos `numeric` de dados e são armazenados usando o formato de armazenamento vardecimal. Para alterar essa opção, use a `vardecimal storage format` opção de [sp_tableoption](/sql/relational-databases/system-stored-procedures/sp-tableoption-transact-sql). O formato de armazenamento vardecimal foi preterido. Em vez disso, use compactação ROW.  
  
 **Espaço de índice**  
 A quantidade de espaço em megabytes que os índices ocupam na tabela. Este valor não inclui o uso do espaço de índice XML para a tabela. Se os índices XML pertencerem à tabela, use [sp_spaceused](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql) .  
  
 **Contagem de linhas**  
 O número de linhas da tabela.  
  
 **Espaço de dados**  
 A quantidade de espaço em megabytes que os dados ocupam na tabela.  
  
### <a name="partitioning"></a>Particionamento  
 Esta seção estará disponível somente se a tabela estiver particionada. Para saber mais, confira [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md).  
  
 **Coluna de partição**  
 O nome da coluna na qual a tabela é particionada.  
  
 **Esquema de partição**  
 Nome do esquema de partição se a tabela estiver particionada. Se a tabela não for particionada, o campo fica em branco.  
  
 **Número of partições**  
 O número de partições da tabela.  
  
 **Esquema de partição FILESTREAM**  
 O nome do esquema de partição FILESTREAM se a tabela estiver particionada. Se a tabela não for particionada, o campo fica em branco.  
  
 O esquema de partição FILESTREAM deve ser simétrico em relação ao esquema especificado na opção **Esquema de partição** .  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir a definição da tabela](view-the-table-definition.md)   
 [Modificar colunas &#40;Mecanismo de Banco de Dados&#41;](../tables/modify-columns-database-engine.md)  
  
  

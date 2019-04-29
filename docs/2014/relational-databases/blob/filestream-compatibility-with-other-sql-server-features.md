---
title: Compatibilidade do FILESTREAM com outros recursos do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], other SQL Server features and
- FILESTREAM [SQL Server], limitations
ms.assetid: d2c145dc-d49a-4f5b-91e6-89a2b0adb4f3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 623b0139d70cec0574aaf9b68e37a1ad6f4f9eaf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874986"
---
# <a name="filestream-compatibility-with-other-sql-server-features"></a>Compatibilidade do FILESTREAM com outros recursos do SQL Server
  Como dados FILESTREAM estão no sistema de arquivos, este tópico fornece algumas considerações, diretrizes e limitações para o uso de FILESTREAM com os seguintes recursos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [SQL Server Integration Services (SSIS)](#ssis)  
  
-   [Consultas distribuídas e servidores vinculados](#distqueries)  
  
-   [Criptografia](#encryption)  
  
-   [Instantâneos do banco de dados](#DatabaseSnapshot)  
  
-   [Replicação](#Replication)  
  
-   [Envio de log](#LogShipping)  
  
-   [Espelhamento de Banco de Dados](#DatabaseMirroring)  
  
-   [Indexação de texto completo](#FullText)  
  
-   [Clustering de failover](#FailoverClustering)  
  
-   [SQL Server Express](#SQLServerExpress)  
  
-   [Bancos de dados independentes](#contained)  
  
##  <a name="ssis"></a> SQL Server Integration Services (SSIS)  
 O SQL Server Integration Services (SSIS) trata os dados FILESTREAM no fluxo de dados como quaisquer outros dados BLOB usando o tipo de dados DT_IMAGE SSIS.  
  
 Você pode usar a transformação Importar Coluna para carregar arquivos do sistema de arquivos em uma coluna FILESTREAM. Você também pode usar a transformação Exportar Coluna para extrair arquivos de uma coluna FILESTREAM para outro local do sistema de arquivos.  
  
##  <a name="distqueries"></a> Consultas distribuídas e servidores vinculados  
 Você pode trabalhar com dados FILESTREAM em consultas distribuídas e servidores vinculados, tratando-os `varbinary(max)` dados. Não é possível usar a função **PathName()** de FILESTREAM em consultas distribuídas que usam um nome de quatro partes, mesmo quando o nome referencia o servidor local. Entretanto, você pode usar **PathName()** na consulta interna de uma consulta passagem que usa **OPENQUERY()**.  
  
##  <a name="encryption"></a> Criptografia  
 Os dados de FILESTREAM não são criptografados mesmo quando a criptografia transparente de dados está habilitada.  
  
##  <a name="DatabaseSnapshot"></a> Instantâneos do banco de dados  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte a [database snapshots](../databases/database-snapshots-sql-server.md) para grupos de arquivos FILESTREAM. Se um grupo de arquivos FILESTREAM for incluído em uma cláusula CREATE DATABASE ON, a instrução falhará e um erro será gerado.  
  
 Ao usar FILESTREAM, você pode criar instantâneos do banco de dados de grupos de arquivos padrão (não FILESTREAM). Os grupos de arquivos FILESTREAM são marcados como offline para esses instantâneos do bancos de dados.  
  
 Uma instrução SELECT executada em uma tabela FILESTREAM em um instantâneo do banco de dados não deve incluir uma coluna FILESTREAM. Caso contrário, a mensagem de erro a seguir será retornada:  
  
 `Could not continue scan with NOLOCK due to data movement.`  
  
##  <a name="Replication"></a> Replication  
 Uma coluna `varbinary(max)` que tenha o atributo FILESTREAM ativado no Publicador pode ser replicada para um Assinante com ou sem o atributo FILESTREAM. Para especificar o modo de replicação da coluna, use a caixa de diálogo **Propriedades do Artigo – \<Artigo>** ou o parâmetro @schema_option de [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) ou [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Dados replicados para uma coluna `varbinary(max)` que não tenham o atributo FILESTREAM não devem exceder o limite de 2 GB daquele tipo de dados. Caso contrário, um erro em tempo de execução será gerado. Recomendamos que você replicar o atributo FILESTREAM, a menos que você esteja replicando dados para [!INCLUDE[ssVersion2005](../../includes/ssversion2000-md.md)] assinantes não é suportada, independentemente da opção de esquema especificado.  
  
> [!NOTE]  
>  A replicação de valores de dados grandes do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para Assinantes do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] é limitada a um máximo de 256 MB de valores de dados. Para obter mais informações, consulte [Especificações de capacidade máxima](https://go.microsoft.com/fwlink/?LinkId=103810).  
  
### <a name="considerations-for-transactional-replication"></a>Considerações sobre replicação transacional  
 Se você usar colunas FILESTREAM em tabelas que são publicadas para replicação transacional, observe as seguintes considerações:  
  
-   Se alguma tabela incluir colunas que tenham o atributo FILESTREAM, não será possível usar valores *database snapshot* ou *database snapshot character* para a propriedade @sync_method de [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql).  
  
-   A opção max text repl size especifica a quantidade máxima de dados que podem ser inseridos em uma coluna publicada para replicação. Essa opção pode ser usada para controlar o tamanho de dados FILESTREAM que são replicados.  
  
-   Se você especificar a opção de esquema para replicar o atributo FILESTREAM, mas filtrar a coluna `uniqueidentifier` requerida pelo FILESTREAM ou se especificar não replicar a restrição UNIQUE da coluna, a replicação não replicará o atributo FILESTREAM. A coluna é replicada apenas como uma coluna `varbinary(max)`.  
  
### <a name="considerations-for-merge-replication"></a>Considerações sobre replicação de mesclagem  
 Se você usar colunas FILESTREAM em tabelas que são publicadas para replicação de mesclagem, observe as seguintes considerações:  
  
-   A replicação de mesclagem e o FILESTREAM exigem uma coluna de tipo de dados `uniqueidentifier` para identificar cada linha em uma tabela. A replicação de mesclagem adicionará uma coluna automaticamente se a tabela não tiver uma. A replicação de mesclagem requer que a coluna tenha a propriedade ROWGUIDCOL definida e um padrão de NEWID() ou de NEWSEQUENTIALID(). Além desses requisitos, o FILESTREAM requer que uma restrição UNIQUE seja definida para a coluna. Esses requisitos têm as seguintes consequências:  
  
    -   Se você adicionar uma coluna FILESTREAM a uma tabela já publicada para replicação de mesclagem, verifique se a coluna `uniqueidentifier` tem uma restrição UNIQUE. Se ela não tiver uma restrição UNIQUE, adicione uma restrição nomeada à tabela no banco de dados de publicação. Por padrão, a replicação de mesclagem publicará essa alteração de esquema e ela será aplicada a cada banco de dados de assinatura.  
  
         Se você adicionar uma restrição UNIQUE manualmente conforme descrito e desejar remover a replicação de mesclagem, deverá primeiro remover a restrição UNIQUE. Caso contrário, haverá falha na remoção da replicação.  
  
    -   Por padrão, a replicação de mesclagem usa NEWSEQUENTIALID() porque ele pode fornecer desempenho melhor que NEWID (). Se você adicionar uma coluna `uniqueidentifier` a uma tabela que será publicada para replicação de mesclagem, especifique NEWSEQUENTIALID() como o padrão.  
  
-   A replicação de mesclagem inclui uma otimização para replicar tipos de objetos grandes. Essa otimização é controlada pelo parâmetro @stream_blob_columns de [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Se você definir a opção de esquema para replicar o atributo FILESTREAM, o parâmetro @stream_blob_columns será definido como `true`. Essa otimização pode ser substituída com [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Esse procedimento armazenado permite que você defina @stream_blob_columns como `false`. Se você adicionar uma coluna FILESTREAM a uma tabela já publicada para replicação de mesclagem, recomendamos definir a opção como `true` usando sp_changemergearticle.  
  
-   A habilitação da opção de esquema para FILESTREAM após a criação de um artigo poderá provocar falha na replicação, se os dados em uma coluna FILESTREAM excederem 2 GB e houver um conflito durante a replicação. Se essa situação for esperada, é recomendável descartar e recriar o artigo de tabela com a opção de esquema FILESTREAM adequada habilitada na hora da criação.  
  
-   A replicação de mesclagem pode sincronizar dados FILESTREAM sobre uma conexão HTTPS usando [Sincronização da Web](../replication/merge/merge-replication.md). Esses dados não podem exceder o limite de 50 MB para Sincronização da Web. Caso contrário, um erro de tempo de execução será gerado.  
  
##  <a name="LogShipping"></a> Envio de log  
 O[Envio de log](../../database-engine/log-shipping/about-log-shipping-sql-server.md) oferece suporte a FILESTREAM. Os servidores primário e secundário devem estar executando o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]ou uma versão posterior e ter o FILESTREAM habilitado.  
  
##  <a name="DatabaseMirroring"></a> Espelhamento de Banco de Dados  
 O espelhamento de banco de dados não oferece suporte a FILESTREAM. Um grupo de arquivos FILESTREAM não pode ser criado no servidor principal. O espelhamento de banco de dados não pode ser configurado para um banco de dados que contenha grupos de arquivos FILESTREAM.  
  
##  <a name="FullText"></a> Indexação de texto completo  
 [Indexação de texto completo](../indexes/indexes.md) funciona com uma coluna FILESTREAM da mesma maneira que faz com um `varbinary(max)` coluna. A tabela FILESTREAM deve ter uma coluna que contenha a extensão do nome do arquivo para cada BLOB FILESTREAM. Para obter mais informações, veja [Consultar com a pesquisa de texto completo](../search/query-with-full-text-search.md), [Configurar e gerenciar filtros para pesquisa](../search/configure-and-manage-filters-for-search.md), e [sys.fulltext_document_types &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql).  
  
 O mecanismo de texto completo indexa o conteúdo dos BLOBs FILESTREAM. Arquivos de indexação como imagens podem não ser úteis. Quando um BLOB FILESTREAM é atualizado, ele é reindexado.  
  
##  <a name="FailoverClustering"></a> Clustering de failover  
 Para clustering de failover, os grupos de arquivos FILESTREAM devem ser colocados em um disco compartilhado. O FILESTREAM deve ser habilitado em cada nó do cluster que hospedará a instância FILESTREAM. Para obter mais informações, veja [Configurar o FILESTREAM em um cluster de failover](set-up-filestream-on-a-failover-cluster.md).  
  
##  <a name="SQLServerExpress"></a> SQL Server Express  
 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] oferece suporte a FILESTREAM. O limite de tamanho do banco de dados do 10 GB não inclui o contêiner de dados FILESTREAM.  
  
##  <a name="contained"></a> Bancos de dados independentes  
 O recurso FILESTREAM exige alguma configuração fora do banco de dados. Portanto, um banco de dados que usa FILESTREAM ou FileTable não é contido completamente.  
  
 Você poderá definir a retenção de banco de dados como PARTIAL se desejar usar determinados recursos de bancos de dados contidos, como usuários contidos. Neste caso, no entanto, você deve estar atento que algumas das configurações de banco de dados não estão contidas no banco de dados e não são movidos automaticamente quando o banco de dados é movido.  
  
## <a name="see-also"></a>Consulte também  
 [Objeto binário grande &#40;Blob&#41; Dados &#40;SQL Server&#41;](binary-large-object-blob-data-sql-server.md)  
  
  

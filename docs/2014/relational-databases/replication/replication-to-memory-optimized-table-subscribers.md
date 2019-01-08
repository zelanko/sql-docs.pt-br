---
title: Replicação para assinantes de tabela com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
ms.assetid: 1a8e6bc7-433e-471d-b646-092dc80a2d1a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d2409c993aad299551dcaf97e11c99fe032a96f1
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52800658"
---
# <a name="replication-to-memory-optimized-table-subscribers"></a>Replicação para assinantes de tabela com otimização de memória
  As tabelas que atuam como assinantes de replicação transacional, com exceção da replicação transacional ponto a ponto, podem ser configuradas como tabelas com otimização de memória. Outras configurações de replicação não são compatíveis com tabelas com otimização de memória.  
  
## <a name="configuring-a-memory-optimized-table-as-a-subscriber"></a>Configurando uma tabela com otimização de memória como um assinante  
 Para configurar uma tabela com otimização de memória como um assinante, execute as etapas a seguir.  
  
 **Criar e habilitar a publicação**  
  
1.  Crie uma publicação.  
  
2.  Adicione artigos à publicação. Para o parâmetro `@upd_cmd`, use a convenção SCALL ou SQL.  
  
    ```  
    EXEC sp_addarticle  
        @publication = N'Publication1',  
        @article = N'Mem_Table',  
        @source_owner = N'dbo',  
        @source_object = N'Mem_Table',  
        @type = N'logbased',  
        @description = null,  
        @creation_script = null,  
        @pre_creation_cmd = N'none',  
        @schema_option = 0x00000000080050DF,  
        @identityrangemanagementoption = N'manual',  
        @destination_table = N'Mem_Table',  
        @destination_owner = N'dbo',  
        @vertical_partition = N'false',  
        @ins_cmd = N'CALL sp_MSins_Mem_Table',  
        @del_cmd = N'CALL sp_MSdel_Mem_Table',  
        @upd_cmd = N'SCALL sp_MSupd_Mem_Table';  
    GO  
    ```  
  
 **Gerar um instantâneo e ajustar o esquema**  
  
1.  Crie um trabalho de instantâneo e gere um instantâneo.  
  
    ```  
    EXEC sp_addpublication_snapshot @publication = N'Publication1', @frequency_type = 1;  
    EXEC sp_startpublication_snapshot @publication = N'Publication1';  
    ```  
  
2.  Navegue para a pasta do instantâneo. O local padrão é "C:\Program Files\Microsoft SQL Server\MSSQL12. \<Instância > \MSSQL\repldata\unc\XXX\YYYYMMDDHHMMSS\\".  
  
3.  Localize o **. SCH** para sua tabela de arquivo e abri-lo no Management Studio. Altere o esquema da tabela e atualize o procedimento armazenado conforme descrito abaixo.  
  
     Avalie os índices definidos no arquivo IDX. Modifique `CREATE TABLE` para especificar os índices necessários, as restrições, a chave primária e a sintaxe com otimização de memória. Para tabelas com otimização de memória, as colunas de índice devem ser NOT NULL e as colunas de índice de tipos de caractere devem ser Unicode e usar a ordenação BIN2. Veja o seguinte exemplo:  
  
    ```  
    SET ANSI_PADDING ON;  
    GO  
  
    SET ANSI_NULLS ON;  
    GO  
  
    SET QUOTED_IDENTIFIER ON;  
    GO  
  
    CREATE TABLE [dbo].[Mem_Table]([c1] [int] NOT NULL,  
        [c2] [float] NOT NULL,  
        [c3] [decimal](10, 2) NOT NULL,  
        [c4] [nvarchar](5) COLLATE SQL_Latin1_General_CP850_BIN2 NOT NULL,  
        INDEX [hash_index_sample_memoryoptimizedtable_c2] HASH (c2) WITH (BUCKET_COUNT = 1024),  
        INDEX [index_sample_memoryoptimizedtable_c3] NONCLUSTERED ([c3]),  
        INDEX [nvarchar_index_sample_memoryoptimizedtable_c4] ([c4]),  
        CONSTRAINT [PK_sample_memoryoptimizedtable] PRIMARY KEY NONCLUSTERED ([c1])) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA);  
    GO  
    ```  
  
4.  Ao usar a convenção SCALL para o parâmetro `@upd_cmd`, acesse o arquivo de esquema (.SCH) e altere a instrução de atualização de tabela em `create procedure [sp_MSupd_<SCHEMA><TABLE_NAME>]` para remover as colunas de chave primária.  
  
     Para oferecer suporte a atualizações de chave primária, use um procedimento armazenado de atualização personalizada para substituir a instrução de atualização de chave primária, da seguinte forma:  
  
    1.  Selecione valores de coluna ausentes (SCALL fornece apenas a coluna envolvida na operação de atualização).  
  
    2.  Exclua o registro existente.  
  
    3.  Insira um novo registro com os novos valores fornecidos incluindo a nova chave primária.  
  
     O procedimento de atualização original tem a seguinte aparência:  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                   @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    update [dbo].[Mem_Table] set  
                   [c1] = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
     Se a chave primária nunca deve ser atualizada em um publicador. Comente a partir da atualização dessas colunas no procedimento de atualização da seguinte maneira:  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                   @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    update [dbo].[Mem_Table] set  
    --             [c1] = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
     Para permitir o suporte a atualizações para a chave primária, modifique o procedimento de atualização para ser da seguinte maneira  
  
    ```  
    create procedure [sp_MSupd_Mem_Table]  
                   @c1 int = NULL,  
                   @c2 float = NULL,  
                   @c3 decimal(10,2) = NULL,  
                   @c4 nvarchar(5) = NULL,  
                    @pkc1 int = NULL,  
                   @bitmap binary(1)  
    as  
    begin    
    if (substring(@bitmap,1,1) & 1 = 1)  
    begin   
    select  
                   @c1 = case substring(@bitmap,1,1) & 1 when 1 then @c1 else [c1] end,  
                   @c2 = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   @c3 = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   @c4 = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    from [dbo].[Mem_Table] where [c1] = @pkc1  
    if @@rowcount <> 0 begin  
            delete [dbo].[Mem_Table] where [c1] = @pkc1  
            if @@rowcount <> 0  
                   insert into [dbo].[Mem_Table]([c1],  
                           [c2],  
                           [c3],  
                           [c4]) values (  
                           @c1,  
                           @c2,  
                           @c3,  
                           @c4  
                   )   
    end  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end    
    else  
    begin   
    update [dbo].[Mem_Table] set  
                   [c2] = case substring(@bitmap,1,1) & 2 when 2 then @c2 else [c2] end,  
                   [c3] = case substring(@bitmap,1,1) & 4 when 4 then @c3 else [c3] end,  
                   [c4] = case substring(@bitmap,1,1) & 8 when 8 then @c4 else [c4] end  
    where [c1] = @pkc1  
    if @@rowcount = 0  
        if @@microsoftversion>0x07320000  
            exec sp_MSreplraiserror 20598  
    end   
    end   
    go  
    ```  
  
5.  Criar banco de dados do assinante usando o **elevar para isolamento de instantâneo** opção e defina o agrupamento padrão como Latin1_General_CS_AS_KS_WS no caso de usando tipos de dados de caractere não Unicode.  
  
    ```  
    CREATE DATABASE [Sub]   
    CONTAINMENT = NONE   
    ON PRIMARY ( NAME = [Sub], FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub.mdf]),   
    FILEGROUP [mem] CONTAINS MEMORY_OPTIMIZED_DATA ( NAME = [mem],   
    FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub])  
    LOG ON ( NAME = [Sub_log], FILENAME = [C:\Program Files\Microsoft SQL Server\MSSQL12\MSSQL\DATA\Sub.ldf])  
    COLLATE Latin1_General_CS_AS_KS_WS;  
  
    ALTER DATABASE [Sub] SET MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT = ON;  
    GO  
    ```  
  
6.  Aplicar o esquema de banco de dados do assinante e salve o esquema para uso futuro.  
  
7.  Carregue os dados do publicador (origem) para o assinante. Os dados não devem ser alterados no publicador até que você adicione uma assinatura.  Você pode usar BCP conforme mostrado abaixo:  
  
    ```  
    bcp Pub.dbo.Mem_Table out Mem_Table.bcp -S. -T -C1252 -n  
    bcp Sub.dbo.Mem_Table in Mem_Table.bcp -S. -T -C1252 -n  
    ```  
  
8.  Reconfigure o artigo para desabilitar alterações de esquema no assinante:  
  
    ```  
    EXEC sp_changearticle  
        @publication = N'Publication1',  
        @article = N'Mem_Table',  
        @property = N'schema_option',  
        @value = 0,  
        @force_invalidate_snapshot = 1,  
        @force_reinit_subscription = 1;  
    GO  
    ```  
  
 **Adicionar assinatura sem sincronização**  
  
 Adicione uma assinatura sem sincronização.  
  
```  
EXEC sp_addsubscription  
    @publication = N' Publication1',  
    @subscriber = @@ServerName,  
    @destination_db = N'Sub',  
    @subscription_type = N'Push',  
    @sync_type = N'replication support only',  
    @article = N'all',  
    @update_mode = N'read only',  
    @subscriber_type = 0;  
GO  
```  
  
 As tabelas com otimização de memória agora devem começar a receber atualizações do publicador.  
  
## <a name="restrictions"></a>Restrictions  
 Somente há suporte para a replicação transacional unidirecional. Não há suporte para a replicação transacional ponto a ponto.  
  
 Não é possível publicar as tabelas com otimização de memória.  
  
 As tabelas de replicação no distribuidor não podem ser configuradas como tabelas com otimização de memória.  
  
 A replicação de mesclagem não pode incluir tabelas com otimização de memória.  
  
 No assinante, as tabelas envolvidas na replicação transacional podem ser configuradas como tabelas com otimização de memória, mas as tabelas do assinante devem atender aos requisitos de tabelas com otimização de memória. Isso requer as restrições a seguir.  
  
-   Para criar uma tabela com otimização de memória em um assinante de replicação transacional, os arquivos de esquema do instantâneo usados para criar as tabelas com otimização de memória deverão ser modificados manualmente. Para obter mais informações, consulte [modificando um arquivo de esquema](#Schema).  
  
-   As tabelas replicadas nas tabelas com otimização de memória em um assinante estão limitadas a 8060 bytes por limite de linha de tabelas com otimização de memória.  
  
-   As tabelas replicadas nas tabelas com otimização de memória em um assinante estão limitadas a tipos de dados permitidos em tabelas com otimização de memória. Para obter mais informações, consulte [suporte para tipos de dados](../in-memory-oltp/supported-data-types-for-in-memory-oltp.md).  
  
-   Há restrições na atualização da chave primária das tabelas que estão sendo replicadas para uma tabela com otimização de memória em um assinante. Para obter mais informações, consulte [replicando alterações para uma chave primária](#PrimaryKey).  
  
-   A chave estrangeira, a restrição exclusiva, os disparadores, as modificações de esquema, ROWGUIDCOL, as colunas computadas, a compactação de dados, os tipos de dados de alias, o controle de versões e os bloqueios não têm suporte em tabelas com otimização de memória. Consulte [Transact-SQL Constructs Not Supported by In-Memory OLTP](../in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md) para obter informações.  
  
##  <a name="Schema"></a> Modificando um arquivo de esquema  
  
-   Índices clusterizados não têm suporte. Altere todos os índices clusterizados para índices não clusterizados.  
  
-   Todas as colunas na chave de um índice devem ser especificadas como `NOT NULL`.  
  
-   Se você estiver usando a opção de tabela com otimização de memória `DURABILITY = SCHEMA_AND_DATA` , a tabela deverá ter um índice de chave primária não clusterizado.  
  
-   ANSI_PADDING deve ser ON.  
  
##  <a name="PrimaryKey"></a> Replicando alterações para uma chave primária  
 A chave primária de uma tabela com otimização de memória não pode ser atualizada. Para replicar uma atualização de chave primária em um assinante, modifique o procedimento armazenado de atualização para fornecer a atualização como um par de inserção e exclusão.  
  
## <a name="see-also"></a>Consulte também  
 [Recursos e tarefas de replicação](replication-features-and-tasks.md)  
  
  

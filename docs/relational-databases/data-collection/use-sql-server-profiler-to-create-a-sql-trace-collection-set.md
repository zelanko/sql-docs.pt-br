---
title: Criar um conjunto de coleta do Rastreamento do SQL com o Profiler
ms.date: 06/03/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- SQL Trace collector set
ms.assetid: b6941dc0-50f5-475d-82eb-ce7c68117489
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: fdd751f282f1ba62150d5257dde04798962ecb84
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715528"
---
# <a name="use-sql-server-profiler-to-create-a-sql-trace-collection-set"></a>Usar o SQL Server Profiler para criar um conjunto de coleta do Rastreamento do SQL
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , você pode explorar as funcionalidades de rastreamento do lado do servidor do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para exportar uma definição de rastreamento que pode ser usada para criar um conjunto de coleta que usa o tipo de coletor de Rastreamento do SQL Genérico. Há duas partes nesse processo:  
  
1.  Crie e exporte um rastreamento [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] .  
  
2.  Faça o script de um novo conjunto de coleta baseado em um rastreamento exportado.  

 O cenário para os procedimentos a seguir envolve a coleta de dados sobre qualquer procedimento armazenado que exija 80 milissegundos ou mais para ser concluído. Para concluir esses procedimentos você deve ser capaz de:  
  
-   Usar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para criar e configurar um rastreamento.  
  
-   Usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para abrir, editar e executar uma consulta.  
  
### <a name="create-and-export-a-sql-server-profiler-trace"></a>Criar e exportar um rastreamento do SQL Server Profiler  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. (No menu **Ferramentas** clique em **SQL Server Profiler**.)  
  
2.  Na caixa de diálogo **Conectar ao Servidor** , clique em **Cancelar**.  
  
3.  Para este cenário, verifique se os valores de duração estão configurados para serem exibidos em milissegundos (o padrão). Para fazer isso, siga estas etapas:  
  
    1.  No menu **Ferramentas** , clique em **Opções**.  
  
    2.  Na área **Opções de Exibição** , verifique se a caixa de seleção Mostrar valores na coluna Duração em microssegundos está selecionada.  
  
    3.  Clique em **OK** para fechar a caixa de diálogo **Opções Gerais** .  
  
4.  No menu **Arquivo** , clique em **Novo Rastreamento**.  
  
5.  Na caixa de diálogo **Conectar ao Servidor** , selecione o servidor com o qual deseja se conectar e clique em **Conectar**.  
  
     É exibida a caixa de diálogo **Propriedades do Rastreamento** .  
  
6.  Na guia **Geral** , faça o seguinte:  
  
    1.  Na caixa **Nome do rastreamento** , digite o nome a ser usado para o rastreamento. Para este exemplo, o nome de rastreamento é **SPgt80**.  
  
    2.  Em **Usar a lista do modelo**, selecione o modelo a ser usado para o rastreamento. Para este exemplo, clique em **TSQL_SPs**.  
  
7.  Na guia **Seleção de Eventos** , faça o seguinte:  
  
    1.  Identifique os eventos a serem usados para o rastreamento. Para este exemplo, desmarque todas as caixas de seleção na coluna **Events** , exceto por **ExistingConnection** e **SP:Completed**.  
  
    2.  No canto inferior direito, selecione a caixa de seleção **Mostrar todas as colunas** .  
  
    3.  Clique na linha **SP:Completed** .  
  
    4.  Role pela linha até a coluna **Duration** e selecione a caixa de seleção **Duração** .  
  
8.  No canto inferior direito, clique em **Filtros de Coluna** para abrir a caixa de diálogo **Editar Filtro** . Na caixa de diálogo **Editar Filtro** , proceda da maneira a seguir:  
  
    1.  Na lista de filtros, clique em **Duração**.  
  
    2.  Na janela do operador booliano, expanda o nó **Maior ou igual a** , digite **80** como o valor e clique em **OK**.  
  
9. Clique em **Executar** para iniciar o rastreamento.  
  
10. Na barra de ferramentas, clique em **Parar Rastreamento Selecionado** ou **Pausar Rastreamento Selecionado**.  
  
11. No menu **Arquivo** , aponte para **Exportar**, para **Definição de Rastreamento de Script**e clique em **Para o Conjunto de Coleta de Rastreamento do SQL**.  
  
12. Na caixa de diálogo **Salvar como** , digite o nome desejado para a definição de rastreamento na caixa **Nome do arquivo** e salve-o no local desejado. Para este exemplo, o nome do arquivo é o mesmo que o nome do rastreamento (SPgt80).  
  
13. Clique em **OK** quando receber uma mensagem que o arquivo foi salvo com êxito e feche o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].  
  
### <a name="script-a-new-collection-set-from-a-sql-server-profiler-trace"></a>Gere o script de um novo conjunto de coleta de um rastreamento do SQL Server Profiler  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no menu **Arquivo** , aponte para **Abrir** e clique em **Arquivo**.  
  
2.  Na caixa de diálogo **Abrir Arquivo** , localize e abra o arquivo criado no procedimento anterior (SPgt80).  
  
     As informações de rastreamento que você salvou são abertas em uma janela de Consulta e mescladas em um script que você pode executar para criar o novo conjunto de coleta.  
  
3.  Role pelo script e faça as substituições a seguir, que são observadas no texto de comentários do script:  
  
    -   Substitua **Nome do Conjunto de Coleta SQLTrace Aqui** pelo nome que você deseja usar para o conjunto de coleta. Para este exemplo, o nome do conjunto de coleta é **SPROC_CollectionSet**.  
  
    -   Substitua **Nome do Item de Coleta SQLTrace Aqui** pelo nome que você deseja usar para o item de coleta. Para este exemplo, o nome do item de coleta é **SPROC_Collection_Item**.  
  
4.  Clique em **Executar** para executar a consulta e criar o conjunto de coleta.  
  
5.  No Pesquisador de Objetos, verifique se o conjunto de coleta foi criado. Para fazer isso, siga estas etapas:  
  
    1.  Clique com o botão direito do mouse em **Gerenciamento**e clique em **Atualizar**.  
  
    2.  Expanda **Gerenciamento**e expanda **Coleta de Dados**.  
  
     O conjunto de coleta **SPROC_CollectionSet** aparece no mesmo nível do nó **Conjuntos de Coleta de Dados do Sistema** . Por padrão, o conjunto de coleta é desabilitado.  
  
6.  Use o Pesquisador de Objetos para editar as propriedades de SPROC_CollectionSet, como o modo de coleta e a agenda de carregamento. Siga os mesmos procedimentos que você usaria para os conjuntos de coleta de Dados do Sistema que são fornecidos com o coletor de dados.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir é o script final resultante das etapas documentadas nos procedimentos anteriores.  
  
```sql
/*************************************************************/  
-- SQL Trace collection set generated from SQL Server Profiler  
-- Date: 11/19/2007  12:55:31 AM  
/*************************************************************/  
  
USE msdb;
GO  
  
BEGIN TRANSACTION  
BEGIN TRY  
  
-- Define collection set  
-- ***  
-- *** Replace 'SqlTrace Collection Set Name Here' in the   
-- *** following script with the name you want  
-- *** to use for the collection set.  
-- ***  
DECLARE @collection_set_id int;  
EXEC [dbo].[sp_syscollector_create_collection_set]  
    @name = N'SPROC_CollectionSet',  
    @schedule_name = N'CollectorSchedule_Every_15min',  
    @collection_mode = 0, -- cached mode needed for Trace collections  
    @logging_level = 0, -- minimum logging  
    @days_until_expiration = 5,  
    @description = N'Collection set generated by SQL Server Profiler',  
    @collection_set_id = @collection_set_id output;  
SELECT @collection_set_id;  
  
-- Define input and output variables for the collection item.  
DECLARE @trace_definition xml;  
DECLARE @collection_item_id int;  
  
-- Define the trace parameters as an XML variable  
SELECT @trace_definition = convert(xml,   
N'<ns:SqlTraceCollector xmlns:ns"DataCollectorType" use_default="0">  
<Events>  
  <EventType name="Sessions">  
    <Event id="17" name="ExistingConnection" columnslist="1,2,14,26,3,35,12" />  
  </EventType>  
  <EventType name="Stored Procedures">  
    <Event id="43" name="SP:Completed" columnslist="1,2,26,34,3,35,12,13,14,22" />  
  </EventType>  
</Events>  
<Filters>  
  <Filter columnid="13" columnname="Duration" logical_operator="AND" comparison_operator="GE" value="80000L" />  
</Filters>  
</ns:SqlTraceCollector>  
');  
  
-- Retrieve the collector type GUID for the trace collector type.  
DECLARE @collector_type_GUID uniqueidentifier;  
SELECT @collector_type_GUID = collector_type_uid
  FROM [dbo].[syscollector_collector_types]
  WHERE name = N'Generic SQL Trace Collector Type';  
  
-- Create the trace collection item.  
-- ***  
-- *** Replace 'SqlTrace Collection Item Name Here' in   
-- *** the following script with the name you want to  
-- *** use for the collection item.  
-- ***  
EXEC [dbo].[sp_syscollector_create_collection_item]  
   @collection_set_id = @collection_set_id,  
   @collector_type_uid = @collector_type_GUID,  
   @name = N'SPROC_Collection_Item',  
   @frequency = 900, -- specified the frequency for checking to see if trace is still running  
   @parameters = @trace_definition,  
   @collection_item_id = @collection_item_id output;  
SELECT @collection_item_id;  
  
COMMIT TRANSACTION;  
END TRY  
  
BEGIN CATCH  
ROLLBACK TRANSACTION;  
DECLARE @ErrorMessage nvarchar(4000);  
DECLARE @ErrorSeverity int;  
DECLARE @ErrorState int;  
DECLARE @ErrorNumber int;  
DECLARE @ErrorLine int;  
DECLARE @ErrorProcedure nvarchar(200);  
SELECT @ErrorLine = ERROR_LINE(),  
       @ErrorSeverity = ERROR_SEVERITY(),  
       @ErrorState = ERROR_STATE(),  
       @ErrorNumber = ERROR_NUMBER(),  
       @ErrorMessage = ERROR_MESSAGE(),  
       @ErrorProcedure = ISNULL(ERROR_PROCEDURE(), '-');  
RAISERROR (14684, @ErrorSeverity, 1 , @ErrorNumber,
  @ErrorSeverity, @ErrorState, @ErrorProcedure, @ErrorLine, @ErrorMessage);  
END CATCH;  
GO  
```  
  
  

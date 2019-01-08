---
title: Criar a função para recuperar os dados de alteração | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],creating function
ms.assetid: 55dd0946-bd67-4490-9971-12dfb5b9de94
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3b49001c7b62be67097223421ef85db2b475aa1d
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52761888"
---
# <a name="create-the-function-to-retrieve-the-change-data"></a>Criar a função para recuperar os dados de alteração
  Após concluir o fluxo de controle de um pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que executa uma carga incremental de dados de alteração, a próxima tarefa é criar uma função com valor de tabela que recupera os dados de alteração. É preciso criar esta função apenas uma vez antes da primeira carga incremental.  
  
> [!NOTE]  
>  A criação de uma função para recuperar os dados de alteração é a segunda etapa no processo de criação de um pacote que realize uma carga incremental de dados de alteração. Para obter uma descrição do processo geral para criar este pacote, consulte [Captura de dados de alteração &#40;SSIS&#41;](change-data-capture-ssis.md).  
  
## <a name="design-considerations-for-change-data-capture-functions"></a>Considerações de design para funções de captura de dados de alteração  
 Para recuperar dados de alteração, um componente de origem no fluxo de dados do pacote chama uma das seguintes funções de consulta de captura de dados de alteração:  
  
-   **cdc.fn_cdc_get_net_changes_<capture_instance>** Para essa consulta, a única linha retornada para cada atualização contém o estado final de cada linha alterada. Na maioria dos casos, você precisa apenas dos dados retornados por uma consulta para alterações líquidas. Para obter mais informações, veja [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql).  
  
-   **cdc.fn_cdc_get_all_changes_<capture_instance>** Essa consulta retorna todas as alterações que ocorreram em cada linha durante o intervalo de captura. Para obter mais informações, veja [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql).  
  
 O componente de origem que recebe os resultados retornados pela função e os passa para transformações e destinos downstream, que aplicam os dados da alteração no destino final.  
  
 No entanto, um componente de origem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não pode chamar estas funções de captura de dados de alteração diretamente. Um componente de origem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] requer metadados sobre as colunas retornadas pela consulta. As funções de captura de dados de alteração não definem as colunas de suas tabelas de saída. Dessa forma, estas funções não retornam metadados suficientes para um componente de origem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Em vez disso, use uma função de invólucro com valor de tabela, pois esse tipo de função define explicitamente as colunas de sua tabela de saída em sua cláusula RETURNS. Esta definição explícita de colunas fornece os metadados que uma componente de origem [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] precisa. É necessário criar esta função para cada tabela para a qual você deseja recuperar os dados de alteração.  
  
 Você tem duas opções para criar a função de invólucro com valor de tabela que chama a função de consulta de captura de dados de alteração:  
  
-   Você chamar o procedimento armazenado de sistema **sys.sp_cdc_generate_wrapper_function** para criar as funções com valor de tabela.  
  
-   Você pode escrever sua própria função com valor de tabela usando as diretrizes e o exemplo neste tópico.  
  
## <a name="calling-a-stored-procedure-to-create-the-table-valued-function"></a>Chamando um procedimento armazenado para criar a função com valor de tabela  
 A maneira mais rápida e fácil de criar funções com valor de tabela de que você precisa é chamar o procedimento armazenado de sistema **sys.sp_cdc_generate_wrapper_function** . Esse procedimento armazenado gera scripts para criar funções de invólucro projetadas especificamente para atender às necessidades de um componente de origem do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  O procedimento armazenado de sistema **sys.sp_cdc_generate_wrapper_function** não cria as funções de invólucro diretamente. Em vez disso, o procedimento armazenado gera os scripts CREATE para as funções de invólucro. O desenvolvedor deve executar os scripts CREATE gerados pelo procedimento armazenado antes de um pacote de carregamento incremental chamar as funções de invólucro.  
  
 Para entender como usar esse procedimento armazenado de sistema, você deve entender o que o procedimento faz, quais scripts o procedimento gera e quais funções de invólucro os scripts criam.  
  
### <a name="understanding-and-using-the-stored-procedure"></a>Entendendo e usando o procedimento armazenado  
 O procedimento armazenado de sistema **sys.sp_cdc_generate_wrapper_function** gera scripts para criar funções de invólucro para uso por pacotes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Estas são as primeiras linhas da definição do procedimento armazenado:  
  
 `CREATE PROCEDURE sys.sp_cdc_generate_wrapper_function`  
  
 `(`  
  
 `@capture_instance sysname = null`  
  
 `@closed_high_end_point bit = 1,`  
  
 `@column_list = null,`  
  
 `@update_flag_list = null`  
  
 `)`  
  
 Todos os parâmetros do procedimento armazenado são opcionais. Se você chamar o procedimento armazenado sem fornecer valores para nenhum dos parâmetros, o procedimento armazenado criará funções de invólucro para todas as instâncias de captura às quais você tem acesso.  
  
> [!NOTE]  
>  Para obter mais informações sobre a sintaxe desse procedimento armazenado e seus parâmetros, consulte [sys.sp_cdc_generate_wrapper_function &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql).  
  
 O procedimento armazenado sempre gera uma função de invólucro para retornar todas as alterações de cada instância de captura. Se o parâmetro *@supports_net_changes* foi definido quando a instância de captura foi criada, o procedimento armazenado também gerará uma função de wrapper para retornar alterações globais de cada instância de captura de aplicativo.  
  
 O procedimento armazenado retorna um conjunto de resultados com duas colunas:  
  
-   O nome da função de invólucro que o procedimento armazenado gerou. Esse procedimento armazenado deriva o nome da função do nome do nome da instância de captura. (O nome da função é 'fn_all_changes_' seguido pelo nome da instância de captura. O prefixo usado para a função de alterações globais, se for criado, será 'fn_net_changes_'.)  
  
-   A instrução CREATE da função de invólucro.  
  
### <a name="understanding-and-using-the-scripts-created-by-the-stored-procedure"></a>Entendendo e usando os scripts criados pelo procedimento armazenado  
 Em geral, um desenvolvedor usa uma instrução INSERT...EXEC para chamar o procedimento armazenado **sys.sp_cdc_generate_wrapper_function** e salvar os scripts criados por esse procedimento em uma tabela temporária. Cada script pode ser selecionado executado individualmente para criar a função de invólucro correspondente. No entanto, um desenvolvedor também pode usar um conjunto de comandos SQL para executar todos os scripts CREATE, conforme mostrado no código de exemplo a seguir:  
  
```  
create table #wrapper_functions  
      (function_name sysname, create_stmt nvarchar(max))  
insert into #wrapper_functions  
exec sys.sp_cdc_generate_wrapper_function  
  
declare @stmt nvarchar(max)  
declare #hfunctions cursor local fast_forward for   
      select create_stmt from #wrapper_functions  
open #hfunctions  
fetch #hfunctions into @stmt  
while (@@fetch_status <> -1)  
begin  
      exec sp_executesql @stmt  
      fetch #hfunctions into @stmt  
end  
close #hfunctions  
deallocate #hfunctions  
```  
  
### <a name="understanding-and-using-the-functions-created-by-the-stored-procedure"></a>Entendendo e usando as funções criadas pelo procedimento armazenado  
 Para percorrer sistematicamente a linha de tempo dos dados de alteração capturados, as funções de wrapper geradas esperam que o parâmetro *@end_time* de um intervalo seja o parâmetro *@start_time* do intervalo subsequente. Quando essa convenção é seguida, as funções de invólucro geradas podem executar as seguintes tarefas:  
  
-   Mapear os valores de data/hora para os valores LSN usados interiormente.  
  
-   Assegurar que nenhum dado seja perdido ou repetido.  
  
 Para simplificar a consulta a todas as linhas de uma alteração, as funções de invólucro geradas também dão suporte às seguintes convenções:  
  
-   Se o parâmetro @start_time for nulo, as funções wrapper usarão o valor LSN mais baixo na instância de captura do limite inferior da consulta.  
  
-   Se o parâmetro @end_time for nulo, as funções do wrapper usarão o valor LSN mais baixo na instância de captura do limite inferior da consulta.  
  
 A maioria dos usuários deverá poder usar as funções de invólucro que o procedimento armazenado de sistema **sys.sp_cdc_generate_wrapper_function** cria sem modificação. No entanto, para personalizar as funções de invólucro, você tem que personalizar os scripts CREATE antes de executar os scripts.  
  
 Quando seu pacote chama as funções de invólucro, o pacote deve fornecer valores para três parâmetros. Esses três parâmetros são como os três parâmetros que as funções de captura de dados de alteração usam. Esses três parâmetros são os seguintes:  
  
-   O valor de data/hora inicial e o valor de data/hora final do intervalo. Enquanto as funções de invólucro usam valores de data/hora como os pontos finais do intervalo de consulta, as funções de captura de dados de alteração usam dois valores LSN como os pontos finais.  
  
-   O filtro de linha. Para as funções de wrapper e as funções de captura de dados de alteração, o parâmetro *@row_filter_option* é o mesmo. Para obter mais informações, consulte [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql) e [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql).  
  
 O conjunto de resultados retornado pelas funções de invólucro inclui os seguintes dados:  
  
-   Todas as colunas solicitadas de dados de alteração.  
  
-   Uma coluna denominada __CDC_OPERATION que usa um campo de um ou dois caracteres para identificar a operação associada à linha. Os valores válidos para esse campo são da seguinte maneira: 'I' para inserção, vinda ' para excluir, 'UO' para atualizar valores antigos e un' ' para atualizar valores novos.  
  
-   Os sinalizadores de atualização, quando você os solicita, aparecem como colunas de bit após o código da operação e na ordem especificada no parâmetro *@update_flag_list* . Essas colunas são denominadas com a anexação de '_uflag' ao nome de coluna associado.  
  
 Se o pacote chamar uma função de wrapper que consulte todas as alterações, essa função também retornará as colunas __CDC_STARTLSN e \__CDC_SEQVAL. Essas duas colunas se tornam a primeira e a segunda colunas, respectivamente, do conjunto de resultados. A função de invólucro também classifica o conjunto de resultados com base nessas duas colunas.  
  
## <a name="writing-your-own-table-value-function"></a>Escrevendo sua própria função do valor de tabela  
 Também é possível usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para escrever sua própria função de wrapper com valor de tabela que chama a função de consulta de captura dos dados de alteração e armazena a função de wrapper com valor de tabela no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre como criar uma função Transact-SQL, consulte [CREATE FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-function-transact-sql).  
  
 O seguinte exemplo define uma função com valor de tabela que recupera alterações de uma tabela Cliente para o intervalo de alteração especificado. Essa função usa funções de captura de dados de alteração para mapear os valores `datetime` para os valores LSN (número de sequência de log) binários usados pelas tabelas de alteração internamente. Esta função também controla diversas condições especiais:  
  
-   Quando um valor nulo é passado como a hora inicial, essa função usa o valor mais baixo disponível.  
  
-   Quando um valor nulo é passado como a hora final, essa função usa o valor mais alto disponível.  
  
-   Quando o LSN inicial é igual ao LSN final, que normalmente indica que não existe registros para o intervalo selecionado, essa função é encerrada.  
  
### <a name="example-of-a-table-value-function-that-queries-for-change-data"></a>Exemplo de uma função com valor de tabela que consulta a existência de dados de alteração  
  
```  
CREATE function CDCSample.uf_Customer (  
     @start_time datetime  
    ,@end_time datetime  
)  
returns @Customer table (  
     CustomerID int  
    ,TerritoryID int  
    ,CustomerType nchar(1)  
    ,rowguid uniqueidentifier  
    ,ModifiedDate datetime  
    ,CDC_OPERATION varchar(1)  
) as  
begin  
    declare @from_lsn binary(10), @to_lsn binary(10)  
  
    if (@start_time is null)  
        select @from_lsn = sys.fn_cdc_get_min_lsn('Customer')  
    else  
        select @from_lsn = sys.fn_cdc_increment_lsn(sys.fn_cdc_map_time_to_lsn('largest less than or equal',@start_time))  
  
    if (@end_time is null)  
        select @to_lsn = sys.fn_cdc_get_max_lsn()  
    else  
        select @to_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal',@end_time)  
  
    if (@from_lsn = sys.fn_cdc_increment_lsn(@to_lsn))  
        return  
  
    -- Query for change data  
    insert into @Customer  
    select   
        CustomerID,      
        TerritoryID,   
        CustomerType,   
        rowguid,   
        ModifiedDate,   
        case __$operation  
                when 1 then 'D'  
                when 2 then 'I'  
                when 4 then 'U'  
                else null  
         end as CDC_OPERATION  
    from   
        cdc.fn_cdc_get_net_changes_Customer(@from_lsn, @to_lsn, 'all')  
  
    return  
end   
go  
  
```  
  
### <a name="retrieving-additional-metadata-with-the-change-data"></a>Recuperando metadados adicionais com os dados de alteração  
 Embora a função com valor de tabela criada pelo usuário mostrada anteriormente use apenas a coluna **__$operation**, a função **cdc.fn_cdc_get_net_changes_<capture_instance>** retorna quatro colunas de metadados para cada linha de alteração. Se quiser usar esses valores no seu fluxo de dados, poderá retorná-los como colunas adicionais com a função de invólucro com valor de tabela.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|`binary(10)`|LSN associado à transação de confirmação da alteração.<br /><br /> Todas as alterações confirmadas na mesma transação compartilham o mesmo LSN de confirmação. Por exemplo, se uma operação de atualização na tabela de origem modificar duas linhas diferentes, a tabela de alteração conterá quatro linhas (duas com os valores antigos e duas com os valores novos), cada uma com o mesmo valor de **__$start_lsn** .|  
|**__$seqval**|`binary(10)`|Valor de sequência usado para organizar as alterações de linha em uma transação.|  
|**__$operation**|`int`|A operação DML (linguagem de manipulação de dados) associada à alteração. Pode ser uma destas opções:<br /><br /> 1 = excluir<br /><br /> 2 = inserir<br /><br /> 3 = atualizar (valores anteriores à operação de atualização).<br /><br /> 4 = atualizar (valores posteriores à operação de atualização).|  
|**__$update_mask**|`varbinary(128)`|Uma máscara de bits com base nos ordinais de coluna da tabela de alteração identificando as colunas que foram alteradas. Você poderia examinar este valor se você tivesse que determinar quais colunas foram alteradas.|  
|**\<colunas da tabela de origem capturada>**|varia|As colunas restantes retornadas pela função são as colunas da tabela de origem que foram identificadas como colunas capturadas quando a instância de captura foi criada. Se nenhuma coluna tiver sido especificada originalmente na lista de colunas capturadas, todas as colunas da tabela de origem serão retornadas.|  
  
 Para obter mais informações, veja [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql).  
  
## <a name="next-step"></a>Próxima etapa  
 Após ter criado a função com valor de tabela que consulta a existência de dados de alteração, a próxima etapa será iniciar a criação do fluxo de dados no pacote.  
  
 **Próximo tópico:** [Recuperar e compreender os dados de alterações](retrieve-and-understand-the-change-data.md)  
  
  

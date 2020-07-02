---
title: cdc.fn_cdc_get_all_changes_&lt;capture_instance&gt;  (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_all_changes_<capture_instance>
- change data capture [SQL Server], querying metadata
- cdc.fn_cdc_get_all_changes_<capture_instance>
ms.assetid: c6bad147-1449-4e20-a42e-b51aed76963c
author: rothja
ms.author: jroth
ms.openlocfilehash: 5e05ef7753ae6375382bfd2bd6e199b6cabffd63
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85647993"
---
# <a name="cdcfn_cdc_get_all_changes_ltcapture_instancegt--transact-sql"></a>cdc.fn_cdc_get_all_changes_&lt;capture_instance&gt;  (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada alteração aplicada à tabela de origem dentro do intervalo LSN (número de sequência de log) especificado. Se uma linha de origem tiver passado por várias alterações durante o intervalo, todas as alterações serão representadas no conjunto de resultados retornado. Além de retornar os dados de alteração, quatro colunas de metadados fornecem as informações necessárias para a aplicação de alterações em outra fonte de dados. As opções de filtragem de linha regem o conteúdo das colunas de metadados, bem como as linhas retornadas no conjunto de resultados. Quando a opção de filtragem de linha 'all' é especificada, cada alteração tem exatamente uma linha para identificar a alteração. Quando a opção 'all update old' é especificada, as operações de atualização são representadas como duas linhas: uma contendo os valores das colunas capturadas antes da atualização e outra contendo os valores das colunas capturadas após a atualização.  
  
 Essa função de enumeração é criada no momento em que uma tabela de origem é habilitada para change data capture. O nome da função é derivado e usa o formato **CDC. fn_cdc_get_all_changes_**_capture_instance_ em que *capture_instance* é o valor especificado para a instância de captura quando a tabela de origem está habilitada para a captura de dados de alterações.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
cdc.fn_cdc_get_all_changes_capture_instance ( from_lsn , to_lsn , '<row_filter_option>' )  
  
<row_filter_option> ::=  
{ all  
 | all update old  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *from_lsn*  
 O valor LSN que representa o ponto de extremidade inferior do intervalo LSN a ser incluído no conjunto de resultados. *from_lsn* é **binary (10)**.  
  
 Somente as linhas no [capture_instance CDC. &#91;&#93;_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) alterar a tabela com um valor de **_ $ start_lsn** maior ou igual a *from_lsn* são incluídas no conjunto de resultados.  
  
 *to_lsn*  
 O valor LSN que representa o ponto de extremidade superior do intervalo LSN a ser incluído no conjunto de resultados. *to_lsn* é **binary (10)**.  
  
 Somente as linhas no [capture_instance CDC. &#91;&#93;_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) alterar a tabela com um valor de **_ $ start_lsn** menor ou igual a *from_lsn* ou igual a *to_lsn* são incluídos no conjunto de resultados.  
  
 <row_filter_option>:: = {ALL | todas as atualizações antigas}  
 Opção que rege o conteúdo das colunas de metadados, assim como as linhas retornadas no conjunto de resultados.  
  
 Pode ser uma das seguintes opções:  
  
 all  
 Retorna todas as alterações do intervalo LSN especificado. Para alterações relativas a uma operação de atualização, essa opção retorna apenas a linha que contém os novos valores após a aplicação da atualização.  
  
 all update old  
 Retorna todas as alterações do intervalo LSN especificado. Com relação às alterações relativas a uma operação de atualização, essa opção retorna tanto a linha que contém os valores da coluna antes da atualização como a linha que contém os valores da coluna após a atualização.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|**binary(10)**|LSN de confirmação associado à alteração que preserva a ordem de confirmação da alteração. Alterações confirmadas na mesma transação compartilham o mesmo valor LSN de confirmação.|  
|**__$seqval**|**binary(10)**|Valor de sequência usado para solicitar alterações em uma linha dentro de uma transação.|  
|**_ de $ operação**|**int**|Identifica a operação DML (linguagem de manipulação de dados) necessária para aplicar a linha de dados de alteração à fonte de dados de destino. Pode ser um dos seguintes:<br /><br /> 1 = excluir<br /><br /> 2 = inserir<br /><br /> 3 = atualizar (valores da coluna capturados são os valores anteriores à operação de atualização). Esse valor se aplica somente quando a opção de filtro de linha 'all update old' for especificada.<br /><br /> 4 = atualizar (valores de coluna capturados são os valores após a operação de atualização)|  
|**_ de $ update_mask**|**varbinary(128)**|Uma máscara de bits com um bit correspondente a cada coluna capturada identificada para a instância de captura. Esse valor tem todos os bits definidos configurados como 1 quando **_ _ $ operation** = 1 ou 2. Quando **_ _ $ operation** = 3 ou 4, somente os bits correspondentes às colunas que foram alteradas são definidos como 1.|  
|**\<captured source table columns>**|varia|As colunas restantes retornadas pela função são as colunas capturadas identificadas quando a instância de captura foi criada. Se nenhuma coluna tiver sido especificada na lista de colunas capturadas, todas as colunas da tabela de origem serão retornadas.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa. Para todos os outros usuários, requer a permissão SELECT em todas as colunas capturadas na tabela de origem e, se uma função associada para a instância de captura tiver sido definida, faça associação nessa função de banco de dados. Quando o chamador não tem permissão para exibir os dados de origem, a função retorna o erro 229 ("a permissão SELECT foi negada no objeto ' fn_cdc_get_all_changes_... ', banco de dados ' \<DatabaseName> ', esquema ' CDC '.").  
  
## <a name="remarks"></a>Comentários  
 Se o intervalo de LSN especificado não estiver dentro da linha de tempo do controle de alterações, a função retornará o erro 208 ("Um número insuficiente de argumentos foi fornecido para o procedimento ou função cdc.fn_cdc_get_all_changes").  
  
 As colunas do tipo de dados **Image**, **Text**e **ntext** sempre recebem um valor nulo quando são **_ de $ Operation** = 1 ou **_ de $ Operation** = 3. As colunas do tipo de dados **varbinary (max)**, **varchar (max)** ou **nvarchar (max)** recebem um valor nulo quando são **_ de $ Operation** = 3, a menos que a coluna seja alterada durante a atualização. Quando **_ elimina $ Operation** = 1, essas colunas recebem seu valor no momento da exclusão. Colunas computadas que são incluídas em uma instância de captura têm sempre um valor de NULL.  
  
## <a name="examples"></a>Exemplos  
 Vários [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] modelos estão disponíveis para mostrar como usar as funções de consulta de captura de dados de alterações. Esses modelos estão disponíveis no menu **Exibir** no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] . Para obter mais informações, consulte [Gerenciador de modelos](../../ssms/template/template-explorer.md).  
  
 Este exemplo mostra o `Enumerate All Changes for Valid Range Template`. Ele usa a função `cdc.fn_cdc_get_all_changes_HR_Department` para relatar todas as alterações disponíveis atualmente para a instância de captura `HR_Department`, que é definida para a tabela de origem HumanResources.Department no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
-- ========  
-- Enumerate All Changes for Valid Range Template  
-- ========  
USE AdventureWorks2012;  
GO  
  
DECLARE @from_lsn binary(10), @to_lsn binary(10);  
SET @from_lsn = sys.fn_cdc_get_min_lsn('HR_Department');  
SET @to_lsn   = sys.fn_cdc_get_max_lsn();  
SELECT * FROM cdc.fn_cdc_get_all_changes_HR_Department  
  (@from_lsn, @to_lsn, N'all');  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CDC. fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [sys. fn_cdc_map_time_to_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)   
 [sys. sp_cdc_get_ddl_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)   
 [sys. sp_cdc_get_captured_columns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md)   
 [sys. sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [Sobre a captura de dados de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  

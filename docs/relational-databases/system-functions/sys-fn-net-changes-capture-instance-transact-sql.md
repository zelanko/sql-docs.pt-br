---
title: sys.fn_net_changes_&lt;capture_instance&gt; (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_net_changes_TSQL
- fn_net_changes_TSQL
- fn_net_changes
- sys.fn_net_changes
dev_langs:
- TSQL
helpviewer_keywords:
- fn_net_changes_<capture_instance>
- sys.fn_net_changes_<capture_instance>
ms.assetid: 342fa030-9fd9-4b74-ae4d-49f6038a5073
author: rothja
ms.author: jroth
ms.openlocfilehash: add3f81793b2dc21c08ca601bb1c48cc7d4588be
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85783080"
---
# <a name="sysfn_net_changes_ltcapture_instancegt-transact-sql"></a>sys.fn_net_changes_&lt;capture_instance&gt; (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Wrappers para as funções de consulta de **alterações líquidas** . Os scripts necessários para criar essas funções são gerados pelo procedimento armazenado sys.sp_cdc_generate_wrapper_function.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn_net_changes_<capture_instance> ('start_time', 'end_time', '<row_filter_option>' )  
  
<capture_instance> ::= The name of the capture instance.  
<row_filter_option> ::=  
{ all  
  | all with mask  
  | all with merge  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *start_time*  
 O valor **DateTime** que representa o ponto de extremidade inferior do intervalo de entradas da tabela de alteração a serem incluídas no conjunto de resultados.  
  
 Somente as linhas na capture_instance CDC. <>_CT alterar a tabela que têm uma hora de confirmação associada estritamente maior que *start_time* são incluídas no conjunto de resultados.  
  
 Se um valor NULL for fornecido para este argumento, o ponto de extremidade inferior do intervalo da consulta corresponderá ao ponto de extremidade inferior de um intervalo válido para a instância de captura.  
  
 *end_time*  
 O valor **DateTime** que representa o ponto de extremidade superior do intervalo de entradas da tabela de alteração a serem incluídas no conjunto de resultados.  
  
 Esse parâmetro pode assumir um dos dois significados, dependendo do valor escolhido para @closed_high_end_point quando sys. sp_cdc_generate_wrapper_function é chamado para gerar o script para criar a função de wrapper:  
  
-   @closed_high_end_point = 1  
  
     Somente as linhas no capture_instance CDC. <>_CT alteram a tabela que têm um valor em \_ \_ $Start _lsn e uma hora de confirmação correspondente menor ou igual a **start_time** são incluídas no conjunto de resultados.  
  
-   @closed_high_end_point = 0  
  
     Somente as linhas no capture_instance CDC. <>_CT alteram a tabela que têm um valor em \_ \_ $Start _lsn e uma hora de confirmação correspondente estritamente menor que **start_time** são incluídas no conjunto de resultados.  
  
 Se um valor NULL for fornecido para este argumento, o ponto de extremidade superior do intervalo da consulta corresponderá ao ponto de extremidade superior de um intervalo válido para a instância de captura.  
  
 *<row_filter_option>* :: = {todos | todos com máscara | tudo com mesclagem}  
 Opção que rege o conteúdo das colunas de metadados, assim como as linhas retornadas no conjunto de resultados. Pode ser uma das seguintes opções:  
  
 all  
 Retorna o conteúdo final de uma linha alterada nas colunas de conteúdo e a operação que é requerida para aplicar a linha na coluna de metadados __CDC_OPERATION.  
  
 all with mask  
 Retorna o conteúdo final de todas as linhas alteradas nas colunas de conteúdo e a operação que é necessária para aplicar cada linha na coluna de metadados __CDC_OPERATION. Se uma lista de sinalizadores atualizada foi especificada durante a geração do script para criar a função de wrapper, essa opção será requerida para popular a máscara atualizada.  
  
 all with merge  
 Retorna o conteúdo final de todas as linhas alteradas nas colunas de conteúdo.  
  
 A coluna __CDC_OPERATION terá um dos seguintes dois valores:  
  
-   D, se a linha dever ser excluída.  
  
-   M, se a linha dever ser inserida ou atualizada.  
  
 A lógica para determinar se uma inserção ou atualização é necessária para aplicação de uma alteração ao destino aumenta a complexidade da consulta. Use essa opção para obter desempenho aprimorado quando não for necessário fazer diferença entre operações de inserção e de atualização. Essa abordagem funciona melhor em ambientes de destino em que uma operação de mesclagem está diretamente disponível, como em um ambiente do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de coluna|Description|  
|-----------------|-----------------|-----------------|  
|\<columns from @column_list>|**consoante**|As colunas identificadas no argumento **column_list** para o sp_cdc_generate_wrapper_function quando ele é chamado para gerar o script para criar o wrapper. Se *column_list* for NULL, todas as colunas de origem rastreadas serão exibidas no conjunto de resultados.|  
|__CDC_OPERATION|**nvarchar(2)**|Um código de operação que indica qual operação é necessária para se aplicar a linha ao ambiente de destino. A operação irá variar com base no valor do argumento *row_filter_option* fornecido na seguinte chamada:<br /><br /> *row_filter_option* = ' all', ' tudo com máscara '<br /><br /> 'D' – exclui a operação<br /><br /> 'I' – insere a operação<br /><br /> 'UN' – atualiza a operação<br /><br /> *row_filter_option* = ' tudo com mesclagem '<br /><br /> 'D' – exclui a operação<br /><br /> 'M – insere ou atualiza a operação|  
|\<columns from @update_flag_list>|**bit**|Um sinalizador de bit é nomeado acrescentando _uflag ao nome da coluna. O sinalizador assume um valor não nulo somente quando *row_filter_option* **= ' all com mask '** e \_ _CDC_OPERATION **= ' un '**. Ele é definido como 1 se a coluna correspondente foi modificada dentro da janela de consulta. Caso contrário, será 0.|  
  
## <a name="remarks"></a>Comentários  
 A função fn_net_changes_<capture_instance> serve como um wrapper para a função de consulta cdc. fn_cdc_get_net_changes_<capture_instance>. O procedimento armazenado sys.sp_cdc_generate_wrapper é usado para criar o script para o wrapper.  
  
 As funções de wrapper não são criadas automaticamente. Há duas coisas que você precisa fazer para criar funções de wrapper:  
  
1.  Executar o procedimento armazenado para gerar o script para criar o wrapper.  
  
2.  Executar o script para realmente criar a função de wrapper.  
  
 As funções de wrapper permitem que os usuários consultem sistematicamente as alterações que ocorreram em um intervalo limitado por valores de **data e hora** em vez de valores LSN. As funções de wrapper executam todas as conversões necessárias entre os valores **DateTime** fornecidos e os valores LSN necessários internamente como argumentos para as funções de consulta. Quando as funções de wrapper são usadas em série para processar um fluxo de dados de alteração, elas garantem que nenhum dado seja perdido ou repetido desde que a seguinte convenção seja seguida: o @end_time valor do intervalo associado a uma chamada é fornecido como o @start_time valor para o intervalo associado à chamada subsequente.  
  
 Usando o parâmetro @closed_high_end_point ao criar o script, você pode gerar wrappers para oferecer suporte a um limite superior fechado ou a um limite superior em aberto na janela de consulta especificada. Ou seja, você pode decidir se as entradas que têm uma hora de confirmação igual ao limite superior do intervalo de extração devem ser incluídas no intervalo. Por padrão, o limite superior é incluído.  
  
 O conjunto de resultados retornado pela função de wrapper **net Changes** retorna somente as colunas rastreadas que estavam no @column_list quando o wrapper foi gerado. Se @column_list for NULL, todas as colunas de origem rastreadas serão retornadas. As colunas de origem são acompanhadas por uma coluna de operação, __CDC_OPERATION, que é uma coluna de um ou dois caracteres que identifica a operação.  
  
 Os sinalizadores de bits são então anexados ao conjunto de resultados para cada coluna identificada no parâmetro @update_flag_list . Para o wrapper de **alterações líquidas** , os sinalizadores de bit sempre serão nulos se o @row_filter_option que for usado na chamada para a função de wrapper for ' all' ou ' tudo com mesclagem '. Se o @row_filter_option for definido como ' all com Mask ' e __CDC_OPERATION for ' ou ' I ', o valor do sinalizador também será NULL. Se \_ _CDC_OPERATION for ' un ', o sinalizador será definido como 1 ou 0, dependendo se a operação de atualização de **rede** causou uma alteração na coluna.  
  
 O modelo de configuração da captura de dados de alterações ' instanciar CDC wrapper TVFs for Schema ' mostra como usar o sp_cdc_generate_wrapper_function procedimento armazenado para obter scripts de criação para todas as funções de wrapper para funções de consulta definidas pelo esquema. Em seguida, o modelo cria esses scripts. Para obter mais informações sobre modelos, consulte [Gerenciador de modelos](../../ssms/template/template-explorer.md).  
  
## <a name="see-also"></a>Consulte Também  
 [sys. sp_cdc_generate_wrapper_function &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)  
  
  

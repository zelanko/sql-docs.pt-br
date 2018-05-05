---
title: sys.fn_net_changes_&lt;capture_instance&gt; (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
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
caps.latest.revision: 16
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bfc1d85252bc07700e093f992f24a887734612b6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysfnnetchangesltcaptureinstancegt-transact-sql"></a>sys.fn_net_changes_&lt;capture_instance&gt; (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Wrappers para o **net alterações** funções de consulta. Os scripts necessários para criar essas funções são gerados pelo procedimento armazenado sys.sp_cdc_generate_wrapper_function.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 O **datetime** valor que representa o ponto de extremidade inferior do intervalo de entradas de tabela de alteração para incluir no conjunto de resultados.  
  
 Apenas as linhas no cdc. < capture_instance > _CT alteração de tabela que tem uma hora de confirmação associada estritamente maior que *start_time* são incluídos no conjunto de resultados.  
  
 Se um valor NULL for fornecido para este argumento, o ponto de extremidade inferior do intervalo da consulta corresponderá ao ponto de extremidade inferior de um intervalo válido para a instância de captura.  
  
 *end_time*  
 O **datetime** valor que representa o ponto de extremidade superior do intervalo de entradas de tabela de alteração para incluir no conjunto de resultados.  
  
 Esse parâmetro pode assumir um dos dois significados, dependendo do valor escolhido para @closed_high_end_point quando sys. sp_cdc_generate_wrapper_function é chamado para gerar o script para criar a função de wrapper:  
  
-   @closed_high_end_point = 1  
  
     Apenas as linhas no cdc. < capture_instance > _CT que têm um valor na tabela de alteração \_ \_$start_lsn e uma confirmação correspondente de tempo menor que ou igual a **start_time** são incluídos no conjunto de resultados.  
  
-   @closed_high_end_point = 0  
  
     Apenas as linhas no cdc. < capture_instance > _CT que têm um valor na tabela de alteração \_ \_$start_lsn e correspondente tempo de confirmação estritamente menor que **start_time** são incluídos no conjunto de resultados.  
  
 Se um valor NULL for fornecido para este argumento, o ponto de extremidade superior do intervalo da consulta corresponderá ao ponto de extremidade superior de um intervalo válido para a instância de captura.  
  
 *< row_filter_option >* :: = {todos | tudo com máscara | tudo com mesclagem}  
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
|\<colunas de @column_list>|**Varia de acordo**|As colunas que são identificadas no **column_list** argumento para a sp_cdc_generate_wrapper_function quando ela é chamada para gerar o script para criar o wrapper. Se *column_list* for NULL, todas as colunas de origem controladas aparecerão no conjunto de resultados.|  
|__CDC_OPERATION|**nvarchar(2)**|Um código de operação que indica qual operação é necessária para se aplicar a linha ao ambiente de destino. A operação variará com base no valor do argumento *row_filter_option* que é fornecido na seguinte chamada:<br /><br /> *row_filter_option* = 'todos', 'all with mask'<br /><br /> 'D' – exclui a operação<br /><br /> 'I' – insere a operação<br /><br /> 'UN' – atualiza a operação<br /><br /> *row_filter_option* = 'all with merge'<br /><br /> 'D' – exclui a operação<br /><br /> 'M – insere ou atualiza a operação|  
|\<colunas de @update_flag_list>|**bit**|Um sinalizador de bit é nomeado acrescentando _uflag ao nome da coluna. O sinalizador assume um valor não nulo somente quando *row_filter_option* **= 'all with mask'** e \__CDC_OPERATION **= 'UN'**. Ele é definido como 1 se a coluna correspondente foi modificada dentro da janela de consulta. Caso contrário, será 0.|  
  
## <a name="remarks"></a>Remarks  
 A função fn_net_changes_<capture_instance> serve como um wrapper para a função de consulta cdc.fn_cdc_get_net_changes_<capture_instance>. O procedimento armazenado sys.sp_cdc_generate_wrapper é usado para criar o script para o wrapper.  
  
 As funções de wrapper não são criadas automaticamente. Há duas coisas que você precisa fazer para criar funções de wrapper:  
  
1.  Executar o procedimento armazenado para gerar o script para criar o wrapper.  
  
2.  Executar o script para realmente criar a função de wrapper.  
  
 Funções de wrapper permitem que os usuários consultem sistematicamente as alterações que ocorreram dentro de um intervalo limitado por **datetime** valores em vez de por valores LSN. As funções de wrapper executam todas as conversões necessárias entre fornecido **datetime** valores e os valores LSN necessários internamente como argumentos para as funções de consulta. Quando as funções de wrapper são usadas em série para processar um fluxo de dados de alteração, elas garantem que nenhum dado seja perdido ou repetido desde que a seguinte convenção seja seguida: o @end_time valor do intervalo associado a uma chamada é fornecido como o @start_time valor para o intervalo associado à chamada subsequente.  
  
 Usando o parâmetro @closed_high_end_point ao criar o script, você pode gerar wrappers para oferecer suporte a um limite superior fechado ou a um limite superior em aberto na janela de consulta especificada. Ou seja, você pode decidir se as entradas que têm uma hora de confirmação igual ao limite superior do intervalo de extração devem ser incluídas no intervalo. Por padrão, o limite superior é incluído.  
  
 O conjunto de resultados retornado pelo **net alterações** wrapper função retorna apenas as colunas rastreadas que estavam no @column_list quando o wrapper foi gerado. Se @column_list for NULL, todas as colunas de origem rastreadas serão retornadas. As colunas de origem são acompanhadas por uma coluna de operação, __CDC_OPERATION, que é uma coluna de um ou dois caracteres que identifica a operação.  
  
 Sinalizadores de bit são acrescentados ao conjunto de resultados para cada coluna identificada no parâmetro @update_flag_list. Para o **net alterações** wrapper, o bit sinalizadores serão sempre NULL se o @row_filter_option que é usado na chamada à função de wrapper for 'all'ou 'all with merge'. Se o @row_filter_option for definido como 'all with mask' e cdc_operation for ' ou 'I', o valor do sinalizador também será NULL. Se \__CDC_OPERATION é 'UN', o sinalizador será definido como 1 ou 0, dependendo se o **net** causada uma alteração na coluna de operação de atualização.  
  
 O modelo de configuração do Change Data Capture 'Criar uma instância de TVFs de wrapper CDC para esquema' mostra como usar o procedimento armazenado sp_cdc_generate_wrapper_function para obter scripts CREATE para todas as funções de wrapper para funções de consulta definidas por um esquema. Em seguida, o modelo cria esses scripts. Para obter mais informações sobre modelos, consulte [Explorador](http://msdn.microsoft.com/library/b9ee55c5-bb44-4f76-90ac-792d8d83b4c8).  
  
## <a name="see-also"></a>Consulte também  
 [sys.sp_cdc_generate_wrapper_function &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)  
  
  

---
title: Trabalhar com os dados de alteração (SQL Server) | Microsoft Docs
ms.date: 01/02/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change data [SQL Server]
- change data capture [SQL Server], query function scenarios
- change data capture [SQL Server], LSN boundaries
- change data capture [SQL Server], query functions
ms.assetid: 5346b852-1af8-4080-b278-12efb9b735eb
author: rothja
ms.author: jroth
ms.openlocfilehash: 2d08ef02a81832ad532e184d6cae79d7fd03119a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006049"
---
# <a name="work-with-change-data-sql-server"></a>Trabalhar com dados de alterações (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]
  Os dados de alteração ficam disponíveis para consumidores de Change Data Capture através das TVFs (funções com valor de tabela). Todas as consultas dessas funções exigem dois parâmetros para definir o intervalo de LSNs (números de sequência de log) qualificados para serem considerados no desenvolvimento do conjunto de dados retornado. Tanto o valor superior quanto o valor inferior do LSN indica que o limite do intervalo é considerado ao ser incluído no intervalo.  
  
 Muitas funções são fornecidas para ajudar a determinar os valores LSN apropriados para serem usados em uma consulta a uma TVF. A função [sys.fn_cdc_get_min_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md) retorna o menor LSN associado a um intervalo de validade da instância de captura. O intervalo de validade é o intervalo de tempo durante o qual os dados de alteração ficam disponíveis para as instâncias de captura. A função [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md) retorna o maior LSN no intervalo de validade. As funções [sys.fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) e [sys.fn_cdc_map_lsn_to_time](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md) estão disponíveis para ajudar a colocar valores LSN em uma linha do tempo convencional. Como a captura de dados de alteração usa intervalos fechados, algumas vezes é necessário gerar o próximo valor LSN em uma sequência para garantir que as alterações não serão duplicadas em janelas de consulta consecutivas. As funções [sys.fn_cdc_increment_lsn](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md) e [sys.fn_cdc_decrement_lsn](../../relational-databases/system-functions/sys-fn-cdc-decrement-lsn-transact-sql.md) são úteis quando é necessário um ajuste incremental em um valor LSN.  
  
##  <a name="LSN"></a> Validando limites de LSN  
 Antes de utilizar os limites de LSN que devem ser usados em uma consulta de TVF, é recomendável validá-los. Os pontos de extremidades nulos ou pontos de extremidade que ficam fora do intervalo de validade da instância de captura forçará um erro que será retornado por uma TVF de captura de dados de alteração.  
  
 Por exemplo, o erro abaixo é retornado para uma consulta de todas as alterações quando um parâmetro que é utilizado para definir o intervalo de consultas não é válido ou está fora do intervalo válido ou quando a opção de filtro de linhas é inválida.  
  
 `Msg 313, Level 16, State 3, Line 1`  
  
 `An insufficient number of arguments were supplied for the procedure or function cdc.fn_cdc_get_all_changes_ ...`  
  
 O erro correspondente retornado para uma consulta **net changes** é o seguinte:  
  
 `Msg 313, Level 16, State 3, Line 1`  
  
 `An insufficient number of arguments were supplied for the procedure or function cdc.fn_cdc_get_net_changes_ ...`  
  
> [!NOTE]  
>  É sabido que a mensagem Msg 313 é equivocada e não informa a causa real da falha. Esse uso inadequado é originário da falta de habilidade para elevar um erro explícito de dentro de uma TVF. No entanto, o valor de retorno de um erro reconhecido, mesmo inexato, foi considerado preferível ao retorno de apenas um resultado vazio. Um conjunto de resultados vazio não seria perceptível a partir de uma consulta válida que não retorna nenhuma alteração.  
  
 Falhas de autorização retornarão falhas ao consultar todas as alterações, como a seguir:  
  
 `Msg 229, Level 14, State 5, Line 1`  
  
 `The SELECT permission was denied on the object 'fn_cdc_get_all_changes_...', database 'MyDB', schema 'cdc'.`  
  
 O mesmo ocorre ao realizar consultas em alterações líquidas:  
  
 `Msg 229, Level 14, State 5, Line 1`  
  
 `The SELECT permission was denied on the object fn_cdc_get_net_changes_...', database 'MyDB', schema 'cdc'.`  
  
 Consulte o modelo Enumerar Alterações Delta Usando TRY CATCH para ver uma demonstração de como interceptar esses erros de TVF conhecidos e retornar informações mais pertinentes sobre a falha.  
  
> [!NOTE]  
>  Para localizar modelos de Captura de Dados de Alterações no SQL Server Management Studio, no menu **Exibir** , clique em **Gerenciador de Modelos**, expanda **Modelos do SQL Server** e expanda a pasta **Captura de Dados de Alterações** .  
  
##  <a name="Functions"></a> Funções de consulta  
 Dependendo das características da tabela de origem que estiver sendo rastreada e da configuração da instância de captura, serão geradas uma ou duas TVFs para consultar dados de alteração.  
  
-   A função [cdc.fn_cdc_get_all_changes_<capture_instance>](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) retorna todas as alterações ocorridas para o intervalo especificado. Essa função sempre é gerada. As entradas sempre são retornadas em ordem, a primeira pelo LSN de confirmação da transação da alteração e, em seguida, por um valor que ordena a alteração dentro de sua transação. Dependendo da opção de filtro de linhas escolhida, ou a linha final é retornada na atualização (opção de filtro de linhas "all") ou os valores novos e antigos são retornados na atualização (opção de filtro de linhas "all update old").  
  
-   A função [cdc.fn_cdc_get_net_changes_<capture_instance>](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md) é gerada quando o parâmetro @supports_net_changes é definido como 1 e a tabela de origem está habilitada.  
  
    > [!NOTE]  
    >  Esta opção só terá suporte se a tabela de origem tiver uma chave primária definida ou se o parâmetro @index_name tiver sido usado para identificar um índice exclusivo.  
  
     A função **netchanges** retorna uma alteração por linha modificada da tabela de origem. Se forem registradas mais de uma alteração para a linha durante o intervalo especificado, os valores da coluna refletirão o conteúdo final da linha. Para identificar corretamente a operação necessária para atualizar o ambiente de destino, a TVF deverá considerar tanto a operação inicial na linha durante o intervalo quanto a operação final na linha. Quando a opção de filtro de linha “all” for especificado, as operações retornadas por uma consulta **net changes** serão insert, delete ou update (novos valores). Esta opção sempre retorna a máscara de atualização como nula, pois há um custo associado ao cálculo de uma máscara de agregação. Caso queira uma máscara de agregação que reflita todas as alterações em uma linha, use a opção 'all with mask'. Se o processamento downstream não exigir que inserções e atualizações sejam diferenciadas, use a opção 'all with merge'. Nesse caso, o valor da operação só vai levar dois valores: 1 para excluir e 5 para uma operação que pode ser uma inserção ou uma atualização. Esta opção elimina o processamento adicional necessário para determinar se a operação derivada deveria ser uma inserção ou uma atualização e pode melhorar o desempenho da consulta quando essa diferenciação não é necessária.  
  
 A máscara de atualização retornada de uma função de consulta é uma representação compacta que identifica todas as colunas que foram alteradas em uma linha de dados de alteração. Normalmente, essas informações são necessárias apenas para um pequeno subconjunto de colunas capturadas. Há funções disponíveis para ajudar a extrair informações da máscara em uma forma que seja mais diretamente utilizável por aplicativos. A função [sys.fn_cdc_get_column_ordinal](../../relational-databases/system-functions/sys-fn-cdc-get-column-ordinal-transact-sql.md) retorna a posição ordinal de uma coluna nomeada relativa a uma dada instância de captura, ao passo que a função [sys.fn_cdc_is_bit_set](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md) retorna a paridade do bit da máscara fornecida com base no ordinal passado na chamada de função. Juntas, essas duas funções permitem que as informações da coluna atualizada sejam extraídas de maneira eficaz e retornadas com a solicitação de dados de alteração. Consulte o modelo Enumerar Alterações Delta Usando All With Mask para ver uma demonstração de como estas funções são utilizadas.  
  
##  <a name="Scenarios"></a> Cenários de funções de consulta  
 As próximas seções descrevem cenários comuns para consultar dados de Change Data Capture usando as funções de consulta cdc.fn_cdc_get_all_changes_<instância_de_captura> e cdc.fn_cdc_get_net_changes_<instância_de_captura>.  
  
### <a name="querying-for-all-changes-within-the-capture-instance-validity-interval"></a>Consultando todas as alterações ocorridas no intervalo de validade de captura da instância de captura  
 A solicitação mais objetiva de dados de alteração é a que retorna todos os dados de alteração atuais em um intervalo de validade da instância de captura. Para fazer essa solicitação, primeiro determine os limites de LSN inferior e superior do intervalo de validade. Em seguida, use esses valores para identificar os parâmetros @from_lsn e @to_lsn passados para a função de consulta cdc.fn_cdc_get_all_changes_<capture_instance> ou cdc.fn_cdc_get_net_changes_<capture_instance>. Use a função [sys.fn_cdc_get_min_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md) para obter o limite inferior e [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md) para obter o limite superior. Consulte o modelo Enumerar Todas as Consultas no Intervalo Válido para que o código de exemplo consulte todas as alterações válidas usando a função de consulta cdc.fn_cdc_get_all_changes_<instância_de_captura>. Consulte o modelo Enumerar Consultas Delta no Intervalo Válido para ver um exemplo semelhante de como usar a função cdc.fn_cdc_get_net_changes_<instância_de_captura>.  
  
### <a name="querying-for-all-new-changes-since-the-last-set-of-changes"></a>Consultando todas as novas alterações feitas desde o último conjunto de alterações  
 Em aplicativos típicos, consultar dados de alteração será um processo constante, fazendo solicitações periódicas de todas as alterações ocorridas desde a última solicitação. Para tais consultas, você pode usar a função [sys.fn_cdc_increment_lsn](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md) para derivar o limite inferior da consulta atual com base no limite superior da consulta anterior. Este método assegura que nenhuma linha seja repetida porque o intervalo de consulta é sempre tratado como um intervalo fechado, onde os dois pontos de extremidade estão incluídos no intervalo. Em seguida, use a função [sys.fn_cdc_get_max_lsn](../../relational-databases/system-functions/sys-fn-cdc-get-max-lsn-transact-sql.md) para obter o ponto de extremidade superior relativo ao intervalo de solicitação. Consulte o modelo Enumerar Todas as Alterações desde a Solicitação Anterior para ver o código de exemplo para mover sistematicamente a janela de consulta e obter todas as alterações feitas desde a última solicitação.  
  
### <a name="querying-for-all-new-changes-up-until-now"></a>Consultando todas as novas alterações feitas até agora  
 Uma restrição típica imposta sobre as alterações retornadas por uma função de consulta é incluir apenas as alterações que ocorreram entre a solicitação anterior e a data e a hora atuais. Para esta consulta, aplique a função sys.fn_cdc_increment_lsn ao valor @from_lsn que foi usado na solicitação anterior para determinar o limite inferior. Como o limite superior sobre o intervalo de tempo é expresso como um momento determinado, ele deve ser convertido em um valor LSN para que possa ser usado por uma função de consulta. Para que o valor de data e hora seja convertido em um valor LSN correspondente, você deve assegurar que o processo de captura processou todas as alterações confirmadas através do limite superior especificado. Isso é necessário para garantir que todas as alterações qualificadas foram propagadas na tabela de alteração. Uma forma de fazer isso é estruturar um loop de espera que verifique periodicamente se o lsn de confirmação máximo atual registrado para qualquer tabela de alteração do banco de dados ultrapassa a hora de término desejada do intervalo de solicitação.  
  
 Depois que o loop de atraso verificar se o processo de captura já processou todas as entradas de log relevantes, use a função [sys.fn_cdc_map_time_to_lsn](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md) para determinar o novo ponto de extremidade superior expresso como um valor LSN. Para assegurar que todas as entradas que foram confirmadas através da hora especificada sejam recuperadas, chame a função sys.fn_cdc_map_time_to_lsn e use a opção 'maior menor que ou igual'.  
  
> [!NOTE]  
>  Em períodos de inatividade, uma entrada fictícia é adicionada à tabela cdc.lsn_time_mapping para indicar que o processo de captura processou as alterações até uma determinada hora de confirmação. Isso impede que se tenha a impressão de que o processo de captura não foi executado quando simplesmente não existem alterações a serem processadas.  
  
 O modelo Enumerar Todas as Alterações Feitas até Agora demonstra como usar a estratégia anterior para consultar dados de alteração.  
  
### <a name="adding-a-commit-time-to-an-all-changes-result-set"></a>Adicionando uma hora de confirmação a um conjunto de resultados Todas as Alterações  
 A hora de confirmação de cada transação com uma entrada associada de uma tabela de alterações do banco de dados fica disponível na tabela [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md). Ao unir o valor __$start_lsn retornado em uma solicitação de todas as alterações com o valor start_lsn de uma entrada da tabela cdc.lsn_time_mapping, você consegue retornar tran_end_time junto com os dados de alteração para gravar a alteração com a hora de confirmação da transação na origem. O modelo Acrescentar Hora de Confirmação ao Conjunto de Resultados Todas as Alterações demonstra como fazer esta junção.  
  
### <a name="joining-change-data-with-other-data-from-the-same-transaction"></a>Unindo dados de alteração com outros dados da mesma transação  
 De vez em quando é útil unir dados de alteração com outras informações coletadas sobre a transação quando confirmada na origem. A coluna tran_begin_lsn da tabela cdc.lsn_time_mapping fornece as informações necessárias para fazer tal junção. Quando ocorre a atualização da origem, o valor de database_transaction_begin_lsn da exibição dinâmica do sistema [sys.dm_tran_database_transactions](../../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md) deve ser salvo junto com qualquer outra informação a ser unida aos dados de alteração. Use a função fn_convertnumericlsntobinary para comparar os valores database_transaction_begin_lsn e tran_begin_lsn. O código para criar esta função está disponível no modelo Criar Função fn_convertnumericlsntobinary. O modelo Retornar Todas as Alterações com um Dado tran_begin_lsn demonstra como efetuar a junção.  
  
### <a name="querying-using-datetime-wrapper-functions"></a>Consultando com funções de wrapper de data e hora  
 Um cenário de aplicativo típico para consultar dados de alteração é solicitar dados de alteração periodicamente usando uma janela deslizante vinculada por valores de data e hora. Para esta classe de consumidores, o Change Data Capture oferece o procedimento armazenado [sys.sp_cdc_generate_wrapper_function](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md) que gera scripts para criar funções de wrapper personalizadas para as funções de consulta do Change Data Capture. Esses wrappers personalizados permitem que o intervalo de consulta seja expresso como um par de data/hora.  
  
 Chamar opções do procedimento armazenado permite que wrappers sejam gerados para todas as instâncias de captura às quais o chamador tem acesso ou apenas para uma instância de captura especificada. As opções com suporte também incluem a capacidade de especificar se o ponto de extremidade superior do intervalo de captura deve ser aberto ou fechado, quais colunas capturadas disponíveis devem ser incluídas no conjunto de resultados e quais colunas incluídas devem ter sinalizadores de atualização associados. O procedimento retorna um conjunto de resultados com duas colunas: o nome de função gerado que é derivado do nome da instância de captura, e a instrução de criação para o procedimento armazenado do wrapper. A função usada para incluir a consulta de todas as alterações sempre é gerada. Se o parâmetro @supports_net_changes foi definido durante a criação da instância de captura, a função usada para encapsular as alterações delta também é gerada.  
  
 É de responsabilidade do designer do aplicativo chamar o procedimento armazenado de geração de script para gerar as instruções de criação para os procedimentos armazenados do wrapper, bem como executar os scripts de criação resultantes para criar as funções. Isso não ocorre automaticamente quando uma instância de captura é criada.  
  
 Os wrappers de data e hora pertencem ao usuário e não são criados no esquema padrão do chamador. A função gerada é adequada e não requer modificação para a maioria dos usuários. Todavia, antes de criar a função sempre é possível aplicar mais personalizações ao script gerado.  
  
 O nome da função usada para incluir a consulta de todas as alterações é fn_all_changes_ seguido pelo nome da instância de captura. O prefixo usado para o wrapper de alterações delta é fn_net_changes_. Ambas as funções usam três argumentos, assim como suas TVFs associadas do Change Data Capture. No entanto, o intervalo de consulta para os wrappers é vinculado por dois valores de data e hora, e não por dois valores LSN. O parâmetro @row_filter_option para os dois conjuntos de funções é o mesmo.  
  
 As funções de wrapper geradas dão suporte à seguinte convenção para percorrer sistematicamente a linha de tempo de captura de dados de alterações: Espera-se que o parâmetro @end_time do intervalo anterior seja usado como o parâmetro @start_time do intervalo subsequente. A função de wrapper mapeia os valores de data e hora para valores LSN e assegura que nenhum dado seja perdido ou repetido se esta convenção for seguida.  
  
 Os wrappers podem ser gerados para dar suporte a um limite superior fechado e a um limite superior aberto na janela de consulta especificada. Ou seja, o chamador pode especificar se as entradas que têm uma hora de confirmação igual ao limite superior do intervalo de extração devem ser incluídas no intervalo. Por padrão, o limite superior é incluído.  
  
 Embora as TVFs da consulta gerada falhem se for indicado um valor nulo para o valor @from_lsn ou @to_lsn, as funções de wrapper de data e hora usam nulo para permitir que esses wrappers retornem todas as alterações atuais. Ou seja, se nulo for passado como o ponto de extremidade inferior da janela de consulta para o wrapper de data e hora, o ponto de extremidade inferior do intervalo de validade da instância de captura será usado na instrução SELECT subjacente aplicada à TVF da consulta. De maneira semelhante, se nulo for passado como o ponto de extremidade superior da janela de consulta, o ponto de extremidade superior do intervalo de validade da instância de captura será usado para fazer uma seleção na TVF da consulta.  
  
 O conjunto de resultados retornado por uma função de wrapper inclui todas as colunas solicitadas seguidas por uma coluna de operação, gravada como um ou dois caracteres que identificam a operação associada à linha. Caso sinalizadores de atualização tenham sido solicitados, serão exibidos como colunas de bit após o código da operação, na ordem especificada no parâmetro @update_flag_list. Para obter informações sobre as opções de chamada para personalizar os wrappers de data e hora gerados, consulte [sys.sp_cdc_generate_wrapper_function &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql.md).  
  
 O modelo Instanciar uma TVF de Wrapper com Sinalizador de Atualização mostra como personalizar uma função de wrapper gerada para acrescentar um sinalizador de atualização de uma coluna especificada ao conjunto de resultados retornado por uma consulta de alterações delta. O modelo Criar uma Instância de TVFs de Wrapper CDC para Esquema mostra como instanciar os Wrappers de Data e Hora das TVFs de Consulta para todas as instâncias de captura criadas para as tabelas de origem em um dado esquema de banco de dados.  
  
 Para ver um exemplo que utiliza um wrapper de data e hora para consultar dados de alteração, consulte o modelo Obter Alterações Delta Usando Wrapper com Sinalizadores de Atualização. Este modelo demonstra como consultar alterações delta com uma função de wrapper quando o wrapper está configurado para retornar sinalizadores de atualização. Observe que a opção de filtro de linhas 'all with mask' é necessária para que a função de consulta subjacente retorne uma máscara de atualização não nula na atualização. Valores nulos são passados para os limites de intervalo de data e hora inferior e superior para indicar que a função deve usar o ponto de extremidade inferior e o ponto de extremidade superior do intervalo de validade da instância de captura ao executar a consulta subjacente baseada em LSN. A consulta retorna uma linha para cada modificação em uma linha de origem ocorrida no intervalo válido para a instância de captura.  
  
### <a name="using-the-datetime-wrapper-functions-to-transition-between-capture-instances"></a>Usando as funções de wrapper de data e hora para transição entre instâncias de captura  
 O Change Data Capture dá suporte a até duas instâncias de captura para uma única tabela de origem rastreada. O principal uso deste recurso é acomodar uma transição entre várias instâncias de captura quando alterações de DDL na tabela de origem expandem o conjunto de colunas disponíveis para controle. Ao transitar para uma nova instância de captura, uma forma de proteger níveis de aplicativos superiores contra alterações nos nomes de funções de consulta subjacentes é usar uma função de wrapper para incluir a chamada subjacente. Em seguida, atente para que o nome da função de wrapper permaneça o mesmo. Quando a transição tiver de ser feita, a antiga função de wrapper poderá ser descartada, e uma nova com o mesmo nome poderá ser criada para fazer referência às novas funções de consulta. Se primeiro você modificar o script gerado para criar uma função de wrapper de mesmo nome, poderá fazer a transição para uma nova instância de captura sem afetar as camadas de aplicativos superiores.  
  
## <a name="see-also"></a>Consulte Também  
 [Controle de alterações de dados &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [Sobre a captura de dados de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [Habilitar e desabilitar a captura de dados de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-data-capture-sql-server.md)   
 [Administrar e monitorar a captura de dados de alteração &#40;SQL Server&#41;](../../relational-databases/track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  

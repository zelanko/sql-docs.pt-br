---
title: Noções básicas sobre tipos de Cursor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4f4d3db7-4f76-450d-ab63-141237a4f034
caps.latest.revision: 51
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1611575b0f0401b47cf468837f39a6a8dd36aa49
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="understanding-cursor-types"></a>Compreendendo os tipos de cursor
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  As operações em um ato de banco de dados relacional em um conjunto completo de linhas. O conjunto de linhas retornado por uma instrução SELECT consiste em todas as linhas que satisfazem as condições na cláusula WHERE da instrução. Este conjunto completo de linhas retornado pela instrução é conhecido como conjunto de resultados. Nem sempre os aplicativos podem trabalhar efetivamente com o conjunto de resultados inteiro como uma unidade. Esses aplicativos precisam de um mecanismo para trabalhar com uma linha ou um bloco pequeno de linhas de cada vez. Os cursores são uma extensão dos conjuntos de resultados que proveem esse mecanismo.  
  
 Os cursores estendem o processamento do conjunto de resultados fazendo o seguinte:  
  
-   Permitirem o posicionamento em linhas específicas do conjunto de resultados.  
  
-   Recuperarem uma linha ou bloco de linhas de posições atuais em um conjunto de resultados.  
  
-   Oferecendo suporte a modificações de dados na linha da posição atual no conjunto de resultados.  
  
-   Oferecerem suporte a diferentes níveis de visibilidade às mudanças feitas por outros usuários ao banco de dados que são apresentados no conjunto de resultados.  
  
> [!NOTE]  
>  Para obter uma descrição completa de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tipos de cursor, consulte o tópico "Tipos de Cursor (mecanismo de banco de dados)" nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
 A especificação do JDBC provê suporte para cursores somente encaminhamento e roláveis que são sensíveis ou insensíveis a alterações feitas por outros trabalhos e podem ser somente leitura ou atualizáveis. Essa funcionalidade é fornecida pelo [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) classe.  
  
## <a name="remarks"></a>Remarks  
 O driver JDBC oferece suporte aos seguintes tipos de cursores:  
  
|Conjunto de resultados<br /><br /> resultados (cursor)|Tipo de cursor do SQL Server|Características|Selecione<br /><br /> Método|Buffer<br /><br /> de resposta|Description|  
|------------------------------------|----------------------------|---------------------|-----------------------|----------------------------|-----------------|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|N/A|Somente encaminhamento, somente leitura|direct|completa|O aplicativo tem que fazer uma única passagem (para a frente) pelo conjunto de resultados. Esse é o comportamento padrão, que é o mesmo de um cursor TYPE_SS_DIRECT_FORWARD_ONLY. O driver lê o conjunto de resultados inteiro do servidor em uma memória durante o tempo de execução da instrução.|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|N/A|Somente encaminhamento, somente leitura|direct|adaptive|O aplicativo tem que fazer uma única passagem (para a frente) pelo conjunto de resultados. O comportamento é igual ao de um cursor TYPE_SS_DIRECT_FORWARD_ONLY. O driver lê as linhas do servidor à medida que o aplicativo as solicita e assim minimiza o uso de memória do lado do cliente.|  
|TYPE_FORWARD_ONLY (CONCUR_READ_ONLY)|Avanço rápido|Somente encaminhamento, somente leitura|cursor|N/A|O aplicativo tem que fazer uma única passagem (para a frente) pelo conjunto de resultados usando um cursor de servidor. O comportamento é igual ao de um cursor TYPE_SS_SERVER_CURSOR_FORWARD_ONLY.<br /><br /> As linhas são recuperadas do servidor em blocos especificados pelo tamanho da busca.|  
|TYPE_FORWARD_ONLY (CONCUR_UPDATABLE)|Dinâmico (somente encaminhamento)|Somente encaminhamento, atualizável|N/A|N/A|O aplicativo tem que fazer uma única passagem (para a frente) pelo conjunto de resultados para atualizar uma ou mais linhas.<br /><br /> As linhas são recuperadas do servidor em blocos especificados pelo tamanho da busca.<br /><br /> Por padrão, o tamanho da busca é fixado quando o aplicativo chama o [setFetchSize](../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md) método o [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.<br /><br /> **Observação:** o driver JDBC fornece um recurso de buffer adaptável que permite recuperar resultados da execução de instrução da [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] como o aplicativo precisa deles, e não tudo de uma vez. Por exemplo, se o aplicativo precisar recuperar um volume de dados grande demais para caber inteiramente na memória do aplicativo, o buffer adaptável permitirá que o aplicativo cliente recupere esse valor como um fluxo. O comportamento padrão do driver é "**adaptável**". No entanto, para obter o buffer adaptável para os conjuntos de resultados atualizáveis de somente avanço, o aplicativo precisa chamar explicitamente o [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) método o [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) objeto fornecendo um **cadeia de caracteres** valor "**adaptável"**. Para um exemplo de código, consulte [amostra de dados grande atualização](../../connect/jdbc/updating-large-data-sample.md).|  
|TYPE_SCROLL_INSENSITIVE|Estático|Rolável, não atualizável.<br /><br /> Atualizações, inserções e exclusões de linhas externas não são visíveis.|N/A|N/A|O aplicativo requer um instantâneo de banco de dados. O conjunto de resultados não é atualizável. Só há suporte para CONCUR_READ_ONLY.  Todos os outros tipos de simultaneidade causarão uma exceção quando usados com este tipo de cursor.<br /><br /> As linhas são recuperadas do servidor em blocos especificados pelo tamanho da busca.|  
|TYPE_SCROLL_SENSITIVE<br /><br /> (CONCUR_READ_ONLY)|Keyset|Rolável, somente leitura. As atualizações de linhas externas são visíveis, e as exclusões aparecem como dados ausentes.<br /><br /> As inserções de linhas externas não são visíveis.|N/A|N/A|O aplicativo tem que ver dados alterados somente para linhas existentes.<br /><br /> As linhas são recuperadas do servidor em blocos especificados pelo tamanho da busca.|  
|TYPE_SCROLL_SENSITIVE<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Keyset|Rolável, atualizável.<br /><br /> As atualizações de linhas externas e internas são visíveis, e as exclusões aparecem como dados ausentes; as inserções não são visíveis.|N/A|N/A|O aplicativo pode alterar dados nas linhas existentes usando o objeto de conjunto de resultados. O aplicativo também deve ser capaz de ver as alterações em linhas feitas por outras pessoas de fora do objeto de conjunto de resultados.<br /><br /> As linhas são recuperadas do servidor em blocos especificados pelo tamanho da busca.|  
|TYPE_SS_DIRECT_FORWARD_ONLY|N/A|Somente encaminhamento, somente leitura|N/A|completo ou adaptável|Valor inteiro = 2003. Fornece um cursor somente leitura do lado do cliente que é totalmente armazenado em buffer. Nenhum cursor de servidor é criado.<br /><br /> Só há suporte para o tipo de simultaneidade CONCUR_READ_ONLY. Todos os outros tipos de simultaneidade causam uma exceção quando usado com esse tipo de cursor.|  
|TYPE_SS_SERVER_CURSOR_FORWARD_ONLY|Avanço rápido|Somente avanço|N/A|N/A|Valor inteiro = 2004. Rápido, acessa todos os dados usando um cursor de servidor. É atualizável quando usado com o tipo de simultaneidade CONCUR_UPDATABLE.<br /><br /> As linhas são recuperadas do servidor em blocos especificados pelo tamanho da busca.<br /><br /> Para obter o buffer adaptável para este caso, o aplicativo precisa chamar explicitamente o [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) método o [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) objeto fornecendo um **cadeia de caracteres**  valor "**adaptável"**. Para um exemplo de código, consulte [amostra de dados grande atualização](../../connect/jdbc/updating-large-data-sample.md).|  
|TYPE_SS_SCROLL_STATIC|Estático|As atualizações de outros usuários não são refletidas.|N/A|N/A|Valor inteiro = 1004. O aplicativo requer um instantâneo do banco de dados. Este é o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-sinônimo específico para o TYPE_SCROLL_INSENSITIVE do JDBC e tem o mesmo comportamento de configuração de simultaneidade.<br /><br /> As linhas são recuperadas do servidor em blocos especificados pelo tamanho da busca.|  
|TYPE_SS_SCROLL_KEYSET<br /><br /> (CONCUR_READ_ONLY)|Keyset|Com rolagem, somente leitura. As atualizações de linhas externas são visíveis, e as exclusões aparecem como dados ausentes.<br /><br /> As inserções de linhas externas não são visíveis.|N/A|N/A|Valor inteiro = 1005. O aplicativo tem que ver dados alterados somente para linhas existentes. Este é o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-sinônimo específico para o TYPE_SCROLL_SENSITIVE do JDBC e tem o mesmo comportamento de configuração de simultaneidade.<br /><br /> As linhas são recuperadas do servidor em blocos especificados pelo tamanho da busca.|  
|TYPE_SS_SCROLL_KEYSET<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Keyset|Rolável, atualizável.<br /><br /> As atualizações de linhas externas e internas são visíveis, e as exclusões aparecem como dados ausentes; as inserções não são visíveis.|N/A|N/A|Valor inteiro = 1005. O aplicativo tem que alterar dados ou ver dados alterados para linhas existentes. Este é o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]-sinônimo específico para o TYPE_SCROLL_SENSITIVE do JDBC e tem o mesmo comportamento de configuração de simultaneidade.<br /><br /> As linhas são recuperadas do servidor em blocos especificados pelo tamanho da busca.|  
|TYPE_SS_SCROLL_DYNAMIC<br /><br /> (CONCUR_READ_ONLY)|Dinâmicos|Rolável, somente leitura.<br /><br /> As atualizações e as inserções de linhas externas são visíveis, e as exclusões aparecem como dados ausentes transitórios no buffer de busca atual.|N/A|N/A|Valor inteiro = 1006. O aplicativo deve ver dados alterados para linhas existentes, além de ver linhas inseridas e excluídas durante o tempo de vida do cursor.<br /><br /> As linhas são recuperadas do servidor em blocos especificados pelo tamanho da busca.|  
|TYPE_SS_SCROLL_DYNAMIC<br /><br /> (CONCUR_UPDATABLE, CONCUR_SS_SCROLL_LOCKS, CONCUR_SS_OPTIMISTIC_CC, CONCUR_SS_OPTIMISTIC_CCVAL)|Dinâmicos|Rolável, atualizável.<br /><br /> As atualizações e as inserções de linhas externas e internas são visíveis, e as exclusões aparecem como dados ausentes transitórios no buffer de busca atual.|N/A|N/A|Valor inteiro = 1006. O aplicativo pode alterar dados para linhas existentes, ou inserir ou excluir linhas usando o objeto de conjunto de resultados. O aplicativo também deve ser capaz de ver as alterações, inserções e exclusões feitas por outras pessoas de fora do objeto de conjunto de resultados.<br /><br /> As linhas são recuperadas do servidor em blocos especificados pelo tamanho da busca.|  
  
## <a name="cursor-positioning"></a>Posicionamento dos cursores  
 Os cursores TYPE_FORWARD_ONLY, TYPE_SS_DIRECT_FORWARD_ONLY e TYPE_SS_SERVER_CURSOR_FORWARD_ONLY oferecem suporte apenas a [próximo](../../connect/jdbc/reference/next-method-sqlserverresultset.md) método de posicionamento.  
  
 O cursor TYPE_SS_SCROLL_DYNAMIC não oferece suporte a [absoluto](../../connect/jdbc/reference/absolute-method-sqlserverresultset.md) e [getRow](../../connect/jdbc/reference/getrow-method-sqlserverresultset.md) métodos. O método absoluto pode ser aproximado por uma combinação de chamadas para o [primeiro](../../connect/jdbc/reference/first-method-sqlserverresultset.md) e [relativo](../../connect/jdbc/reference/relative-method-sqlserverresultset.md) métodos para cursores dinâmicos.  
  
 O método getRow é suportado por apenas cursores TYPE_FORWARD_ONLY, TYPE_SS_DIRECT_FORWARD_ONLY, TYPE_SS_SERVER_CURSOR_FORWARD_ONLY, TYPE_SS_SCROLL_KEYSET e TYPE_SS_SCROLL_STATIC. O método getRow com todos os tipos de cursor somente encaminhamento retorna o número de linhas lidas até o momento através do cursor.  
  
> [!NOTE]  
>  Quando um aplicativo faz um chamada ou uma chamada sem suporte para o método getRow de posicionamento do cursor sem suporte, uma exceção será lançada com a mensagem, "a operação solicitada não é suportada com esse tipo de cursor."  
  
 Só o cursor TYPE_SS_SCROLL_KEYSET e o TYPE_SCROLL_SENSITIVE equivalente expõem linhas excluídas. Se o cursor estiver posicionado em uma linha excluída, os valores de coluna não estão disponíveis e o [rowDeleted](../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md) método retorna "true". Chamadas para obter\<tipo > métodos lançam uma exceção com a mensagem, "Não é possível obter o valor de uma linha excluída". As linhas excluídas não podem ser atualizadas. Se você tentar chamar uma atualização\<tipo > método em uma linha excluída, uma exceção será lançada com a mensagem, "uma linha excluída não pode ser atualizada". O cursor TYPE_SS_SCROLL_DYNAMIC tem o mesmo comportamento até ser movido para fora do buffer de busca atual.  
  
 Os cursores dinâmicos e de avançar expõem as linhas excluídas de modo semelhante, mas só enquanto permanecem acessíveis no buffer de busca. Para os cursores de avançar, isso é bastante direto. Para os cursores dinâmicos, é mais complexo quando o tamanho da busca é maior que 1. Um aplicativo pode mover o cursor para a frente e para trás dentro da janela definida pelo buffer de busca, mas a linha excluída desaparecerá quando a ação sair do buffer de busca original no qual ocorreu a atualização. Se um aplicativo não desejar ver as linhas excluídas transitórias usando cursores dinâmicos, deverá ser usado um relativo de busca (0).  
  
 Se os valores-chave de uma linha de cursor TYPE_SS_SCROLL_KEYSET ou TYPE_SCROLL_SENSITIVE forem atualizados com o cursor, a linha reterá sua posição original no conjunto de resultados, quer a linha atualizada atenda ou não aos critérios de seleção do cursor. Se a linha foi atualizada fora do cursor, uma linha excluída aparecerá na posição original da linha, mas a linha só aparecerá no cursor se outra linha com os novos valores-chave estava presente no cursor, mas foi excluída subsequentemente.  
  
 Para cursores dinâmicos, as linhas atualizadas reterão sua posição dentro do buffer de busca até que a ação saia da janela definida pelo buffer de busca. Linhas atualizadas podem reaparecer subsequentemente em posições diferentes dentro do conjunto de resultados ou podem desaparecer completamente. Os aplicativos que precisam evitar inconsistências transitórias no conjunto de resultados devem usar um tamanho de busca igual a 1 (o padrão é 8 linhas com simultaneidade de CONCUR_SS_SCROLL_LOCKS e 128 linhas com outras simultaneidades).  
  
## <a name="cursor-conversion"></a>Conversão de cursores  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] às vezes, pode optar por implementar um tipo de cursor diferente do solicitado, que é conhecido como uma conversão implícita de cursor (ou degradação de cursor). Para obter mais informações sobre conversão implícita de cursor, consulte o tópico "Usando conversões de Cursor implícitas" nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Manuais Online.  
  
 Com [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)], quando você atualizar os dados por meio do resultado ResultSet.TYPE_SCROLL_SENSITIVE e ResultSet.CONCUR_UPDATABLE definida, uma exceção será lançada com a mensagem "o cursor é READ ONLY". Essa exceção ocorre porque o [!INCLUDE[ssVersion2000](../../includes/ssversion2000_md.md)] fez uma conversão implícita de cursor para esse resultado definido e não retornou o cursor atualizável que foi solicitado.  
  
 Para solucionar esse problema, você pode usar uma das duas soluções a seguir:  
  
-   Verifique se a tabela subjacente tem uma chave primária  
  
-   Use [Type_ss_scroll_dynamic](../../connect/jdbc/reference/type-ss-scroll-dynamic-field-sqlserverresultset.md) em vez de ResultSet.TYPE_SCROLL_SENSITIVE durante a criação de uma instrução.  
  
## <a name="cursor-updating"></a>Atualização de cursores  
 Há suporte para atualizações in-loco de cursores nos casos em que a simultaneidade e o tipo do cursor oferecem suporte a atualizações. Se o cursor não está posicionado em uma linha atualizável no conjunto de resultados (nenhuma get\<tipo > chamada de método foi bem-sucedida), uma chamada para uma atualização\<tipo > método lançará uma exceção com a mensagem, "o conjunto de resultados não tem linha atual." A especificação do JDBC declara que uma exceção ocorre quando um método de atualização é chamado para uma coluna de um cursor que é CONCUR_READ_ONLY. Em situações em que a linha não é atualizável, por exemplo, devido a um conflito de simultaneidade otimista como uma atualização ou exclusão concorrente, a exceção poderá não ocorrer até [insertRow](../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md), [updateRow](../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md), ou [deleteRow](../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md) é chamado.  
  
 Depois de uma chamada para atualizar\<tipo >, a coluna afetada não pode ser acessada pelo get\<tipo > até que updateRow ou [cancelRowUpdates](../../connect/jdbc/reference/cancelrowupdates-method-sqlserverresultset.md) foi chamado. Isso evita problemas em que uma coluna é atualizada usando um tipo diferente do tipo retornado pelo servidor, e chamadas de getter subsequentes poderiam invocar conversões de tipo do lado do cliente com resultados inexatos. Chamadas para obter\<tipo > lançará uma exceção com a mensagem, "não não possível acessar as colunas atualizadas até que updateRow () ou Cancelrowupdates foi chamado."  
  
> [!NOTE]  
>  Se o método updateRow é chamado quando nenhuma coluna tiver sido atualizada, o driver JDBC lançará uma exceção com a mensagem, "updateRow () chamado quando não há colunas foram atualizadas."  
  
 Depois de [moveToInsertRow](../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md) foi chamado, uma exceção será lançada se qualquer método de obter\<tipo >, atualizar\<tipo >, insertRow e os métodos de posicionamento do cursor (inclusive [ moveToCurrentRow](../../connect/jdbc/reference/movetocurrentrow-method-sqlserverresultset.md)) for chamado no conjunto de resultados. O método moveToInsertRow efetivamente coloca o conjunto de resultados em modo de inserção e métodos de posicionamento do cursor terminam o modo de inserção. Chamadas de posicionamento relativo do cursor mova o cursor em relação à posição em que ele se encontrava antes moveToInsertRow foi chamado. Após chamadas de posicionamento do cursor, a futura posição de destino do cursor se torna a nova posição do cursor.  
  
 Se o cursor posicionamento chamada feita em insert modo for bem-sucedida, a posição do cursor após a chamada com falha é a posição do cursor original antes de moveToInsetRow foi chamada. Se insertRow falha, o cursor permanecerá na linha de inserção e o cursor permanecerá no modo de inserção.  
  
 As colunas na linha de inserção estão inicialmente em um estado não inicializado. Chamadas para a atualização\<tipo > método define o estado da coluna como inicializado. Uma chamada a get\<tipo > método para uma coluna não inicializada lança uma exceção. Uma chamada para o método insertRow retorna todas as colunas na linha de inserção para um estado não inicializado.  
  
 Se todas as colunas são inicializadas quando o método insertRow é chamado, o valor padrão para a coluna é inserido. Se não houver um valor padrão, mas a coluna for anulável, será inserido NULL. Se não houver um valor padrão e a coluna não for anulável, o servidor retornará um erro e uma exceção será lançada.  
  
> [!NOTE]  
>  Chamadas para o método getRow retorna 0 quando no modo de inserção.  
>   
>  O driver JDBC não oferece suporte a atualizações ou exclusões posicionadas. De acordo com a especificação do JDBC, o [setCursorName](../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md) método não tem nenhum efeito e o [getCursorName](../../connect/jdbc/reference/getcursorname-method-sqlserverresultset.md) método lançará uma exceção se for chamado.  
>   
>  Os cursores somente leitura e estáticos nunca são atualizáveis.  
>   
>  O SQL Server restringe os cursores de servidor a um único conjunto de resultados. Se um procedimento em lote ou armazenado contiver várias instruções, um cursor de cliente somente encaminhamento e somente leitura deverá ser usado.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando conjuntos de resultados com o JDBC Driver](../../connect/jdbc/managing-result-sets-with-the-jdbc-driver.md)  
  
  

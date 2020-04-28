---
title: Desenvolvendo o reconhecimento do pool de conexões em um driver ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c63d5cae-24fc-4fee-89a9-ad0367cddc3e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f77fea1d8439ac9ce7374b7dd47db5665686cfbc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283426"
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC
Este tópico discute os detalhes do desenvolvimento de um driver ODBC que contém informações sobre como o driver deve fornecer serviços de pooling de conexão.  
  
## <a name="enabling-driver-aware-connection-pooling"></a>Habilitando o pool de conexões com reconhecimento de driver  
 Um driver deve implementar as seguintes funções SPI (interface do provedor de serviços ODBC):  
  
-   SQLSetConnectAttrForDbcInfo  
  
-   SQLSetConnectInfo  
  
-   SQLSetDriverConnectInfo  
  
-   SQLGetPoolID  
  
-   SQLRateConnection  
  
-   SQLPoolConnect  
  
-   SQLCleanupConnectionPoolID  
  
 Consulte [referência da SPI (interface do provedor de serviços ODBC)](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md) para obter mais informações.  
  
 Um driver também deve implementar as seguintes funções existentes para que o pool com reconhecimento de driver possa ser habilitado:  
  
|Função|Funcionalidade adicionada|  
|--------------|-------------------------|  
|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|Suporte para o novo tipo de identificador: SQL_HANDLE_DBC_INFO_TOKEN (consulte a descrição abaixo).|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|Suporte ao novo atributo de conexão somente de conjunto: SQL_ATTR_DBC_INFO_TOKEN para redefinir a conexão (consulte a descrição abaixo).|  
  
> [!NOTE]  
>  Funções preteridas, como **SqlError** e **SQLSetConnectOption** , não têm suporte para pool de conexões com suporte a driver.  
  
## <a name="the-pool-id"></a>A ID do pool  
 A ID do pool é uma ID específica do driver de comprimento de ponteiro para representar um grupo específico de conexões que podem ser usadas de forma intercambiável. Dado um conjunto de informações de conexão, um driver deve ser capaz de deduzir rapidamente a ID de pool correspondente.  
  
 Por exemplo, a ID do pool deve codificar as informações de nome e credencial do servidor. No entanto, o nome do banco de dados não é necessário porque um driver pode ser capaz de reutilizar uma conexão e, em seguida, alterar o banco de dados em menos tempo do que fazer uma nova conexão.  
  
 Um driver deve definir um conjunto de atributos de chave, que incluirá a ID do pool. O valor desses atributos de chave pode vir de atributos de conexão, Cadeia de conexão e DSN. Caso haja conflitos nessas fontes, a política de resolução específica do driver existente deve ser usada para compatibilidade com versões anteriores.  
  
 O Gerenciador de driver usará um pool diferente para IDs de pool diferentes. Todas as conexões no mesmo pool são reutilizáveis. O Gerenciador de driver nunca reutilizará uma conexão com uma ID de pool diferente.  
  
 Portanto, os drivers devem atribuir uma ID de pool exclusiva para cada grupo de conexões com o mesmo valor em seus atributos de chave definidos. Se um driver usar a mesma ID de pool para duas conexões com valores diferentes em seus atributos de chave, o Gerenciador de driver ainda as colocará no mesmo pool (o Gerenciador de driver não sabe nada sobre os atributos de chave específicos do driver). Isso significa que o driver precisará relatar ao Gerenciador de driver que uma conexão com um conjunto diferente de atributos de chave não é reutilizável na [função SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md). Isso pode diminuir o desempenho e isso não é recomendado.  
  
 O Gerenciador de driver não reutilizará uma conexão alocada de outro ambiente de driver, mesmo se todas as informações de conexão forem correspondentes. O Gerenciador de driver usará um pool diferente para um ambiente diferente, mesmo quando as conexões tiverem a mesma ID de pool. Portanto, a ID do pool é local para seu ambiente de driver.  
  
 A função para obter a ID do pool do driver é a [função SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md).  
  
## <a name="the-connection-rating"></a>A classificação de conexão  
 Em comparação com o estabelecimento de uma nova conexão, você pode obter melhor desempenho redefinindo algumas informações de conexão (como banco de dados) em uma conexão em pool. Portanto, talvez você não queira que o nome do banco de dados esteja em seu conjunto de atributos de chave. Caso contrário, você pode ter um pool separado para cada banco de dados, o que pode não ser bom em aplicativos de camada intermediária, em que os clientes usam várias cadeias de conexão diferentes.  
  
 Sempre que você reutiliza uma conexão que tem alguma incompatibilidade de atributo, você deve redefinir os atributos incompatíveis com base na nova solicitação de aplicativo, para que a conexão retornada seja idêntica à solicitação do aplicativo (consulte a discussão do atributo SQL_ATTR_DBC_INFO_TOKEN na [função SQLSetConnectAttr](https://go.microsoft.com/fwlink/?LinkId=59368)). No entanto, a redefinição desses atributos pode diminuir o desempenho. Por exemplo, redefinir um banco de dados requer uma chamada de rede para o servidor. Portanto, reutilize uma conexão perfeitamente correspondida, se houver uma disponível.  
  
 Uma função de classificação no driver pode avaliar uma conexão existente com uma nova solicitação de conexão. Por exemplo, a função de classificação do driver pode determinar:  
  
-   Se a conexão existente for perfeitamente correspondida com a solicitação.  
  
-   Se houver apenas algumas incompatibilidades insignificantes, como tempo limite de conexão, que não exigem comunicação com o servidor a ser redefinido.  
  
-   Se houver alguns atributos incompatíveis que exigem uma comunicação com o servidor para redefinir, mas ainda resultarão em um melhor desempenho do que estabelecer uma nova conexão.  
  
-   Se o erro for incompatível para um atributo que é muito demorado para redefinir (o desenvolvedor do driver pode considerar adicionar esse atributo ao conjunto de atributos de chave, que é usado para gerar a ID do pool).  
  
 Uma pontuação entre 0 e 100 é possível, onde 0 significa não reutilizar e 100 significa perfeitamente correspondido. [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md) é a função para classificar uma conexão.  
  
## <a name="new-odbc-handle---sql_handle_dbc_info_token"></a>Novo identificador ODBC-SQL_HANDLE_DBC_INFO_TOKEN  
 Para dar suporte ao pool de conexões com suporte a Driver, o driver precisa de informações de conexão para calcular a ID do pool. O driver também precisa de informações de conexão para comparar novas solicitações de conexão com conexões no pool.  Sempre que nenhuma conexão no pool puder ser reutilizada, o driver precisará estabelecer uma nova conexão, portanto, exigindo informações de conexão.  
  
 Como as informações de conexão podem vir de várias fontes (cadeia de conexão, atributos de conexão e DSN), o driver pode precisar analisar a cadeia de conexão e resolver o conflito entre essas fontes em cada uma das chamadas de função acima.  
  
 Portanto, um novo identificador ODBC é introduzido: SQL_HANDLE_DBC_INFO_TOKEN. Com o SQL_HANDLE_DBC_INFO_TOKEN, um driver não precisa analisar a cadeia de conexão e resolver conflitos em informações de conexão mais de uma vez. Como essa é uma estrutura de dados específica de driver, o driver pode armazenar dados, como informações de conexão ou ID do pool.  
  
 Esse identificador é usado apenas como uma interface entre o Gerenciador de driver e o driver. Um aplicativo não pode alocar esse identificador diretamente.  
  
 O identificador pai desse identificador é do tipo SQL_HANDLE_ENV, o que significa que o driver pode obter as informações de ambiente do identificador HENV durante a resolução de informações de conexão.  
  
 Sempre que receber uma nova solicitação de conexão, o Gerenciador de driver irá alocar um identificador do tipo SQL_HANDLE_DBC_INFO_TOKEN para armazenar informações de conexão, depois de confirmar que o driver dá suporte ao reconhecimento de pool de conexões. Quando terminar de usar o identificador (mas antes de retornar alguns códigos de retorno diferentes de SQL_STILL_EXECUTING de [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) ou [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)), o Gerenciador de driver liberará o identificador. Portanto, o identificador é criado após a chamada SQLAllocHandle e destruído após a chamada SQLFreeHandle. O Gerenciador de driver garante que o identificador será liberado antes de liberar seu HENV associado (quando [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) ou [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) retornar um erro).  
  
 O driver deve modificar as seguintes funções para aceitar o novo tipo de identificador SQL_HANDLE_DBC_INFO_TOKEN:  
  
1.  [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 O Gerenciador de driver garante que vários threads não usarão o mesmo identificador de SQL_HANDLE_DBC_INFO_TOKEN simultaneamente. Portanto, o modelo de sincronização desse identificador pode ser muito simples dentro do driver. O Gerenciador de driver não usará um bloqueio de ambiente antes de alocar e liberar SQL_HANDLE_DBC_INFO_TOKEN.  
  
 O **SQLAllocHandle** e o **SQLFreeHandle** do Gerenciador de driver não aceitam esse novo tipo de identificador.  
  
 SQL_HANDLE_DBC_INFO_TOKEN pode conter informações confidenciais, como credenciais. Portanto, um driver deve limpar com segurança o buffer de memória (usando [SecureZeroMemory](https://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx)) que contém as informações confidenciais antes de liberar esse identificador com **SQLFreeHandle**. Sempre que o identificador de ambiente de um aplicativo for fechado, todos os pools de conexão associados serão fechados.  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>Algoritmo de classificação do pool de conexões do Gerenciador de driver  
 Esta seção discute o algoritmo de classificação para o pool de conexões do Gerenciador de driver. Os desenvolvedores de driver podem implementar o mesmo algoritmo para compatibilidade com versões anteriores. Esse algoritmo pode não ser o melhor. Você deve refinar esse algoritmo com base na sua implementação (caso contrário, não há motivo para implementar esse recurso).  
  
 O Gerenciador de driver retornará uma classificação integral de 0 a 100 para cada conexão do pool. 0 significa que a conexão não pode ser reutilizada e 100 indica uma correspondência perfeita. Suponha que a solicitação de conexão seja nomeada hRequest e a conexão existente do pool seja nomeada como hCandidate. Se qualquer uma das seguintes condições for falsa, a conexão em pool hCandidate não poderá ser reutilizada para hRequest (o Gerenciador de driver atribuirá uma classificação de 0).  
  
-   hCandidate e hRequest vêm de uma API UNICODE (como SQLDriverConnectW) ou da API ANSI (como SQLDriverConnectA). (Os drivers UNICODE podem ter comportamento diferente da API ANSI e da API UNICODE (consulte o atributo de conexão SQL_ATTR_ANSI_APP).)  
  
-   hCandidate e hRequest são criados pela mesma função; SQLDriverConnect ou SQLConnect.  
  
-   A cadeia de conexão usada para abrir hCandidate deve ser a mesma que hRequest, quando SQLDriverConnect é usado.  
  
-   O ServerName (ou DSN), o nome de usuário e a senha usados para abrir hCandidate devem ser os mesmos usados para abrir o hRequest quando o SQLConnect é usado.  
  
-   O SID (identificador de segurança) do thread atual deve ser o mesmo que o SID usado para abrir o hCandidate.  
  
-   Para o driver que é caro para se inscrever e desinscrever (consulte a discussão de SQL_DTC_TRANSITION_COST em [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)), a reutilização de *hRequest* não deve exigir inscrição extra ou cannela.  
  
 A tabela a seguir mostra a atribuição de Pontuação para diferentes cenários.  
  
|Comparação de atributos de conexão entre a conexão em pool e a solicitação|Nenhuma Inscrição/Desinscrição|Exigir Inscrição/Desinscrição extra|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|O catálogo (SQL_ATTR_CURRENT_CATALOG) é diferente|60|50|  
|Alguns atributos de conexão são diferentes, mas o catálogo é o mesmo|90|70|  
|Todos os atributos de conexão perfeitamente correspondidos|100|80|  
  
## <a name="sequence-diagram"></a>Diagrama de sequências  
 Este diagrama de sequência mostra o mecanismo básico de Pooling descrito neste tópico. Ele mostra apenas o uso de [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) , mas o caso de [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) é semelhante.  
  
 ![Diagrama de sequências](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>Diagrama de estado  
 Esse diagrama de estado mostra o objeto token de informações de conexão, descrito neste tópico. O diagrama mostra apenas [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) , mas o caso de [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) é semelhante. Como o Gerenciador de driver pode precisar manipular erros a qualquer momento, o Gerenciador de driver pode chamar [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md) para qualquer Estado.  
  
 ![Diagrama de estado](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>Consulte Também  
 [Pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Referência da SPI (Interface do Provedor de Serviços) do ODBC](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)

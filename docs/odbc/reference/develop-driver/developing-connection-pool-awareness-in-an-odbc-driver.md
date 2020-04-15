---
title: Desenvolvendo a conscientização do pool de conexões em um driver ODBC | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283426"
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC
Este tópico discute os detalhes do desenvolvimento de um driver ODBC que contém informações sobre como o motorista deve fornecer serviços de pooling de conexão.  
  
## <a name="enabling-driver-aware-connection-pooling"></a>Habilitando o pool de conexões com reconhecimento de driver  
 Um driver deve implementar as seguintes funções De Interface do Provedor de Serviços ODBC (SPI):  
  
-   SQLSetConnectAttrForDbcInfo  
  
-   SQLSetConnectInfo  
  
-   SqlSetDriverConnectInfo  
  
-   Sqlgetpoolid  
  
-   Conexão SQLRate  
  
-   SQLpoolConnect  
  
-   SQLCleanupConnectionPoolID  
  
 Consulte [a referência spi (Service Provider Interface, interface de provedor de serviços odbc)](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md) para obter mais informações.  
  
 O driver também deve implementar as seguintes funções existentes para que o pool de controle de motorista possa ser ativado:  
  
|Função|Funcionalidade adicionada|  
|--------------|-------------------------|  
|[SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|Apoie o novo tipo de alça: SQL_HANDLE_DBC_INFO_TOKEN (veja a descrição abaixo).|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|Suporte ao novo atributo de conexão somente set: SQL_ATTR_DBC_INFO_TOKEN para redefinir a conexão (veja a descrição abaixo).|  
  
> [!NOTE]  
>  Funções depreciadas como **SQLError** e **SQLSetConnectOption** não são suportadas para pool de conexões com reconhecimento de driver.  
  
## <a name="the-pool-id"></a>O ID da Piscina  
 O ID do pool é um ID específico do driver de comprimento de ponteiro para representar um determinado grupo de conexões que podem ser usados de forma intercambiável. Dado um conjunto de informações de conexão, um motorista deve ser capaz de deduzir rapidamente o ID correspondente do pool.  
  
 Por exemplo, o ID do pool deve codificar o nome do servidor e as informações de credencial. No entanto, o nome do banco de dados não é necessário porque um driver pode ser capaz de reutilizar uma conexão e, em seguida, alterar o banco de dados em menos tempo do que fazer uma nova conexão.  
  
 Um driver deve definir um conjunto de atributos-chave, que comporão o ID do pool. O valor desses atributos-chave pode vir de atributos de conexão, string de conexão e DSN. Caso haja conflitos nessas fontes, a política de resolução específica do driver existente deve ser usada para retrocompatibilidade.  
  
 O Driver Manager usará um pool diferente para diferentes IDs de pool. Todas as conexões na mesma piscina são reutilizáveis. O Driver Manager nunca reutilizará uma conexão com um ID de pool diferente.  
  
 Portanto, os drivers devem atribuir um ID de pool exclusivo para cada grupo de conexões com o mesmo valor em seus atributos-chave definidos. Se um driver usar o mesmo ID de pool para duas conexões com valores diferentes em seus atributos principais, o Driver Manager ainda os colocará no mesmo pool (o Driver Manager não sabe nada sobre os atributos de chave específicos do driver). Isso significa que o driver precisará informar ao Gerenciador de driver que uma conexão com um conjunto diferente de atributos-chave não é reutilizável dentro [da função SQLRateConnection Function](../../../odbc/reference/syntax/sqlrateconnection-function.md). Isso pode diminuir o desempenho e isso não é recomendado.  
  
 O Driver Manager não reutilizará uma conexão alocada em outro ambiente do driver, mesmo que todas as informações de conexão sejam correspondias. O Driver Manager usará um pool diferente para ambientes diferentes, mesmo quando as conexões tiverem o mesmo ID de pool. Portanto, o ID da piscina é local para o seu ambiente de motorista.  
  
 A função para obter o ID do pool do driver é [a função SQLGetPoolID .](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
## <a name="the-connection-rating"></a>A classificação de conexão  
 Em comparação com o estabelecimento de uma nova conexão, você pode obter um melhor desempenho redefinindo algumas informações de conexão (como BANCO DE DADOS) em uma conexão agrupada. Assim, você pode não querer que o nome do banco de dados esteja no seu conjunto de atributos-chave. Caso contrário, você pode ter um pool separado para cada banco de dados, o que pode não ser bom em aplicativos intermediários, onde os clientes usam várias strings de conexão diferentes.  
  
 Sempre que você reutilizar uma conexão que tenha alguma incompatibilidade de atributos, você deve redefinir os atributos incompatíveis com base na nova solicitação de aplicativo, de modo que a conexão retornada seja idêntica à solicitação do aplicativo (veja a discussão do atributo SQL_ATTR_DBC_INFO_TOKEN na [função SQLSetConnectAttr](https://go.microsoft.com/fwlink/?LinkId=59368)). No entanto, a redefinição desses atributos pode diminuir o desempenho. Por exemplo, a redefinição de um banco de dados requer uma chamada de rede para o servidor. Portanto, reutilize uma conexão perfeitamente compatível, se estiver disponível.  
  
 Uma função de classificação no driver pode avaliar uma conexão existente com uma nova solicitação de conexão. Por exemplo, a função de classificação do driver pode determinar:  
  
-   Se a conexão existente estiver perfeitamente combinada com a solicitação.  
  
-   Se houver apenas algumas incompatibilidades insignificantes, como o tempo de intervalo de conexão, que não requerem comunicação com o servidor para reiniciar.  
  
-   Se houver alguns atributos incompatíveis que requerem uma comunicação com o servidor para reiniciar, mas ainda assim resultaria em um melhor desempenho do que estabelecer uma nova conexão.  
  
-   Se o incompatível ocorreu para um atributo que é muito demorado para redefinir (o desenvolvedor do driver pode considerar adicionar esse atributo no conjunto de atributos-chave, que é usado para gerar o ID do pool).  
  
 Uma pontuação entre 0 e 100 é possível, onde 0 significa não reutilizar e 100 significa perfeitamente compatível. [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md) é a função para classificar uma conexão.  
  
## <a name="new-odbc-handle---sql_handle_dbc_info_token"></a>Nova alça ODBC - SQL_HANDLE_DBC_INFO_TOKEN  
 Para suportar o pool de conexões com reconhecimento de driver, o motorista precisa de informações de conexão para calcular o Pool ID. O driver também precisa de informações de conexão para comparar novas solicitações de conexão com conexões no pool.  Sempre que nenhuma conexão no pool pode ser reutilizada, o motorista tem que estabelecer uma nova conexão, exigindo assim informações de conexão.  
  
 Uma vez que as informações de conexão podem vir de várias fontes (seqüência de conexão, atributos de conexão e DSN), o driver pode precisar analisar a cadeia de conexão e resolver o conflito entre essas fontes em cada uma das chamadas de função acima.  
  
 Por isso, uma nova alça ODBC é introduzida: SQL_HANDLE_DBC_INFO_TOKEN. Com SQL_HANDLE_DBC_INFO_TOKEN, um driver não precisa analisar a cadeia de conexão e resolver conflitos em informações de conexão mais de uma vez. Como se trata de uma estrutura de dados específica do driver, o motorista pode armazenar dados como informações de conexão ou ID de pool.  
  
 Esta alça é usada apenas como uma interface entre o Driver Manager e o driver. Um aplicativo não pode alocar essa alça diretamente.  
  
 A alça pai desta alça é de tipo SQL_HANDLE_ENV, o que significa que o motorista pode obter as informações do ambiente a partir do cabo HENV durante a resolução das informações de conexão.  
  
 Sempre que receber uma nova solicitação de conexão, o Driver Manager alocará uma alça do tipo SQL_HANDLE_DBC_INFO_TOKEN para armazenar informações de conexão, depois de confirmar que o driver suporta a conscientização do pool de conexões. Quando terminar de usar a alça (mas antes de retornar alguns códigos de retorno que não sejam SQL_STILL_EXECUTING do [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) ou [SQLConnect),](../../../odbc/reference/syntax/sqlconnect-function.md)o Driver Manager liberará a alça. Portanto, a alça é criada após a chamada SQLAllocHandle e destruída após a chamada SQLFreeHandle. O Driver Manager garante que a alça será liberada antes de liberar seu HENV associado (quando [o SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) ou [o SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) retornar em um erro).  
  
 O driver deve modificar as seguintes funções para aceitar o novo tipo de alça SQL_HANDLE_DBC_INFO_TOKEN:  
  
1.  [SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 O Driver Manager garante que vários segmentos não usarão o mesmo SQL_HANDLE_DBC_INFO_TOKEN manusear simultaneamente. Portanto, o modelo de sincronização desta alça pode ser muito simples dentro do driver. O Driver Manager não fará um bloqueio de ambiente antes de alocar e liberar SQL_HANDLE_DBC_INFO_TOKEN.  
  
 O **SQLAllocHandle** e **o SQLFreeHandle** do Driver Manager não aceitarão esse novo tipo de alça.  
  
 SQL_HANDLE_DBC_INFO_TOKEN podem conter informações confidenciais, como credenciais. Portanto, um driver deve limpar com segurança o buffer de memória (usando [SecureZeroMemory](https://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx)) que contém as informações confidenciais antes de liberar esta alça com **SQLFreeHandle**. Sempre que a alça do ambiente de um aplicativo estiver fechada, todas as piscinas de conexão associadas serão fechadas.  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>Algoritmo de classificação do pool de conexão do driver manager  
 Esta seção discute o algoritmo de classificação para pool de conexão Driver Manager. Os desenvolvedores de drivers podem implementar o mesmo algoritmo para compatibilidade retrógrada. Este algoritmo pode não ser o melhor. Você deve refinar este algoritmo com base na sua implementação (caso contrário, não há razão para implementar esse recurso).  
  
 O Driver Manager retornará uma classificação integral de 0 a 100 para cada conexão do pool. 0 significa que a conexão não pode ser reutilizada e 100 indica uma combinação perfeita. Suponha que a solicitação de conexão seja nomeada hSolicit e a conexão existente no pool seja nomeada como hCandidate. Se qualquer uma das seguintes condições for falsa, o hCandidate de conexão agrupada não poderá ser reutilizado para hRequest (o Driver Manager atribuirá uma classificação de 0).  
  
-   hCandidate e hRequest ambos vêm da API UNICODE (como sqldriverconnectW) ou da ANSI API (como o SQLDriverConnectA). (Os drivers UNICODE podem se compor diferenteda API ANSI e API UNICODE (veja o atributo de conexão SQL_ATTR_ANSI_APP).)  
  
-   hCandidate e hRequest são criados pela mesma função; SQLDriverConnect ou SQLConnect.  
  
-   A seqüência de conexões usada para abrir hCandidate deve ser a mesma do hRequest, quando o SQLDriverConnect é usado.  
  
-   O ServerName (ou DSN), nome de usuário e senha usado supérfluo deve ser o mesmo usado para abrir hRequest quando o SQLConnect é usado.  
  
-   O identificador de segurança (SID) do segmento atual deve ser o mesmo que o SID usado para abrir o hCandidate.  
  
-   Para driver que é caro para se alistar e não se alistar (ver a discussão de SQL_DTC_TRANSITION_COST no [SQLConnect),](../../../odbc/reference/syntax/sqlconnect-function.md)a reutilização *hRequest* não deve exigir um alistamento extra ou desalistamento.  
  
 A tabela a seguir mostra a atribuição de pontuação para diferentes cenários.  
  
|Comparação entre os atributos de conexão entre a conexão agrupada e a solicitação|Sem alistamento/ desalistamento|Exigir alistamento extra / desalistamento|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|Catálogo (SQL_ATTR_CURRENT_CATALOG) é diferente|60|50|  
|Alguns atributos de conexão são diferentes, mas o catálogo é o mesmo|90|70|  
|Todos os atributos de conexão combinavam perfeitamente|100|80|  
  
## <a name="sequence-diagram"></a>Diagrama de sequências  
 Este diagrama de seqüência mostra o mecanismo básico de agrupamento descrito neste tópico. Ele só mostra o uso do [SQLDriverConnect,](../../../odbc/reference/syntax/sqldriverconnect-function.md) mas o caso [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) é semelhante.  
  
 ![Diagrama de sequências](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>Diagrama de estado  
 Este diagrama de estado mostra o objeto token de informações de conexão, descrito neste tópico. O diagrama mostra apenas [SQLDriverConnect,](../../../odbc/reference/syntax/sqldriverconnect-function.md) mas o caso [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) é semelhante. Uma vez que o Gerenciador de driver pode precisar lidar com erros a qualquer momento, o Gerenciador de driver pode chamar [sQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md) para qualquer estado.  
  
 ![Diagrama de estado](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>Consulte Também  
 [Pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Referência da SPI (Interface do Provedor de Serviços) do ODBC](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)

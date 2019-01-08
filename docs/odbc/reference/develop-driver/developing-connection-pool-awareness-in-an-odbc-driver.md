---
title: Desenvolvendo o reconhecimento de Pool de Conexão em um Driver ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: c63d5cae-24fc-4fee-89a9-ad0367cddc3e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b82e56dd7998ca19ce9e401369cd8d2f52b58573
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52417367"
---
# <a name="developing-connection-pool-awareness-in-an-odbc-driver"></a>Desenvolvimento um reconhecimento de pool de conexão em um driver ODBC
Este tópico discute os detalhes do desenvolvimento de um driver ODBC que contém informações sobre como o driver deve fornecer os serviços de pooling de conexão.  
  
## <a name="enabling-driver-aware-connection-pooling"></a>Habilitando o Pooling de Conexão de reconhecimento de Driver  
 Um driver deve implementar as seguintes funções de ODBC Service Provider Interface (SPI):  
  
-   SQLSetConnectAttrForDbcInfo  
  
-   SQLSetConnectInfo  
  
-   SQLSetDriverConnectInfo  
  
-   SQLGetPoolID  
  
-   SQLRateConnection  
  
-   SQLPoolConnect  
  
-   SQLCleanupConnectionPoolID  
  
 Ver [referência de Interface de provedor de serviço (SPI) ODBC](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md) para obter mais informações.  
  
 Um driver também deve implementar as seguintes funções existentes para que o pool de reconhecimento de driver pode ser habilitado:  
  
|Função|Funcionalidade adicionada|  
|--------------|-------------------------|  
|[Falha de SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)<br /><br /> [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)<br /><br /> [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)<br /><br /> [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)|Suporte para o novo tipo de identificador: SQL_HANDLE_DBC_INFO_TOKEN (consulte a descrição abaixo).|  
|[SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|Suporte para o novo atributo de conexão somente conjunto: SQL_ATTR_DBC_INFO_TOKEN para redefinir a conexão (consulte a descrição abaixo).|  
  
> [!NOTE]  
>  Funções preteridas, como **SQLError** e **SQLSetConnectOption** não têm suporte para o pool de conexão de reconhecimento de driver.  
  
## <a name="the-pool-id"></a>A ID do Pool  
 A ID do pool é uma ID de específicos do driver de tamanho de ponteiro para representar um determinado grupo de conexões que podem ser usados alternadamente. Dado um conjunto de informações de conexão, um driver deve ser capaz de deduzir rapidamente a ID do pool correspondente.  
  
 Por exemplo, a ID do pool deve codificar as informações de nome e uma credencial do servidor. No entanto, o nome do banco de dados não é necessário porque um driver pode ser capaz de reutilizar uma conexão e, em seguida, altere o banco de dados em menos tempo do que fazer uma nova conexão.  
  
 Um driver deve definir um conjunto de atributos de chave, que compõem a ID do pool. O valor desses atributos chave pode vir de atributos de conexão, a cadeia de caracteres de conexão e o DSN. Caso haja qualquer conflito dessas origens, a política de resolução específicos do driver, existente, deve ser usada para compatibilidade com versões anteriores.  
  
 O Gerenciador de Driver usará um pool diferente para diferentes IDs do pool. Todas as conexões no mesmo pool são reutilizáveis. O Gerenciador de Driver nunca reutilizará uma conexão com uma ID do pool diferente.  
  
 Portanto drivers devem atribuir uma ID de pool exclusivo para cada grupo de conexões com o mesmo valor em seus atributos chave definidos. Se um driver usa a mesma ID do pool para duas conexões com valores diferentes em seus atributos de chave, o Gerenciador de Driver continuará colocando-los no mesmo pool (o Gerenciador de Driver sabe nada sobre os atributos de chave específicos do driver). Isso significa que o driver será necessário relatar para o Gerenciador de Driver que uma conexão com um conjunto diferente de atributos de chave não é reutilizável dentro [função SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md). Isso pode diminuir o desempenho e isso não é recomendado.  
  
 O Gerenciador de Driver não reutilizará uma conexão alocado de outro ambiente de driver, mesmo se correspondem a todas as informações de conexão. O Gerenciador de Driver usará um pool diferente para um ambiente diferente, mesmo quando as conexões têm a mesma ID do pool. Portanto, a ID do pool é local para seu ambiente de driver.  
  
 É a função para obter a ID do pool de driver [função SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md).  
  
## <a name="the-connection-rating"></a>A classificação de Conexão  
 Em comparação com o estabelecimento de uma nova conexão, você pode obter um melhor desempenho, redefinindo algumas informações de conexão (por exemplo, o banco de dados) em uma conexão em pool. Portanto, você pode não querer o nome do banco de dados em seu conjunto de atributos de chave. Caso contrário, você pode ter um pool separado para cada banco de dados, que pode não ser bom em aplicativos de camada intermediária, em que os clientes usam várias cadeias de caracteres de conexão diferente.  
  
 Sempre que você reutilize uma conexão que tem alguma incompatibilidade do atributo, você deve redefinir os atributos incompatíveis com base na nova solicitação de aplicativo, para que a conexão retornada é idêntica à solicitação de aplicativo (consulte a discussão sobre o atributo SQL_ATTR _DBC_INFO_TOKEN na [função SQLSetConnectAttr](https://go.microsoft.com/fwlink/?LinkId=59368)). No entanto, redefinir esses atributos pode diminuir o desempenho. Por exemplo, a redefinição de um banco de dados requer uma chamada de rede ao servidor. Portanto, reutilize uma conexão que é correspondida perfeitamente, se houver uma disponível.  
  
 Uma função de classificação no driver pode avaliar uma conexão existente com uma nova solicitação de conexão. Por exemplo, a função de classificação do driver pode determinar:  
  
-   Se a conexão existente é perfeitamente correspondente com a solicitação.  
  
-   Se houver apenas algumas insignificantes incompatibilidades, como o tempo limite de conexão, que não exigem comunicação com o servidor a redefinir.  
  
-   Se houver alguns atributos incompatíveis que exigem uma comunicação com o servidor para a redefinição, mas ainda pode resultar em desempenho melhor do que o estabelecimento de uma nova conexão.  
  
-   Se o incompatíveis ocorreram para um atributo que é muito demorado redefinir (o desenvolvedor do driver, considere adicionar esse atributo no conjunto de atributos de chave, que é usado para gerar a ID do pool).  
  
 Uma pontuação entre 0 e 100 é possível, onde 0 significa não reutilize e 100 significa que perfeitamente adequados. [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md) é a função de classificação de uma conexão.  
  
## <a name="new-odbc-handle---sqlhandledbcinfotoken"></a>Novo identificador ODBC - SQL_HANDLE_DBC_INFO_TOKEN  
 Para dar suporte a pool de conexão reconhecimento de driver, o driver precisa de informações de conexão para calcular a ID do Pool. O driver também precisa de informações de conexão a ser comparado a novas solicitações de conexão com conexões no pool.  Sempre que pode ser reutilizada sem conexão no pool, o driver deve estabelecer uma nova conexão, exigindo, portanto, as informações de conexão.  
  
 Como as informações de conexão podem vir de várias fontes (cadeia de caracteres de conexão, os atributos de conexão e DSN), o driver seja necessário analisar a cadeia de caracteres de conexão e resolver o conflito entre essas fontes em cada chamada de função acima.  
  
 Portanto, foi introduzido um novo identificador ODBC: SQL_HANDLE_DBC_INFO_TOKEN. Com SQL_HANDLE_DBC_INFO_TOKEN, um driver não precisa analisar a cadeia de conexão e resolver conflitos em informações de conexão de mais de uma vez. Como essa é uma estrutura de dados específicos do driver, o driver pode armazenar dados, como informações de conexão ou ID do pool.  
  
 Esse identificador é usado apenas como uma interface entre o Gerenciador de Driver e o driver. Um aplicativo não pode alocar esse identificador diretamente.  
  
 O identificador pai deste identificador é do tipo SQL_HANDLE_ENV, que significa que o driver pode obter as informações de ambiente do identificador HENV durante a resolução de informações de conexão.  
  
 Sempre que receber uma nova solicitação de conexão, o Gerenciador de Driver será alocar um identificador de tipo SQL_HANDLE_DBC_INFO_TOKEN para armazenar informações de conexão, depois que ela confirma que o driver dá suporte a reconhecimento de pool de conexão. Quando concluído usando o identificador (mas antes de retornar alguns códigos diferente de SQL_STILL_EXECUTING a partir de retorno [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) ou [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)), o Gerenciador de Driver irá liberar o identificador. Portanto, o identificador é criado após a chamada de SQLAllocHandle e destruído após a chamada SQLFreeHandle. O Gerenciador de Driver garante que o identificador será liberado antes de liberar seu HENV associado (quando [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) ou [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) retornará um erro).  
  
 O driver deve modificar as seguintes funções para aceitar o novo tipo de identificador SQL_HANDLE_DBC_INFO_TOKEN:  
  
1.  [Falha de SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)  
  
2.  [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md)  
  
3.  [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)  
  
4.  [SQLGetDiagRec](../../../odbc/reference/syntax/sqlgetdiagrec-function.md)  
  
 O Gerenciador de Driver garante que vários threads não usará o mesmo identificador SQL_HANDLE_DBC_INFO_TOKEN simultaneamente. Portanto, o modelo de sincronização desse identificador pode ser muito simple no driver. O Gerenciador de Driver não terão um bloqueio de ambiente antes de alocar e liberar SQL_HANDLE_DBC_INFO_TOKEN.  
  
 O Gerenciador de Driver **SQLAllocHandle** e **SQLFreeHandle** não aceitará esse novo tipo de identificador.  
  
 SQL_HANDLE_DBC_INFO_TOKEN podem conter informações confidenciais, como credenciais. Portanto, um driver com segurança deve limpar o buffer de memória (usando [SecureZeroMemory](https://msdn.microsoft.com/library/windows/desktop/aa366877\(v=vs.85\).aspx)) que contém as informações confidenciais antes de liberar esse identificador com **SQLFreeHandle**. Sempre que o identificador de ambiente do aplicativo é fechado, todos os pools de conexão associada serão fechados.  
  
## <a name="driver-manager-connection-pool-rating-algorithm"></a>Pool de Conexão do Gerenciador de driver de algoritmo de classificação  
 Esta seção discute o algoritmo de classificação para o pool de conexão do Gerenciador de Driver. Os desenvolvedores de driver podem implementar o mesmo algoritmo para compatibilidade com versões anteriores. Esse algoritmo não pode ser melhor. Você deverá refinar esse algoritmo com base em sua implementação (caso contrário, há nenhum motivo para implementar esse recurso).  
  
 O Gerenciador de Driver retornará uma classificação integral de 0 a 100 para cada conexão do pool. 0 significa que a conexão não pode ser reutilizada e 100 indica a correspondência de um perfeito. Suponha que a solicitação de conexão é denominada hRequest, e a conexão existente do pool como hCandidate. Se qualquer uma das seguintes condições for false, o hCandidate de conexão em pool não pode ser reutilizado para hRequest (o Gerenciador de Driver atribuirá uma classificação de 0).  
  
-   hCandidate e hRequest vêm de API do UNICODE (por exemplo, SQLDriverConnectW) ou ANSI API (por exemplo, SQLDriverConnectA). (Drivers do UNICODE podem comportamento diferente considerando API ANSI e UNICODE API (consulte o atributo de conexão SQL_ATTR_ANSI_APP).)  
  
-   hCandidate e hRequest são criados na mesma função; SQLDriverConnect ou SQLConnect.  
  
-   A cadeia de caracteres de conexão usada para abrir hCandidate deve ser o mesmo que hRequest, quando SQLDriverConnect é usado.  
  
-   O nome de usuário ServerName (ou DSN), e a senha usada para abrir hCandidate deve ser o mesmo usado para abrir hRequest quando SQLConnect é usado.  
  
-   O identificador de segurança (SID) do thread atual deve ser o mesmo como o SID usado para abrir hCandidate.  
  
-   Para o driver é caro para se inscrever e inscrição (veja a discussão de SQL_DTC_TRANSITION_COST na [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)), reutilizando *hRequest* não deve exigir uma inscrição adicional ou unenlistment.  
  
 A tabela a seguir mostra a atribuição de pontuação para cenários diferentes.  
  
|Comparação em atributos de conexão entre a conexão em pool e a solicitação|Nenhuma inscrição / unenlistment|Exige a inscrição Extra / Unenlistment|  
|---------------------------------------------------------------------------------------|-----------------------------------|----------------------------------------------|  
|Catálogo (SQL_ATTR_CURRENT_CATALOG) é diferente|60|50|  
|Alguns atributos de conexão são diferentes, mas o catálogo é o mesmo|90|70|  
|Todos os atributos de conexão perfeitamente adequados|100|80|  
  
## <a name="sequence-diagram"></a>Diagrama de sequências  
 Este diagrama de sequência mostra o mecanismo básico de pooling descrito neste tópico. Ela mostra o uso de apenas [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) , mas o [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) caso é semelhante.  
  
 ![Diagrama de sequência](../../../odbc/reference/develop-driver/media/odbc_seq_dia.gif "odbc_seq_dia")  
  
## <a name="state-diagram"></a>Diagrama de estado  
 Este diagrama de estado mostra conexão info objeto de token, descrito neste tópico. O diagrama mostra apenas [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) , mas o [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md) caso é semelhante. Uma vez que o Gerenciador de Driver, talvez seja necessário tratar os erros a qualquer momento, o Gerenciador de Driver pode chamar [SQLFreeHandle](../../../odbc/reference/syntax/sqlfreehandle-function.md) para qualquer estado.  
  
 ![Diagrama de estado](../../../odbc/reference/develop-driver/media/odbc_state_diagram.gif "odbc_state_diagram")  
  
## <a name="see-also"></a>Consulte também  
 [Pooling de Conexão de reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md)   
 [Referência da SPI (Interface do Provedor de Serviços) do ODBC](../../../odbc/reference/syntax/odbc-service-provider-interface-spi-reference.md)

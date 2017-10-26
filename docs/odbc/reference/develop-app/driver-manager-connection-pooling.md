---
title: "Pooling de Conexão de Gerenciador de driver | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connection pooling [ODBC]
- pooled connections [ODBC]
- connecting to driver [ODBC], connection pooling
- connecting to data source [ODBC], connection pooling
ms.assetid: ee95ffdb-5aa1-49a3-beb2-7695b27c3df9
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b589f7aa0e110767b7dca9be7aa82edee486b058
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="driver-manager-connection-pooling"></a>Pooling de Conexão de Gerenciador de driver
O pool de Conexão permite que um aplicativo para usar uma conexão de um pool de conexões que não precisam ser restabelecida para cada uso. Depois que uma conexão foi criado e colocado em um pool, um aplicativo pode reutilizar essa conexão sem executar o processo de conexão completa.  
  
 Usar uma conexão em pool pode resultar em ganhos significativos de desempenho, porque os aplicativos podem salvar a sobrecarga envolvida em estabelecer uma conexão. Isso pode ser particularmente significativo para aplicativos de camada intermediária que se conectam através de uma rede ou para aplicativos que se conectar e desconectarem, como aplicativos de Internet repetidamente.  
  
 Além de ganhos de desempenho, a arquitetura do pool de conexão permite que um ambiente e suas conexões associadas a ser usado por vários componentes em um único processo. Isso significa que componentes autônomos no mesmo processo podem interagir entre si sem conhecimento uns dos outros. Uma conexão em um pool de conexão pode ser usada repetidamente por vários componentes.  
  
> [!NOTE]  
>  Pooling de Conexão pode ser usado por um aplicativo ODBC apresentando ODBC 2. *x* comportamento, desde que o aplicativo pode chamar *SQLSetEnvAttr*. Ao usar o pooling de conexão, o aplicativo não deve executar instruções SQL que alterar o banco de dados ou o contexto do banco de dados, como alterar o \< *banco de dados**nome*>, que Altera o catálogo usado por uma fonte de dados.  
  
 Um driver ODBC deve ser totalmente thread-safe, e as conexões não devem ter afinidade de threads para dar suporte ao pooling de conexão. Isso significa que o driver é capaz de lidar com uma chamada em qualquer segmento a qualquer momento e é capaz de se conectar em um thread, para usar a conexão em outro thread e para desconectá-lo em um thread de terceiro.  
  
 O pool de conexão é mantido pelo Gerenciador de Driver. Conexões são desenhadas no pool de quando o aplicativo chama **SQLConnect** ou **SQLDriverConnect** e são retornadas ao pool quando o aplicativo chama **SQLDisconnect**. O tamanho do pool de aumenta dinamicamente, com base nas alocações de recurso solicitado. Ele diminui com base no tempo limite de inatividade: se uma conexão estiver inativa por um período de tempo (ele não foi usado em uma conexão), ele será removido do pool. O tamanho do pool é limitado somente por restrições de memória e limites no servidor.  
  
 O Gerenciador de Driver determina se uma conexão específica em um pool de deve ser usado de acordo com os argumentos passados em **SQLConnect** ou **SQLDriverConnect**e de acordo com os atributos de conexão Defina após a conexão foi alocada.  
  
 Quando o Gerenciador de Driver é pooling de conexões, ele precisa ser capaz de determinar se uma conexão ainda está funcionando antes de enviar a conexão. Caso contrário, o Gerenciador de Driver mantém em enviar a conexão inativa para o aplicativo sempre que ocorrer uma falha de rede transitório. Um novo atributo de conexão foi definido em ODBC 3*. x*: SQL_ATTR_CONNECTION_DEAD. Este é um atributo de conexão somente leitura que retornará SQL_CD_TRUE ou SQL_CD_FALSE. O valor SQL_CD_TRUE significa que a conexão foi perdida, enquanto o valor SQL_CD_FALSE significa que a conexão ainda está ativa. (Drivers de acordo com as versões anteriores do ODBC podem também dar suporte a esse atributo.)  
  
 Um driver deve implementar essa opção com eficiência, ou ele será prejudicar o desempenho do pool de conexão. Especificamente, uma chamada para obter esse atributo de conexão não deve causar uma viagem para o servidor. Em vez disso, um driver de apenas deve retornar o último estado de conexão. A conexão é inativa se o último processamento para o servidor falhou e não inativo se o último processamento foi bem-sucedida.  
  
## <a name="remarks"></a>Comentários  
 Se uma conexão foi perdida (relatada por SQL_ATTR_CONNECTION_DEAD), o Gerenciador de Driver ODBC destruirá essa conexão chamando SQLDisconnect no driver. Novas solicitações de conexão não podem localizar uma conexão utilizável no pool. Eventualmente o Gerenciador de Driver pode fazer uma nova conexão, supondo que o pool está vazio.  
  
 Para usar um pool de conexão, um aplicativo executa as seguintes etapas:  
  
1.  Permite que o pool de conexão chamando **SQLSetEnvAttr** para definir o atributo de ambiente SQL_ATTR_CONNECTION_POOLING SQL_CP_ONE_PER_DRIVER ou SQL_CP_ONE_PER_HENV. Essa chamada deve ser feita antes do aplicativo aloca o ambiente compartilhado para o qual conexão pooling será habilitada. O identificador de ambiente na chamada para **SQLSetEnvAttr** deve ser definido como null, o que torna SQL_ATTR_CONNECTION_POOLING um atributo de nível de processo. Se o atributo é definido como SQL_CP_ONE_PER_DRIVER, um pool de conexão única tem suporte para cada driver. Se um aplicativo funciona com muitos drivers e alguns ambientes, isso pode ser mais eficiente porque menos comparações podem ser necessárias. Se definido como SQL_CP_ONE_PER_HENV, um pool de conexão única é suportado para cada ambiente. Se um aplicativo funciona com alguns drivers e de muitos ambientes, isso pode ser mais eficiente porque menos comparações podem ser necessárias. Pooling de Conexão está desativado, definindo SQL_ATTR_CONNECTION_POOLING para SQL_CP_OFF.  
  
2.  Aloca um ambiente chamando **SQLAllocHandle** com o *HandleType* argumento definido como SQL_HANDLE_ENV. O ambiente alocado por essa chamada será um ambiente compartilhado implícito porque o pool de conexão foi ativado. O ambiente a ser usado não é determinado, no entanto, enquanto **SQLAllocHandle** com um *HandleType* SQL_HANDLE_DBC é chamado neste ambiente.  
  
3.  Aloca uma conexão chamando **SQLAllocHandle** com *InputHandle* definido como SQL_HANDLE_DBC e o *InputHandle* definido como o identificador de ambiente alocado para pool de conexão. O Gerenciador de Driver tenta encontrar um ambiente existente que correspondem aos atributos de ambiente definidos pelo aplicativo. Se tal ambiente não existir, um será criado, com uma contagem de referência (mantida pelo Gerenciador de Driver) de 1. Se um ambiente compartilhado correspondente for encontrado, o ambiente é retornado para o aplicativo e sua contagem de referência é incrementada. (A conexão atual a ser usado não é determinado pelo Gerenciador de Driver até **SQLConnect** ou **SQLDriverConnect** é chamado.)  
  
4.  Chamadas **SQLConnect** ou **SQLDriverConnect** para fazer a conexão. O Gerenciador de Driver usa as opções de conexão na chamada para **SQLConnect** (ou as palavras-chave de conexão na chamada para **SQLDriverConnect**) e os atributos de conexão definidos após a alocação de conexão Determine qual conexão no pool deve ser usado.  
  
    > [!NOTE]  
    >  Como uma conexão solicitada está de acordo com uma conexão em pool é determinada pelo atributo SQL_ATTR_CP_MATCH ambiente. Para obter mais informações, consulte [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
     Aplicativos ODBC usando o pool de conexão devem chamar [CoInitializeEx](http://go.microsoft.com/fwlink/?LinkID=116307) durante a inicialização do aplicativo e [CoUninitialize](http://go.microsoft.com/fwlink/?LinkId=116310) quando o aplicativo for fechado.  
  
5.  Chamadas **SQLDisconnect** quando concluir a conexão. A conexão é retornado para o pool de conexão e se torna disponível para reutilização.  
  
 Para uma discussão mais profunda, consulte [pool no Microsoft Data Access Components](http://go.microsoft.com/fwlink/?LinkId=120776).  
  
## <a name="connection-pooling-considerations"></a>Considerações sobre o pool de Conexão  
 Executar qualquer uma das ações a seguir usando um comando SQL (em vez de por meio da API do ODBC) pode afetar o estado da conexão e causar problemas inesperados ao pooling de conexão está ativa:  
  
-   Abrir uma conexão e alterar o banco de dados padrão.  
  
-   Usando a instrução SET para alterar as opções configuráveis (incluindo SET ROWCOUNT, ANSI_NULL, IMPLICIT_TRANSACTIONS, plano de execução, estatísticas, tamanho do texto e DATEFORMAT).  
  
-   Criando tabelas temporárias e procedimentos armazenados.  
  
 Se qualquer uma das seguintes ações são executadas fora do API do ODBC, o próximo usuário que usa a conexão herdarão automaticamente as configurações anteriores, tabelas ou procedimentos.  
  
> [!NOTE]  
>  Não espera que certas configurações no estado de conexão. Você sempre deve definir o estado de conexão em seu aplicativo e certifique-se de que o aplicativo remove qualquer configurações do pool de conexão não utilizado.  
  
## <a name="driver-aware-connection-pooling"></a>Pool de conexões com reconhecimento de driver  
 Começando no Windows 8, um driver ODBC pode usar conexões no pool de forma mais eficiente. Para obter mais informações, consulte [Pooling de Conexão com reconhecimento de Driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
## <a name="see-also"></a>Consulte também  
 [Conectando a dados de um fonte ou Driver](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pool no Microsoft Data Access Components](http://go.microsoft.com/fwlink/?LinkId=120776)


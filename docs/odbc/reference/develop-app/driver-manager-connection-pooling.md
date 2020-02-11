---
title: Pool de conexões do Gerenciador de driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection pooling [ODBC]
- pooled connections [ODBC]
- connecting to driver [ODBC], connection pooling
- connecting to data source [ODBC], connection pooling
ms.assetid: ee95ffdb-5aa1-49a3-beb2-7695b27c3df9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 92aab28274d3709047e46c55192b437449e252ac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68047016"
---
# <a name="driver-manager-connection-pooling"></a>Pool de conexões do Gerenciador de Driver
O pool de conexões permite que um aplicativo use uma conexão de um pool de conexões que não precisam ser restabelecidas para cada uso. Depois que uma conexão é criada e colocada em um pool, um aplicativo pode reutilizar essa conexão sem executar o processo de conexão completa.  
  
 O uso de uma conexão em pool pode resultar em ganhos de desempenho significativos, pois os aplicativos podem economizar a sobrecarga envolvida na criação de uma conexão. Isso pode ser particularmente significativo para aplicativos de camada intermediária que se conectam por uma rede ou para aplicativos que se conectam e desconectam repetidamente, como aplicativos de Internet.  
  
 Além dos ganhos de desempenho, a arquitetura de pooling de conexão permite que um ambiente e suas conexões associadas sejam usados por vários componentes em um único processo. Isso significa que os componentes autônomos no mesmo processo podem interagir entre si sem estar cientes uns dos outros. Uma conexão em um pool de conexões pode ser usada repetidamente por vários componentes.  
  
> [!NOTE]
>  O pooling de conexão pode ser usado por um aplicativo ODBC que exibe o ODBC 2. comportamento *x* , contanto que o aplicativo possa chamar *SQLSetEnvAttr*. Ao usar o pool de conexões, o aplicativo não deve executar instruções SQL que alteram o banco de dados ou o contexto do banco de dados \<, como alterar o *nome do banco* de dados>, que altera o catálogo usado por uma fonte de dado.  


 Um driver ODBC deve ser totalmente seguro para thread e as conexões não devem ter afinidade de thread para dar suporte ao pooling de conexão. Isso significa que o driver é capaz de lidar com uma chamada em qualquer thread a qualquer momento e pode se conectar em um thread, para usar a conexão em outro thread e para se desconectar em um terceiro thread.  
  
 O pool de conexões é mantido pelo Gerenciador de driver. As conexões são desenhadas do pool quando o aplicativo chama **SQLConnect** ou **SQLDriverConnect** e retorna ao pool quando o aplicativo chama **SQLDisconnect**. O tamanho do pool aumenta dinamicamente, com base nas alocações de recursos solicitadas. Ele diminui com base no tempo limite de inatividade: se uma conexão estiver inativa por um período de tempo (ela não foi usada em uma conexão), ela será removida do pool. O tamanho do pool é limitado apenas por restrições de memória e limites no servidor.  
  
 O Gerenciador de driver determina se uma conexão específica em um pool deve ser usada de acordo com os argumentos passados em **SQLConnect** ou **SQLDriverConnect**e de acordo com os atributos de conexão definidos depois que a conexão foi alocada.  
  
 Quando o Gerenciador de driver está pooling de conexões, ele precisa ser capaz de determinar se uma conexão ainda está funcionando antes de entregar a conexão. Caso contrário, o Gerenciador de driver continua a distribuir a conexão inativa para o aplicativo sempre que ocorrer uma falha de rede transitória. Um novo atributo de conexão foi definido no ODBC 3 *. x*: SQL_ATTR_CONNECTION_DEAD. Esse é um atributo de conexão somente leitura que retorna SQL_CD_TRUE ou SQL_CD_FALSE. O valor SQL_CD_TRUE significa que a conexão foi perdida, enquanto o valor SQL_CD_FALSE significa que a conexão ainda está ativa. (Os drivers que estão em conformidade com as versões anteriores do ODBC também podem dar suporte a esse atributo.)  
  
 Um driver deve implementar essa opção de forma eficiente ou prejudicará o desempenho do pool de conexões. Especificamente, uma chamada para obter esse atributo de conexão não deve causar uma viagem de ida e volta ao servidor. Em vez disso, um driver deve retornar apenas o último estado conhecido da conexão. A conexão ficará inativa se a última viagem ao servidor falhar e não ficar inoperante se a última viagem tiver sido bem-sucedida.  
  
## <a name="remarks"></a>Comentários  
 Se uma conexão tiver sido perdida (relatada via SQL_ATTR_CONNECTION_DEAD), o Gerenciador de driver ODBC destruirá essa conexão chamando SQLDisconnect no driver. Novas solicitações de conexão podem não encontrar uma conexão utilizável no pool. Eventualmente, o Gerenciador de driver pode fazer uma nova conexão, supondo que o pool esteja vazio.  
  
 Para usar um pool de conexões, um aplicativo executa as seguintes etapas:  
  
1.  Habilita o pool de conexões chamando **SQLSetEnvAttr** para definir o atributo de ambiente SQL_ATTR_CONNECTION_POOLING como SQL_CP_ONE_PER_DRIVER ou SQL_CP_ONE_PER_HENV. Essa chamada deve ser feita antes que o aplicativo aloque o ambiente compartilhado para o qual o pool de conexões deve ser habilitado. O identificador de ambiente na chamada para **SQLSetEnvAttr** deve ser definido como NULL, o que faz SQL_ATTR_CONNECTION_POOLING um atributo de nível de processo. Se o atributo for definido como SQL_CP_ONE_PER_DRIVER, um único pool de conexões terá suporte para cada driver. Se um aplicativo funcionar com muitos drivers e poucos ambientes, isso pode ser mais eficiente, pois menos comparações podem ser necessárias. Se estiver definido como SQL_CP_ONE_PER_HENV, um único pool de conexões terá suporte para cada ambiente. Se um aplicativo funcionar com muitos ambientes e poucos drivers, isso pode ser mais eficiente, pois menos comparações podem ser necessárias. O pool de conexões é desabilitado pela configuração de SQL_ATTR_CONNECTION_POOLING para SQL_CP_OFF.  
  
2.  Aloca um ambiente chamando **SQLAllocHandle** com o argumento *HandleType* definido como SQL_HANDLE_ENV. O ambiente alocado por essa chamada será um ambiente compartilhado implícito porque o pool de conexões foi habilitado. O ambiente a ser usado não é determinado, no entanto, até que **SQLAllocHandle** com um *handletype* de SQL_HANDLE_DBC seja chamado nesse ambiente.  
  
3.  Aloca uma conexão chamando **SQLAllocHandle** com *InputHandle* definido como SQL_HANDLE_DBC e o *InputHandle* definido como o identificador de ambiente alocado para o pool de conexões. O Gerenciador de driver tenta localizar um ambiente existente que corresponda aos atributos de ambiente definidos pelo aplicativo. Se esse ambiente não existir, um será criado, com uma contagem de referência (mantida pelo Gerenciador de driver) de 1. Se um ambiente compartilhado correspondente for encontrado, o ambiente será retornado para o aplicativo e sua contagem de referência será incrementada. (A conexão real a ser usada não é determinada pelo Gerenciador de driver até que **SQLConnect** ou **SQLDriverConnect** seja chamado.)  
  
4.  Chama **SQLConnect** ou **SQLDriverConnect** para fazer a conexão. O Gerenciador de driver usa as opções de conexão na chamada para **SQLConnect** (ou as palavras-chave de conexão na chamada de **SQLDriverConnect**) e os atributos de conexão definidos após a alocação de conexão para determinar qual conexão no pool deve ser usada.  
  
    > [!NOTE]  
    >  A forma como uma conexão solicitada é correspondida a uma conexão em pool é determinada pelo atributo de ambiente SQL_ATTR_CP_MATCH. Para obter mais informações, consulte [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
     Os aplicativos ODBC que usam o pool de conexões devem chamar [CoInitializeEx](https://go.microsoft.com/fwlink/?LinkID=116307) durante a inicialização do aplicativo e [CoUninitialize](https://go.microsoft.com/fwlink/?LinkId=116310) quando o aplicativo é fechado.  
  
5.  Chama **SQLDisconnect** quando terminar com a conexão. A conexão é retornada para o pool de conexões e fica disponível para reutilização.  
  
 Para uma discussão aprofundada, consulte [pooling nos componentes de acesso a dados da Microsoft](https://go.microsoft.com/fwlink/?LinkId=120776).  
  
## <a name="connection-pooling-considerations"></a>Considerações sobre pooling de conexão  
 Executar qualquer uma das seguintes ações usando um comando SQL (em vez de por meio da API ODBC) pode afetar o estado da conexão e causar problemas inesperados quando o pool de conexões está ativo:  
  
-   Abrir uma conexão e alterar o banco de dados padrão.  
  
-   Usando a instrução SET para alterar quaisquer opções configuráveis (incluindo SET ROWCOUNT, ANSI_NULL, IMPLICIT_TRANSACTIONS, SHOWPLAN, STATISTICs, TEXTSIZE e DATEFORMAT).  
  
-   Criando tabelas temporárias e procedimentos armazenados.  
  
 Se qualquer uma dessas ações for executada fora da API ODBC, a próxima pessoa que usa a conexão herdará automaticamente as configurações, tabelas ou procedimentos anteriores.  
  
> [!NOTE]  
>  Não espere que determinadas configurações estejam presentes no estado da conexão. Você deve sempre definir o estado de conexão em seu aplicativo e garantir que o aplicativo remova as configurações de pool de conexões não utilizadas.  
  
## <a name="driver-aware-connection-pooling"></a>Pool de conexões com reconhecimento de driver  
 A partir do Windows 8, um driver ODBC pode usar conexões no pool com mais eficiência. Para obter mais informações, consulte [pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Conectando-se a uma fonte de dados ou driver](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [Desenvolvendo um driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Pooling nos componentes de acesso a dados da Microsoft](https://go.microsoft.com/fwlink/?LinkId=120776)

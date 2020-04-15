---
title: Pooling de conexão do driver manager | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 84ccc0db8f9a54eecc8337ca5efbc7b4c4baa239
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305817"
---
# <a name="driver-manager-connection-pooling"></a>Pool de conexões do Gerenciador de Driver
O pool de conexões permite que um aplicativo use uma conexão a partir de um pool de conexões que não precisam ser restabelecidas para cada uso. Uma vez que uma conexão tenha sido criada e colocada em um pool, um aplicativo pode reutilizar essa conexão sem executar o processo completo de conexão.  
  
 O uso de uma conexão em poolpode resultar em ganhos significativos de desempenho, porque os aplicativos podem salvar a sobrecarga envolvida na criação de uma conexão. Isso pode ser particularmente significativo para aplicativos intermediários que se conectam em uma rede ou para aplicativos que se conectam e desconectam repetidamente, como aplicativos da Internet.  
  
 Além dos ganhos de desempenho, a arquitetura de pooling de conexões permite que um ambiente e suas conexões associadas sejam usados por vários componentes em um único processo. Isso significa que componentes autônomos no mesmo processo podem interagir uns com os outros sem estarem cientes uns dos outros. Uma conexão em um pool de conexão pode ser usada repetidamente por vários componentes.  
  
> [!NOTE]
>  O pool de conexões pode ser usado por um aplicativo ODBC que exibe ODBC 2. *x* comportamento, desde que o aplicativo possa chamar *SQLSetEnvAttr*. Ao usar o pool de conexões, o aplicativo não deve executar instruções SQL \<que alteram o banco de dados ou o contexto do banco de dados, como alterar o nome do banco de *dados*>, que altera o catálogo usado por uma fonte de dados.  


 Um driver ODBC deve ser totalmente seguro para rosca, e as conexões não devem ter afinidade de rosca para suportar o pool de conexões. Isso significa que o driver é capaz de lidar com uma chamada em qualquer segmento a qualquer momento e é capaz de se conectar em um segmento, usar a conexão em outro segmento e desconectar em um terceiro segmento.  
  
 O pool de conexões é mantido pelo Driver Manager. As conexões são retiradas do pool quando o aplicativo chama **SQLConnect** ou **SQLDriverConnect** e são devolvidas ao pool quando o aplicativo chama **SQLDisconnect**. O tamanho da piscina cresce dinamicamente, com base nas alocações de recursos solicitadas. Ele encolhe com base no tempo de inatividade: Se uma conexão estiver inativa por um período de tempo (não foi usada em uma conexão), ela é removida da piscina. O tamanho do pool é limitado apenas por restrições de memória e limites no servidor.  
  
 O Gerenciador de driver determina se uma conexão específica em um pool deve ser usada de acordo com os argumentos passados no **SQLConnect** ou **SQLDriverConnect**e de acordo com os atributos de conexão definidos após a alocação da conexão.  
  
 Quando o Driver Manager está agrupando conexões, ele precisa ser capaz de determinar se uma conexão ainda está funcionando antes de distribuir a conexão. Caso contrário, o Driver Manager continua distribuindo a conexão morta ao aplicativo sempre que ocorre uma falha transitória de rede. Um novo atributo de conexão foi definido em ODBC 3 *.x*: SQL_ATTR_CONNECTION_DEAD. Este é um atributo de conexão somente leitura que retorna SQL_CD_TRUE ou SQL_CD_FALSE. O valor SQL_CD_TRUE significa que a conexão foi perdida, enquanto o valor SQL_CD_FALSE significa que a conexão ainda está ativa. (Drivers em conformidade com versões anteriores do ODBC também podem suportar esse atributo.)  
  
 Um driver deve implementar essa opção de forma eficiente ou prejudicará o desempenho do pool de conexão. Especificamente, uma chamada para obter esse atributo de conexão não deve causar uma ida e volta ao servidor. Em vez disso, um motorista deve apenas retornar o último estado conhecido da conexão. A conexão está morta se a última viagem ao servidor falhar, e não morrer se a última viagem foi bem sucedida.  
  
## <a name="remarks"></a>Comentários  
 Se uma conexão tiver sido perdida (relatada via SQL_ATTR_CONNECTION_DEAD), o Gerenciador de Driver oDBC destruirá essa conexão ligando para SQLDisconnect no driver. Novas solicitações de conexão podem não encontrar uma conexão utilizável na piscina. Eventualmente, o Driver Manager pode fazer uma nova conexão, assumindo que o pool está vazio.  
  
 Para usar um pool de conexões, um aplicativo executa as seguintes etapas:  
  
1.  Habilita o pool de conexões ligando para **SQLSetEnvAttr** para definir o atributo do ambiente SQL_ATTR_CONNECTION_POOLING para SQL_CP_ONE_PER_DRIVER ou SQL_CP_ONE_PER_HENV. Essa chamada deve ser feita antes que o aplicativo aloque o ambiente compartilhado para o qual o pool de conexões deve ser ativado. O cabo de ambiente na chamada para **SQLSetEnvAttr** deve ser definido como nulo, o que torna SQL_ATTR_CONNECTION_POOLING um atributo de nível de processo. Se o atributo estiver definido como SQL_CP_ONE_PER_DRIVER, um único pool de conexões será suportado para cada driver. Se um aplicativo funciona com muitos drivers e poucos ambientes, isso pode ser mais eficiente porque menos comparações podem ser necessárias. Se definido para SQL_CP_ONE_PER_HENV, um único pool de conexões é suportado para cada ambiente. Se um aplicativo funciona com muitos ambientes e poucos drivers, isso pode ser mais eficiente porque menos comparações podem ser necessárias. O pool de conexões é desativado definindo SQL_ATTR_CONNECTION_POOLING para SQL_CP_OFF.  
  
2.  Aloca um ambiente ligando para **SQLAllocHandle** com o argumento *HandleType* definido como SQL_HANDLE_ENV. O ambiente alocado por esta chamada será um ambiente compartilhado implícito porque o pool de conexões foi ativado. O ambiente a ser usado, no entanto, não é determinado até **que o SQLAllocHandle** com um *HandleType* de SQL_HANDLE_DBC seja chamado para este ambiente.  
  
3.  Aloca uma conexão ligando para **SQLAllocHandle** com *InputHandle* definido para SQL_HANDLE_DBC e o *conjunto InputHandle* para a alça do ambiente alocada para pool de conexões. O Gerenciador de drivers tenta encontrar um ambiente existente que corresponda aos atributos de ambiente definidos pelo aplicativo. Se esse ambiente não existir, um deles é criado, com uma contagem de referência (mantida pelo Driver Manager) de 1. Se um ambiente compartilhado correspondente for encontrado, o ambiente será devolvido ao aplicativo e sua contagem de referência será incrementada. (A conexão real a ser usada não é determinada pelo Driver Manager até que **o SQLConnect** ou **o SQLDriverConnect sejam** chamados.)  
  
4.  Chama **SQLConnect** ou **SQLDriverConnect** para fazer a conexão. O Driver Manager usa as opções de conexão na chamada para **SQLConnect** (ou as palavras-chave de conexão na chamada para **SQLDriverConnect**) e os atributos de conexão definidos após a alocação da conexão para determinar qual conexão no pool deve ser usada.  
  
    > [!NOTE]  
    >  A forma como uma conexão solicitada é combinada com uma conexão combinada é determinada pelo SQL_ATTR_CP_MATCH atributo do ambiente. Para obter mais informações, consulte [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
     Os aplicativos ODBC que usam pooling de conexões devem chamar [CoInitializeEx](https://go.microsoft.com/fwlink/?LinkID=116307) durante a inicialização do aplicativo e [CoUninitializar](https://go.microsoft.com/fwlink/?LinkId=116310) quando o aplicativo fecha.  
  
5.  Chama **SQLDisconnect** quando feito com a conexão. A conexão é devolvida ao pool de conexão e fica disponível para reutilização.  
  
 Para uma discussão aprofundada, consulte [Pooling nos Componentes de Acesso a Dados da Microsoft](https://go.microsoft.com/fwlink/?LinkId=120776).  
  
## <a name="connection-pooling-considerations"></a>Considerações sobre pooling de conexões  
 A execução de qualquer uma das seguintes ações usando um comando SQL (em vez de através da API ODBC) pode afetar o estado da conexão e causar problemas inesperados quando o pool de conexão estiver ativo:  
  
-   Abrindo uma conexão e alterando o banco de dados padrão.  
  
-   Usando a eda SET para alterar quaisquer opções configuráveis (incluindo SET ROWCOUNT, ANSI_NULL, IMPLICIT_TRANSACTIONS, SHOWPLAN, STATISTICS, TEXTSIZE e DATEFORMAT).  
  
-   Criando tabelas temporárias e procedimentos armazenados.  
  
 Se alguma dessas ações for realizada fora da API ODBC, a próxima pessoa que usar a conexão herdará automaticamente as configurações, tabelas ou procedimentos anteriores.  
  
> [!NOTE]  
>  Não espere que certas configurações estejam presentes no estado de conexão. Você deve sempre definir o estado de conexão em seu aplicativo e garantir que o aplicativo remova quaisquer configurações de pooling de conexão não utilizadas.  
  
## <a name="driver-aware-connection-pooling"></a>Pool de conexões com reconhecimento de driver  
 A partir do Windows 8, um driver ODBC pode usar conexões no pool de forma mais eficiente. Para obter mais informações, consulte [Pooling de conexão com reconhecimento de driver](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Conectando-se a uma fonte de dados ou driver](../../../odbc/reference/develop-app/connecting-to-a-data-source-or-driver.md)   
 [Desenvolvendo um Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Agrupamento nos componentes de acesso a dados da Microsoft](https://go.microsoft.com/fwlink/?LinkId=120776)

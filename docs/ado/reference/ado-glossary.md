---
description: Glossário ADO
title: Glossário do ADO | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.topic: conceptual
helpviewer_keywords:
- ADO, glossary
ms.assetid: b0478836-4123-4357-969a-c5784fc28be5
author: rothja
ms.author: jroth
ms.openlocfilehash: 0a9f2795906dce8c6a43b66397eefc1679ea22d6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987657"
---
# <a name="ado-glossary"></a>Glossário ADO
Este tópico define os termos relevantes para o ADO.  
  
## <a name="a"></a>Um  
 URL absoluta  
 Uma URL totalmente qualificada que especifica o local de um recurso que reside na Internet ou em uma intranet. Consulte também *URL* e *URL relativa*.  
  
 Controle ActiveX  
 O Autoregistro, componente COM em processo que geralmente tem um elemento visual em tempo de design ou em tempo de execução. Os controles ActiveX também têm a capacidade de se comunicar com um contêiner de documento ativo, como o Microsoft Internet Explorer.  
  
 ADISAPI (interface de programação de aplicativos do servidor de Internet de dados avançados)  
 Uma DLL ISAPI que fornece análise, controle de automação, empacotamento de conjunto de registros e empacotamento de MIME. O componente ADISAPI funciona por meio da API fornecida pelo Serviços de Informações da Internet (IIS). Consulte também *ISAPI*.  
  
 função de agregação  
 Em uma consulta, uma função como COUNT, AVG ou DESVPAD que calcula um valor usando todas as linhas em uma coluna de uma tabela. Em expressões de escrita e em programação, você pode usar funções de agregação SQL (incluindo as três listadas acima) e funções de agregação de domínio para determinar várias estatísticas.  
  
 alias  
 Um nome alternativo que você atribui a uma coluna ou expressão em uma instrução SQL SELECT, geralmente mais curto ou mais significativo. Por exemplo, BobSales é o alias na instrução SELECT a seguir: "Select WR-Sales as BobSales from SalesDB". Um alias pode ser usado para atribuir colunas dinamicamente para controlar associações no objeto DataControl.  
  
 Threading de apartamento  
 Um modelo de Threading COM em que todas as chamadas para um objeto ocorrem em um thread. No Threading Apartment, o COM sincroniza e realiza o marshaling de chamadas. Consulte também *COMmddefcom*.  
  
 operação assíncrona  
 Uma operação que retorna o controle para o programa de chamada sem aguardar a conclusão da operação. Antes que a operação seja concluída, a execução do código continua. Consulte também *operação síncrona*.  
  
## <a name="b"></a>B  
 entrada de associação  
 Um mapeamento entre um campo em uma tabela e uma variável. Nas extensões de Visual C++ do ADO, os campos do **conjunto de registros** são mapeados para as variáveis C/C++.  
  
 bitmask  
 Um valor numérico destinado a uma comparação de valor bit a bit com outros valores numéricos, normalmente para sinalizar opções no parâmetro ou valores de retorno. Normalmente, essa comparação é feita com operadores lógicos de bit a bit, como **e** e **ou** em Visual Basic, **&** e **&#124;** em C++.  
  
 Por exemplo, os valores ADO **FieldAttributeEnum** podem ser usados como bitmasks para determinar os atributos de um campo. Suponha que você quisesse determinar se um campo era atualizável. Você poderia testar isso com a seguinte expressão no Visual Basic:`Field.Attributes AND adFldUpdatable`  
  
 Se o resultado for TRUE, o campo será atualizável.  
  
 indicador  
 Um marcador que identifica exclusivamente uma linha dentro de um conjunto de linhas para que um usuário possa navegar rapidamente para ela.  
  
 objeto comercial  
 Um objeto que executa um conjunto definido de operações, como validação de dados ou lógica de regra de negócio. Os objetos comerciais geralmente residem na camada intermediária.  
  
 regra de negócio  
 A combinação de edições de validação, verificações de logon, pesquisas de banco de dados, políticas e transformações de algoritmos que constituem a maneira da empresa de fazer negócios. Também conhecida como *lógica de negócios*.  
  
## <a name="c"></a>C  
 expressão calculada  
 Uma expressão que não é constante, mas cujo valor depende de outros valores. Para ser avaliado, uma expressão calculada deve obter e computar valores de outras fontes, normalmente em outros campos ou linhas.  
  
 6  
 Uma referência a um intervalo de linhas de uma fonte de dados. No ADO, um capítulo é normalmente uma referência a outro **conjunto de registros**.  
  
 As colunas de capítulo possibilitam definir uma relação *pai-filho* em que o *pai* é o **conjunto de registros** que contém a coluna de capítulo e o *filho* é o conjunto de **registros** representado pelo capítulo.  
  
 chapter-alias  
 Um alias que se refere à coluna anexada ao pai.  
  
 conjunto de caracteres  
 Um mapeamento de um conjunto de caracteres para seus valores numéricos. Por exemplo, o Unicode é um conjunto de caracteres de 16 bits capaz de codificar todos os caracteres conhecidos e usado como um padrão de codificação de caracteres mundial.  
  
 filho  
 O lado dependente de uma relação hierárquica. Um filho é um nó em uma estrutura hierárquica que tem outro nó acima dele (mais próximo da raiz). Consulte também relação *filho-alias*, *pai-filho*, *pai*.  
  
 child-alias  
 Um alias que se refere ao filho. Consulte também *alias*, *filho*.  
  
 CLSID (identificador de classe)  
 Um UUID (identificador universal exclusivo) que identifica um componente COM. Cada componente COM tem seu CLSID no registro do Windows para que ele possa ser carregado por outros aplicativos. Consulte também *ProgID*, *com*.  
  
 camada de cliente  
 Uma camada lógica de um sistema distribuído que normalmente apresenta dados e processa a entrada do usuário, às vezes chamado de *front-end*. Normalmente, a camada de cliente solicita dados de um servidor com base na entrada e, em seguida, formata e exibe o resultado. Consulte também *camada intermediária*, *camada de fonte de dados*, *aplicativo distribuído*.  
  
 COM (Component Object Model)  
 Um padrão binário que permite que os objetos interoperem em um ambiente de rede, independentemente do idioma em que foram desenvolvidos ou em quais computadores eles residem. As tecnologias baseadas em COM incluem controles ActiveX, automação e vinculação e inserção de objetos (OLE). COM permite que um objeto exponha sua funcionalidade a outros componentes e hospede aplicativos. Ele define como o objeto se expõe e como essa exposição funciona em processos e em redes. COM também define o ciclo de vida do objeto.  
  
 Componente COM  
 Arquivo binário-como. dll,. ocx e alguns arquivos. exe – que dão suporte ao padrão COM para fornecer objetos. Esse arquivo contém código para uma ou mais fábricas de classe, classes COM, mecanismos de entrada de registro, código de carregamento e assim por diante.  
  
 Operador de comparação  
 Um operador que compara duas expressões e retorna um valor booliano.  
  
 Um parâmetro de critérios que pode ser expresso como ">" (maior que), " \<" (less than), "=" (equal), "> =" (maior ou igual), "<=" (menor ou igual), "<>" (não igual) ou "Like" (correspondência de padrões).  
  
 componente  
 Um objeto que encapsula dados e código e fornece um conjunto bem especificado de serviços publicamente disponíveis.  
  
 arquivo composto  
 Uma implementação de armazenamento estruturado COM para arquivos. Um arquivo composto armazena objetos separados em um único arquivo estruturado que consiste em dois elementos principais: objetos de armazenamento e objetos de fluxo. Juntos, eles funcionam como um sistema de arquivos em um arquivo.  
  
 Vários arquivos individuais ligados em um arquivo físico. Cada arquivo individual em um arquivo composto pode ser acessado como se fosse um único arquivo físico.  
  
 constante  
 Um valor numérico ou de cadeia de caracteres que não é alterado. Enumerações do ADO nomeadas (constantes enumeradas) podem ser usadas em seu código em vez de valores reais, por exemplo, **adUseClient** é uma constante cujo valor é 3. (Const adUseClient = 3). Consulte também *Enumeração*.  
  
 cursor  
 Um elemento Database que controla a navegação de registros, a capacidade de atualização dos dados e a visibilidade das alterações feitas no banco de dado por outros usuários.  
  
## <a name="d"></a>D  
 associação de dados  
 O processo de associar objetos ou controles de um aplicativo a uma fonte de dados. Um controle associado a uma fonte de dados é chamado de *controle vinculado a dados*.  
  
 O conteúdo de um controle associado a dados é associado a valores de um banco de dado. Por exemplo, um controle de grade que está associado a um objeto **Recordset** pode ser atualizado quando as linhas no **conjunto de registros** são atualizadas. Quando novos valores são recuperados pelo **conjunto de registros**, novos valores são exibidos na grade.  
  
 provedor de dados  
 O software que expõe dados a um aplicativo ADO diretamente ou por meio de um provedor de serviços. Consulte também provedor de serviços.  
  
 Data Shaping  
 Uma técnica que usa uma sintaxe formalizada (chamada **linguagem Shape**) para definir um objeto **Recordset** especializado (chamado de conjunto de *registros moldado*) que contém não apenas dados, mas também faz referência a outros objetos **Recordset** e/ou valores computados com base nesses outros objetos **Recordset** .  
  
 camada de fonte de dados  
 Uma camada lógica de um sistema distribuído que representa um computador que executa um DBMS, como um banco de dados SQL Server. Consulte também *camada de cliente*, *camada intermediária*, *aplicativo distribuído*.  
  
 DCOM  
 Um protocolo de conexão que permite que os componentes COM se comuniquem diretamente entre si em uma rede. Consulte também *com*, *componente*.  
  
 DDL (linguagem de definição de dados)  
 Essas instruções no SQL que definem, em vez de manipular, os dados. O esquema de um banco de dados é criado ou modificado com DDL. Por exemplo, **CREATE TABLE**, **CREATE INDEX**, **Grant**e **REVOKE** são instruções SQL DDL.  
  
 fluxo padrão  
 Um fluxo de texto ou binário (representado por um objeto de **fluxo** ) que está associado a objetos de **registro** ou **conjunto de registros** ao usar determinados provedores de OLE DB, como o provedor de OLE DB da Microsoft para publicação na Internet. O fluxo padrão normalmente contém o conteúdo de um arquivo, como o código HTML para a raiz de um site da Web.  
  
 aplicativo distribuído  
 Um programa escrito para que o processamento possa ser dividido em vários computadores em uma rede. Normalmente, um aplicativo distribuído é dividido *em camadas de*apresentação, lógica de negócios e armazenamento de dados ou camadas. Consulte também camada de cliente, camada intermediária, camada de fonte de dados.  
  
 Conjunto de registros desconectado  
 Um objeto **Recordset** em um cache de cliente que não tem mais uma conexão dinâmica com o servidor. Se a fonte de dados original precisar ser acessada novamente por algum motivo, como atualizar dados, a conexão deverá ser restabelecida. No entanto, as coleções, as propriedades e os métodos de um **conjunto de registros** desconectado ainda podem ser acessados.  
  
 DML (linguagem de manipulação de dados)  
 Essas instruções no SQL que manipulam, em oposição a definir, os dados. Os valores em um banco de dados são selecionados e modificados com DML. Por exemplo, **Inserir**, **Atualizar**, **excluir**e **selecionar** são instruções SQL DML.  
  
 provedor de origem do documento  
 Uma classe especial de provedores que gerencia pastas e documentos. Quando um documento é representado por um objeto de **registro** ou uma pasta de documentos é representada por um objeto **Recordset** , o provedor de origem do documento popula esses objetos com um conjunto exclusivo de campos que descrevem as características do documento, em vez do próprio documento propriamente dito. Consulte também registro de recurso.  
  
 DSN (nome da fonte de dados)  
 A coleção de informações usadas para conectar seu aplicativo a um banco de dados ODBC específico. O Gerenciador de driver ODBC usa essas informações para criar uma conexão com o banco de dados. Um DSN pode ser armazenado em um arquivo (um DSN de arquivo) ou no registro do Windows (um DSN de máquina).  
  
 Propriedade dinâmica  
 Uma propriedade específica para um provedor de dados ou o serviço de cursor. A coleção **Properties** de um objeto é populada com elas automaticamente ("dinamicamente"). Um objeto não tem propriedades dinâmicas até que ele esteja conectado a uma fonte de dados por meio de um provedor de dados específico. Consulte também provedor de dados, cursor.  
  
## <a name="e"></a>E  
 Enumeração  
 Uma lista de constantes nomeadas. Os valores enumerados não precisam ser exclusivos. No entanto, o nome de cada valor deve ser exclusivo dentro do escopo em que a enumeração é definida. No ADO, as enumerações são usadas para parâmetros numéricos e valores de retorno, para adicionar significado ao código ADO e para proteger o desenvolvedor dos valores numéricos (que podem mudar de versão para versão). Por exemplo, para abrir um **conjunto de registros**estático, use o valor enumerado **adOpenStatic** : `Recordset.Open ,,adOpenStatic`  
  
 Também conhecido como *constante enumerada*. Confira também *constante*.  
  
 event  
 Uma ação reconhecida por um objeto, para o qual você pode escrever código para responder. Os eventos podem ser gerados pela execução do comando, conclusão da transação, navegação do conjunto de registros e atualizações de dados, entre outras ações. Consulte também *manipulador de eventos*.  
  
 manipulador de eventos  
 Um manipulador de eventos é o código que é executado quando ocorre um evento. Consulte também evento.  
  
## <a name="h"></a>H  
 handler  
 Uma rotina que gerencia uma condição ou operação comum e relativamente simples, como recuperação de erro ou gerenciamento de dados.  
  
 Conjunto de registros hierárquico  
 Um **conjunto de registros** que contém outro **conjunto de registros**. Consulte também data Shaping, capítulo.  
  
 Para obter mais informações, consulte [acessando linhas em um conjunto de registros hierárquico](../guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
 hierarquia  
 Em geral, uma hierarquia é uma estrutura classificada com níveis de nível superior e subordinado. No ADO, os **conjuntos de registros** hierárquicos são usados para representar a relação pai-filho entre um registro e um capítulo. Além disso, os objetos ADO, **Record** e **Stream** podem ser usados para acessar estruturas hierárquicas de árvore, como uma pasta e documentos. ADO MD também inclui objetos de **hierarquia** para representar uma relação entre os níveis de uma dimensão em um cubo OLAP. Consulte também conjuntos de registros hierárquicos, relação pai-filho, capítulo, árvore.  
  
## <a name="i-l"></a>I-L  
 ISAPI (interface de programação de aplicativo de servidor da Internet)  
 Um conjunto de funções para servidores de Internet, como um servidor Windows NT® Server/Windows 2000 executando o Microsoft® Serviços de Informações da Internet (IIS).  
  
 Chave  
 Uma coluna ou colunas em uma tabela que identifica exclusivamente uma linha; geralmente usado para indexar uma tabela.  
  
## <a name="m"></a>M  
 marshaling  
 O processo de empacotamento, envio e desempacotamento de parâmetros de método de interface entre limites de thread ou processo.  
  
 camada intermediária  
 A camada lógica em um sistema distribuído entre uma interface do usuário ou um cliente Web e o banco de dados. Normalmente, isso é onde os objetos comerciais são instanciados. A camada intermediária é uma coleção de regras de negócios e funções que geram e operam após o recebimento de informações. Eles realizam isso por meio de regras de negócio, que podem ser alteradas com frequência e, portanto, são encapsuladas em componentes que são separados fisicamente da lógica do aplicativo em si. Também conhecida como *camada de servidor de aplicativos*. Consulte também aplicativo distribuído, camada de cliente, camada de fonte de dados.  
  
 MIME (extensão de multi-propósito da Internet mail)  
 Um protocolo de Internet originalmente desenvolvido para permitir o intercâmbio de mensagens de email com conteúdo rico em ambientes de rede, computador e email heterogêneos. Na prática, o MIME também foi adotado e estendido por aplicativos que não são de email.  
  
 MIME é um padrão que permite que dados binários sejam publicados e lidos na Internet. O cabeçalho de um arquivo com dados binários contém o tipo MIME dos dados; Isso informa os programas cliente (navegadores da Web e pacotes de email, por exemplo) de que eles precisarão para lidar com os dados de uma maneira diferente do que manipulam texto simples. Por exemplo, o cabeçalho de um documento da Web que contém um gráfico JPEG contém o tipo MIME específico para o formato de arquivo JPEG. Isso permite que um navegador exiba o arquivo com seu visualizador de JPEG, se houver um.  
  
## <a name="n-o"></a>N-O  
 nó  
 Um elemento em uma estrutura de árvore hierárquica. Um nó pode ser a raiz ou o filho de outro nó. Um nó também pode ser pai de vários filhos. Consulte também hierarquia, árvore, raiz, filho, pai.  
  
 variável de objeto  
 Uma variável que contém uma referência a um objeto. Por exemplo, `objCustomObject` é uma variável que aponta para um objeto do tipo customobject:`Set objCustomObject = CreateObject(adodb.Recordset)`  
  
 ODBC (Open Database Connectivity)  
 Uma interface de linguagem de programação padrão usada para se conectar a uma variedade de fontes de dados. Normalmente, isso é acessado por meio do painel de controle, em que os nomes de fontes de dados (DSNs) podem ser atribuídos para usar drivers ODBC específicos.  
  
 OLE DB  
 Um conjunto de interfaces que expõe dados de uma variedade de fontes usando COM. As interfaces de OLE DB fornecem aplicativos com acesso uniforme aos dados armazenados em diversas fontes de informações. Essas interfaces dão suporte à quantidade de funcionalidade de DBMS apropriada à fonte de dados, permitindo que ela Compartilhe seus dados. Consulte também COM.  
  
 bloqueio otimista  
 Um tipo de bloqueio no qual a página de dados que contém um ou mais registros, incluindo o registro que está sendo editado, não está disponível para outros usuários somente enquanto o registro está sendo atualizado pelo método **Update** , mas está disponível antes e depois da chamada para **Update**.  
  
 O bloqueio otimista é usado quando o objeto **Recordset** é aberto com o parâmetro **LockType** ou a propriedade definida como **adLockOptimistic** ou **adLockBatchOptimistic**. Consulte também bloqueio pessimista.  
  
 valor ordinal  
 O local numérico de um item em um pedido. Em uma coleção ADO, o valor ordinal do primeiro item é zero (0). O próximo item é um (1) e assim por diante.  
  
## <a name="p"></a>P  
 comando com parâmetros  
 Uma consulta ou um comando que permite que você defina valores de parâmetro antes da execução do comando. Por exemplo, uma cadeia de caracteres SQL pode ser parametrizada inserindo marcadores de parâmetro na cadeia de caracteres SQL (designada pelo caractere "?"). Em seguida, o aplicativo especifica valores para cada parâmetro e executa o comando.  
  
 pai  
 O lado de controle de uma relação hierárquica. Em uma estrutura hierárquica, um pai tem um ou mais nós filho diretamente abaixo dele na hierarquia. Consulte também relação pai-alias, pai-filho, filho.  
  
 parent-alias  
 Um alias que se refere ao pai. Consulte também alias, pai.  
  
 relação pai-filho  
 Uma relação em uma estrutura hierárquica na qual o pai está um nível acima e diretamente associado a um ou mais filhos. Um filho é um nível inferior e deve ter um pai. Consulte também pai, filho.  
  
 bloqueio pessimista  
 Um tipo de bloqueio no qual a página que contém um ou mais registros, incluindo o registro que está sendo editado, não está disponível para outros usuários para garantir que uma atualização será feita. O comportamento de bloqueio pessimista é definido pelo provedor de OLE DB. Normalmente, os registros são bloqueados na edição e permanecem indisponíveis até que o método de **atualização** seja concluído.  
  
 O bloqueio pessimista é habilitado quando o objeto **Recordset** é aberto com o parâmetro **LockType** ou a propriedade definida como **adLockPessimistic**. Consulte também bloqueio otimista.  
  
 pool  
 Uma otimização de desempenho com base no uso de coleções de recursos alocados previamente, como objetos ou conexões de banco de dados. É mais eficiente desenhar um recurso existente do pool do que criar um novo recurso.  
  
 ProgID (identificador programático)  
 Um nome exclusivo mapeado para o registro do Windows por um aplicativo COM. O ProgID de uma conexão ADO é "ADODB. Conexão ". Consulte também CLSID, COM.  
  
 proxy  
 Um objeto específico de interface que fornece o marshaling de parâmetro e a comunicação necessários para um cliente chamar um objeto de aplicativo que está sendo executado em um ambiente de execução diferente, como em um thread diferente ou em outro processo. O proxy está localizado com o cliente e se comunica com um stub correspondente que está localizado com o objeto de aplicativo que está sendo chamado. Consulte também stub.  
  
## <a name="r"></a>R  
 URL relativa  
 Uma URL parcialmente qualificada que especifica um recurso na Internet ou uma intranet cujo local é relativo a um ponto de partida especificado por uma URL absoluta ou um objeto de conexão ADO equivalente. Na verdade, as URLs absolutas e relativas concatenadas consitutem uma URL completa. Consulte também URL e URL absoluta.  
  
 fonte de dados remota  
 Uma fonte de dados que existe em um outro computador, em vez de no sistema local (onde o aplicativo cliente é executado).  
  
 registro de recurso  
 Um registro de um provedor de origem de documento que contém campos para a definição e a descrição de uma pasta ou documento. O documento em si não está contido no registro de recurso, mas normalmente pode ser acessado pelo fluxo padrão ou por um campo no registro de recurso que contém uma URL. Consulte também provedor de origem de documento, fluxo padrão, URL.  
  
 conjunto de linhas  
 Um conjunto de linhas de uma fonte de dados, todos tendo o mesmo esquema de campo. Um conjunto de linhas pode representar todos ou alguns campos de uma tabela. Um conjunto de linhas também pode representar uma tabela virtual, criada por uma consulta ou uma junção de duas ou mais tabelas. No ADO, conjuntos de linhas são representados por objetos **Recordset** .  
  
## <a name="s"></a>S  
 Escopo  
 O intervalo de referência para um objeto ou uma variável ou um intervalo de registros em uma exibição ou tabela. Por exemplo, variáveis locais podem ser referenciadas somente dentro do procedimento no qual elas foram definidas. As variáveis públicas podem ser acessadas de qualquer lugar no aplicativo. Os objetos, como o banco de dados atual, estarão no escopo se estiverem no caminho de pesquisa definido. Os intervalos de registros podem ser especificados com uma cláusula Scope em muitos comandos.  
  
 provedor de serviços  
 Software que encapsula um serviço, produzindo e consumindo dados, aumentando os recursos em seus aplicativos ADO. É um provedor que não expõe dados diretamente, em vez disso, ele fornece um serviço, como o processamento de consulta. O provedor de serviços pode processar os dados fornecidos por um provedor de dados. Consulte também provedor de dados.  
  
 Conjunto de registros moldado  
 Um **conjunto de registros** cujas colunas foram especificamente definidas para conter não apenas dados, mas também referencia (chamados de capítulos) a outros objetos de **conjunto de registros** e/ou valores computados com base em outros objetos **Recordset** .  
  
 irmão  
 Quaisquer dois ou mais nós em uma estrutura hierárquica que estejam no mesmo nível na hierarquia. O nó raiz em uma hierarquia não tem irmãos.  
  
 procedimento armazenado  
 Uma coleção pré-compilada de código, como instruções SQL e instruções de controle de fluxo opcionais armazenadas com um nome e processadas como uma unidade. Os procedimentos armazenados são armazenados em um banco de dados; Eles podem ser executados com uma chamada de um aplicativo e permitem variáveis declaradas pelo usuário, execução condicional e outros recursos de programação avançados.  
  
 Gerenciador  
 Um objeto específico de interface que fornece o marshaling de parâmetro e a comunicação necessários para um objeto de aplicativo receber chamadas de um cliente que está sendo executado em um ambiente de execução diferente, como em um thread diferente ou em outro processo. O stub está localizado com o objeto Application e se comunica com um proxy correspondente que está localizado com o cliente que o chama. Consulte também proxy.  
  
 subnó  
 Consulte filho.  
  
 operação síncrona  
 Uma operação iniciada pelo código que é concluída antes que a próxima operação possa ser iniciada. Consulte também operação assíncrona.  
  
## <a name="t-z"></a>T-Z  
 Árvore  
 Uma estrutura que representa uma relação hierárquica entre elementos (nós). Há um nó no nível superior de uma árvore (a raiz). Sob a raiz, pode haver vários filhos. Cada filho pode, por sua vez, ser o pai de outros filhos, por isso, ramificando como uma árvore. Uma pasta que contém documentos e outras pastas é um exemplo típico de uma estrutura de árvore. Consulte também hierarquia, nó, raiz, filho, pai.  
  
 Servidor Web  
 Um computador que fornece serviços Web e páginas para usuários de intranet e Internet.
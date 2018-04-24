---
title: Glossário do ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, glossary
ms.assetid: b0478836-4123-4357-969a-c5784fc28be5
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d327b5e991127a533d4b599daf8c52cfb2dba1ba
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="ado-glossary-terms"></a>Glossário de termos de ADO
Este tópico define condições relevantes para ADO.

## <a name="a"></a>A
 absoluto URL uma URL totalmente qualificada que especifica o local de um recurso que reside na Internet ou intranet. Consulte também *URL* e *URL relativa*.

 Componente COM o registro automático, no processo que geralmente tem um elemento visual no tempo de design ou no tempo de execução de controles ActiveX. Controles ActiveX também têm a capacidade de se comunicar com um contêiner de documento ativo, como o Microsoft Internet Explorer.

 ADISAPI (Advanced dados Internet Server Application Programming Interface) uma DLL ISAPI que fornece a análise, controle de automação, realização de marshaling de conjunto de registros e empacotamento de MIME. O componente ADISAPI funciona por meio da API fornecida pelo Internet Information Services (IIS). Consulte também *ISAPI*.

 função de agregação em uma consulta, uma função como COUNT, AVG ou STDEV que calcula um valor usando todas as linhas em uma coluna de uma tabela. Em expressões de gravação e em programação, você pode usar funções de agregação SQL (incluindo os três listados acima) e funções de agregação de domínio para determinar diversas estatísticas.

 alias um nome alternativo dado a uma coluna ou expressão em uma instrução SQL SELECT, geralmente mais curta ou mais significativa. Por exemplo, BobSales é o alias na instrução SELECT a seguir: "Selecione vendas gravar h como BobSales de SalesDB". Um alias pode ser usado para atribuir dinamicamente colunas para associações de controle no objeto DataControl.

 apartment threading COM um modelo de threading em que todas as chamadas para um objeto ocorrerem em um thread. Apartment threading, COM sincroniza e realiza marshaling de chamadas. Consulte também *COMmddefcom*.

 operação assíncrona uma operação que retorna o controle para o programa de chamada sem aguardar a conclusão da operação. Antes da operação for concluída, continua a execução de código. Consulte também *operação síncrona*.

## <a name="b"></a>B
 associação de mapeamento de entrada um entre um campo em uma tabela e uma variável. Nas extensões do Visual C++ de ADO, **registros** campos são mapeados para variáveis de C/C++.

 valor numérico de bitmask um deve ser uma comparação de valor de bit a bit com outros valores numéricos, normalmente para opções de sinalizador no parâmetro ou valores de retorno. Normalmente essa comparação é feita com operadores lógicos, como **e** e **ou** no Visual Basic, **&** e **&#124;** em C++.

 Por exemplo, o ADO **FieldAttributeEnum** valores podem ser usados como bitmasks para determinar os atributos de um campo. Suponha que você desejava determinar se um campo foi atualizável. Você pode testar isso com a seguinte expressão no Visual Basic:`Field.Attributes AND adFldUpdatable`

 Se o resultado for TRUE, o campo é atualizável.

 marcar um marcador que identifica exclusivamente uma linha dentro de um conjunto de linhas para que um usuário pode navegar rapidamente a ele.

 Um objeto que executa um conjunto de operações, como validação de dados ou lógica de regra de negócios definido do objeto de negócios. Objetos de negócios residem na camada intermediária.

 regra de negócio a combinação de edições de validação, verificações de logon, pesquisas de banco de dados, políticas e transformações algorítmicos que constituem a forma de uma empresa de negócios. Também conhecido como *lógica de negócios*.

## <a name="c"></a>C
 calculado a expressão de uma expressão que não é constante, mas cujo valor depende de outros valores. Para ser avaliada, uma expressão calculada deve obter e calcular valores de outras fontes, geralmente em outros campos ou linhas.

 referência de capítulo um a um intervalo de linhas de uma fonte de dados. No ADO, um capítulo normalmente é uma referência a outro **registros**.

 Colunas de capítulo possibilitam definir um *pai-filho* relação onde a *pai* é o **registros** que contém a coluna de capítulo e  *filho* é o **registros** representado pelo capítulo.

 alias de capítulo um alias que se refere à coluna anexado ao pai.

 Um mapeamento de um conjunto de caracteres do conjunto de caracteres para seus valores numéricos. Por exemplo, o Unicode é um caractere de 16 bits definido capaz de codificar todos os caracteres conhecidos e usado como um padrão de codificação de caracteres em todo o mundo.

 o lado dependente de uma relação hierárquica do filho. Um filho é um nó em uma estrutura hierárquica com outro nó acima dele (próximo da raiz). Consulte também *filho alias*, *relação pai-filho*, *pai*.

 Um alias que se refere a filho de alias de filho. Consulte também *alias*, *filho*.

 O CLSID (identificador de classe) um identificador universalmente exclusivo (UUID) que identifica um componente COM. Cada componente do COM tem sua CLSID no registro do Windows para que ele possa ser carregado por outros aplicativos. Consulte também *ProgID*, *COM*.

 camada de lógica da camada de um cliente de um sistema distribuído que geralmente apresenta dados e processos de entrada do usuário, também conhecido como o *front-end*. Normalmente, a camada do cliente solicita dados de um servidor com base na entrada e, em seguida, formata e exibe o resultado. Consulte também *camada intermediária*, *da camada de fonte de dados*, *aplicativo distribuído*.

 COM (Component Object Model) um binário padrão que permite que objetos interoperar em um ambiente de rede independentemente da linguagem em que foram desenvolvidos ou em quais computadores residem. COM base em tecnologias incluem controles ActiveX, automação e objeto vinculando e inserindo (OLE). COM permite que um objeto expor sua funcionalidade a outros componentes e aplicativos do host. Ele define como o objeto expõe em si e como essa exposição funciona em processos e em redes. COM também define o ciclo de vida do objeto.

 Arquivo binário de componente COM — como. dll,. ocx e alguns arquivos .exe — que oferece suporte ao padrão COM para fornecer objetos. Esse arquivo contém código para um ou mais fábricas de classes, classes COM, mecanismos de entrada de registro, código de carregamento e assim por diante.

 Um operador que compara duas expressões e retorna um valor booliano de operador de comparação.

 Um parâmetro de critérios que pode ser expressas como ">" (maior que), "\<" (menor que), "=" (igual), "> =" (maior ou igual), "< =" (menor ou igual), "<>" (não igual), ou "como" (correspondência de padrão).

 Um objeto que encapsula os dados e o código e fornece um conjunto de serviços disponíveis publicamente bem especificado do componente.

 arquivo composto uma implementação de COM o armazenamento para arquivos estruturado. Um arquivo composto armazena objetos separados em um único arquivo estruturado consiste em dois elementos principais: objetos de armazenamento e objetos de fluxo. Juntos, eles funcionam como um sistema de arquivos dentro de um arquivo.

 Um número de arquivos individuais, agrupadas em um arquivo físico. Cada arquivo individual em um arquivo composto pode ser acessado como se fosse um único arquivo físico.

 constante de um valor numérico ou cadeia de caracteres que não é alterado. Enumerações de ADO nomeadas (constantes enumeradas) podem ser usadas em seu código em vez de valores reais, por exemplo, **adUseClient** é uma constante cujo valor é 3. (AdUseClient const = 3). Consulte também *enumeração*.

 Um elemento de banco de dados que controla a visibilidade das alterações feitas no banco de dados por outros usuários, capacidade de atualização de dados e navegação de registros do cursor.

## <a name="d"></a>D
 o processo de associar a controles de um aplicativo para uma fonte de dados ou objetos de associação de dados. Um controle associado a uma fonte de dados é chamado um *controle associado a dados*.

 O conteúdo de um controle associado a dados está associado com valores de um banco de dados. Por exemplo, um controle de grade que está associado a um **Recordset** objeto pode ser atualizado quando as linhas no **Recordset** são atualizadas. Quando os novos valores são recuperados, o **registros**, novos valores são exibidos na grade.

 provedor de dados do Software que expõe dados em um aplicativo ADO diretamente ou por meio de um provedor de serviços. Consulte também o provedor de serviços.

 Uma técnica que torna a modelagem de dados usam uma sintaxe formal (chamado **Formatar idioma**) para definir uma **registros** objeto (chamado um *em forma de conjunto de registros*) que contém não apenas os dados, mas também as referências a outros **registros** objetos e/ou valores calculados com base nas outras **registros** objetos.

 A lógica camada de um sistema distribuído que representa um computador que executa o DBMS, como um banco de dados do SQL Server da fonte de dados. Consulte também *da camada do cliente*, *camada intermediária*, *aplicativo distribuído*.

 Protocolo de transmissão do DCOM A que permite que os componentes para se comunicar diretamente com o outro em uma rede. Consulte também *COM*, *componente*.

 DDL (Data Definition Language) essas instruções SQL que define, em oposição a manipulação de dados. O esquema de banco de dados é criado ou modificado com DDL. Por exemplo, **CREATE TABLE**, **CREATE INDEX**, **GRANT**, e **REVOGAR** são instruções SQL DDL.

 padrão de fluxo de um fluxo de texto ou binário (representado por um **fluxo** objeto) que está associado com **registro** ou **registros** objetos ao usar determinados provedores OLE DB, como o provedor OLE DB da Microsoft para publicação na Internet. O fluxo padrão normalmente contém o conteúdo de um arquivo, como o código HTML para a raiz de um site da Web.

 programa de aplicativo distribuído A escrito para que o processamento pode ser dividido em vários computadores em uma rede. Normalmente, um aplicativo distribuído é dividido apresentação, lógica de negócios e dados de camadas de armazenamento, ou *camadas*. Consulte também a camada de cliente, camada intermediária, camada de fonte de dados.

 desconectado Recordset A **registros** objeto em um cache de cliente que não tem uma conexão ao vivo para o servidor. Se a fonte de dados original precisa ser acessados novamente por algum motivo, como a atualização de dados, a conexão deve ser restabelecida. No entanto, as coleções, propriedades e métodos de um desconectada **registros** ainda pode ser acessado.

 DML (Data Manipulation Language) essas instruções que manipulam, em vez de definir dados no SQL. Os valores em um banco de dados são selecionados e modificados com DML. Por exemplo, **inserir**, **atualização**, **excluir**, e **selecione** são instruções DML SQL.

 provedor de origem de documento uma classe especial de provedores que gerenciam pastas e documentos. Quando um documento é representado por um **registro** objeto ou uma pasta de documentos é representado por um **registros** do objeto, o provedor de origem do documento preenche esses objetos com um conjunto exclusivo de campos que descrevem as características do documento, em vez do próprio documento. Consulte também o registro de recurso.

 DSN (nome de fonte de dados), a coleção de informações usada para conectar seu aplicativo para um determinado banco de dados ODBC. O Gerenciador de Driver ODBC usa essas informações para criar uma conexão ao banco de dados. Um DSN pode ser armazenado em um arquivo (um DSN de arquivo) ou no registro do Windows (um DSN de máquina).

 dinâmico uma propriedade específica para um provedor de dados ou o serviço de cursor. O **propriedades** coleção de um objeto é preenchida automaticamente com estas ("dinamicamente"). Um objeto não tem dinâmicas propriedades até que ele está conectado a uma fonte de dados por meio de um provedor de dados específico. Consulte também dados do provedor, o cursor.

## <a name="e"></a>E
 Lista de enumeração A de constantes nomeadas. Valores enumerados não precisam ser exclusivos. No entanto, o nome de cada valor deve ser exclusivo dentro do escopo em que a enumeração está definida. No ADO, enumerações são usadas para o parâmetro numérico em valores de retorno, adicionar significado para código ADO e protegem o desenvolvedor contra os valores numéricos (que podem ser alterados de versão para versão). Por exemplo, para abrir um estático **registros**, use o **adOpenStatic** enumerados valor: `Recordset.Open ,,adOpenStatic`

 Também conhecido como *constante enumerada*. Consulte também *constante*.

 evento uma ação reconhecida por um objeto para o qual você pode escrever código para responder. Eventos podem ser gerados pela execução do comando, a conclusão da transação, navegação de conjunto de registros e atualizações de dados, entre outras ações. Consulte também *manipulador de eventos*.

 manipulador de eventos um manipulador de eventos é o código que é executado quando ocorre um evento. Consulte também o evento.

## <a name="h"></a>H
 rotina do manipulador A que gerencia uma operação, como gerenciamento de dados ou de recuperação de erro ou condição comuns e relativamente simple.

 hierárquica Recordset A **registros** que contém outro **registros**. Consulte também data shaping capítulo.

 Para obter mais informações, consulte [acessar linhas em um conjunto de registros hierárquicos](../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).

 hierarquia em geral, uma hierarquia é uma estrutura de classificação com um superior nível e níveis subordinados. No ADO, hierárquico **conjuntos de registros** são usados para representar a relação pai-filho entre um registro e um capítulo. Também no ADO, **registro** e **fluxo** objetos podem ser usados para acessar as estruturas de árvore hierárquica, como documentos e uma pasta. Também inclui o ADO MD **hierarquia** objetos para representar uma relação entre os níveis de uma dimensão em um cubo OLAP. Consulte também conjuntos de registros hierárquicos, relação pai-filho, o capítulo, a árvore.

## <a name="i-l"></a>I-L
 ISAPI (Internet Server Application Programming Interface) um conjunto de funções de servidores de Internet, como um Windows NT® Server/Windows 2000 Server, executando o Microsoft® Internet Information Services (IIS).

 Chave de uma coluna ou colunas em uma tabela que identifica exclusivamente uma linha; geralmente usado para indexar uma tabela.

## <a name="m"></a>M
 o processo de empacotamento, envio e descompactação parâmetros de método de interface de empacotamento entre limites de thread ou processo.

 a camada lógica em um sistema distribuído entre uma interface do usuário ou cliente da Web e o banco de dados de camada intermediária. Normalmente, isso é onde os objetos comerciais são instanciados. A camada intermediária é uma coleção de regras de negócio e funções que geram e operam receber informações. Realiza isso por meio de regras de negócio, que podem ser alterados com frequência e, portanto, são encapsuladas em componentes que estão fisicamente separados da lógica do aplicativo em si. Também conhecido como *nível de servidor de aplicativo*. Consulte também aplicativo distribuído, camada do cliente, a camada de fonte de dados.

 Protocolo um MIME (extensão de email de Internet multiuso) originalmente desenvolvido para permitir a troca de mensagens de email com conteúdo rico em rede heterogênea, máquina e ambientes de email. Na prática, MIME também foi adotado e estendido por aplicativos de email não.

 MIME é um padrão que permite que os dados binários a ser publicado e de leitura na Internet. O cabeçalho de um arquivo com dados binários contém o tipo MIME dos dados. Isso informa programas cliente (Web navegadores e pacotes de email, por exemplo) que eles precisam lidar com os dados de maneira diferente que tratam de texto simples. Por exemplo, o cabeçalho de um documento da Web que contém uma imagem JPEG contém o tipo MIME específico para o formato de arquivo JPEG. Isso permite que um navegador para exibir o arquivo com o visualizador JPEG, se houver.

## <a name="n-o"></a>N-O
 nó de um elemento em uma estrutura de árvore hierárquica. Um nó pode ser a raiz ou o filho de outro nó. Um nó também pode ser o pai de vários filhos. Consulte também hierarquia de árvore, raiz, filho, pai.

 variável de variável de um objeto que contém uma referência a um objeto. Por exemplo, `objCustomObject` é uma variável que aponta para um objeto do tipo ObjetoPersonalizado:`Set objCustomObject = CreateObject(adodb.Recordset)`

 ODBC (Open Database Connectivity) uma interface padrão de linguagem de programação usada para se conectar a uma variedade de fontes de dados. Isso geralmente é acessado por meio do painel de controle, em que os nomes de fonte de dados (DSNs) podem ser atribuídos a usar drivers ODBC específicos.

 OLE DB um conjunto de interfaces que expõem os dados de uma variedade de fontes usando COM. Interfaces do OLE DB fornecem aplicativos acesso padronizado aos dados armazenados em fontes diferentes de informações. Essas interfaces suportam a quantidade de funcionalidade DBMS apropriada para a fonte de dados, permitindo que ele compartilhe seus dados. Consulte também COM.

 otimista de bloqueio de um tipo de proteção no qual a página de dados que contém um ou mais registros, inclusive o registro que está sendo editado, está disponível para outros usuários somente enquanto o registro está sendo atualizada pelo **atualização** método, mas está disponível antes e após a chamada a **atualização**.

 Bloqueio otimista é usado quando o **registros** objeto é aberto com o **LockType** parâmetro ou a propriedade definida como **adLockOptimistic** ou  **adLockBatchOptimistic**. Consulte também pessimista.

 o local numérico de um item em uma ordem de valor ordinal. Em uma coleção de ADO, o valor ordinal do primeiro item é zero (0). O próximo item é um (1) e assim por diante.

## <a name="p"></a>P
 consulta com parâmetros de comando ou o comando que permite que você defina valores de parâmetro para que o comando é executado. Por exemplo, uma cadeia de caracteres SQL pode ser parametrizada inserindo marcadores de parâmetro na cadeia de caracteres SQL (designado pelo '?' caracteres). O aplicativo, em seguida, especifica valores para cada parâmetro e executa o comando.

 pai do controle lado de uma relação hierárquica. Em uma estrutura hierárquica, um pai tem um ou mais nós filho diretamente abaixo na hierarquia. Consulte também alias pai, filho e relação pai-filho.

 Um alias que se refere ao pai de alias pai. Consulte também alias, pai.

 relação de um da relação pai-filho em uma estrutura hierárquica em que o pai é um nível superior e diretamente associado a um ou mais filhos. Um filho é um nível inferior e deve ter um pai. Consulte também pai, filho.

 pessimista bloqueio de um tipo de proteção no qual a página que contém um ou mais registros, inclusive o registro que está sendo editado, está disponível para outros usuários para garantir que uma atualização será feita. Comportamento de bloqueio pessimista é definido pelo provedor OLE DB. Normalmente, os registros estão bloqueados na edição e estarão disponíveis até que o **atualização** método foi concluída.

 Bloqueio pessimista é habilitado quando o **registros** objeto é aberto com o **LockType** parâmetro ou a propriedade definida como **adLockPessimistic**. Consulte também otimista.

 Uma otimização de desempenho com base no uso de coleções de recursos pré-alocados, como conexões de banco de dados ou objetos do pool. É mais eficiente para desenhar um recurso existente do pool que criar um novo recurso.

 ProgID (identificador programático) um nome exclusivo que mapeados para o registro do Windows, um aplicativo COM. O ProgID para uma Conexão ADO é "ADODB. Conexão". Consulte também o CLSID, COM.

 proxy de um objeto específico de interface que fornece o parâmetro de empacotamento e comunicação necessária para um cliente chamar um objeto de aplicativo que está em execução em um ambiente de execução diferente, como em um thread diferente ou em outro processo. O proxy está localizado com o cliente e se comunica com um stub correspondente que encontra-se com o objeto de aplicativo que está sendo chamado. Consulte também o stub.

## <a name="r"></a>R
 URL relativa A parcialmente qualificado URL que especifica um recurso na Internet ou intranet cujo local é relativo ao ponto de partida especificado por uma URL absoluta ou o objeto de Conexão ADO equivalente. Na realidade, o concatenado absoluta e relativa URLs consitute uma URL completa. Consulte também URL e a URL absoluta.

 Uma fonte de dados existente em um outro computador, em vez de no sistema local (onde o aplicativo cliente é executado) da fonte de dados remotos.

 Um registro de um provedor de origem do documento que contém campos para a definição e a descrição de uma pasta ou um documento de registro de recurso. O documento em si não está contido no registro de recurso, mas normalmente pode ser acessado por fluxo padrão ou um campo no registro de recurso que contém uma URL. Consulte também o provedor de origem do documento, fluxo de padrão de URL.

 Um conjunto de linhas o conjunto de linhas de uma fonte de dados, todos com o mesmo esquema de campo. Um conjunto de linhas pode representar alguns ou todos os campos de uma tabela. Um conjunto de linhas também pode representar uma tabela virtual, criada por uma consulta ou uma junção de duas ou mais tabelas. No ADO, conjuntos de linhas são representados por **registros** objetos.

## <a name="s"></a>P
 O escopo do intervalo de referência para um objeto ou uma variável ou um intervalo de registros em uma tabela ou exibição. Por exemplo, variáveis locais podem ser referenciadas apenas dentro do procedimento no qual eles foram definidos. Variáveis públicas são acessíveis de qualquer lugar no aplicativo. Objetos, como o banco de dados atual, estão no escopo se eles estão no caminho de pesquisa definidos. Intervalos de registro podem ser especificados com uma cláusula de escopo em muitos comandos.

 provedor de serviços de Software que encapsula um serviço, produzindo e consumo de dados, aumentando os recursos em seus aplicativos do ADO. É um provedor que não expõe dados diretamente, em vez disso, ele fornece um serviço, como o processamento de consulta. O provedor de serviços pode processar os dados fornecidos pelo provedor de dados. Consulte também o provedor de dados.

 em forma de Recordset A **registros** cujas colunas foram definidas especificamente para conter não apenas dados, mas também (chamadas capítulos) de referências a outras **registros** objetos e/ou valores calculados com base em outros **registros** objetos.

 irmão dois ou mais nós em uma estrutura hierárquica que estão no mesmo nível na hierarquia. O nó raiz em uma hierarquia não tem nenhum irmãos.

 o procedimento armazenado A pré-compilados a coleção de código, como instruções SQL e instruções de controle de fluxo opcionais armazenadas sob um nome e processadas como uma unidade. Procedimentos armazenados são armazenados em um banco de dados; eles podem ser executados com uma chamada de um aplicativo e permitem variáveis declarados por usuário, execução condicional e outros recursos avançados de programação.

 stub um objeto específico de interface que fornece o parâmetro de empacotamento e a comunicação necessária para um objeto de aplicativo para receber chamadas de um cliente que está em execução em um ambiente de execução diferente, como em um thread diferente ou em outro processo. O fragmento de código está localizado com o objeto de aplicativo e se comunica com um proxy correspondente que encontra-se com o cliente que o chama. Consulte também o proxy.

 filho de consulte subnó.

 Uma operação iniciada pelo código que seja concluída antes da próxima operação de operação síncrona pode ser iniciado. Consulte também operação assíncrona.

## <a name="t-z"></a>T-Z
 Estrutura de árvore um que representa uma relação hierárquica entre elementos (nós). Há um nó de nível superior de uma árvore (raiz). Abaixo da raiz, pode haver vários filhos. Cada filho por sua vez pode ser o pai de outros filhos, assim, a ramificação como uma árvore. Uma pasta que contém outras pastas e documentos é um exemplo típico de uma estrutura de árvore. Consulte também hierarquia, nó, raiz, filho, pai.

 Um computador que fornece serviços da Web e páginas para usuários de Internet e intranet do servidor de Web.

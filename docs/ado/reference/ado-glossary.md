---
title: Glossário ADO | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, glossary
ms.assetid: b0478836-4123-4357-969a-c5784fc28be5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1af86e92d689f262833e1bc00d8caf0fb0c78b39
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66709976"
---
# <a name="ado-glossary"></a>Glossário ADO
Este tópico define termos relevantes à ADO.  
  
## <a name="a"></a>Um  
 URL absoluta  
 Uma URL totalmente qualificada que especifica o local de um recurso que reside na Internet ou intranet. Consulte também *URL* e *URL relativa*.  
  
 Controle ActiveX  
 Registro automático no processo componente COM que geralmente tem um elemento visual no tempo de design ou no tempo de execução. Controles ActiveX também têm a capacidade de se comunicar com um contêiner de documento ativo, como o Microsoft Internet Explorer.  
  
 ADISAPI (Interface de programação de aplicativo do servidor de Internet dados de Avançado)  
 Um ISAPI DLL que fornece análise, controle de automação, conjunto de registros de marshaling e empacotamento de MIME. O componente ADISAPI funciona por meio da API fornecida pelo Internet Information Services (IIS). Consulte também *ISAPI*.  
  
 função de agregação  
 Em uma consulta, uma função como COUNT, AVG ou STDEV que calcula um valor usando todas as linhas em uma coluna de uma tabela. Escrever expressões e programação, você pode usar funções de agregação SQL (incluindo os três listados acima) e funções de agregação de domínio para determinar diversas estatísticas.  
  
 alias  
 Um nome alternativo dado a uma coluna ou expressão em uma instrução SQL SELECT, mais frequentemente curta ou significativa. Por exemplo, BobSales é o alias na instrução SELECT a seguir: "Selecione vendas wr como BobSales de SalesDB". Um alias pode ser usado para atribuir dinamicamente colunas a associações de controle no objeto DataControl.  
  
 Apartamento de threading  
 Um modelo em que todas as chamadas para um objeto ocorrerem em um thread de threading do COM. No apartamento de threading, COM sincroniza e realiza marshaling de chamadas. Consulte também *COMmddefcom*.  
  
 operação assíncrona  
 Uma operação que retorna o controle ao programa de chamada sem aguardar a conclusão da operação. Antes da operação for concluída, continua a execução de código. Consulte também *operação síncrona*.  
  
## <a name="b"></a>B  
 entrada de associação  
 Um mapeamento entre um campo em uma tabela e uma variável. Nas extensões do Visual C++ de ADO, **Recordset** campos são mapeados para variáveis de C/C++.  
  
 bitmask  
 Um valor numérico destinado a uma comparação de valor de bit por bit com outros valores numéricos, normalmente para sinalizar opções em valores de retornados ou parâmetro. Normalmente, essa comparação é feita com operadores lógicos bit a bit, tal como **e** e **ou** no Visual Basic **&** e **&#124;** em C++.  
  
 Por exemplo, o ADO **FieldAttributeEnum** valores podem ser usados como máscaras de bits para determinar os atributos de um campo. Suponha que você quiser determinar se um campo era atualizável. Você pode testar isso com a seguinte expressão no Visual Basic:`Field.Attributes AND adFldUpdatable`  
  
 Se o resultado for TRUE, o campo é atualizável.  
  
 indicador  
 Um marcador que identifica exclusivamente uma linha dentro de um conjunto de linhas para que um usuário pode navegar rapidamente para ele.  
  
 objeto de negócios  
 Um objeto que executa um conjunto definido de operações, como a lógica de regra de negócios ou validação de dados. Objetos de negócios normalmente residem na camada intermediária.  
  
 regra de negócio  
 A combinação de edições de validação, as verificações de logon, pesquisas de banco de dados, políticas e transformações algorítmicos que constituem a forma de uma empresa de fazer negócios. Também conhecido como *lógica de negócios*.  
  
## <a name="c"></a>C  
 expressão calculada  
 Uma expressão que não é constante, mas cujo valor depende de outros valores. Para ser avaliada, uma expressão calculada deve obter e computar valores de outras fontes, geralmente em outros campos ou linhas.  
  
 Capítulo  
 Uma referência a um intervalo de linhas de uma fonte de dados. No ADO, um capítulo normalmente é uma referência a outro **conjunto de registros**.  
  
 Colunas de capítulo tornam possível definir uma *pai-filho* relação em que o *pai* é o **conjunto de registros** que contém a coluna de capítulo e o  *filho* é o **Recordset** representado pelo capítulo.  
  
 alias do capítulo  
 Um alias que se refere à coluna acrescentada ao pai.  
  
 conjunto de caracteres  
 Um mapeamento de um conjunto de caracteres para seus valores numéricos. Por exemplo, o Unicode é um caractere de 16 bits definido capazes de codificar todos os caracteres conhecidos e usado como um padrão de codificação de caracteres em todo o mundo.  
  
 filho  
 O lado dependente de uma relação hierárquica. Um filho é um nó em uma estrutura hierárquica que tem outro nó acima dele (mais próximo da raiz). Consulte também *filho alias*, *relação pai-filho*, *pai*.  
  
 alias de filho  
 Um alias que se refere ao filho. Consulte também *alias*, *filho*.  
  
 CLSID (identificador de classe)  
 Um identificador universalmente exclusivo (UUID) que identifica um componente COM. Cada componente COM tem sua CLSID no registro do Windows para que ele pode ser carregado por outros aplicativos. Consulte também *ProgID*, *COM*.  
  
 camada do cliente  
 Uma camada de lógica de um sistema distribuído que normalmente apresenta dados e processos de entrada do usuário, também conhecido como o *front-end*. Normalmente, a camada do cliente e solicita dados de um servidor com base na entrada, em seguida, formata e exibe o resultado. Consulte também *camada intermediária*, *camada de fonte de dados*, *aplicativo distribuído*.  
  
 COM (Component Object Model)  
 Um padrão binário que permite que objetos interoperem em um ambiente de rede, independentemente da linguagem na qual eles foram desenvolvidos ou em quais computadores eles residem. COM base em tecnologias incluem controles ActiveX, automação e vinculação e incorporação de objetos (OLE). COM permite que um objeto exponha sua funcionalidade a outros componentes e aplicativos host. Ele define como expõe o objeto em si e como essa exposição funciona entre processos e entre redes. COM também define o ciclo de vida do objeto.  
  
 Componente COM  
 Arquivo binário - como. dll,. ocx e alguns arquivos .exe - que dá suporte ao padrão COM para fornecer a objetos. Esse arquivo contém o código para um ou mais fábricas de classes, classes COM, mecanismos de entrada do registro, código de carregamento e assim por diante.  
  
 Operador de comparação  
 Um operador que compara duas expressões e retorna um valor booliano.  
  
 Um parâmetro de critérios que pode ser expresso como ">" (maior que), "\<" (menor que), "=" (igual), "> =" (maior que ou igual), "< =" (menor ou igual), "<>" (não igual), ou "como" (correspondência de padrões).  
  
 componente  
 Um objeto que encapsula dados e código e fornece um conjunto bem específico de serviços disponíveis publicamente.  
  
 arquivo composto  
 Uma implementação de COM o armazenamento para arquivos estruturado. Um arquivo composto armazena objetos separados em um único arquivo estruturado consiste em dois elementos principais: objetos de armazenamento e transmissão de objetos. Juntos, eles funcionam como um sistema de arquivos dentro de um arquivo.  
  
 Um número de arquivos individuais são associados juntos em um arquivo físico. Cada arquivo individual em um arquivo composto pode ser acessado como se fosse um único arquivo físico.  
  
 constante  
 Um valor numérico ou cadeia de caracteres que não são alterados. Enumerações de ADO nomeadas (constantes enumeradas) podem ser usadas em seu código, em vez de valores reais, por exemplo, **adUseClient** é uma constante cujo valor é 3. (Const adUseClient = 3). Consulte também *enumeração*.  
  
 cursor  
 Um elemento de banco de dados que controla a navegação de registro, a capacidade de atualização de dados e a visibilidade das alterações feitas no banco de dados por outros usuários.  
  
## <a name="d"></a>D  
 Associação de dados  
 O processo de associar os objetos ou controles de um aplicativo para uma fonte de dados. Um controle associado a uma fonte de dados é chamado um *controle ligado a dados*.  
  
 O conteúdo de um controle associado a dados está associado com valores de um banco de dados. Por exemplo, um controle de grade é associado a um **conjunto de registros** objeto pode ser atualizado quando as linhas na **Recordset** são atualizados. Quando os novos valores são recuperados, o **Recordset**, novos valores são exibidos na grade.  
  
 provedor de dados  
 Software que expõe dados para um aplicativo ADO diretamente ou por meio de um provedor de serviços. Consulte também o provedor de serviços.  
  
 modelagem de dados  
 Uma técnica que usa uma sintaxe formalizada (chamado **linguagem de forma**) para definir um especializado **conjunto de registros** objeto (chamado um *em forma de conjunto de registros*) que não contém apenas dados, mas também referências a outras **conjunto de registros** objetos de e/ou valores calculados com base nas informações outra **Recordset** objetos.  
  
 camada de fonte de dados  
 Uma camada lógica de um sistema distribuído que representa um computador executando um DBMS, como um banco de dados do SQL Server. Consulte também *camada do cliente*, *camada intermediária*, *aplicativo distribuído*.  
  
 DCOM  
 Um protocolo de transmissão que permite que os componentes se comunicam diretamente uns com os outros em uma rede. Consulte também *COM*, *componente*.  
  
 DDL (linguagem de definição de dados)  
 Essas instruções SQL que definem, em vez de manipular os dados. O esquema de banco de dados é criado ou modificado com DDL. Por exemplo, **CREATE TABLE**, **CREATE INDEX**, **GRANT**, e **REVOGAR** são instruções DDL de SQL.  
  
 fluxo padrão  
 Um fluxo de texto ou binário (representado por um **Stream** objeto) que está associado com **registro** ou **Recordset** objetos ao usar determinados provedores OLE DB, como o Provedor Microsoft OLE DB para publicação na Internet. O fluxo padrão normalmente contém o conteúdo de um arquivo, como o código HTML para a raiz de um site da Web.  
  
 aplicativo distribuído  
 Um programa escrito de forma que o processamento pode ser dividido em vários computadores em uma rede. Normalmente, um aplicativo distribuído é dividido em apresentação, lógica de negócios e dados de camadas de armazenamento, ou *camadas*. Consulte também camada do cliente, a camada intermediária, a camada de fonte de dados.  
  
 conjunto de registros desconectado  
 Um **Recordset** objeto em um cache de cliente que não tem mais uma conexão ao vivo para o servidor. Se a fonte de dados original precisa ser acessados novamente por algum motivo, como a atualização de dados, a conexão deverá ser restabelecida. No entanto, as coleções, propriedades e métodos de um desconectada **Recordset** ainda podem ser acessados.  
  
 DML (linguagem de manipulação de dados)  
 Essas instruções em SQL que manipulam, em vez de definir os dados. Os valores em um banco de dados são selecionados e modificados com DML. Por exemplo, **inserir**, **atualização**, **excluir**, e **selecione** são instruções DML SQL.  
  
 provedor de código-fonte do documento  
 Uma classe especial de provedores que gerenciam as pastas e documentos. Quando um documento é representado por um **registro** objeto ou uma pasta de documentos é representado por uma **conjunto de registros** do objeto, o provedor de código-fonte do documento preenche esses objetos com um conjunto exclusivo de campos que descrevem as características do documento, em vez do próprio documento. Consulte também o registro de recurso.  
  
 DSN (nome de fonte de dados)  
 A coleção de informações usadas para conectar seu aplicativo para um determinado banco de dados ODBC. O Gerenciador de Driver ODBC usa essas informações para criar uma conexão ao banco de dados. Um DSN pode ser armazenado em um arquivo (um arquivo DSN) ou no registro do Windows (um DSN de máquina).  
  
 propriedade dinâmica  
 Uma propriedade específica para um provedor de dados ou o serviço de cursor. O **propriedades** coleção de um objeto é preenchida automaticamente com estas ("dinamicamente"). Um objeto não tem nenhuma propriedades dinâmicas até que ele está conectado a uma fonte de dados através de um provedor de dados específico. Consulte também data provider, o cursor.  
  
## <a name="e"></a>E  
 Enumeração  
 Uma lista de constantes nomeadas. Valores enumerados não precisam ser exclusivos. No entanto, o nome de cada valor deve ser exclusivo dentro do escopo em que a enumeração for definida. No ADO, enumerações são usadas para o parâmetro numérico em retornam valores, para adicionar o significado para código ADO e protegem o desenvolvedor contra os valores numéricos (que pode ser alterada com a versão). Por exemplo, para abrir um estático **conjunto de registros**, use o **adOpenStatic** valor enumerado: `Recordset.Open ,,adOpenStatic`  
  
 Também conhecido como *constante enumerada*. Consulte também *constante*.  
  
 event  
 Uma ação reconhecida por um objeto para o qual você pode escrever código para responder. Eventos podem ser gerados pela execução do comando, a conclusão da transação, navegação de conjunto de registros e atualizações de dados, entre outras ações. Consulte também *manipulador de eventos*.  
  
 manipulador de eventos  
 Um manipulador de eventos é o código que é executado quando ocorre um evento. Consulte também o evento.  
  
## <a name="h"></a>H  
 Manipulador  
 Uma rotina que gerencia uma operação, como o gerenciamento de dados ou de recuperação de erro ou condição comuns e relativamente simple.  
  
 conjunto de registros hierárquico  
 Um **conjunto de registros** que contém outra **conjunto de registros**. Consulte também data shaping capítulo.  
  
 Para obter mais informações, consulte [acessar linhas em um conjunto de registros hierárquicos](../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
 hierarquia  
 Em geral, uma hierarquia é uma estrutura com classificação com um top de nível e níveis subordinados. No ADO, hierárquico **conjuntos de registros** são usados para representar a relação de pai-filho entre um registro e um capítulo. Também no ADO, **registro** e **Stream** objetos podem ser usados para acessar estruturas de árvore hierárquica, como uma pasta e documentos. Também inclui ADO MD **hierarquia** objetos para representar uma relação entre os níveis de uma dimensão em um cubo OLAP. Consulte também conjuntos de registros hierárquicos, relação pai-filho, o capítulo, a árvore.  
  
## <a name="i-l"></a>I-L  
 ISAPI (Interface de programação de aplicativo de servidor da Internet)  
 Um conjunto de funções de servidores de Internet, como um Windows NT® Server/Windows 2000 Server executando o Microsoft® Internet Information Services (IIS).  
  
 Chave  
 Uma coluna ou colunas em uma tabela que identifica exclusivamente uma linha; geralmente usado para indexar uma tabela.  
  
## <a name="m"></a>M  
 Marshaling  
 O processo de empacotamento, envio e de descompactação parâmetros de método de interface entre os limites de thread ou processo.  
  
 Camada intermediária  
 A camada de lógica em um sistema distribuído entre uma interface do usuário ou cliente Web e o banco de dados. Normalmente, isso é onde os objetos comerciais são instanciados. A camada intermediária é uma coleção de regras de negócio e funções que geram e operam em cima de receber informações. Eles realizam isso por meio de regras de negócio que podem ser alterados com frequência e, portanto, são encapsuladas em componentes que estão fisicamente separadas da lógica do aplicativo em si. Também conhecido como *camada de servidor de aplicativo*. Consulte também aplicativo distribuído, a camada do cliente, a camada de fonte de dados.  
  
 MIME (Multi-purpose Internet Mail Extension)  
 Um protocolo originalmente desenvolvido para permitir a troca de mensagens de email com conteúdo avançado em ambientes de email, computador e rede heterogênea. Na prática, MIME também foi adotado e estendida por aplicativos não são de correio.  
  
 MIME é um padrão que permite que os dados binários a ser publicado e ler na Internet. O cabeçalho de um arquivo com dados binários contém o tipo MIME dos dados. Isso informa os programas clientes (navegadores da Web e pacotes de email, por exemplo) que será necessário manipular os dados de maneira diferente do que tratam de texto simples. Por exemplo, o cabeçalho de um documento da Web que contém uma imagem JPEG contém o tipo MIME específico para o formato de arquivo JPEG. Isso permite que um navegador exibir o arquivo com o visualizador JPEG, caso haja algum.  
  
## <a name="n-o"></a>N-O  
 nó  
 Um elemento em uma estrutura de árvore hierárquica. Um nó pode ser a raiz ou o filho de outro nó. Um nó também pode ser o pai de vários filhos. Consulte também hierarquia, árvore, raiz, filho e pai.  
  
 variável de objeto  
 Uma variável que contém uma referência a um objeto. Por exemplo, `objCustomObject` é uma variável que aponta para um objeto do tipo ObjetoPersonalizado:`Set objCustomObject = CreateObject(adodb.Recordset)`  
  
 ODBC (Open Database Connectivity)  
 Uma linguagem interface de programação padrão usada para se conectar a uma variedade de fontes de dados. Isso geralmente é acessado por meio do painel de controle, em que os nomes de fonte de dados (DSNs) podem ser atribuídos a usar drivers ODBC específicos.  
  
 OLE DB  
 Um conjunto de interfaces que expõem dados de uma variedade de fontes usando COM. Interfaces do OLE DB oferecem aplicativos acesso padronizado aos dados armazenados em várias fontes de informação. Essas interfaces de suporte a quantidade de funcionalidade do DBMS apropriada para a fonte de dados, permitindo que ele compartilhe os próprios dados. Consulte também COM.  
  
 bloqueio otimista  
 Um tipo de proteção no qual a página de dados que contém um ou mais registros, incluindo o registro que está sendo editado, não está disponível para outros usuários somente enquanto o registro está sendo atualizado pela **atualização** método, mas está disponível antes e depois o chamada para **atualização**.  
  
 Bloqueio otimista é usado quando o **conjunto de registros** objeto é aberto com o **LockType** parâmetro ou a propriedade definida como **adLockOptimistic** ou  **adLockBatchOptimistic**. Consulte também pessimista.  
  
 valor ordinal  
 O local numérico de um item em um pedido. Em uma coleção de ADO, o valor ordinal do primeiro item é zero (0). O próximo item é um (1) e assim por diante.  
  
## <a name="p"></a>P  
 comando com parâmetros  
 Uma consulta ou um comando que permite que você defina valores de parâmetro antes do comando é executado. Por exemplo, uma cadeia de caracteres SQL pode ser parametrizada, inserindo marcadores de parâmetro na cadeia de caracteres SQL (designado pelo '?' caracteres). O aplicativo, em seguida, especifica valores para cada parâmetro e executa o comando.  
  
 pai  
 O lado de controle de uma relação hierárquica. Em uma estrutura hierárquica, um pai tem um ou mais nós filho diretamente abaixo na hierarquia. Consulte também alias pai, filho e relação pai-filho.  
  
 parent-alias  
 Um alias que se refere ao pai. Consulte também alias, o pai.  
  
 relação pai-filho  
 Uma relação em uma estrutura hierárquica no qual o pai é um nível superior e diretamente associado a um ou mais filhos. Um filho é um nível inferior e deve ter um pai. Consulte também o pai, filho.  
  
 Bloqueio pessimista  
 Um tipo de proteção no qual a página que contém um ou mais registros, incluindo o registro que está sendo editado, está disponível para outros usuários para garantir que uma atualização será feita. Comportamento de bloqueio pessimista é definido pelo provedor OLE DB. Normalmente, os registros estão bloqueados na edição e ficam indisponíveis até que o **atualização** método for concluído.  
  
 Bloqueio pessimista é habilitado quando o **conjunto de registros** objeto é aberto com o **LockType** parâmetro ou a propriedade definida como **adLockPessimistic**. Consulte o bloqueio otimista também.  
  
 Pooling  
 Uma otimização de desempenho com base no uso de coleções de recursos pré-alocados, como conexões de banco de dados ou objetos. Ele é mais eficiente para desenhar um recurso existente do pool que criar um novo recurso.  
  
 ProgID (identificador programático)  
 Um nome exclusivo mapeado para o registro do Windows por um aplicativo COM. O ProgID para uma Conexão ADO é "ADODB. Conexão". Consulte também o CLSID, COM.  
  
 Proxy  
 Um objeto específico de interface que fornece o marshaling do parâmetro e comunicação necessárias para um cliente chamar um objeto de aplicativo que está em execução em um ambiente de execução diferente, como em um thread diferente ou em outro processo. O proxy está localizado com o cliente e se comunica com um stub correspondente que está localizado com o objeto de aplicativo que está sendo chamado. Consulte também o stub.  
  
## <a name="r"></a>R  
 URL relativa  
 Uma URL parcialmente qualificada que especifica um recurso na Internet ou intranet cujo local é relativo ao ponto de partida especificado por uma URL absoluta ou um objeto de Conexão ADO equivalente. Em vigor, o concatenado absoluta e relativa URLs consitute uma URL completa. Consulte também URL e a URL absoluta.  
  
 fonte de dados remota  
 Uma fonte de dados que existe em um outro computador, em vez de no sistema local (em que o aplicativo cliente é executado).  
  
 resource record  
 Um registro de um provedor de origem de documento que contém campos para a definição e a descrição de uma pasta ou documento. O documento em si não está contido no registro de recurso, mas normalmente pode ser acessado por fluxo padrão ou um campo no registro de recurso que contém uma URL. Consulte também o provedor de código-fonte do documento, fluxo de padrão de URL.  
  
 conjunto de linhas  
 Um conjunto de linhas de uma fonte de dados, tudo que tem o mesmo esquema de campo. Um conjunto de linhas pode representar alguns ou todos os campos de uma tabela. Um conjunto de linhas também pode representar uma tabela virtual, criada por uma consulta ou uma junção de duas ou mais tabelas. No ADO, conjuntos de linhas são representados por **Recordset** objetos.  
  
## <a name="s"></a>P  
 Scope  
 O intervalo de referência para um objeto ou variável ou um intervalo de registros em uma tabela ou exibição. Por exemplo, variáveis locais podem ser referenciadas apenas dentro do procedimento no qual eles foram definidos. Variáveis públicas são acessíveis de qualquer lugar no aplicativo. Objetos, como o banco de dados atual, estão no escopo se eles estão no caminho de pesquisa definido. Intervalos de registro podem ser especificados com uma cláusula de escopo em muitos comandos.  
  
 provedor de serviços  
 Software que encapsula um serviço, produzindo e consumindo dados, aumentando os recursos em seus aplicativos do ADO. É um provedor que não expõe dados diretamente, em vez disso, ele fornece um serviço, como processamento de consulta. O provedor de serviço pode processar os dados fornecidos pelo provedor de dados. Consulte também o provedor de dados.  
  
 conjunto de registros moldado  
 Um **conjunto de registros** cujas colunas foram definidas especificamente para conter não apenas dados, mas também (chamadas de capítulos) de referências a outras **Recordset** objetos e/ou valores calculados com base em outros **Recordset** objetos.  
  
 irmão  
 Quaisquer duas ou mais nós em uma estrutura hierárquica que estão no mesmo nível na hierarquia. O nó de raiz em uma hierarquia não tem nenhum irmão.  
  
 procedimento armazenado  
 Uma coleção pré-compilada de código, como instruções SQL e instruções de controle de fluxo opcionais armazenadas sob um nome e processadas como uma unidade. Procedimentos armazenados são armazenados dentro de um banco de dados; eles podem ser executados com uma chamada de um aplicativo e permitem variáveis declarado pelo usuário, execução condicional e outros recursos avançados de programação.  
  
 Stub  
 Um objeto específico de interface que fornece o marshaling do parâmetro e a comunicação necessária para um objeto de aplicativo receber chamadas de um cliente que está em execução em um ambiente de execução diferente, como em um thread diferente ou em outro processo. O fragmento de código está localizado com o objeto de aplicativo e se comunica com um proxy correspondente que está localizado com o cliente que o chama. Consulte também o proxy.  
  
 subnó  
 Consulte filho.  
  
 operação síncrona  
 Uma operação iniciada pelo código que seja concluído antes da próxima operação pode iniciar. Consulte também a operação assíncrona.  
  
## <a name="t-z"></a>T-Z  
 trEE  
 Uma estrutura que representa uma relação hierárquica entre os elementos (nós). Há um nó de nível superior de uma árvore (raiz). Abaixo da raiz, pode haver vários filhos. Cada filho por sua vez pode ser o pai de outros filhos, ramificação, portanto, como uma árvore. Uma pasta que contém outras pastas e documentos é um exemplo típico de uma estrutura de árvore. Consulte também hierarquia, nó, raiz, filho e pai.  
  
 Servidor Web  
 Um computador que fornece serviços da Web e páginas para usuários de Internet e intranet.

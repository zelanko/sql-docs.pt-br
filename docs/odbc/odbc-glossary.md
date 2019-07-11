---
title: Glossário do ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], glossary
- glossary [ODBC]
ms.assetid: e8227000-1944-42e5-a881-1f549e1ff9d1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a6741b5f07f2427ef502f5177bbf01acd56c4d5b
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794175"
---
# <a name="odbc-glossary"></a>Glossário do ODBC
## <a name="a"></a>Um  
 **plano de acesso**  
 Um plano gerado pelo mecanismo de banco de dados para executar uma instrução SQL. Equivalente ao código executável compilado a partir de uma linguagem de terceira geração, como C.  
  
 **Função de agregação**  
 Uma função que gera um único valor de um grupo de valores, frequentemente usado com **GROUP BY** e **HAVING** cláusulas. Incluem funções agregadas **AVG**, **contagem**, **MAX**, **MIN**, e **soma**. Também conhecido como *funções do conjunto*. *Consulte também* função escalar.  
  
 **ANSI**  
 American National Standards Institute. A API ODBC baseia-se na Interface de nível de chamada de ANSI.  
  
 **APD**  
 *Consulte* parâmetro APD (descritor aplicativo).  
  
 **API**  
 Interface de programação de aplicativo. Um conjunto de rotinas que um aplicativo usa para solicitar e executar serviços de nível inferior. A API do ODBC é composta de funções ODBC.  
  
 **application**  
 Um programa executável que chama as funções na API do ODBC.  
  
 **parâmetro APD (descritor aplicativo)**  
 Um descritor que descreve os parâmetros dinâmicos usados em uma instrução SQL antes de qualquer conversão especificado pelo aplicativo.  
  
 **descritor de linha de aplicativo (descartar)**  
 Um descritor que representa os metadados de coluna e dados em buffers do aplicativo, que descreve uma linha de dados seguindo qualquer conversão de dados especificado pelo aplicativo.  
  
 **DESCARTAR**  
 *Consulte* descritor de linha de aplicativo (descartar).  
  
 **modo de confirmação automática**  
 Um modo de confirmação de transação na qual as transações são confirmadas imediatamente depois que eles sejam executados.  
  
## <a name="b"></a>B  
 **alteração de comportamento**  
 Uma alteração em determinada funcionalidade do ODBC *3.x* comportamento ao ODBC *2.x* comportamento, ou vice-versa. Causado por alterar o atributo de ambiente SQL_ATTR_ODBC_VERSION.  
  
 **Objeto binário grande (BLOB)**  
 Quaisquer dados binários durante um determinado número de bytes, como 255. Normalmente muito maior. Esses dados geralmente são enviados para e recuperados da fonte de dados em partes. Também conhecido como *dados long*.  
  
 **binding**  
 Como um verbo, o ato de associar uma coluna em um conjunto de resultados ou um parâmetro em uma instrução SQL com uma variável de aplicativo. Como um substantivo, a associação.  
  
 **deslocamento de associação**  
 Um valor adicionado para os endereços de buffer de dados e comprimento/indicador buffer para todos os associado ao parâmetro ou coluna de dados, produzir novos endereços.  
  
 **cursor em bloco**  
 Um cursor com capacidade de busca de mais de uma linha de dados por vez.  
  
 **buffer**  
 Uma parte da memória de aplicativo usada para passar dados entre o aplicativo e o driver. Buffers geralmente vêm em pares: uma *buffer de dados* e uma *buffer de comprimento de dados*.  
  
 **byte**  
 Oito bits ou um octeto. *Consulte também* octeto.  
  
## <a name="c"></a>C  
 **Tipo de dados C**  
 O tipo de dados de uma variável em um programa C, neste caso, o aplicativo.  
  
 **catalog**  
 O conjunto de tabelas do sistema em um banco de dados que descrevem a forma do banco de dados. Também conhecido como um *esquema* ou *dicionário de dados*.  
  
 **função de catálogo**  
 Uma função ODBC usada para recuperar informações do catálogo do banco de dados.  
  
 **CLI**  
 *Consulte* API.  
  
 **client/server**  
 Uma estratégia de acesso de banco de dados no qual um ou mais clientes acessam dados por meio de um servidor. Os clientes geralmente implementam a interface do usuário, enquanto os controles de servidor de banco de dados access.  
  
 **column**  
 O contêiner para um único item de informações em uma linha. Também conhecido como *campo*.  
  
 **commit**  
 Para fazer as alterações em uma transação permanente.  
  
 **concurrency**  
 A capacidade de mais de uma transação para acessar os mesmos dados ao mesmo tempo.  
  
 **nível de conformidade**  
 Um conjunto discreto de funcionalidade com suporte por uma driver ou fonte de dados. ODBC define os níveis de conformidade de API e níveis de conformidade do SQL.  
  
 **conexão**  
 Uma instância específica de uma fonte de dados e driver.  
  
 **navegação de conexão**  
 Pesquisar a rede para fontes de dados para se conectar ao. Navegação de Conexão pode envolver várias etapas. Por exemplo, o usuário pode primeiro procurar servidores na rede e, em seguida, procure um servidor específico para um banco de dados.  
  
 **Identificador de conexão**  
 Um identificador para uma estrutura de dados que contém informações sobre uma conexão.  
  
 **Linha atual**  
 Atualmente, a linha apontada pelo cursor. Operações posicionadas atuam na linha atual.  
  
 **cursor**  
 Uma parte do software que retorna linhas de dados para o aplicativo. Provavelmente é chamado após o cursor piscando em um computador com terminal; Assim como o cursor indica a posição atual na tela, um cursor em um conjunto de resultados indica a posição atual no conjunto de resultados.  
  
## <a name="d"></a>D  
 **data buffer**  
 Um buffer usado para passar dados. Muitas vezes associados com dados de um buffer é uma *buffer de comprimento de dados*.  
  
 **dicionário de dados**  
 *Consulte* catálogo.  
  
 **buffer de comprimento de dados**  
 Um buffer usado para passar o comprimento do valor em uma correspondente *buffer de dados*. O buffer de comprimento de dados também é usado para armazenar os indicadores, como se o valor de dados é terminada em nulo.  
  
 **Fonte de dados**  
 Os dados que o usuário deseja acesso e seu sistema operacional associado, DBMS e plataforma de rede (se houver).  
  
 **Tipo de dados**  
 O tipo de uma parte dos dados. ODBC define os tipos de dados SQL e C. *Consulte também* indicador de tipo.  
  
 **coluna de dados em execução**  
 Uma coluna para o qual os dados são enviados após **SQLSetPos** é chamado. Esse nome porque os dados são enviados no tempo de execução em vez de ser colocada em um buffer de conjunto de linhas. Dados Long geralmente são enviados em partes em tempo de execução.  
  
 **parâmetro de dados em execução**  
 Um parâmetro para o qual os dados são enviados após **SQLExecute** ou **SQLExecDirect** é chamado. Esse nome porque os dados são enviados quando a instrução SQL é executada em vez de ser colocada em um buffer de parâmetro. Dados Long geralmente são enviados em partes em tempo de execução.  
  
 **banco de dados**  
 Um conjunto discreto de dados em um DBMS. Também é um DBMS.  
  
 **Mecanismo de banco de dados**  
 O software em um DBMS que analisa e executa instruções SQL e acessa os dados físicos.  
  
 **DBMS**  
 Sistema de gerenciamento de banco de dados. Uma camada de software entre um banco de dados físico e o usuário. O DBMS gerencia todo o acesso ao banco de dados.  
  
 **Drivers baseados em DBMS**  
 Um driver que acessa dados físicos por meio de um mecanismo de banco de dados autônomo.  
  
 **DDL**  
 Linguagem de definição de dados. Essas instruções SQL que definem, em vez de manipular os dados. Por exemplo, **CREATE TABLE**, **CREATE INDEX**, **GRANT**, e **REVOGAR**.  
  
 **delimited identifier**  
 Um identificador que é colocado entre caracteres de aspas do identificador para que ele possa conter caracteres especiais ou corresponder a palavras-chave (também conhecido como um identificador entre aspas).  
  
 **descriptor**  
 Uma estrutura de dados que contém informações sobre os dados da coluna ou parâmetros dinâmicos. A representação física do descritor não está definida. os aplicativos obtêm acesso direto para um descritor de apenas por meio da manipulação seus campos chamando funções ODBC com o identificador do descritor.  
  
 **banco de dados da área de trabalho**  
 Um DBMS projetado para ser executado em um computador pessoal. Geralmente, esses DBMSs não fornecem um mecanismo de banco de dados autônomo e devem ser acessados por meio de um driver com base em arquivo. Os mecanismos desses drivers geralmente reduziram o suporte para SQL e transações. Por exemplo, dBASE, Paradox, Btrieve ou FoxPro para Microsoft®.  
  
 **diagnostic**  
 Um registro que contém informações de diagnóstico sobre a última função chamada que usado um identificador específico. Registros de diagnóstico são associados com ambiente, conexão, instrução e identificadores de descritor.  
  
 **DML**  
 Linguagem de manipulação de dados. Essas instruções em SQL que manipulam, em vez de definir os dados. Por exemplo, **inserir**, **atualização**, **excluir**, e **selecione**.  
  
 **driver**  
 Uma biblioteca de rotina que expõe as funções na API do ODBC. Drivers são específicos para um único DBMS.  
  
 **Driver Manager**  
 Uma biblioteca de rotina que gerencia o acesso aos drivers para o aplicativo. O Gerenciador de Driver carrega e descarrega (ou se conecta ao e desconecta) chamadas de drivers e passa para funções ODBC para o driver correto.  
  
 **DLL de instalação do driver**  
 Uma DLL que contém funções de instalação e configuração específicos do driver.  
  
 **cursor dinâmico**  
 Um cursor rolável capaz de detectar linhas atualizadas, excluídas ou inseridas no conjunto de resultados.  
  
 **dynamic SQL**  
 Um tipo de SQL inserido no qual o SQL instruções são criadas e compiladas em tempo de execução. *Consulte também* SQL estático.  
  
## <a name="e"></a>E  
 **SQL inserido**  
 Instruções SQL que são incluídas diretamente em um programa escrito em outra linguagem, como COBOL ou ODBC C. não use embedded SQL. *Consulte também* SQL estático *e* SQL dinâmico.  
  
 **environment**  
 Um contexto global no qual acessar dados; associado com o ambiente é todas as informações que são globais por natureza, como uma lista de todas as conexões no ambiente.  
  
 **Identificador de ambiente**  
 Um identificador para uma estrutura de dados que contém informações sobre o ambiente.  
  
 **cláusula de escape**  
 Uma cláusula em uma instrução SQL.  
  
 **execute**  
 Para executar uma instrução SQL.  
  
## <a name="f"></a>F  
 **cursor FAT**  
 *Consulte* cursor em bloco.  
  
 **fetch**  
 Para recuperar uma ou mais linhas de um conjunto de resultados.  
  
 **field**  
 *Consulte* coluna.  
  
 **com base no arquivo de driver**  
 Um driver que acessa dados físicos diretamente. Nesse caso, o driver contém um mecanismo de banco de dados e atua como o driver e a fonte de dados.  
  
 **fonte de dados de arquivo**  
 Uma fonte de dados para o qual conexão informações são armazenadas em um arquivo. DSN.  
  
 **Chave estrangeira**  
 Uma coluna ou colunas em uma tabela que corresponde à chave primária em outra tabela.  
  
 **cursor de somente avanço**  
 Um cursor que só pode mover para frente por meio do conjunto de resultados e, em geral, buscará apenas uma linha por vez. A maioria dos bancos de dados relacionais dão suporte a apenas os cursores de somente avanço.  
  
## <a name="h"></a>H  
 **handle**  
 Um valor que identifica exclusivamente algo como uma estrutura de dados ou arquivo. Os identificadores são significativos apenas para o software que cria e usa-los, mas é passado por outros softwares para identificar as coisas. ODBC define identificadores para ambientes, conexões, instruções e descritores.  
  
## <a name="i"></a>I  
 **descritor de parâmetro de implementação (IPD)**  
 Um descritor que descreve os parâmetros dinâmicos usados em uma instrução SQL após qualquer conversão especificado pelo aplicativo.  
  
 **descritor de linha de implementação (IRD)**  
 Um descritor que descreve uma linha de dados antes de qualquer conversão especificado pelo aplicativo.  
  
 **DLL do instalador**  
 Uma DLL que instala os componentes ODBC e configura fontes de dados.  
  
 **Integrity Enhancement Facility**  
 Um subconjunto de SQL criado para manter a integridade de um banco de dados.  
  
 **nível de conformidade de interface**  
 O nível da interface ODBC 3.7 compatível com um driver. pode ser o Core, nível 1 ou nível 2.  
  
 **interoperability**  
 A capacidade de um aplicativo para usar o mesmo código, ao acessar dados em DBMSs diferentes.  
  
 **IPD**  
 *Consulte* descritor de parâmetro de implementação (IPD).  
  
 **IRD**  
 *Consulte* linha de implementação IRD (descritor).  
  
 **ISO/IEC**  
 Padrões internacionais comissão de eletrotécnica internacional/organização. A API de ODBC é baseada na Interface de nível de chamada de ISO/IEC.  
  
## <a name="j"></a>J  
 **join**  
 Uma operação em um banco de dados relacional que vincula as linhas em duas ou mais tabelas combinando valores de colunas especificadas.  
  
## <a name="k"></a>K  
 **key**  
 Uma coluna ou colunas cujos valores de identificam uma linha. *Consulte também* chave estrangeira *e* chave primária.  
  
 **keyset**  
 Um conjunto de chaves usado por um cursor misto ou controlados por para buscar linhas.  
  
 **cursor controlado por conjunto de chaves**  
 Um cursor rolável que detecta linhas atualizadas e excluídas por meio de um conjunto de chaves.  
  
## <a name="l"></a>L  
 **literal**  
 Uma representação de caractere de um valor de dados reais em uma instrução SQL.  
  
 **locking**  
 O processo pelo qual um DBMS restringe o acesso a uma linha em um ambiente multiusuário. O DBMS geralmente define um bit em uma linha ou página física que contém uma linha que indica a linha ou página é bloqueada.  
  
 **dados Long**  
 Quaisquer dados binários ou de caractere em um determinado comprimento, como 255 bytes ou caracteres. Normalmente muito maior. Esses dados geralmente são enviados para e recuperados da fonte de dados em partes. Também conhecido como *BLOB*s ou *CLOB*s.  
  
## <a name="m"></a>M  
 **fonte de dados de máquina**  
 Uma fonte de dados para o qual conexão informações são armazenadas no sistema (por exemplo, o registro).  
  
 **Modo de confirmação manual**  
 Um modo de confirmação de transação na qual as transações devem ser confirmadas explicitamente chamando **SQLTransact**.  
  
 **metadata**  
 Dados que descrevem um parâmetro em uma instrução SQL ou uma coluna em um conjunto de resultados. Por exemplo, o tipo de dados, comprimento em bytes e a precisão de um parâmetro.  
  
 **driver de várias camadas**  
 *Consulte* drivers baseados em DBMS.  
  
## <a name="n"></a>N  
 **Valor nulo**  
 Não tendo nenhum valor explicitamente atribuído. Em particular, um valor NULL é diferente de zero ou um espaço em branco.  
  
## <a name="o"></a>O  
 **octet**  
 Oito bits ou um byte. *Consulte também* bytes.  
  
 **octet length**  
 O comprimento em octetos de um buffer ou os dados que ele contém.  
  
 **ODBC**  
 Abrir a conectividade de banco de dados. Uma especificação de uma API que define um conjunto padrão de rotinas com o qual um aplicativo pode acessar dados em uma fonte de dados.  
  
 **Administrador de ODBC**  
 Um programa executável que chama o instalador do DLL para configurar fontes de dados.  
  
 Open Group  
 Uma empresa que publica os padrões. Em particular, ele publica os padrões de grupo de acesso do SQL (SAG).  
  
 **Simultaneidade otimista**  
 Uma estratégia para aumentar a simultaneidade no qual linhas não são bloqueadas. Em vez disso, antes que eles são atualizados ou excluídos, um cursor verifica para ver se eles foram alterados desde que eles foram lidos pela última vez. Nesse caso, a atualização ou exclusão falhará. *Consulte também* simultaneidade pessimista.  
  
 **junção externa**  
 Uma junção em quais linhas não correspondentes e correspondentes são retornadas. Os valores de todas as colunas da tabela sem correspondência no linhas não correspondentes são definidos como NULL.  
  
 **owner**  
 O proprietário de uma tabela.  
  
## <a name="p"></a>P  
 **parameter**  
 Uma variável em uma instrução SQL, marcada com um marcador de parâmetro ou um ponto de interrogação (?). Parâmetros são associados a variáveis de aplicativo e seus valores recuperados quando a instrução é executada.  
  
 **descritor de parâmetro**  
 Um descritor que descreve os parâmetros de tempo de execução usados em uma instrução SQL, tanto antes de qualquer conversão especificada pelo aplicativo (um descritor de parâmetro de aplicativo ou APD) ou após qualquer conversão especificado pelo aplicativo (uma implementação descritor de parâmetro ou IPD).  
  
 **matriz de operação de parâmetros**  
 Uma matriz que contém valores que um aplicativo pode definir para indicar que o parâmetro correspondente deve ser ignorado em uma **SQLExecDirect** ou **SQLExecute** operação.  
  
 **matriz de status de parâmetro**  
 Uma matriz que contém o status de um parâmetro após uma chamada para **SQLExecDirect** ou **SQLExecute**.  
  
 **simultaneidade pessimista**  
 Uma estratégia para a implementação de serialização, em que linhas são bloqueadas para que outras transações não podem alterá-los. *Consulte também* simultaneidade otimista *e* serialização.  
  
 **operação posicionada**  
 Qualquer operação que atua na linha atual. Por exemplo, posicionado atualização e instruções, delete **SQLGetData**, e **SQLSetPos**.  
  
 **instrução de atualização posicionadas**  
 Uma instrução SQL usada para atualizar os valores na linha atual.  
  
 **instrução delete posicionadas**  
 Uma instrução SQL usada para excluir a linha atual.  
  
 **prepare**  
 Para compilar uma instrução SQL. Um plano de acesso é criado por preparar uma instrução SQL.  
  
 **Chave primária**  
 Uma coluna ou colunas que identifica exclusivamente uma linha em uma tabela.  
  
 **procedure**  
 Um grupo de um ou mais pré-compilada de instruções SQL que são armazenadas como um objeto nomeado em um banco de dados.  
  
 **coluna de procedimento**  
 Um argumento em uma chamada de procedimento, o valor retornado por um procedimento ou uma coluna em um conjunto de resultados criado por um procedimento.  
  
## <a name="q"></a>Q  
 **qualifier**  
 Um banco de dados que contém uma ou mais tabelas.  
  
 **query**  
 Uma instrução SQL. Às vezes, é usado para significar uma **selecionar** instrução.  
  
 **identificador entre aspas**  
 Um identificador que é colocado entre caracteres de aspas do identificador para que ele possa conter caracteres especiais ou corresponder a palavras-chave (também conhecidas em SQL-92, como um identificador delimitado).  
  
## <a name="r"></a>R  
 **radix**  
 A base de um sistema de número. Normalmente, 2 ou 10.  
  
 **record**  
 *Consulte* linha.  
  
 **conjunto de resultados**  
 O conjunto de linhas criados pela execução de um **selecionar** instrução.  
  
 **Código de retorno**  
 O valor retornado por uma função ODBC.  
  
 **Reverter**  
 Para retornar os valores alterados por uma transação para seu estado original.  
  
 **row**  
 Um conjunto de colunas relacionadas que descrevem uma entidade específica. Também conhecido como um *registro*.  
  
 **descritor de linha**  
 Um descritor que descreve as colunas de um conjunto de resultados, antes de qualquer conversão especificada pelo aplicativo (um descritor de linha de implementação ou IRD) ou após qualquer conversão especificado pelo aplicativo (um descritor de linha de aplicativo ou descartar).  
  
 **matriz de operação de linha**  
 Uma matriz que contém valores que um aplicativo pode definir para indicar que a linha correspondente deve ser ignorada em uma **SQLSetPos** operação.  
  
 **matriz de status de linha**  
 Uma matriz que contém o status de uma linha após uma chamada para **SQLFetch**, **SQLFetchScroll**, ou **SQLSetPos**.  
  
 **rowset**  
 O conjunto de linhas retornadas em uma única busca por um cursor em bloco.  
  
 **buffers de conjunto de linhas**  
 Os buffers associados às colunas de um conjunto de resultados e, em que os dados para um conjunto de linhas inteiro serão retornados.  
  
## <a name="s"></a>P  
 **SAG**  
 *Consulte* SQL Access Group (SAG).  
  
 **função escalar**  
 Uma função que gera um único valor de um único valor. Por exemplo, uma função que altera o caso de dados de caracteres.  
  
 **schema**  
 *Consulte* catálogo.  
  
 **cursor rolável**  
 Um cursor que pode se mover para frente ou para trás com o conjunto de resultados.  
  
 **serializability**  
 Se duas transações sendo executadas simultaneamente produzem um resultado que é o mesmo que a execução serial (ou sequencial) dessas transações. Transações serializáveis são necessários para manter a integridade do banco de dados.  
  
 **banco de dados do servidor**  
 Um DBMS são projetados para serem executados em um ambiente cliente/servidor. Esses DBMSs fornecem um mecanismo de banco de dados autônomo que fornece suporte avançado para SQL e transações. Eles são acessados por meio de drivers baseados em DBMS. Por exemplo, Oracle, Informix, DB/2 ou o Microsoft® SQL Server.  
  
 **função Set**  
 *Consulte* função de agregação.  
  
 **DLL de instalação**  
 *Ver* DLL de instalação do driver *e* DLL de instalação do conversor.  
  
 **driver de camada única**  
 *Consulte* driver baseado em arquivo.  
  
 **SQL**  
 Linguagem de consulta estruturada. Um idioma usado por bancos de dados relacionais para consultar, atualizar e gerenciar dados.  
  
 **Grupo de acesso do SQL (SAG)**  
 Um consórcio do setor de empresas se preocupa com DBMSs de SQL. Interface de nível de chamada do The Open Group baseia-se no trabalho realizado originalmente pelo grupo de acesso de SQL.  
  
 **Nível de conformidade do SQL**  
 O nível de gramática de SQL-92 com suporte por um driver; pode ser a entrada, Transitional FIPS, intermediário ou completo.  
  
 **Tipo de dados SQL**  
 O tipo de dados de uma coluna ou parâmetro conforme ele é armazenado na fonte de dados.  
  
 **SQLSTATE**  
 Um valor de cinco caracteres que indica um erro específico.  
  
 **Instrução SQL**  
 Uma frase completa em SQL que começa com uma palavra-chave e descreve completamente uma ação a ser executada. Por exemplo, selecione * de pedidos. Instruções SQL não devem ser confundidas com instruções.  
  
 **state**  
 Uma condição bem definida de um item. Por exemplo, uma conexão tem sete estados, incluindo dados não alocados, alocados, conectados e precisando. Determinadas operações podem ser feitas somente quando um item está em um estado específico. Por exemplo, uma conexão pode ser liberado apenas quando ele está em um estado alocado e não, por exemplo, quando ele está em um estado conectado.  
  
 **transição de estado**  
 A movimentação de um item de um estado para outro. ODBC define transições de estado rigorosos para ambientes, conexões e instruções.  
  
 **instrução**  
 Um contêiner para todas as informações relacionadas a uma instrução SQL. Instruções não devem ser confundidas com instruções SQL.  
  
 **Identificador de instrução**  
 Um identificador para uma estrutura de dados que contém informações sobre uma instrução.  
  
 **cursor estático**  
 Um cursor rolável que não consegue detectar atualizações, exclui ou insere no conjunto de resultados. Geralmente é implementado fazendo uma cópia do conjunto de resultados.  
  
 **static SQL**  
 Um tipo de SQL inserido no qual o SQL instruções são embutidos e compiladas quando o restante do programa é compilado. *Consulte também* SQL dinâmico.  
  
 **procedimento armazenado**  
 *Consulte* procedimento.  
  
## <a name="t"></a>T  
 **table**  
 Uma coleção de linhas.  
  
 **thunking**  
 A conversão de 16 bits endereços para os endereços de 32 bits ou vice-versa, quando os aplicativos de 16 bits são usados com drivers ODBC de 32 bits.  
  
 **transaction**  
 Uma unidade atômica de trabalho. O trabalho em uma transação deve ser concluído como um todo; Se qualquer parte da transação falhar, a transação inteira falhará.  
  
 **Isolamento de transação**  
 O ato de isolamento de transação de um dos efeitos de todas as outras transações.  
  
 **Nível de isolamento da transação**  
 Uma medida de quão bem uma transação é isolada. Há cinco níveis de isolamento da transação: Leitura não confirmada, leia a leitura confirmada, repetível, serializável e o controle de versão.  
  
 **tradutor de DLL**  
 Uma DLL usada para converter dados de um conjunto de caracteres para outra.  
  
 **DLL de instalação do tradutor**  
 Uma DLL que contém funções de instalação e configuração específicas do conversor.  
  
 **confirmação de duas fases**  
 O processo de confirmação de uma transação distribuída em duas fases. Na primeira fase, o processador de transação verifica que todas as partes da transação podem ser confirmadas. Na segunda fase, todas as partes da transação serão confirmadas. Se qualquer parte da transação indica na primeira fase, que não pode ser confirmada, a segunda fase não ocorrerá. ODBC não dá suporte a confirmações em duas fases.  
  
 **Indicador de tipo**  
 Um valor inteiro passado para ou retornado de uma função ODBC para indicar o tipo de dados de uma variável de aplicativo, um parâmetro ou uma coluna. ODBC define indicadores de tipo para tipos de dados C e SQL.  
  
## <a name="v"></a>V  
 **modo de exibição**  
 Uma maneira alternativa de examinar os dados em uma ou mais tabelas. Geralmente, uma exibição é criada como um subconjunto das colunas de uma ou mais tabelas. No ODBC, as exibições são geralmente equivalentes às tabelas.

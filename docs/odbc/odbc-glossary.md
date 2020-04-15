---
title: Glossário ODBC | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac454a8c57fe6e2f12724440dc37c3a1953e4c85
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302897"
---
# <a name="odbc-glossary"></a>Glossário do ODBC
## <a name="a"></a>Um  
 **plano de acesso**  
 Um plano gerado pelo mecanismo de banco de dados para executar uma declaração SQL. Equivalente ao código executável compilado a partir de uma linguagem de terceira geração, como C.  
  
 **função agregada**  
 Uma função que gera um único valor a partir de um grupo de valores, muitas vezes usado com cláusulas **GROUP BY** e **HAVING.** As funções agregadas incluem **AVG,** **COUNT,** **MAX,** **MIN**e **SUM**. Também conhecido como *funções de conjunto*. *Veja também* a função escalar.  
  
 **ANSI**  
 Instituto Americano de Padrões Nacionais. A API ODBC é baseada na Interface de Nível de Chamada ANSI.  
  
 **APD**  
 *Consulte* o descritor do parâmetro de aplicação (APD).  
  
 **API**  
 Interface de programação de aplicativos. Um conjunto de rotinas que um aplicativo usa para solicitar e executar serviços de nível inferior. A API ODBC é composta pelas funções ODBC.  
  
 **aplicativo**  
 Um programa executável que chama funções na API ODBC.  
  
 **descritor de parâmetro de aplicação (APD)**  
 Um descritor que descreve os parâmetros dinâmicos usados em uma declaração SQL antes de qualquer conversão especificada pelo aplicativo.  
  
 **descritor de linha de aplicação (ARD)**  
 Um descritor que representa os metadados e dados da coluna nos buffers do aplicativo, descrevendo uma linha de dados após qualquer conversão de dados especificada pelo aplicativo.  
  
 **Ard**  
 *Consulte* o descritor da linha de aplicação (ARD).  
  
 **modo de confirmação automática**  
 Um modo de confirmação de transações no qual as transações são cometidas imediatamente após a execução.  
  
## <a name="b"></a>B  
 **mudança comportamental**  
 Uma mudança em certas funcionalidades do comportamento do ODBC *3.x* para o comportamento do ODBC *2.x,* ou vice-versa. Causada pela alteração do atributo SQL_ATTR_ODBC_VERSION ambiente.  
  
 **Objeto grande binário (BLOB)**  
 Quaisquer dados binários sobre um certo número de bytes, como 255. Normalmente muito mais tempo. Esses dados são geralmente enviados e recuperados da fonte de dados em partes. Também conhecido como *dados longos*.  
  
 **Ligação**  
 Como verbo, o ato de associar uma coluna em um conjunto de resultados ou um parâmetro em uma declaração SQL com uma variável de aplicação. Como um nome, a associação.  
  
 **compensação vinculante**  
 Um valor adicionado aos endereços de buffer de dados e endereços de buffer de comprimento/indicador para todos os dados de coluna ou parâmetro vinculados, produzindo novos endereços.  
  
 **cursor em bloco**  
 Um cursor capaz de obter mais de uma linha de dados de cada vez.  
  
 **Buffer**  
 Um pedaço de memória de aplicativo usado para passar dados entre o aplicativo e o motorista. Os buffers geralmente vêm em pares: um *buffer de dados* e um buffer de comprimento de *dados*.  
  
 **byte**  
 Oito bits ou um octeto. *Veja também* octeto.  
  
## <a name="c"></a>C  
 **Tipos de dados do C**  
 O tipo de dados de uma variável em um programa C, neste caso a aplicação.  
  
 **Catálogo**  
 O conjunto de tabelas de sistema em um banco de dados que descreve a forma do banco de dados. Também conhecido como *um esquema* ou dicionário *de dados*.  
  
 **função catálogo**  
 Uma função ODBC usada para recuperar informações do catálogo do banco de dados.  
  
 **CLI**  
 *Veja* Api.  
  
 **cliente/servidor**  
 Uma estratégia de acesso ao banco de dados na qual um ou mais clientes acessam dados através de um servidor. Os clientes geralmente implementam a interface de usuário enquanto o servidor controla o acesso ao banco de dados.  
  
 **Coluna**  
 O recipiente para um único item de informação em uma fileira. Também conhecido como *campo*.  
  
 **Cometer**  
 Para tornar permanentes as alterações em uma transação.  
  
 **Simultaneidade**  
 A capacidade de mais de uma transação para acessar os mesmos dados ao mesmo tempo.  
  
 **nível de conformidade**  
 Um conjunto discreto de funcionalidade suportado por um driver ou fonte de dados. A ODBC define os níveis de conformidade da API e os níveis de conformidade SQL.  
  
 **Conexão**  
 Um exemplo específico de um driver e fonte de dados.  
  
 **navegação de conexão**  
 Pesquisando na rede para obter fontes de dados para se conectar. A navegação de conexão pode envolver várias etapas. Por exemplo, o usuário pode primeiro navegar na rede por servidores e, em seguida, navegar em um servidor específico para um banco de dados.  
  
 **alça de conexão**  
 Um cabo para uma estrutura de dados que contém informações sobre uma conexão.  
  
 **linha atual**  
 A linha atualmente apontada pelo cursor. As operações posicionadas atuam na linha atual.  
  
 **cursor**  
 Um software que retorna linhas de dados para o aplicativo. Provavelmente nomeado após o cursor piscando em um terminal de computador; assim como o cursor indica a posição atual na tela, um cursor em um conjunto de resultados indica a posição atual no conjunto de resultados.  
  
## <a name="d"></a>D  
 **buffer de dados**  
 Um buffer usado para passar dados. Muitas vezes associado a um buffer de dados é um *buffer de comprimento de dados*.  
  
 **dicionário de dados**  
 *Veja* catálogo.  
  
 **buffer de comprimento de dados**  
 Um buffer usado para passar o comprimento do valor em um *buffer de dados*correspondente . O buffer de comprimento de dados também é usado para armazenar indicadores, como se o valor dos dados é nulo.  
  
 **fonte de dados**  
 Os dados que o usuário deseja acessar e seu sistema operacional associado, DBMS e plataforma de rede (se houver).  
  
 **tipo de dados**  
 O tipo de dados. O ODBC define os tipos de dados C e SQL. *Consulte também* o indicador de digite.  
  
 **coluna data-at-execution**  
 Uma coluna para a qual os dados são enviados após **sqlsetpos** é chamado. Assim nomeado porque os dados são enviados no momento da execução em vez de serem colocados em um buffer de conjunto de linhas. Dados longos geralmente são enviados em partes no momento da execução.  
  
 **parâmetro de dados em execução**  
 Um parâmetro para o qual os dados são enviados após **SQLExecute** ou **SQLExecDirect** é chamado. Assim nomeado porque os dados são enviados quando a declaração SQL é executada em vez de ser colocada em um buffer de parâmetro. Dados longos geralmente são enviados em partes no momento da execução.  
  
 **database**  
 Uma discreta coleta de dados em um DBMS. Também um DBMS.  
  
 **motor de banco de dados**  
 O software em um DBMS que analisa e executa instruções SQL e acessa os dados físicos.  
  
 **DBMS**  
 Sistema de Gestão de Banco de Dados. Uma camada de software entre um banco de dados físico e o usuário. O DBMS gerencia todo o acesso ao banco de dados.  
  
 **Driver baseado em DBMS**  
 Um driver que acessa dados físicos através de um mecanismo de banco de dados autônomo.  
  
 **DDL**  
 Linguagem de definição de dados. Essas declarações no SQL que definem, em vez de manipular, dados. Por exemplo, **CRIAR TABELA,** **CRIAR ÍNDICE,** **CONCESSÃO**e **REVOGAR**.  
  
 **identificador delimitado**  
 Um identificador que é incluído em caracteres de citação de identificador para que ele possa conter caracteres especiais ou combinar palavras-chave (também conhecido como identificador citado).  
  
 **Descritor**  
 Uma estrutura de dados que contém informações sobre dados de coluna ou parâmetros dinâmicos. A representação física do descritor não está definida; os aplicativos ganham acesso direto a um descritor apenas manipulando seus campos, chamando funções ODBC com a alça do descritor.  
  
 **banco de dados de desktop**  
 Um DBMS projetado para ser executado em um computador pessoal. Geralmente, esses DBMSs não fornecem um mecanismo de banco de dados autônomo e devem ser acessados através de um driver baseado em arquivos. Os motores desses drivers geralmente têm suporte reduzido para SQL e transações. Por exemplo, dBASE, Paradox, Btrieve ou Microsoft® FoxPro®.  
  
 **Diagnóstico**  
 Um registro contendo informações de diagnóstico sobre a última função chamada que usou uma alça específica. Os registros de diagnóstico estão associados a meio ambiente, conexão, declaração e alças descritores.  
  
 **DML**  
 Linguagem de Manipulação de Dados. Essas afirmações em SQL que manipulam, ao contrário de definir, dados. Por exemplo, **INSERT,** **UPDATE,** **DELETE**e **SELECT**.  
  
 **Driver**  
 Uma biblioteca de rotina que expõe as funções na API ODBC. Os drivers são específicos para um único DBMS.  
  
 **Gerenciador de Driver**  
 Uma biblioteca de rotina que gerencia o acesso aos motoristas para o aplicativo. O Driver Manager carrega e descarrega (ou se conecta e se desconecta) drivers e passa chamadas para funções ODBC para o driver correto.  
  
 **configuração do driver DLL**  
 Uma DLL que contém funções de instalação e configuração específicas do driver.  
  
 **cursor dinâmico**  
 Um cursor rolável capaz de detectar linhas atualizadas, excluídas ou inseridas no conjunto de resultados.  
  
 **SQL dinâmico**  
 Um tipo de SQL incorporado no qual as instruções SQL são criadas e compiladas em tempo de execução. *Veja também* SQL estático.  
  
## <a name="e"></a>E  
 **SQL incorporado**  
 As instruções SQL que são incluídas diretamente em um programa escrito em outro idioma, como COBOL ou C. ODBC não usa SQL incorporado. *Veja também* SQL estático *e* SQL dinâmico.  
  
 **Ambiente**  
 Um contexto global em que acessar dados; associado ao meio ambiente é qualquer informação de natureza global, como uma lista de todas as conexões nesse ambiente.  
  
 **lidar com o meio ambiente**  
 Um cabo para uma estrutura de dados que contém informações sobre o meio ambiente.  
  
 **cláusula de fuga**  
 Uma cláusula em uma declaração SQL.  
  
 **Executar**  
 Para executar uma declaração SQL.  
  
## <a name="f"></a>F  
 **cursor de gordura**  
 *Veja* o cursor de blocos.  
  
 **Buscar**  
 Para recuperar uma ou mais linhas de um conjunto de resultados.  
  
 **Campo**  
 *Veja* a coluna.  
  
 **driver baseado em arquivos**  
 Um driver que acessa dados físicos diretamente. Neste caso, o driver contém um mecanismo de banco de dados e atua como driver e fonte de dados.  
  
 **fonte de dados de arquivo**  
 Uma fonte de dados para a qual as informações de conexão são armazenadas em um arquivo .dsn.  
  
 **chave estrangeira**  
 Uma coluna ou colunas em uma tabela que correspondam à tecla principal em outra tabela.  
  
 **cursor somente para a frente**  
 Um cursor que só pode avançar através do conjunto de resultados e geralmente busca apenas uma linha de cada vez. A maioria dos bancos de dados relacionais suporta apenas cursores somente para frente.  
  
## <a name="h"></a>H  
 **Lidar com**  
 Um valor que identifica exclusivamente algo como um arquivo ou estrutura de dados. As alças são significativas apenas para o software que as cria e usa, mas são passadas por outros softwares para identificar coisas. O ODBC define alças para ambientes, conexões, declarações e descritores.  
  
## <a name="i"></a>I  
 **descritor de parâmetro de implementação (IPD)**  
 Um descritor que descreve os parâmetros dinâmicos usados em uma declaração SQL após qualquer conversão especificada pelo aplicativo.  
  
 **descritor de linha de implementação (IRD)**  
 Um descritor que descreve uma linha de dados antes de qualquer conversão especificada pelo aplicativo.  
  
 **instalador DLL**  
 Uma DLL que instala componentes ODBC e configura fontes de dados.  
  
 **Facilidade de aprimoramento de integridade**  
 Um subconjunto de SQL projetado para manter a integridade de um banco de dados.  
  
 **nível de conformidade de interface**  
 O nível da interface ODBC 3.7 suportado por um driver; pode ser Núcleo, Nível 1 ou Nível 2.  
  
 **Interoperabilidade**  
 A capacidade de um aplicativo de usar o mesmo código ao acessar dados em DBMSs diferentes.  
  
 **IPD**  
 *Veja* Descritor de parâmetros de implementação (IPD).  
  
 **Ird**  
 *Veja* Descritor de linha de implementação (IRD).  
  
 **ISO/IEC**  
 Organização Internacional de Padrões/Comissão Eletrotécnica Internacional. A API ODBC é baseada na interface de nível de chamada ISO/IEC.  
  
## <a name="j"></a>J  
 **Juntar**  
 Uma operação em um banco de dados relacional que vincula as linhas em duas ou mais tabelas por meio da correspondência de valores em colunas especificadas.  
  
## <a name="k"></a>K  
 **Chave**  
 Uma coluna ou colunas cujos valores identificam uma linha. *Veja também* a chave estrangeira *e* a chave principal.  
  
 **Keyset**  
 Um conjunto de teclas usadas por um cursor misto ou orientado por chavepara rebuscar linhas.  
  
 **cursor controlado por conjunto de chaves**  
 Um cursor rolável que detecta linhas atualizadas e excluídas usando um conjunto de chaves.  
  
## <a name="l"></a>L  
 **Literal**  
 Uma representação de caracterede um valor de dados real em uma declaração SQL.  
  
 **Bloqueio**  
 O processo pelo qual um DBMS restringe o acesso a uma linha em um ambiente multiusuário. O DBMS geralmente define um pouco em uma linha ou a página física contendo uma linha que indica que a linha ou página está bloqueada.  
  
 **dados longos**  
 Quaisquer dados binários ou de caracteres em um determinado comprimento, como 255 bytes ou caracteres. Normalmente muito mais tempo. Esses dados são geralmente enviados e recuperados da fonte de dados em partes. Também conhecido como *BLOB*s ou *CLOB*s.  
  
## <a name="m"></a>M  
 **fonte de dados da máquina**  
 Uma fonte de dados para a qual as informações de conexão são armazenadas no sistema (por exemplo, o registro).  
  
 **modo de confirmação manual**  
 Um modo de confirmação de transações no qual as transações devem ser explicitamente cometidas ligando para **o SQLTransact**.  
  
 **Metadados**  
 Dados que descrevem um parâmetro em uma declaração SQL ou uma coluna em um conjunto de resultados. Por exemplo, o tipo de dados, o comprimento do byte e a precisão de um parâmetro.  
  
 **driver de vários níveis**  
 *Veja* Driver baseado em DBMS.  
  
## <a name="n"></a>N  
 **Valor NULO**  
 Não ter valor explicitamente atribuído. Em particular, um valor NULL é diferente de um zero ou um branco.  
  
## <a name="o"></a>O   
 **Octeto**  
 Oito bits ou um byte. *Veja também* byte.  
  
 **comprimento octeto**  
 O comprimento em octetos de um buffer ou os dados que ele contém.  
  
 **ODBCODBC**  
 Conectividade de banco de dados aberto. Uma especificação para uma API que define um conjunto padrão de rotinas com as quais um aplicativo pode acessar dados em uma fonte de dados.  
  
 **Administrador ODBC**  
 Um programa executável que chama o instalador de DLL para configurar fontes de dados.  
  
 Grupo Aberto  
 Uma empresa que publica normas. Em particular, publica as normas do SQL Access Group (SAG).  
  
 **simultaneidade otimista**  
 Uma estratégia para aumentar a concorrência em que as linhas não estão bloqueadas. Em vez disso, antes de serem atualizados ou excluídos, um cursor verifica se eles foram alterados desde que foram lidos pela última vez. Nesse caso, a atualização ou exclusão falhará. *Veja também* a concorrência pessimista.  
  
 **externa juntar**  
 Uma junta na qual as linhas correspondentes e não correspondentes são devolvidas. Os valores de todas as colunas da tabela incomparável em linhas não correspondentes são definidos como NULL.  
  
 **Proprietário**  
 O dono de uma mesa.  
  
## <a name="p"></a>P  
 **Parâmetro**  
 Uma variável em uma declaração SQL, marcada com um marcador de parâmetro ou ponto de interrogação (?). Os parâmetros são vinculados às variáveis de aplicação e seus valores recuperados quando a declaração é executada.  
  
 **descritor de parâmetro**  
 Um descritor que descreve os parâmetros de tempo de execução usados em uma declaração SQL, antes de qualquer conversão especificada pelo aplicativo (um descritor de parâmetro de aplicativo, ou APD) ou após qualquer conversão especificada pelo aplicativo (um descritor de parâmetro de implementação ou IPD).  
  
 **matriz de operação parâmetro**  
 Um array contendo valores que um aplicativo pode definir para indicar que o parâmetro correspondente deve ser ignorado em uma operação **SQLExecDirect** ou **SQLExecute.**  
  
 **matriz de status parâmetro**  
 Uma matriz contendo o status de um parâmetro após uma chamada para **SQLExecDirect** ou **SQLExecute**.  
  
 **simultaneidade pessimista**  
 Uma estratégia para implementar a serializabilidade, na qual as linhas são bloqueadas para que outras transações não possam alterá-las. *Veja também* a concorrência otimista *e* a serlizabilidade.  
  
 **operação posicionada**  
 Qualquer operação que atue na linha atual. Por exemplo, instruções de atualização e exclusão posicionadas, **SQLGetData**e **SQLSetPos**.  
  
 **declaração de atualização posicionada**  
 Uma declaração SQL usada para atualizar os valores na linha atual.  
  
 **declaração de exclusão posicionada**  
 Uma declaração SQL usada para excluir a linha atual.  
  
 **Preparar**  
 Para compilar uma declaração SQL. Um plano de acesso é criado preparando uma declaração SQL.  
  
 **chave primária**  
 Uma coluna ou colunas que identificam exclusivamente uma linha em uma tabela.  
  
 **Procedimento**  
 Um grupo de uma ou mais instruções SQL pré-compiladas que são armazenadas como um objeto nomeado em um banco de dados.  
  
 **coluna de procedimento**  
 Um argumento em uma chamada de procedimento, o valor devolvido por um procedimento, ou uma coluna em um conjunto de resultados criado por um procedimento.  
  
## <a name="q"></a>Q  
 **Qualificador**  
 Um banco de dados que contém uma ou mais tabelas.  
  
 **Consulta**  
 Uma declaração sql. Às vezes costumava significar uma declaração **SELECT.**  
  
 **identificador entre aspas**  
 Um identificador que é incluído em caracteres de citação de identificador para que ele possa conter caracteres especiais ou combinar palavras-chave (também conhecido no SQL-92 como um identificador delimitado).  
  
## <a name="r"></a>R  
 **Base**  
 A base de um sistema numérdia. Normalmente 2 ou 10.  
  
 **Registro**  
 *Veja* a fila.  
  
 **conjunto de resultados**  
 O conjunto de linhas criadas executando uma declaração **SELECT.**  
  
 **código de retorno**  
 O valor devolvido por uma função ODBC.  
  
 **reverter**  
 Para devolver os valores alterados por uma transação para o seu estado original.  
  
 **Linha**  
 Um conjunto de colunas relacionadas que descrevem uma entidade específica. Também conhecido como *um registro.*  
  
 **descritor de linha**  
 Um descritor que descreve as colunas de um conjunto de resultados, antes de qualquer conversão especificada pelo aplicativo (um descritor de linha de implementação, ou IRD) ou após qualquer conversão especificada pelo aplicativo (um descritor de linha de aplicativo, ou ARD).  
  
 **matriz de operação de linha**  
 Uma matriz contendo valores que um aplicativo pode definir para indicar que a linha correspondente deve ser ignorada em uma operação **SQLSetPos.**  
  
 **matriz de status de linha**  
 Uma matriz contendo o status de uma linha após uma chamada para **SQLFetch,** **SQLFetchScroll**ou **SQLSetPos**.  
  
 **Linhas**  
 O conjunto de linhas retornou em uma única busca por um cursor de bloco.  
  
 **buffers de conjunto de linhas**  
 Os buffers vinculados às colunas de um conjunto de resultados e nos quais os dados de um conjunto de linhas inteiros são retornados.  
  
## <a name="s"></a>S  
 **Sag**  
 *Veja* SQL Access Group (SAG).  
  
 **função escalar**  
 Uma função que gera um único valor a partir de um único valor. Por exemplo, uma função que altera o caso dos dados de caracteres.  
  
 **Esquema**  
 *Veja* catálogo.  
  
 **cursor rolável**  
 Um cursor que pode mover-se para frente ou para trás através do conjunto de resultados.  
  
 **serializabilidade**  
 Se duas transações executando simultaneamente produzem um resultado que é o mesmo que a execução serial (ou seqüencial) dessas transações. Transações serializáveis são necessárias para manter a integridade do banco de dados.  
  
 **banco de dados de servidores**  
 Um DBMS projetado para ser executado em um ambiente cliente/servidor. Esses DBMSs fornecem um mecanismo de banco de dados autônomo que fornece suporte rico para SQL e transações. Eles são acessados através de drivers baseados em DBMS. Por exemplo, Oracle, Informix, DB/2 ou Microsoft® SQL Server.  
  
 **definir função**  
 *Veja* a função agregada.  
  
 **Configuração DLL**  
 *Consulte* a configuração do driver DLL *e* a configuração do tradutor DLL.  
  
 **driver de nível único**  
 *Consulte* o driver baseado em arquivos.  
  
 **SQL**  
 Linguagem de consulta estruturada. Uma linguagem usada por bancos de dados relacionais para consultar, atualizar e gerenciar dados.  
  
 **SQL Access Group (SAG)**  
 Um consórcio do setor de empresas preocupadas com SQL DBMSs. A Interface de Nível de Chamada do Grupo Aberto é baseada no trabalho originalmente feito pelo SQL Access Group.  
  
 **Nível de conformidade SQL**  
 O nível de gramática SQL-92 suportado por um driver; pode ser Entrada, FIPS Transicional, Intermediária ou Completa.  
  
 **Tipo de dados SQL**  
 O tipo de dados de uma coluna ou parâmetro como ele é armazenado na fonte de dados.  
  
 **Sqlstate**  
 Um valor de cinco caracteres que indica um erro particular.  
  
 **Declaração SQL**  
 Uma frase completa em SQL que começa com uma palavra-chave e descreve completamente uma ação a ser tomada. Por exemplo, SELECIONE * DE pedidos. As declarações SQL não devem ser confundidas com declarações.  
  
 **Estado**  
 Uma condição bem definida de um item. Por exemplo, uma conexão tem sete estados, incluindo dados não alocados, alocados, conectados e que precisam de dados. Certas operações só podem ser feitas quando um item está em um estado específico. Por exemplo, uma conexão só pode ser liberada quando está em um estado alocado e não, por exemplo, quando está em um estado conectado.  
  
 **transição estadual**  
 O movimento de um item de um estado para outro. A ODBC define transições de estado rigorosas para ambientes, conexões e declarações.  
  
 **Declaração**  
 Um recipiente para todas as informações relacionadas a uma declaração SQL. As declarações não devem ser confundidas com declarações SQL.  
  
 **lidar com a declaração**  
 Um cabo para uma estrutura de dados que contém informações sobre uma declaração.  
  
 **cursor estático**  
 Um cursor rolável que não pode detectar atualizações, exclusões ou inserções no conjunto de resultados. Geralmente implementado fazendo uma cópia do conjunto de resultados.  
  
 **SQL estático**  
 Um tipo de SQL incorporado no qual as instruções SQL são codificadas e compiladas quando o resto do programa é compilado. *Veja também* SQL dinâmico.  
  
 **procedimento armazenado**  
 *Veja* o procedimento.  
  
## <a name="t"></a>T  
 **table**  
 Uma coleção de filas.  
  
 **Conversão**  
 A conversão de endereços de 16 bits para endereços de 32 bits, ou vice-versa, quando aplicativos de 16 bits são usados com drivers ODBC de 32 bits.  
  
 **Transação**  
 Uma unidade atômica de trabalho. O trabalho em uma transação deve ser concluído como um todo; se qualquer parte da transação falhar, a transação inteira falhará.  
  
 **isolamento de transações**  
 O ato de isolar uma transação dos efeitos de todas as outras transações.  
  
 **nível de isolamento de transações**  
 Uma medida de quão bem uma transação é isolada. Existem cinco níveis de isolamento de transações: Leia Não Comprometido, Leia Comprometido, Leitura Repetível, Serializable e Versioning.  
  
 **tradutor DLL**  
 Uma DLL usada para traduzir dados de um caractere definido para outro.  
  
 **configuração tradutor A DLL**  
 Uma DLL que contém funções de instalação e configuração específicas do tradutor.  
  
 **protocolo 2PC**  
 O processo de cometer uma transação distribuída em duas fases. Na primeira fase, o processador de transações verifica se todas as partes da transação podem ser cometidas. Na segunda fase, todas as partes da transação são comprometidas. Se alguma parte da transação indicar na primeira fase que ela não pode ser cometida, a segunda fase não ocorrerá. A ODBC não suporta compromissos bifásicos.  
  
 **indicador de tipo**  
 Um valor inteiro passou ou retornou de uma função ODBC para indicar o tipo de dados de uma variável de aplicação, um parâmetro ou uma coluna. A ODBC define indicadores de tipo para os tipos de dados C e SQL.  
  
## <a name="v"></a>V  
 **Ver**  
 Uma maneira alternativa de olhar para os dados em uma ou mais tabelas. Uma exibição é geralmente criada como um subconjunto das colunas de uma ou mais tabelas. No ODBC, as visualizações são geralmente equivalentes a tabelas.

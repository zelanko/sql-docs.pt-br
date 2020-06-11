---
title: Guia de controle de versão de linha e bloqueio de transações do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/24/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: c7757153-9697-4f01-881c-800e254918c9
author: rothja
ms.author: jroth
ms.openlocfilehash: d5b098d42c8e770496b67f365dd8ccd7bd8ad640
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528398"
---
# <a name="sql-server-transaction-locking-and-row-versioning-guide"></a>Guia de Controle de Versão de Linha e Bloqueio de Transações do SQL Server

  Em um banco de dados, o gerenciamento incorreto de transações normalmente leva a problemas de contenção e de desempenho em sistemas com muitos usuários. À medida que o número de usuários que acessam os dados aumenta, torna-se importante ter aplicativos que utilizem as transações de maneira eficaz. Este guia descreve os mecanismos de bloqueio e de controle de versão de linha que o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] usa para assegurar a integridade física de cada transação, além de fornecer informações sobre como os aplicativos podem controlar as transações de maneira eficiente.  
  
**Aplica-se a**: a [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] menos que indicado o contrário.  
  
##  <a name="in-this-guide"></a><a name="Top"></a>Neste guia  

 [Noções básicas da transação](#Basics)  
  
 [Noções básicas de controle de versão de bloqueio e linha](#Lock_Basics)  
  
 [Bloqueios no mecanismo de banco de dados](#Lock_Engine)  
  
 [Níveis de isolamento com base no controle de versão de linha no Mecanismo de Banco de Dados](#Row_versioning)  
  
 [Personalizando o bloqueio para um índice](#Customize)  
  
 [Informações de transações avançadas](#Advanced)  
  
##  <a name="transaction-basics"></a><a name="Basics"></a> Noções básicas sobre transações  

 Uma transação é uma sequência de operações executadas como uma única unidade lógica de trabalho. Uma unidade lógica de trabalho deve mostrar quatro propriedades, designadas pelas iniciais ACID (atomicidade, consistência, isolamento e durabilidade), para que seja qualificada como uma transação.  
  
 Atomicidade  
 Uma transação deve ser uma unidade atômica de trabalho; ou todas as suas modificações de dados são executadas ou nenhuma delas é executada.  
  
 Consistência  
 Quando concluída, uma transação deve deixar todos os dados em um estado consistente. Em um banco de dados relacional, todas as regras devem ser aplicadas às modificações da transação para manter toda a integridade dos dados. Todas as estruturas de dados internas, tais como índices em árvore B ou listas duplamente vinculadas, devem estar corretas ao término da transação.  
  
 Isolamento  
 Modificações feitas por transações simultâneas devem ser isoladas das modificações feitas por qualquer outra transação simultânea. Uma transação reconhece os dados no estado em que estavam antes de outra transação simultânea tê-los modificado ou reconhece os dados depois que a segunda transação tiver sido concluída, mas não reconhece um estado intermediário. Isso é chamado serializabilidade porque resulta na capacidade de recarregar os dados iniciais e reexecutar uma série de transações de modo que os dados obtidos estejam no mesmo estado em que estavam depois que as transações originais foram executadas.  
  
 Durabilidade  
 Depois que uma transação totalmente durável tiver sido concluída, seus efeitos ficam permanentemente no sistema. As modificações persistem até mesmo no caso de uma queda do sistema. [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] e posteriores habilitam transações duráveis atrasadas. As transações duráveis atrasadas são confirmadas antes do registro de log de transação ser persistente no disco. Para obter mais informações sobre durabilidade de transações atrasadas, consulte o tópico [Durabilidade da transação](../relational-databases/logs/control-transaction-durability.md).  
  
 Os programadores SQL são responsáveis por iniciar e terminar transações em pontos que imponham a consistência lógica dos dados. O programador deve definir a sequência de modificações de dados que deixem os dados em um estado consistente em relação às regras comerciais da organização. O programador inclui essas instruções de modificação em uma única transação de modo que o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] possa aplicar a integridade física da transação.  
  
 É de responsabilidade de um sistema de banco de dados empresarial, tal como uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)], oferecer mecanismos que assegurem a integridade física de cada transação. O [!INCLUDE[ssDE](../includes/ssde-md.md)] oferece:  
  
-   Recursos de bloqueio que preservam o isolamento da transação.  
  
-   Recursos de log garantem a durabilidade da transação. Para transações completamente duráveis, o registro de log é protegido no disco antes da confirmação das transações. Assim, mesmo se o hardware do servidor, o sistema operacional ou a instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] falhar, a instância usará os logs de transações ao reinicializar para reverter automaticamente qualquer transação incompleta até o ponto da falha do sistema. As transações duráveis atrasadas confirmar antes que o registro de log de transação é protegido no disco. Essas transações podem ser perdidas se houver uma falha do sistema antes de o registro de log ser protegido no disco. Para obter mais informações sobre durabilidade de transações atrasadas, consulte o tópico [Durabilidade da transação](../relational-databases/logs/control-transaction-durability.md).  
  
-   Recursos de administração de transação que impõem a atomicidade e a consistência da transação. Depois que uma transação tiver sido iniciada, ela deve ser concluída com êxito (confirmada) ou o [!INCLUDE[ssDE](../includes/ssde-md.md)] desfará todas as modificações de dados feitas desde que a transação foi iniciada. Essa operação é denominada de reversão da transação porque retorna os dados ao estado anterior a essas alterações.  
  
### <a name="controlling-transactions"></a>Controle de transações  

 Os aplicativos controlam transações principalmente ao especificar quando uma transação começa e termina. O controle pode ser especificado pelo uso de instruções [!INCLUDE[tsql](../includes/tsql-md.md)] ou funções de interface de programação de aplicativo (API) de banco de dados. O sistema também deve ser capaz de processar corretamente os erros que encerram uma transação antes de sua conclusão. Para obter mais informações, consulte [instruções de transação &#40;&#41;Transact-SQL ](/sql/t-sql/language-elements/transactions-transact-sql), [transações em ODBC](https://technet.microsoft.com/library/ms131281.aspx) e [Transações no SQL Server Native Client (OleDb)](https://msdn.microsoft.com/library/ms130918.aspx).  
  
 Por padrão, as transações são gerenciadas no nível de conexão. Quando uma transação é iniciada em uma conexão, todas as instruções [!INCLUDE[tsql](../includes/tsql-md.md)] executadas nessa conexão fazem parte da transação até a conclusão da transação. Porém, em uma sessão de vários conjuntos de resultados ativos (MARS), uma transação [!INCLUDE[tsql](../includes/tsql-md.md)] explícita ou implícita se torna uma transação no escopo do lote gerenciada no nível do lote. Quando o lote for concluído, se a transação no escopo do lote não for confirmada ou revertida, ela será revertida automaticamente pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Mars (vários conjuntos de resultados ativos) no SQL Server](https://msdn.microsoft.com/library/ms345109(v=SQL.90).aspx).  
  
#### <a name="starting-transactions"></a>Iniciando transações  

 Ao usar funções de API e instruções [!INCLUDE[tsql](../includes/tsql-md.md)], você pode iniciar transações em uma instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] como transações explícitas, autoconfirmadas ou implícitas.  
  
 **Transações explícitas**  
 Uma transação explícita é aquela na qual você pode definir explicitamente o início e o término da transação pela função de API ou pela emissão de instruções [!INCLUDE[tsql](../includes/tsql-md.md)] BEGIN TRANSACTION, COMMIT TRANSACTION, COMMIT WORK, ROLLBACK TRANSACTION ou ROLLBACK WORK [!INCLUDE[tsql](../includes/tsql-md.md)]. Quando a transação terminar, a conexão volta ao modo de transação em que estava antes de a transação explícita ser iniciada, seja o modo implícito ou de confirmação automática.  
  
 Você pode usar todas as instruções [!INCLUDE[tsql](../includes/tsql-md.md)] em uma transação explícita, com exceção das seguintes instruções:  
  
||||  
|-|-|-|  
|ALTER DATABASE|CREATE DATABASE|DROP FULLTEXT INDEX|  
|ALTER FULLTEXT CATALOG|CREATE FULLTEXT CATALOG|RECONFIGURE|  
|ALTER FULLTEXT INDEX|CREATE FULLTEXT INDEX|RESTORE|  
|BACKUP|DROP DATABASE|Procedimentos armazenados do sistema de texto completo|  
|CREATE DATABASE|DROP FULLTEXT CATALOG|sp_dboption para definir opções de banco de dados ou usar um procedimento do sistema que modifique o banco de dados mestre dentro de transações explícitas ou implícitas.|  
  
> [!NOTE]  
>  UPDATE STATISTICS pode ser usada dentro de uma transação explícita. Mas, ela será confirmada independentemente da transação envolvida e não poderá ser revertida.  
  
 **Transações de Confirmação Automática**  
 O modo de confirmação automática é o modo padrão de gerenciamento de transações do mecanismo de banco de dados do SQL Server. Toda instrução Transact-SQL é confirmada ou revertida quando concluída. Se uma instrução for concluída com sucesso, será confirmada; se encontrar qualquer erro, será revertida. A conexão a uma instância do mecanismo de banco de dados opera em modo de confirmação automática sempre que esse modo padrão não for substituído por transações explícitas ou implícitas. O modo de confirmação automática também é o modo padrão para ADO, OLE DB, ODBC e DB-Library.  
  
 **Transações implícitas**  
 Quando uma conexão operar em modo de transação implícita, a instância do mecanismo de banco de dados iniciará automaticamente uma nova transação depois que a transação atual for confirmada ou revertida. Você não faz nada para determinar o início de uma transação; apenas confirma ou reverte cada uma das transações. O modo de transação implícita gera uma cadeia contínua de transações. Defina o modo de transação implícito como ativado por uma função de API ou pela instrução [!INCLUDE[tsql](../includes/tsql-md.md)] SET IMPLICIT_TRANSACTIONS ON.  
  
 Após a configuração do modo de transação implícita em uma conexão, a instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] iniciará automaticamente a transação ao executar pela primeira vez cada uma destas instruções:  
  
||||  
|-|-|-|  
|ALTER TABLE|FETCH|REVOKE|  
|CREATE|GRANT|SELECT|  
|Delete (excluir)|INSERT|TRUNCATE TABLE|  
|DROP|OPEN|UPDATE|  
  
 **Transações no escopo do lote**  
 Aplicável apenas a MARS (Conjuntos de Resultados Ativos Múltiplos), a transação [!INCLUDE[tsql](../includes/tsql-md.md)] explícita ou implícita iniciada em uma sessão MARS se torna uma transação de escopo de lote. A transação de escopo de lote que não é confirmada ou revertida quando um lote é concluído, será revertida automaticamente pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 **Transações distribuídas**  
 Transações distribuídas abrangem dois ou mais servidores conhecidos como gerenciadores de recursos. O gerenciamento da transação deve ser coordenado entre os gerenciadores de recursos por um componente de servidor chamado de gerenciador de transações. Cada instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] pode operar como um gerenciador de recursos em transações distribuídas coordenadas por gerenciadores de transações, como o MS DTC (Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../includes/msconame-md.md)]), ou outros gerenciadores de transações que dão suporte à especificação XA do Open Group para processamento de transações distribuídas. Para obter mais informações, consulte a documentação do MS DTC.  
  
 Uma transação em uma instância única do [!INCLUDE[ssDE](../includes/ssde-md.md)] que abrange dois ou mais bancos de dados é, de fato, uma transação distribuída. A instância gerencia a transação distribuída internamente. Para o usuário, ela opera como uma transação local.  
  
 No aplicativo, uma transação distribuída é gerenciada da mesma forma como uma transação local. No final da transação, o aplicativo solicita que a transação seja confirmada ou revertida. Uma confirmação distribuída deve ser gerenciada de forma diferenciada pelo gerenciador de transações para minimizar o risco de que uma falha de rede possa resultar em alguns gerenciadores de recurso que confirmam com êxito enquanto outros revertem a transação. Isso é obtido pelo gerenciamento do processo de confirmação em duas fases (a fase de preparação e a fase de confirmação), o que é conhecido como um protocolo 2PC.  
  
 Fase de preparo  
 Quando o gerenciador de transações recebe uma solicitação de confirmação, ele envia um comando de preparação a todos os gerenciadores de recursos envolvidos na transação. Cada gerenciador executa todas as ações necessárias para tornar a transação durável, e todos os buffers que mantêm imagens de log da transação são liberados no disco. À medida que cada gerenciador de recursos conclui a fase de preparação, ele retorna informações de êxito ou de falha ao gerenciador de transações. [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] introduziu a durabilidade da transação atrasada. As transações duráveis atrasadas são confirmadas antes de imagens de log da transação serem liberadas para o disco. Para obter mais informações sobre durabilidade de transações atrasadas, consulte o tópico [Durabilidade da transação](../relational-databases/logs/control-transaction-durability.md).  
  
 Fase de confirmação  
 Se o gerenciador de transações receber preparos bem-sucedidos de todos os gerenciadores de recursos, ele enviará comandos de confirmação a cada gerenciador de recursos. Em seguida, os gerenciadores de recursos podem concluir a confirmação. Se todos os gerenciadores de recursos relatarem uma confirmação bem-sucedida, o gerenciador de transações enviará uma notificação de êxito ao aplicativo. Se um gerenciador de recursos informar uma falha na preparação, o gerenciador de transações enviará um comando de reversão a cada gerenciador de recursos e indicará a falha da confirmação ao aplicativo.  
  
 Os aplicativos [!INCLUDE[ssDE](../includes/ssde-md.md)] podem gerenciar transações distribuídas por meio de [!INCLUDE[tsql](../includes/tsql-md.md)] ou da API do banco de dados. Para obter mais informações, veja [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/begin-distributed-transaction-transact-sql).  
  
#### <a name="ending-transactions"></a>Finalizando transações  

 Você pode finalizar transações com uma instrução COMMIT ou ROLLBACK ou com uma função de API correspondente.  
  
 COMMIT  
 Se uma transação for concluída com êxito, confirme-a. Uma instrução COMMIT garante que todas as modificações na transação fazem parte permanente do banco de dados. Um COMMIT também libera recursos, como bloqueios, usados pela transação.  
  
 ROLLBACK  
 Se ocorrer um erro em uma transação ou se o usuário decidir cancelá-la, reverta a transação. Uma instrução ROLLBACK desfaz todas as modificações feitas na transação retornando os dados ao estado anterior ao início da transação. Um ROLLBACK também libera recursos usados pela transação.  
  
> [!NOTE]  
>  Em conexões habilitadas para oferecer suporte a vários conjuntos de resultados ativos (MARS), uma transação explícita iniciada por uma função de API não pode ser confirmada enquanto houver solicitações pendentes para execução. Qualquer tentativa de confirmação desse tipo de transação enquanto houver operações pendentes sendo executadas resultará em um erro.  
  
#### <a name="errors-during-transaction-processing"></a>Erros durante o processamento de transações  

 Se um erro impedir a conclusão bem-sucedida de uma transação, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] reverterá automaticamente a transação e liberará todos os recursos usados por ela. Se a conexão de rede do cliente com uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] for interrompida, quaisquer transações pendentes para a conexão serão revertidas quando a rede notificar a instância sobre a interrupção. Se o aplicativo cliente falhar ou se o computador cliente for desligado ou reiniciado, isso também interromperá a conexão e a instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] reverterá quaisquer conexões pendentes quando a rede notificar a interrupção. Se o cliente fizer logoff do aplicativo, quaisquer transações pendentes serão revertidas.  
  
 Se ocorrer um erro de instrução de tempo de execução (como uma violação de restrição) em um lote, o comportamento padrão no [!INCLUDE[ssDE](../includes/ssde-md.md)] será reverter somente a instrução que gerou o erro. Você pode alterar esse comportamento usando a instrução SET XACT_ABORT. Depois que SET XACT_ABORT ON for executada, qualquer erro de instrução em tempo de execução fará com que a transação atual seja revertida. Os erros de compilação, como erros de sintaxe, não são afetados por SET XACT_ABORT. Para obter mais informações, veja [SET XACT_ABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-xact-abort-transact-sql).  
  
 Quando ocorrerem erros, a ação corretiva (COMMIT ou ROLLBACK) deverá ser incluída em um código de aplicativo. Uma ferramenta eficaz para lidar com erros, incluindo aqueles em transações, é a [!INCLUDE[tsql](../includes/tsql-md.md)] tentativa... CAPTURAR construção. Para obter mais informações com exemplos que incluem transações, veja [TRY...CATCH &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/try-catch-transact-sql). A partir [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] do, você pode usar a instrução Throw para gerar uma exceção e transfere a execução para um bloco catch de um try... CAPTURAR construção. Para obter mais informações, veja [THROW &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/throw-transact-sql).  
  
##### <a name="compile-and-run-time-errors-in-autocommit-mode"></a>Erros em tempo de execução e de compilação no modo de confirmação automática  

 No modo de confirmação automática, às vezes parece que uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] reverteu um lote inteiro, em vez de apenas uma instrução SQL. Isto acontece se o erro encontrado for um erro de compilação, não um erro em tempo de execução. Um erro de compilação impede o [!INCLUDE[ssDE](../includes/ssde-md.md)] de criar um plano de execução, assim nada no lote é executado. Embora pareça que todas as instruções antes daquela que gerou o erro tenham sido revertidas, o erro impediu que tudo no lote fosse executado. No exemplo a seguir, nenhuma das instruções `INSERT` no terceiro lote foram executadas por causa de um erro de compilação. Parece que as primeiras duas instruções `INSERT` foram revertidas, mas elas nunca foram executadas.  
  
```sql
CREATE TABLE TestBatch (Cola INT PRIMARY KEY, Colb CHAR(3));  
GO  
INSERT INTO TestBatch VALUES (1, 'aaa');  
INSERT INTO TestBatch VALUES (2, 'bbb');  
INSERT INTO TestBatch VALUSE (3, 'ccc');  -- Syntax error.  
GO  
SELECT * FROM TestBatch;  -- Returns no rows.  
GO  
```  
  
 No exemplo a seguir, a terceira instrução `INSERT` gera um erro de duplicação de chave primária em tempo de execução. As primeiras duas instruções `INSERT` têm êxito e são confirmadas; portanto, elas permanecem depois do erro em tempo de execução.  
  
```sql  
CREATE TABLE TestBatch (Cola INT PRIMARY KEY, Colb CHAR(3));  
GO  
INSERT INTO TestBatch VALUES (1, 'aaa');  
INSERT INTO TestBatch VALUES (2, 'bbb');  
INSERT INTO TestBatch VALUES (1, 'ccc');  -- Duplicate key error.  
GO  
SELECT * FROM TestBatch;  -- Returns rows 1 and 2.  
GO  
```  
  
 O [!INCLUDE[ssDE](../includes/ssde-md.md)] usa resolução de nome adiada, na qual os nomes de objetos não são resolvidos até o tempo de execução. No exemplo a seguir, as primeiras duas instruções `INSERT` são executadas e confirmadas, e essas duas linhas permanecem na tabela `TestBatch`, depois que a terceira instrução `INSERT` gera um erro em tempo de execução, referindo-se a uma tabela que não existe.  
  
```sql
CREATE TABLE TestBatch (Cola INT PRIMARY KEY, Colb CHAR(3));  
GO  
INSERT INTO TestBatch VALUES (1, 'aaa');  
INSERT INTO TestBatch VALUES (2, 'bbb');  
INSERT INTO TestBch VALUES (3, 'ccc');  -- Table name error.  
GO  
SELECT * FROM TestBatch;  -- Returns rows 1 and 2.  
GO  
```  
  
 ![Ícone de seta usado com o link voltar ao início](media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [neste guia](#Top)  
  
##  <a name="locking-and-row-versioning-basics"></a><a name="Lock_Basics"></a> Noções básicas sobre bloqueio e controle de versão de linha  

 O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] usa os seguintes mecanismos para garantir a integridade de transações e manter a consistência dos bancos de dados quando vários usuários estão acessando os dados ao mesmo tempo:  
  
-   Bloqueio  
  
     Cada transação solicita bloqueios de tipos diferentes nos recursos, como linhas, páginas ou tabelas, dos quais depende a transação. Os bloqueios não permitem que outras transações modifiquem os recursos de uma maneira que causaria problemas para a transação que solicita o bloqueio. Cada transação libera seus bloqueios quando não depende mais dos recursos bloqueados.  
  
-   Controle de versão de linha  
  
     Quando um nível de isolamento baseado em controle de versão de linha é habilitado, o [!INCLUDE[ssDE](../includes/ssde-md.md)] mantém versões de cada linha modificada. Os aplicativos podem especificar que uma transação use as versões da linha para exibir dados da forma como eram no início da transação ou consulta ao invés de proteger todas as leituras com bloqueios. Usando o controle de versão de linha, a possibilidade de uma operação de leitura bloquear outras transações é muito reduzida.  
  
 O bloqueio e o controle de versão de linha impedem que os usuários leiam dados não confirmados e impedem que vários usuários tentem alterar os mesmos dados ao mesmo tempo. Sem o bloqueio ou o controle de versão de linha, as consultas executadas em relação a esses dados podem produzir resultados inesperados retornando dados que ainda não foram confirmados no banco de dados.  
  
 Os aplicativos podem escolher níveis de isolamento da transação que definem o nível de proteção da transação contra efeitos de modificações feitas por outras transações. Podem ser especificadas dicas em nível de tabela para instruções [!INCLUDE[tsql](../includes/tsql-md.md)] individuais para personalizar ainda mais o comportamento para atender aos requisitos do aplicativo.  
  
### <a name="managing-concurrent-data-access"></a>Gerenciando o acesso simultâneo a dados  

 Os usuários que acessam um recurso ao mesmo tempo estão acessando o recurso simultaneamente. O acesso simultâneo a dados exige mecanismos para impedir efeitos adversos quando vários usuários tentam modificar recursos que outros usuários estão utilizando.  
  
#### <a name="concurrency-effects"></a>Efeitos de simultaneidade  

 Os usuários que modificam dados podem afetar outros usuários que estejam lendo ou modificando os mesmos dados ao mesmo tempo. Dizemos que esses usuários estão acessando os dados simultaneamente. Se um sistema de armazenamento de dados não tiver nenhum controle de simultaneidade, os usuários verão os seguintes efeitos colaterais:  
  
-   Atualizações perdidas  
  
     As atualizações perdidas acontecem quando duas ou mais transações selecionam a mesma linha e então atualizam a linha com base no valor selecionado originalmente. Cada transação não tem conhecimento das outras transações. A última atualização substitui atualizações feitas pelas outras transações, o que resulta em dados perdidos.  
  
     Por exemplo, dois editores fazem uma cópia eletrônica do mesmo documento. Cada editor altera a cópia de maneira independentemente e salva a cópia alterada, substituindo, portanto, o documento original. O editor que salva a cópia alterada por último substitui as alterações feitas pelo outro editor. Esse problema poderia ser evitado se um editor não pudesse acessar o arquivo até que o outro editor tivesse terminado e confirmado a transação.  
  
-   Dependência não confirmada (leitura suja)  
  
     A dependência não confirmada acontece quando uma segunda transação seleciona uma linha que está sendo atualizada por outra transação. A segunda transação está lendo dados que não foram confirmados ainda e podem ser alterados pela transação que atualiza a linha.  
  
     Por exemplo, um editor está fazendo mudanças em um documento eletrônico. Durante as mudanças, um segundo editor pega uma cópia do documento que inclui todas as mudanças feitas até o momento e distribui o documento para a audiência destinada. O primeiro editor decide então que as mudanças feitas até o momento estão erradas, remove as edições e salva o documento. O documento distribuído contém edições que já não existem e que deveriam ser tratadas como se nunca tivessem existido. Esse problema poderia ser evitado se ninguém pudesse ler o documento alterado até que o primeiro editor salvasse a versão final com as modificações e confirmasse a transação.  
  
-   Análise inconsistente (leitura não repetível)  
  
     Ocorre análise inconsistente quando uma segunda transação acessa a mesma linha várias vezes e lê dados diferentes a cada vez. A análise inconsistente é semelhante à dependência não confirmada, no sentido em que outra transação está alterando os dados que uma segunda transação está lendo. No entanto, na análise inconsistente os dados lidos pela segunda transação foram confirmados pela transação que fez as alterações. Além disso, a análise inconsistente envolve leituras múltiplas (duas ou mais) da mesma fila, e a cada vez as informações são alterada por outra transação; daí a denominação leitura não repetível.  
  
     Por exemplo, um editor lê o mesmo documento duas vezes, mas entre cada leitura o escritor reescreve o documento. Quando o editor lê o documento pela segunda vez, este já foi alterado. A leitura original não era repetível. Esse problema poderia ser evitado se o gravador não pudesse alterar o documento até que o editor tivesse terminado de lê-lo pela última vez.  
  
-   Leituras fantasma  
  
     A leitura fantasma é uma situação que ocorre quando são executadas duas consultas idênticas e a coleção de linhas retornada pela segunda consulta é diferente. O exemplo abaixo mostra como isso pode ocorrer. Suponha que as duas transações abaixo sejam executadas ao mesmo tempo. As duas instruções SELECT na primeira transação podem retornar resultados diferentes, pois a instrução INSERT na segunda transação altera os dados usados por ambas.  
  
    ```  
    --Transaction 1  
    BEGIN TRAN;  
    SELECT ID FROM dbo.employee  
    WHERE ID > 5 and ID < 10;  
    --The INSERT statement from the second transaction occurs here.  
    SELECT ID FROM dbo.employee  
    WHERE ID > 5 and ID < 10;  
    COMMIT;  
  
    ```  
  
    ```  
    --Transaction 2  
    BEGIN TRAN;  
    INSERT INTO dbo.employee  
       SET name = 'New' WHERE ID = 5;  
    COMMIT;   
    ```  
  
-   Leituras ausentes e duplicadas provocadas por atualizações de linha  
  
    -   Perdendo uma linha atualizada ou vendo uma linha atualizada várias vezes  
  
         Transações que estejam sendo executadas no nível READ UNCOMMITTED não emitem bloqueios compartilhados para impedir que outras transações modifiquem os dados lidos pela transação atual. Transações que estejam sendo executadas no nível READ COMMITTED emitem bloqueios compartilhados, mas os bloqueios de linha ou de página são liberados depois que a linha é lida. Em qualquer dos dois casos, quando você estiver percorrendo um índice, se outro usuário alterar a coluna de chave de índice da linha durante sua leitura, a linha poderia aparecer novamente se a alteração de chave movesse a linha para uma posição à frente de sua leitura. De maneira semelhante, a linha poderia não aparecer se a alteração de chave movesse a linha para uma posição no índice que você já tinha lido. Para evitar isto, use a dica SERIALIZABLE ou HOLDLOCK ou controle de versão de linha. Para obter mais informações, consulte [Dicas de tabela &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table).  
  
    -   Perdendo uma ou mais linhas que não eram o destino da atualização  
  
         Quando você estiver usando READ UNCOMMITTED, se sua consulta ler linhas que usem uma varredura de ordem de alocação (usando páginas IAM), você poderá perder linhas se outra transação estiver provocando uma divisão de página. Isso não pode acontecer quando você estiver usando leitura confirmada, porque um bloqueio de tabela é mantido durante uma divisão de página, e não ocorre se a tabela não tiver um índice clusterizado, porque as atualizações não provocam divisões de página.  
  
#### <a name="types-of-concurrency"></a>Tipos de simultaneidade  

 Quando muitas pessoas tentam modificar dados em um banco de dados ao mesmo tempo, um sistema de controles deve ser implementado de forma que as modificações feitas por uma pessoa não afetem adversamente as de outra pessoa. Isso é chamado controle de simultaneidade.  
  
 A teoria do controle de simultaneidade tem duas classificações para os métodos de instituição do controle de simultaneidade:  
  
-   Controle de simultaneidade pessimista  
  
     Um sistema de bloqueios impede que os usuários modifiquem os dados de uma forma que afete outros usuários. Depois que um usuário executa uma ação que aplica um bloqueio, outros usuários não podem executar ações que estariam em conflito com o bloqueio até o proprietário liberar o bloqueio. Isso é chamado de controle pessimista porque é principalmente usado em ambientes em que existe contenção elevada dos dados, e que o custo da proteção dos dados com bloqueios é inferior ao custo de reversão de transações, caso ocorram conflitos de simultaneidade.  
  
-   Controle de simultaneidade otimista  
  
     No controle de simultaneidade otimista, os usuários não bloqueiam os dados quando os leem. Quando um usuário atualiza os dados, o sistema verifica se outro usuário alterou os dados depois de lidos. Se outro usuário tiver atualizado os dados, um erro é ativado. Normalmente, o usuário que recebe o erro reverte a transação e inicia novamente. Isso é chamado de controle otimista porque é usado principalmente em ambientes em que existe contenção reduzida dos dados, e que o custo de reversão ocasional de uma transação é inferior ao custo de bloqueio dos dados quando os mesmos são lidos.  
  
 O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] oferece suporte a uma variedade de controles de simultaneidade. Os usuários especificam o tipo de controle de simultaneidade selecionando níveis de isolamento da transação para conexões ou opções de simultaneidade em cursores. Esses atributos podem ser definidos usando instruções [!INCLUDE[tsql](../includes/tsql-md.md)], ou pelas propriedades e atributos de APIs (interfaces de programação de aplicativo) de banco de dados, como ADO, ADO.NET, OLE DB e ODBC.  
  
#### <a name="isolation-levels-in-the-database-engine"></a>Níveis de isolamento no Mecanismo de Banco de Dados  

 As transações especificam um nível de isolamento que define o grau em que uma transação deve ser isolada contra modificações de recursos ou de dados feitas por outras transações. Os níveis de isolamento são descritos em termos de quais efeitos colaterais de simultaneidade são permitidos, como leituras sujas ou leituras fantasma.  
  
 Níveis de isolamento da transação controlam:  
  
-   Se são feitos bloqueios quando os dados são lidos, e que tipo de bloqueio é solicitado.  
  
-   Por quanto tempo os bloqueios de leitura são mantidos.  
  
-   Se uma linha de referência de operação de leitura foi modificada por outra transação:  
  
    -   Bloqueia até que o bloqueio exclusivo na linha seja liberado.  
  
    -   Recupera a versão confirmada da linha existente no momento em que a instrução ou transação foi iniciada.  
  
    -   Lê a modificação de dados não confirmados.  
  
> [!IMPORTANT]  
>  Escolhendo um nível de isolamento da transação não afeta os bloqueios obtidos para proteger as modificações de dados. Uma transação sempre obtém um bloqueio exclusivo em quaisquer dados que modifica e mantém tal bloqueio até que a transação seja concluída, sem considerar o conjunto de níveis de isolamento para a transação em questão. Para operações de leitura, níveis de isolamento da transação definem principalmente o nível de proteção dos efeitos das modificações feitas por outras transações.  
  
 Um nível de isolamento inferior aumenta a capacidade de muitos usuários acessarem dados ao mesmo tempo, mas aumenta o número de efeitos de simultaneidade (como leituras sujas ou atualizações perdidas) que os usuários podem encontrar. Inversamente, um nível de isolamento mais alto reduz os tipos de efeito de simultaneidade que os usuários podem encontrar, mas requer mais recursos do sistema e aumenta as chances de uma transação bloquear outra. Escolher o nível de isolamento apropriado depende de equilibrar os requisitos de integridade de dados do aplicativo em relação à sobrecarga de cada nível de isolamento. O nível de isolamento mais alto, serializável, garante que uma transação recuperará exatamente os mesmos dados toda vez que repetir uma operação de leitura, mas faz isto executando um nível de bloqueio que provavelmente causará impacto em outros usuários em sistemas multiusuários. O mais baixo nível de isolamento, leitura de dados não confirmados, pode recuperar dados que foram modificados mas não foram confirmados por outras transações. Todos os efeitos colaterais de simultaneidade podem acontecer em leitura não confirmada, mas não há nenhum bloqueio de leitura ou controle de versão, assim a sobrecarga é minimizada.  
  
##### <a name="database-engine-isolation-levels"></a>Níveis de isolamento do Mecanismo de Banco de Dados  

 O padrão ISO define os seguintes níveis de isolamento, todos têm suporte pelo [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]:  
  
|Nível de Isolamento|Definição|  
|---------------------|----------------|  
|Leitura não confirmada|O nível de isolamento mais baixo, no qual as transações só estão isoladas o bastante para assegurar que dados corrompidos fisicamente não são sejam lidos. Nesse nível, são permitidas leituras sujas, para que uma transação tenha acesso às alterações ainda não confirmadas de outras transações.|  
|Leitura confirmada|Permite que uma transação leia dados lidos anteriormente (não modificados) por outra transação, sem esperar pela conclusão da primeira transação. O [!INCLUDE[ssDE](../includes/ssde-md.md)] mantém bloqueios de gravação (adquiridos em dados selecionados) até o término da transação, mas os bloqueios de leitura são liberados assim que a operação SELECT é efetuada. Esse é o nível padrão do [!INCLUDE[ssDE](../includes/ssde-md.md)].|  
|Leitura repetida|O [!INCLUDE[ssDE](../includes/ssde-md.md)] mantém os bloqueios de gravação e leitura adquiridos em dados selecionados até o término da transação. Contudo, poderão ocorrer leituras fantasmas, pois os bloqueios de intervalo não são gerenciados.|  
|Serializável|O nível mais alto, no qual as transações estão completamente isoladas umas das outras. O [!INCLUDE[ssDE](../includes/ssde-md.md)] mantém os bloqueios de gravação e leitura adquiridos em dados selecionados para que sejam liberados ao final da transação. Os bloqueios de intervalo são adquiridos quando uma operação SELECT usa uma cláusula WHERE em intervalo, sobretudo para evitar leituras fantasmas.<br /><br /> **Observação:** pode haver falha em operações e transações DDL em tabelas replicadas quando o nível de isolamento serializável é solicitado. Isso ocorre porque as consultas de replicação usam dicas que podem ser incompatíveis com o nível de isolamento serializável.|  
  
 O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] também oferece suporte a dois níveis adicionais de isolamento da transação que usam controle de versão de linha. O primeiro consiste em uma implementação nova de isolamento de leitura confirmada e o segundo consiste em um nível de isolamento da transação novo, instantâneo.  
  
|Nível de isolamento do controle de versão de linha|Definição|  
|------------------------------------|----------------|  
|Instantâneo de leitura confirmada|Quando a opção de banco de dados READ_COMMITTED_SNAPSHOT estiver definida como ON, o isolamento de leitura confirmada usará o controle de versão de linha para fornecer consistência de leitura no nível da instrução. Operações de leitura só requerem bloqueios de nível de tabela SCH-S e nenhum bloqueio de página ou linha. Ou seja, o mecanismo do banco de dados usa o controle de versão de linha para apresentar a cada instrução um instantâneo transacionalmente consistente dos dados conforme se encontravam no início da instrução. Não são usados bloqueios para proteger os dados contra atualizações efetuadas por outras transações. Uma função definida pelo usuário pode retornar dados confirmados depois do horário de início da instrução que contém que o UDF.<br /><br /> Quando a opção de banco de dados READ_COMMITTED_SNAPSHOT estiver configurada como OFF, que é a configuração padrão, o isolamento de leitura confirmada usará os bloqueios compartilhados para evitar que outras transações modifiquem linhas enquanto a transação atual estiver executando uma operação de leitura. Os bloqueios compartilhados também bloqueiam a instrução de ler linhas modificadas por outras transações até que a outra transação seja concluída. Ambas as implementações satisfazem a definição de ISO de isolamento de leitura confirmada.|  
|Instantâneo|O nível de isolamento do instantâneo usa controle de versão de linha para fornecer consistência de leitura em nível de transação. Operações de leitura não requerem bloqueios de página ou linha; apenas bloqueios de tabela SCH-S são necessários. Ao ler linhas modificadas por outra transação, elas recuperam a versão da linha que existia na inicialização da transação. É possível usar o Isolamento do instantâneo em um banco de dados quando a opção de banco de dados ALLOW_SNAPSHOT_ISOLATION estiver definida como ON. Por padrão, essa opção é definida como OFF para bancos de dados de usuários.<br /><br /> **Observação: o **  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não tem suporte para controle de versão de metadados. Por isso, há restrições nas operações de DDL que podem ser executadas em uma transação explícita que está sendo executada sob isolamento do instantâneo. As instruções de DDL a seguir não são permitidas sob isolamento do instantâneo depois de uma instrução BEGIN TRANSACTION: ALTER TABLE, CREATE INDEX, CREATE XML INDEX, ALTER INDEX, DROP INDEX, DBCC REINDEX, ALTER PARTITION FUNCTION, ALTER PARTITION SCHEME ou qualquer instrução CRL (Common Language Runtime) DDL. Essas instruções serão permitidas quando você estiver usando o isolamento de instantâneo em transações implícitas. Uma transação implícita, por definição, é uma instrução única que torna possível impor semânticas de isolamento do instantâneo, até mesmo com instruções DDL. Violações desse princípio podem causar o erro 3961: “Falha na transação de isolamento do instantâneo no banco de dados '%. * ls' porque o objeto acessado pela instrução foi modificado por uma instrução de DDL em outra transação simultânea desde o início dessa transação. Isso não é permitido porque os metadados não têm controle de versão. Uma atualização simultânea para metadados poderia gerar inconsistências se misturada com isolamento do instantâneo."|  
  
 A tabela a seguir mostra os efeitos colaterais de simultaneidade habilitados por níveis de isolamento diferentes.  
  
|Nível de isolamento|Leitura suja|Leitura não repetível|Fantasma|  
|---------------------|----------------|------------------------|-------------|  
|**Leitura não confirmada**|Sim|Sim|Yes|  
|**Leitura confirmada**|Não|Sim|Yes|  
|**Leitura repetida**|Não|Não|Sim|  
|**Instantâneo**|Não|Não|Não|  
|**Serializável**|Não|Não|Não|  
  
 Para obter mais informações sobre os tipos específicos de controle de versão de linha ou bloqueio controlado pelos níveis de isolamento de transação, veja [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql).  
  
 Níveis de isolamento da transação podem ser definidos usando [!INCLUDE[tsql](../includes/tsql-md.md)] ou por uma API de banco de dados.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)]  
 Scripts [!INCLUDE[tsql](../includes/tsql-md.md)] usam a instrução SET TRANSACTION ISOLATION LEVEL.  
  
 ADO  
 Aplicativos ADO definem a propriedade `IsolationLevel` do objeto **Connection** como adXactReadUncommitted, adXactReadCommitted, adXactRepeatableRead ou adXactReadSerializable.  
  
 ADO.NET  
 Aplicativos ADO.NET que usam o namespace gerenciado `System.Data.SqlClient` podem chamar o método `SqlConnection.BeginTransaction` e definir a opção *IsolationLevel* como Unspecified, Chaos, ReadUncommitted, ReadCommitted, RepeatableRead, Serializable e Snapshot.  
  
 OLE DB  
 Ao iniciar uma transação, aplicativos que usam OLE DB chamam `ITransactionLocal::StartTransaction` com *isoLevel* definido como ISOLATIONLEVEL_READUNCOMMITTED, ISOLATIONLEVEL_READCOMMITTED, ISOLATIONLEVEL_REPEATABLEREAD, ISOLATIONLEVEL_SNAPSHOT ou ISOLATIONLEVEL_SERIALIZABLE.  
  
 Ao especificar o nível de isolamento da transação em modo de confirmação automática, aplicativos OLE DB podem definir a propriedade DBPROPSET_SESSION como DBPROP_SESS_AUTOCOMMITISOLEVELS DBPROPVAL_TI_CHAOS, DBPROPVAL_TI_READUNCOMMITTED, DBPROPVAL_TI_BROWSE, DBPROPVAL_TI_CURSORSTABILITY, DBPROPVAL_TI_READCOMMITTED, DBPROPVAL_TI_REPEATABLEREAD, DBPROPVAL_TI_SERIALIZABLE, DBPROPVAL_TI_ISOLATED ou DBPROPVAL_TI_SNAPSHOT.  
  
 ODBCODBC  
 Aplicativos ODBC chamam `SQLSetConnectAttr` com *Attribute* definido como SQL_ATTR_TXN_ISOLATION e *ValuePtr* definido como SQL_TXN_READ_UNCOMMITTED, SQL_TXN_READ_COMMITTED, SQL_TXN_REPEATABLE_READ ou SQL_TXN_SERIALIZABLE.  
  
 Para transações de instantâneo, os aplicativos chamam `SQLSetConnectAttr` com Atributo definido como SQL_COPT_SS_TXN_ISOLATION e ValuePtr definido como SQL_TXN_SS_SNAPSHOT. Uma transação de instantâneo que usa SQL_COPT_SS_TXN_ISOLATION ou SQL_ATTR_TXN_ISOLATION pode ser recuperada.  
  
 ![Ícone de seta usado com o link voltar ao início](media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [neste guia](#Top)  
  
##  <a name="locking-in-the-database-engine"></a><a name="Lock_Engine"></a>Bloqueio no Mecanismo de Banco de Dados  

 O bloqueio é um mecanismo usado pelo [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] para sincronizar o acesso de vários usuários à mesma parte dos dados simultaneamente.  
  
 Antes que uma transação adquira uma dependência de uma parte dos dados no estado atual, como por ler ou modificar os dados, ela deve se proteger contra os efeitos de outra transação que modifique os mesmos dados. A transação faz isso, solicitando um bloqueio na parte dos dados. Os bloqueios têm modos diferentes, como compartilhado ou exclusivo. O modo de bloqueio define o nível de dependência que a transação tem nos dados. Nenhuma transação pode receber um bloqueio que conflite com o modo de um bloqueio já atribuído àqueles dados por outra transação. Se uma transação requisitar um modo de bloqueio que conflite com um bloqueio que já tenha sido atribuído aos mesmos dados, a instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] fará uma pausa na transação requerida até que o primeiro bloqueio seja liberado.  
  
 Quando uma transação modifica uma parte dos dados, ela mantém o bloqueio protegendo a modificação até o fim da transação. O tempo que uma transação mantém os bloqueios adquiridos, para proteger as operações de leitura, depende da configuração do nível de isolamento da transação. Todos os bloqueios mantidos por uma transação são liberados quando a transação for concluída (confirma ou reverte).  
  
 Os aplicativos normalmente não solicitam bloqueios diretamente. Os bloqueios são administrados internamente por uma parte do [!INCLUDE[ssDE](../includes/ssde-md.md)] chamado de gerenciador de bloqueio. Quando uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] processa uma instrução [!INCLUDE[tsql](../includes/tsql-md.md)], o [!INCLUDE[ssDE](../includes/ssde-md.md)] processador de consulta determina quais recursos devem ser acessados. O processador de consulta determina que tipos de bloqueio são necessários para proteger cada recurso baseado no tipo de acesso e no nível configurado de isolamento da transação. O processador de consulta solicita os bloqueios apropriados ao gerenciador de bloqueio. O gerenciador de bloqueio concede os bloqueios, se não houver bloqueios conflitantes mantidos por outras transações.  
  
### <a name="lock-granularity-and-hierarchies"></a>Bloqueio de granularidade e hierarquias  

 O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] tem bloqueio multigranular que permite a uma transação bloquear diferentes tipos de recursos. Para minimizar o custo de bloqueio, o [!INCLUDE[ssDE](../includes/ssde-md.md)] bloqueia recursos automaticamente, em um nível apropriado para a tarefa. Bloquear em uma granularidade menor como, por exemplo linhas, aumenta a concorrência mas tem uma sobrecarga maior, devido à exigência de mais bloqueios mantidos, se muitas linhas forem bloqueadas. Bloqueando em uma granularidade maior, como tabelas, é dispendioso em termos de simultaneidade, porque bloquear a tabela inteira restringe o acesso a qualquer parte da tabela por outras transações. No entanto, tem uma sobrecarga menor, porque menos bloqueios estão sendo mantidos.  
  
 O [!INCLUDE[ssDE](../includes/ssde-md.md)] precisa, frequentemente, adquirir bloqueios em vários níveis de granularidade para proteger totalmente um recurso. Esse grupo de bloqueios em vários níveis de granularidade é chamado de uma hierarquia de bloqueio. Por exemplo, para proteger inteiramente a leitura de um índice, uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] pode ter que adquirir bloqueios compartilhados em linhas e bloqueios intencionais compartilhados nas páginas e na tabela.  
  
 A tabela seguinte mostra os recursos que o [!INCLUDE[ssDE](../includes/ssde-md.md)] pode bloquear.  
  
|Recurso|Descrição|  
|--------------|-----------------|  
|RID|Um identificador de linha usado para bloquear uma única linha dentro de um heap.|  
|KEY|Um bloqueio de linha dentro de um índice usado para proteger um intervalo de chaves em transações serializáveis.|  
|PAGE|Uma página de 8 quilobytes (KB) em um banco de dados, como dados ou páginas de índice.|  
|EXTENT|Um grupo contíguo de oito páginas, como dados ou páginas de índice.|  
|HoBT|Um heap ou árvore-B. Um bloqueio protegendo uma árvore-B (índice) ou o heap de páginas de dados que não tem um índice clusterizado.|  
|TABLE|A tabela inteira, inclusive todos os dados e índices.|  
|FILE|Um arquivo do banco de dados.|  
|APPLICATION|Um recurso de aplicativo especificado.|  
|METADATA|Bloqueios de metadados.|  
|ALLOCATION_UNIT|Uma unidade de alocação.|  
|DATABASE|O banco de dados inteiro.|  
  
> [!NOTE]  
>  HoBT e bloqueios de TABLE podem ser afetados pela opção de LOCK_ESCALATION de [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql).  
  
### <a name="lock-modes"></a>Modos de bloqueio  

 O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] bloqueia recursos que, usando diferentes modos de bloqueio, determinam como os recursos podem ser acessados por transações simultâneas.  
  
 A tabela a seguir mostra o recurso de modos de bloqueio que o [!INCLUDE[ssDE](../includes/ssde-md.md)] utiliza.  
  
|Modo de bloqueio|Description|  
|---------------|-----------------|  
|Compartilhado (S)|Usado para operações de leitura que não alteram ou atualizam dados, como uma instrução SELECT.|  
|Atualização (U)|Usado em recursos que podem ser atualizados. Evita uma forma comum de deadlock que ocorre quando várias sessões estão lendo, bloqueando e potencialmente atualizando recursos mais tarde.|  
|Exclusivo (X)|Usado para operações da modificação de dados, como INSERT, UPDATE ou DELETE. Assegura que várias atualizações não sejam realizadas no mesmo recurso ao mesmo tempo.|  
|Intencional|Usado para estabelecer uma hierarquia de bloqueio. Os tipos de bloqueios intencionais são: intencional compartilhado (IS), intencional exclusivo (IX) e compartilhado com intenção exclusiva (SIX).|  
|Esquema|Usado quando uma operação dependente do esquema de uma tabela está em execução. Os tipos de bloqueios de esquema são: modificação de esquema (Sch-M) e estabilidade de esquema (Sch-S).|  
|Atualização em massa (BU).|Usado ao copiar dados em massa em uma tabela e a dica **TABLOCK** é especificada.|  
|Intervalo de chave|Protege o intervalo de leitura de linhas lido por uma consulta ao usar o nível de isolamento da transação serializável. Assegura que outras transações não possam inserir linhas que se qualifiquem para consultas da transação serializável se as consultas forem executadas novamente.|  
  
#### <a name="shared-locks"></a>Bloqueios compartilhados  

 Bloqueios compartilhados (S) permitem que transações simultâneas leiam um recurso (SELECT) sob controle de simultaneidade pessimista. Nenhuma outra transação pode modificar os dados enquanto bloqueios compartilhados (S) existirem no recurso. Bloqueios compartilhados (S) em um recurso são liberados quando a operação de leitura termina, exceto se o nível de isolamento da transação for configurado para leitura repetida ou maior ou uma dica de bloqueio for usada para reter os bloqueios compartilhados (S) pela duração da transação.  
  
#### <a name="update-locks"></a>Bloqueios de atualização  

 Bloqueios de atualização (U) evitam que um formulário comum faça deadlock. Em uma transação serializável ou em leitura repetida, a transação lê os dados, adquire um bloqueio compartilhado (S) no recurso (página ou linha) e, então, modifica os dados, o que requer uma conversão para um bloqueio exclusivo (X). Se duas transações adquirem bloqueios em modo compartilhado em um recurso e tentam atualizar os dados simultaneamente, uma das transações tenta uma conversão do bloqueio para um bloqueio exclusivo (X). A conversão de bloqueio de modo compartilhado para exclusivo precisa esperar, porque o bloqueio exclusivo para uma transação não é compatível com o bloqueio em modo compartilhado da outra transação; ocorre uma espera por bloqueio. A segunda transação tenta adquirir um bloqueio exclusivo (X) para sua atualização. Como ambas as transações estão convertendo para bloqueios exclusivos (X), e ambas estão esperando pela outra transação liberar seu bloqueio em modo compartilhado, ocorre um deadlock.  
  
 Para evitar esse problema de potencial deadlock, são usados bloqueios de atualização (U). Só uma transação, de cada vez, pode obter um bloqueio de atualização (U) para um recurso. Se uma transação modificar um recurso, o bloqueio de atualização (U) será convertido para um bloqueio exclusivo (X).  
  
#### <a name="exclusive-locks"></a>Bloqueios exclusivos  

 Bloqueios exclusivos (X) evitam o acesso a um recurso através de transações simultâneas. Com um bloqueio exclusivo (X), nenhuma outra transação pode modificar os dados; operações de leitura podem ser realizadas apenas com o uso da dica NOLOCK ou nível de isolamento de leitura não confirmada.  
  
 Instruções de modificação de dados como INSERT, UPDATE e DELETE combinam operações de modificação e de leitura. A instrução primeiro executa as operações de leitura para adquirir dados, antes de executar as operações de modificação necessárias. Assim, as instruções de modificação de dados normalmente solicitam bloqueios compartilhados e bloqueios exclusivos. Por exemplo, uma instrução UPDATE poderia modificar linhas em uma tabela com base em uma junção com outra tabela. Nesse caso, a instrução UPDATE solicita bloqueios compartilhados nas linhas lidas na junção de tabela, além de solicitar bloqueios exclusivos nas linhas atualizadas.  
  
#### <a name="intent-locks"></a>Bloqueios intencionais  

 O [!INCLUDE[ssDE](../includes/ssde-md.md)] usa bloqueios intencionais para proteger a colocação de um bloqueio compartilhado (S) ou bloqueio exclusivo (X) em um recurso inferior na hierarquia de bloqueio. Bloqueios intencionais são assim chamados porque eles são adquiridos antes de um bloqueio em um nível inferior, e dessa forma, sinalizam a intenção de colocar bloqueios em um nível inferior.  
  
 Os bloqueios intencionais têm duas finalidades:  
  
-   Para evitar que outras transações modifiquem recursos de alto nível de uma forma que inviabilizaria o bloqueio em um nível inferior.  
  
-   Para melhorar a eficiência do [!INCLUDE[ssDE](../includes/ssde-md.md)], detectando conflitos de bloqueio em um nível mais alto de granularidade.  
  
 Por exemplo, um bloqueio intencional compartilhado é solicitado no nível de tabela antes que os bloqueios compartilhados (S) sejam solicitados em páginas ou linhas dentro dessa tabela. Configurar um bloqueio intencional no nível de tabela evita que outra transação subsequentemente adquira um bloqueio exclusivo (X) em uma tabela contendo essa página. Bloqueios intencionais aumentam o desempenho porque o [!INCLUDE[ssDE](../includes/ssde-md.md)] examina os bloqueios intencionais somente no nível de tabela para determinar se a transação pode adquirir um bloqueio de forma segura nessa tabela. Isso remove a necessidade de examinar cada bloqueio de linha ou página na tabela para determinar se a transação pode bloquear a tabela inteira.  
  
 Os bloqueios intencionais incluem intencional compartilhado (IS), intencional exclusivo (IX) e compartilhado com intenção exclusiva (SIX).  
  
|Modo de bloqueio|Description|  
|---------------|-----------------|  
|Intencional compartilhado (IS)|Protege bloqueios solicitados ou bloqueios compartilhados adquiridos em alguns (mas não todos) recursos mais baixos na hierarquia.|  
|Intencional exclusivo (IX)|Protege os bloqueios solicitados ou bloqueios exclusivos adquiridos em alguns (mas não todos) recursos mais baixos na hierarquia. IX é um superconjunto de IS, e também protege solicitando bloqueios compartilhados em recursos de nível mais baixo.|  
|Compartilhado com intenção exclusiva (SIX)|Protege bloqueios compartilhados solicitados ou adquiridos em todos os recursos inferiores na hierarquia e bloqueios intencionais exclusivos em alguns (mas não todos) recursos de nível mais baixo. São permitido bloqueios IS simultâneos no recurso de nível mais alto. Por exemplo, adquirir um bloqueio SIX, em uma tabela, também adquire bloqueios intencionais exclusivos nas páginas que estão sendo modificadas e bloqueios exclusivos nas linhas modificadas. Só pode haver um bloqueio SIX por recurso de cada vez, evitando atualizações feitas no recurso por outras transações, embora outras transações possam ler recursos, em uma hierarquia mais baixa, obtendo bloqueios IS no nível de tabela.|  
|Atualização intencional (IU).|Protege os bloqueios de atualização solicitados ou adquiridos, em todos os recursos dos níveis mais baixos da hierarquia. Bloqueios de IU só são usados em recursos de página. Bloqueios IU são convertidos a bloqueios IX se houver uma operação de atualização.|  
|Atualização intencional compartilhado (SIU)|Uma combinação de bloqueios S e IU, como resultado de aquisição desses bloqueios, separadamente e simultaneamente, mantendo ambos os bloqueios. Por exemplo, uma transação executa uma consulta com a dica PAGLOCK e, então, executa uma operação de atualização. A consulta com a dica PAGLOCK adquire o bloqueio de S e a operação de atualização adquire o bloqueio IU.|  
|Atualização intencional exclusiva (UIX)|Uma combinação de bloqueios U e IX, como resultado de aquisição desses bloqueios, separadamente e simultaneamente, mantendo ambos os bloqueios.|  
  
#### <a name="schema-locks"></a>Bloqueios de esquema  

 O [!INCLUDE[ssDE](../includes/ssde-md.md)] usa esquema de bloqueios de modificação (Sch-M) durante a operação de definição de linguagem dos dados da tabela (DDL), tal como adicionar uma coluna ou cancelar uma tabela. Durante o tempo em ele é mantido, o bloqueio Sch-M evita o acesso simultâneo à tabela. Isso significa que o bloqueio Sch-M bloqueia todos as operações externas até que o bloqueio seja liberado.  
  
 Algumas operações DML (Data Manipulation Language), tais como truncamento da tabela, usam o bloqueio Sch-M para impedir o acesso à tabelas afetadas por operações simultâneas.  
  
 O [!INCLUDE[ssDE](../includes/ssde-md.md)] usa bloqueios de estabilidade de esquema (Sch-S) quando compila e executa consultas. Os bloqueios de Sch-S não bloqueiam quaisquer bloqueios transacionais, inclusive bloqueios exclusivos (X). Assim sendo, outras transações, incluindo aquelas com bloqueios X em uma tabela, continuam executando enquanto a consulta é compilada. Porém, operações simultâneas DDL e operações simultâneas DML que adquirem bloqueios Sch-M, não podem ser executadas na tabela.  
  
#### <a name="bulk-update-locks"></a>Bloqueios de atualização em massa  

 Os bloqueios de atualização em massa (BU) permitem a vários threads carregarem simultaneamente dados em massa para a mesma tabela, evitando que outros processos, que não são carregamentos de dados em massa acessem a tabela. O [!INCLUDE[ssDE](../includes/ssde-md.md)] usa bloqueios de atualização em massa (BU) quando as condições a seguir forem verdadeiras.  
  
-   Você usa a instrução Transact-SQL BULK INSERT, ou a função OPENROWSET(BULK), ou um dos comandos de API de inserção em massa, como .NET SqlBulkCopy, OLEDB Fast Load APIs, ou as APIs de cópia em massa do ODBC para copiar dados em massa para uma tabela.  
  
-   A dica **TABLOCK** é especificada ou a opção de tabela **bloqueio da tabela em carregamento em massa** é configurada usando **sp_tableoption**.  
  
> [!TIP]  
>  Diferentemente da instrução BULK INSERT, que contém um bloqueio de atualização em massa menos restritivo, INSERT INTO...SELECT com a dica TABLOCK contém um bloqueio exclusivo (X) na tabela. Isso significa que você não pode inserir linhas usando operações de inserção paralelas.  
  
#### <a name="key-range-locks"></a>Bloqueios de intervalo de chave  

 Os bloqueios de intervalos com chave protegem um intervalo de linhas implicitamente incluídas em um conjunto de registros sendo lido por uma instrução [!INCLUDE[tsql](../includes/tsql-md.md)], ao mesmo tempo em que utiliza o nível de isolamento de transação serializável. O bloqueio de intervalo de chave impede leituras fantasmas. Ao proteger os intervalos de chaves entre as linhas, ele também evita inserções fantasmas ou exclusões em um conjunto de registros acessado por uma transação.  
  
### <a name="lock-compatibility"></a>Compatibilidade de bloqueios  

 A compatibilidade de bloqueios controla se várias transações adquirem bloqueios, no mesmo recurso ao mesmo tempo. Se um recurso já estiver bloqueado por outra transação, um novo pedido de bloqueio apenas pode ser feito se o modo do bloqueio solicitado for compatível com o modo do bloqueio existente. Se o modo de pedido de bloqueio não for compatível com o bloqueio existente, a transação que solicita um novo bloqueio espera a liberação do bloqueio existente ou que o intervalo de tempo limite se esgote. Por exemplo, nenhum modo de bloqueio é compatível com bloqueios exclusivos. Enquanto um bloqueio exclusivo (X) for mantido, nenhuma outra transação pode adquirir um bloqueio de nenhum tipo (compartilhado, atualizado ou exclusivo) naquele recurso até que o bloqueio exclusivo (X) seja liberado. Opcionalmente, se um bloqueio compartilhado (S) tiver sido aplicado a um recurso, outras transações podem também irão adquirir um bloqueio compartilhado (U) nesse item, mesmo que a primeira transação não esteja concluída. No entanto, outras transações não podem adquirir um bloqueio exclusivo até que o bloqueio compartilhado tenha sido liberado.  
  
 A tabela a seguir mostra a compatibilidade dos modos de bloqueio mais comumente encontrados.  
  
||Modo concedido existente||||||  
|------|---------------------------|------|------|------|------|------|  
|**Modo solicitado**|**FOR**|**S**|**U**|**IX**|**SIX**|**X**|  
|**Intencional compartilhado (IS)**|Yes|Yes|Yes|Yes|Sim|No|  
|**Compartilhado (S)**|Yes|Yes|Sim|Não|Não|Não|  
|**Atualização (U)**|Sim|Sim|Não|Não|Não|Não|  
|**Intencional exclusivo (IX)**|Sim|Não|Não|Sim|Não|Não|  
|**Compartilhado com intenção exclusiva (SIX)**|Sim|Não|Não|Não|Não|Não|  
|**Exclusivo (X)**|Não|Não|Não|Não|Não|Não|  
  
> [!NOTE]  
>  Um bloqueio intencional exclusivo (IX) é compatível com um modo de bloqueio IX porque IX significa que a intenção é atualizar somente algumas linhas em vez de todas. Outras transações que tentarem ler ou atualizar algumas das linhas também são permitidas, exceto se não forem as mesmas linhas que estejam sendo atualizadas por outras transações. Além disso, se duas transações tentarem atualizar a mesma linha, ambas receberão um bloqueio IX no nível de tabela e página. No entanto, uma transação receberá um bloqueio X no nível de linha. A outra transação deve aguardar até que o bloqueio de nível de linha seja removido.  
  
 Use a tabela a seguir para determinar a compatibilidade de todos os modos de bloqueio disponíveis no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 ![Diagrama que mostra a matriz de compatibilidade de bloqueio](media/lockconflicttable.gif "Diagrama que mostra a matriz de compatibilidade de bloqueio")  
  
### <a name="key-range-locking"></a>Bloqueio de intervalo de chave  

 Os bloqueios de intervalos com chave protegem um intervalo de linhas implicitamente incluídas em um conjunto de registros sendo lido por uma instrução [!INCLUDE[tsql](../includes/tsql-md.md)], ao mesmo tempo em que utiliza o nível de isolamento de transação serializável. O nível de isolamento serializável requer que qualquer consulta executada durante uma transação deva obter o mesmo conjunto de linhas, toda vez que seja executada durante a transação. Um bloqueio de intervalo de chave protege esse requisito, impedindo que outras transações insiram novas linhas cujas chaves falhariam no intervalo de chaves lido pela transação serializável.  
  
 O bloqueio de intervalo de chave impede leituras fantasmas. Ao proteger os intervalos de chaves entre as linhas, ele também evita inserções fantasmas em um conjunto de registros acessado por uma transação.  
  
 Um bloqueio de intervalo de chave é colocado em um índice, especificando um valor de chave inicial e final. Esse bloqueio impede quaisquer tentativas de inserção, atualização ou exclusão de qualquer linha de um valor de chave que falhe no intervalo, pois essas operações primeiro teriam que obter um bloqueio no índice. Por exemplo, uma transação serializável pode emitir uma instrução SELECT que leia todas as linhas cujos valores das chaves estejam entre **'** AAA **'** e **'** CZZ **'**. Um bloqueio no intervalo de chave sobre o valor da chave de **'** AAA **'** até **'** CZZ **'** evita que outras transações insiram linhas com valores de chave em qualquer posição daquele intervalo, tais como **'** ADG **'**, **'** BBD **'**, ou **'** CAL **'**.  
  
#### <a name="key-range-lock-modes"></a>Modos de bloqueio de intervalo de chave  

 O bloqueio de intervalo de chave inclui um intervalo e um componente de linha especificados no formato intervalo-linha:  
  
-   O intervalo representa o modo de bloqueio que protege o intervalo entre duas entradas consecutivas de índice.  
  
-   A fila representa o modo de bloqueio que protege a entrada de índice.  
  
-   O modo representa o modo de bloqueio combinado em uso. Os modos de bloqueio de intervalo de chave consistem de duas partes. A primeira representa o tipo de bloqueio utilizado para bloquear o intervalo de índice (Range*T*), e a segunda representa o tipo de bloqueio utilizado para bloquear uma chave específica (*K*). As duas partes são conectadas com um hífen (-), como o intervalo*T* - *K*.  
  
    |Intervalo|Linha|Mode|Description|  
    |-----------|---------|----------|-----------------|  
    |RangeS|S|RangeS-S|Intervalo compartilhado, bloqueio de recurso compartilhado; exame de intervalo serializável.|  
    |RangeS|U|RangeS-U|Intervalo compartilhado, bloqueio de recurso compartilhado; exame de atualização serializável.|  
    |RangeI|Null|RangeI-N|Insere o intervalo, anula o bloqueio de recurso; usado para testar intervalos antes de inserir uma nova chave em um índice.|  
    |RangeX|X|RangeX-X|Intervalo exclusivo, bloqueio de recurso exclusivo; usado ao atualizar uma chave em um intervalo.|  
  
> [!NOTE]  
>  O modo de bloqueio interno Nulo é compatível com todos os outros modos de bloqueio.  
  
 Os modos de bloqueio de intervalo de chave têm uma matriz de compatibilidade que mostra quais bloqueios são compatíveis com outros bloqueios obtidos em chaves e intervalos sobrepostos.  
  
||Modo concedido existente|||||||  
|------|---------------------------|------|------|------|------|------|------|  
|**Modo solicitado**|**S**|**U**|**X**|**RangeS-S**|**RangeS-U**|**RangeI-N**|**RangeX-X**|  
|**Compartilhado (S)**|Yes|Sim|Não|Sim|Yes|Sim|Não|  
|**Atualização (U)**|Sim|Não|Não|Sim|Não|Sim|No|  
|**Exclusivo (X)**|Não|Não|Não|Não|Não|Sim|No|  
|**RangeS-S**|Yes|Sim|Não|Sim|Sim|Não|Não|  
|**RangeS-U**|Sim|Não|Não|Sim|Não|Não|Não|  
|**RangeI-N**|Yes|Yes|Sim|Não|Não|Sim|No|  
|**RangeX-X**|Não|Não|Não|Não|Não|Não|Não|  
  
#### <a name="conversion-locks"></a>Bloqueios de Conversão  

 Os bloqueios de conversão são criados quando um bloqueio de intervalo de chave se sobrepuser a outro bloqueio.  
  
|Bloqueio 1|Bloqueio 2|Bloqueio de Conversão|  
|------------|------------|---------------------|  
|S|RangeI-N|RangeI-S|  
|U|RangeI-N|RangeI-U|  
|X|RangeI-N|RangeI-X|  
|RangeI-N|RangeS-S|RangeX-S|  
|RangeI-N|RangeS-U|RangeX-U|  
  
 Os bloqueios de conversão podem ser observados por um curto período de tempo sob diferentes circunstâncias complexas, às vezes enquanto executando processos simultâneos.  
  
#### <a name="serializable-range-scan-singleton-fetch-delete-and-insert"></a>Varredura de Intervalo Serializável, Busca de Singleton, Exclusão e Inserção  

 O bloqueio de intervalo de chave garante que as seguintes operações sejam serializáveis:  
  
-   Consulta de varredura de intervalo  
  
-   Busca de singleton em linha inexistente  
  
-   Operação de exclusão  
  
-   Operação de Inserção  
  
 Antes que o bloqueio de intervalo de chave possa ocorrer, as seguintes condições devem ser satisfeitas:  
  
-   O nível de isolamento da transação deve ser definido como SERIALIZABLE.  
  
-   O processador de consulta deve usar um índice para implementar o predicado de filtro do intervalo. Por exemplo, a cláusula WHERE em uma instrução SELECT poderia estabelecer uma condição de intervalo com esse predicado: ColumnX BETWEEN N **'** AAA **'** AND N **'** CZZ **'**. Um bloqueio de intervalo de chave só poderá ser adquirido se a **ColumnX** estiver coberta por uma chave de índice.  
  
#### <a name="examples"></a>Exemplos  

 A seguinte tabela e índice são usados como base para os exemplos de intervalo de chave que seguem.  
  
 ![Tabela de banco de dados com ilustração de índice de árvore b](media/btree4.gif "Tabela de banco de dados com ilustração de índice de árvore b")  
  
##### <a name="range-scan-query"></a>Consulta de Varredura de Intervalo  

 Para garantir que uma consulta de varredura de intervalo seja serializável, a mesma consulta deve retornar os mesmos resultados a cada vez que seja executada dentro de uma mesma transação. Novas linhas não devem ser inseridas dentro da consulta de varredura de intervalo por outras transações; caso contrário, elas se tornam inserções fantasmas. Por exemplo, a consulta seguinte usa a tabela e índice da ilustração anterior:  
  
```  
SELECT name  
    FROM mytable  
    WHERE name BETWEEN 'A' AND 'C';  
```  
  
 Os bloqueios de intervalo de chave são posicionados nas entradas do índice correspondentes ao intervalo das linhas de dados, onde o nome está entre os valores Adam e Dale, evitando que novas linhas que se qualifiquem na consulta anterior sejam acrescentadas ou exclusas. Embora o primeiro nome desse intervalo seja Adam, o bloqueio de intervalo de chave RangeS-S dessa entrada de índice garante que nenhum nome novo começando com a letra A possa ser adicionado antes de Adam, como por exemplo Abigail. De forma semelhante, o bloqueio de intervalo de chave RangeS-S na entrada do índice garante que nenhum nome novo começando com a letra C possa ser adicionado depois de Carlos, como Clive por exemplo.  
  
> [!NOTE]  
>  O número de bloqueios que RangeS-S contém é *n*+1, em que *n* é o número de linhas que satisfazem a consulta.  
  
##### <a name="singleton-fetch-of-nonexistent-data"></a>Busca Singleton de Dados Inexistentes  

 Se uma consulta dentro de uma transação tenta selecionar uma fila que não existe, a emissão da consulta em um momento posterior dentro da mesma transação terá que retornar o mesmo resultado. Nenhuma outra transação terá permissão de inserir essa linha inexistente. Por exemplo, nessa consulta:  
  
```  
SELECT name  
    FROM mytable  
    WHERE name = 'Bill';  
```  
  
 Um bloqueio de intervalo de chave é posicionado na entrada de índice correspondendo ao intervalo de nome de `Ben` a `Bing` pois o nome `Bill` seria inserido entre essas duas entradas adjacentes. O bloqueio de intervalo de chave do modo RangeS-S é posicionado na entrada de índice `Bing`. Isso impede que qualquer outra transação insira valores, como `Bill`, entre as entradas de índice `Ben` e `Bing`.  
  
##### <a name="delete-operation"></a>Operação de Exclusão  

 Ao excluir um valor dentro de uma transação, o intervalo no qual o valor se encaixa não tem que ser bloqueado durante a transação que está executando a operação de exclusão. Bloquear o valor de chave excluso até o fim da transação é suficiente para manter a serialização. Por exemplo, na seguinte instrução DELETE:  
  
```  
DELETE mytable  
    WHERE name = 'Bob';  
```  
  
 Um bloqueio (X) exclusivo é posicionado na entrada de índice correspondente ao nome `Bob`. Outras transações podem inserir ou excluir valores entre ou após o valor excluído `Bob`. Entretanto, qualquer transação que tente ler, inserir, ou excluir o valor `Bob` será bloqueada até que a transação de exclusão seja confirmada ou revertida.  
  
 A exclusão de intervalo pode ser executada utilizando três modos básicos de bloqueio: de linha, de página, ou de tabela. A estratégia de bloqueio de linha, página, ou tabela, é decidida pelo otimizador de consultas, ou pode ser especificada pelo usuário através de dicas como ROWLOCK, PAGLOCK, ou TABLOCK. Quando PAGLOCK ou TABLOCK são usadas, o [!INCLUDE[ssDE](../includes/ssde-md.md)] desaloca imediatamente uma página de entrada, se todas as linhas dessa página forem exclusas. Por outro lado, quando ROWLOCK é usada, todas as linhas exclusas são marcadas apenas como exclusas; elas são depois removidas da página de índice usando-se uma tarefa em segundo plano.  
  
##### <a name="insert-operation"></a>Operação de Inserção  

 Ao inserir um valor dentro de uma transação, o intervalo no qual o valor se encaixa não tem que ser bloqueado durante a transação que está executando a operação de inserção. Bloquear o valor da chave inserida até o término da transação é suficiente para manter a serialização. Por exemplo, na seguinte instrução INSERT:  
  
```  
INSERT mytable VALUES ('Dan');  
```  
  
 O bloqueio de intervalo de chave no modo RangeI-N é posicionado na entrada de índice correspondente ao nome David, para testar o intervalo. Se o bloqueio é concedido, `Dan` é inserido, e um bloqueio (X) exclusivo é posicionado no valor `Dan`. O bloqueio de intervalo de chave no modo RangeI-N, só é necessário para testar o intervalo, e não é mantido durante a transação que executa a operação de inserção. Outras transações podem inserir ou excluir valores antes ou após o valor inserido `Dan`. Entretanto, qualquer transação que tente ler, inserir, ou excluir o valor `Dan` será bloqueada até que a transação de inserção seja confirmada ou revertida.  
  
### <a name="dynamic-locking"></a>Bloqueio dinâmico  

 Usar bloqueios de nível baixo, como bloqueios de linha, aumenta a simultaneidade diminuindo a probabilidade de duas transações solicitarem bloqueios, da mesma parte dos dados, ao mesmo tempo. Bloqueios de nível baixo também aumentam o número de bloqueios e os recursos necessários para administrá-los. Usar tabela de nível alto ou bloqueios de página diminui a sobrecarga, porém causando diminuição da simultaneidade.  
  
 ![Diagrama que mostra custo versus granularidade](media/lockcht.gif "Diagrama que mostra custo versus granularidade")  
  
 O [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] usa uma estratégia de bloqueio dinâmico para determinar os bloqueios mais eficazes. O [!INCLUDE[ssDE](../includes/ssde-md.md)] determina automaticamente quais os bloqueios mais apropriados quando a consulta é executada, com base nas características do esquema e da consulta. Por exemplo, para reduzir a sobrecarga de bloqueios, o otimizador pode escolher bloqueios no nível de página em um índice, ao executar uma verificação do índice.  
  
 O bloqueio dinâmico tem as seguintes vantagens:  
  
-   Administração de banco de dados simplificada. Os administradores do banco de dados não precisam ajustar os limites de escalonamento de bloqueio.  
  
-   Desempenho superior. O [!INCLUDE[ssDE](../includes/ssde-md.md)] minimiza a sobrecarga do sistema usando bloqueios adequados à tarefa.  
  
-   Os desenvolvedores de aplicativos podem se concentrar no desenvolvimento. O [!INCLUDE[ssDE](../includes/ssde-md.md)] ajusta o bloqueio automaticamente.  
  
 No [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] e em versões posteriores, o comportamento do escalonamento de bloqueios foi alterado com a introdução da opção LOCK_ESCALATION. Para obter mais informações, consulte a opção LOCK_ESCALATION de [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql).  
  
### <a name="deadlocking"></a>Deadlock  

 Um deadlock acontece quando duas ou mais tarefas bloqueiam permanentemente uma à outra; uma tarefa está bloqueando um recurso que a outra tarefa está tentando bloquear. Por exemplo:  
  
-   A transação A adquire um bloqueio compartilhado da linha 1.  
  
-   A transação B adquire um bloqueio compartilhado da linha 2.  
  
-   A transação A agora solicita um bloqueio exclusivo na linha 2 e é bloqueado até que a transação B termine e libere o bloqueio compartilhado que tem na linha 2.  
  
-   A transação B agora solicita um bloqueio exclusivo na linha 1 e é bloqueado até que a transação A termine e libere o bloqueio compartilhado que tem na linha 1.  
  
 A transação A não pode terminar até que a transação B termine, mas a transação B está bloqueada pela transação A. Essa condição é também chamada de dependência cíclica: a transação A tem uma dependência da transação B, e a transação B fecha o círculo tendo uma dependência da transação A.  
  
 Ambas as transações em um deadlock esperarão indefinidamente, a menos que o deadlock seja quebrado por um processo externo. O monitor de deadlock [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] verifica periodicamente as tarefas que estão em um deadlock. Se o monitor detectar uma dependência cíclica, ele escolhe uma das tarefas como vítima e termina sua transação com um erro. Isso permite que a outra tarefa complete sua transação. O aplicativo com a transação que terminou com um erro pode repetir a transação, a qual normalmente é concluída depois que a outra transação em deadlock é encerrada.  
  
 O deadlock é frequentemente confundido com bloqueio normal. Quando uma transação solicita um bloqueio em um recurso bloqueado por outra transação, a transação solicitante espera até que o bloqueio seja liberado. Por padrão, as transações [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não têm tempo limite, a menos que LOCK_TIMEOUT seja configurado. A transação solicitante é bloqueada, não em deadlock, por que ela não fez nada para bloquear a transação que deve o bloqueio. Finalmente, a transação proprietária vai terminar e liberar o bloqueio e a transação solicitante terá o bloqueio atribuído e processado.  
  
 Os deadlocks às vezes são chamados de abraço mortal.  
  
 Deadlock é uma condição que pode ocorrer em qualquer sistema com vários threads, não só em sistemas de gerenciamento de banco de dados relacional, e pode ocorrer para outros recursos, além de bloqueios de objetos em bancos de dados. Por exemplo, um thread em um sistema operacional de vários threads pode adquirir um ou mais recursos, como bloqueios de memória. Se o recurso sendo adquirido é atualmente propriedade de outro thread, o primeiro thread pode ter que esperar o thread proprietário liberar o recurso alvo. O thread em espera tem uma dependência do thread proprietário para aquele recurso em particular. Em uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)], sessões podem fazer um deadlock ao adquirir recursos que não são de banco de dados, como memória ou threads.  
  
 ![Diagrama mostrando o deadlock de transação](media/dedlck1.gif "Diagrama mostrando o deadlock de transação")  
  
 Na ilustração, a transação T1 tem uma dependência da transação T2 para o recurso de bloqueio de tabela **Part**. Da mesma forma, a transação T2 tem uma dependência da transação T1 para o recurso de bloqueio de tabela **Supplier**. Devido a essas dependências formarem um ciclo, há um deadlock entre as transações T1 e T2.  
  
 Os deadlocks também podem ocorrer quando uma tabela é particionada e a configuração LOCK_ESCALATION do ALTER TABLE é configurada para AUTO. Quando LOCK_ESCALATION é definido como AUTO, a simultaneidade aumenta, permitindo que o [!INCLUDE[ssDE](../includes/ssde-md.md)] bloqueie partições de tabela no nível de HoBT em vez de no nível de tabela. Entretanto, quando transações separadas mantêm bloqueios de partição em uma tabela e querem um bloqueio em algum lugar de outra partição de transações, isso causa um deadlock. Esse tipo de deadlock pode ser evitado configurando LOCK_ESCALATION para TABLE; embora essa configuração irá reduzir a simultaneidade forçando as atualizações extensas em uma partição a esperarem por um bloqueio de tabela.  
  
#### <a name="detecting-and-ending-deadlocks"></a>Detectando e encerrando deadlocks  

 Um deadlock acontece quando duas ou mais tarefas bloqueiam permanentemente uma à outra; uma tarefa está bloqueando um recurso que a outra tarefa está tentando bloquear. O seguinte gráfico apresenta uma exibição de alto nível de um estado de deadlock em que:  
  
-   A tarefa T1 tem um bloqueio no recurso R1 (indicado pela seta de R1 para T1) e solicitou um bloqueio no recurso R2 (indicado pela seta de T1 para R2).  
  
-   A tarefa T2 tem um bloqueio no recurso R2 (indicado pela seta de R2 a T2) e solicitou um bloqueio no recurso R1 (indicado pela seta de T2 a R1).  
  
-   Como nenhuma tarefa pode continuar até que um recurso esteja disponível e nenhum recurso pode ser liberado até que uma tarefa continue, ocorre um estado de deadlock.  
  
 ![Diagrama mostrando tarefas em um estado de deadlock](media/task-deadlock-state.gif "Diagrama mostrando tarefas em um estado de deadlock")  
  
 O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] detecta ciclos de deadlock automaticamente dentro do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. O [!INCLUDE[ssDE](../includes/ssde-md.md)] escolhe uma das sessões como vítima de deadlock e a transação atual é encerrada com um erro para quebrar o deadlock.  
  
##### <a name="resources-that-can-deadlock"></a>Recursos que podem acarretar deadlock  

 Cada sessão de usuário pode ter uma ou mais tarefas sendo executadas em seu nome, sendo que cada tarefa pode adquirir ou aguardar para adquirir uma variedade de recursos. Os tipos de recursos a seguir podem causar bloqueio que pode resultar em um deadlock.  
  
-   **Bloqueios**. A espera para adquirir bloqueios em recursos, como objetos, páginas, linhas, metadados e aplicativos pode causar deadlock. Por exemplo, a transação T1 tem um bloqueio compartilhado (S) na linha r1 e está esperando para obter um bloqueio exclusivo (X) em r2. A transação T2 tem um bloqueio compartilhado (S) na linha r1 e está esperando para obter um bloqueio exclusivo (X) em r1. Isso resulta em um ciclo de bloqueio no qual T1 e T2 esperam que uma libere os recursos bloqueados da outra.  
  
-   **Threads de trabalho**. Uma tarefa em fila aguardando um thread de trabalho pode causar um deadlock. Se a tarefa em fila possuir recursos que estão bloqueando todos os threads de trabalhado, haverá um deadlock. Por exemplo, a sessão S1 inicia uma transação e adquire um bloqueio compartilhado (S) na linha r1 e, depois, fica suspenso. As sessões ativas em execução em todos os threads de trabalhado disponíveis estão tentando adquirir bloqueios exclusivos (X) na linha r1. Como a sessão S1 não pode adquirir um thread de trabalho, ela não pode confirmar a transação e liberar o bloqueio na linha r1. Isso resulta em um deadlock.  
  
-   **Memória**. Quando solicitações simultâneas estão esperando por concessões de memória que não podem ser satisfeitas com a memória disponível, pode ocorrer um deadlock. Por exemplo, duas consultas simultâneas, Q1 e Q2, são executadas como funções definidas pelo usuário que adquirem 10MB e 20MB de memória, respectivamente. Se cada consulta precisar de 30MB e a memória disponível total for de 20MB, Q1 e Q2 deverão esperar uma pela outra para liberar memória. Isso resulta em um deadlock.  
  
-   **Recursos relacionados à execução de consultas paralelas** Threads de coordenador, produtor ou consumidor associados a uma porta de troca podem bloquear uns aos outros, provocando um deadlock, normalmente ao incluir pelo menos um outro processo que não faz parte da consulta paralela. Além disso, quando uma consulta paralela começa a ser executada, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] determina o grau de paralelismo, ou o número de threads de trabalho, com base na carga de trabalho atual. Se a carga de trabalho do sistema for alterada inesperadamente, por exemplo, quando novas consultas forem executadas no servidor ou o sistema ficar sem threads de trabalho, poderá ocorrer um deadlock.  
  
-   **Recursos MARS (conjunto de resultados ativos múltiplos)**. Esses recursos são usados para controlar a intercalação de várias solicitações ativas em MARS. Para obter mais informações, consulte [Mars (vários conjuntos de resultados ativos) no SQL Server](https://msdn.microsoft.com/library/ms345109(v=SQL.90).aspx).  
  
    -   **Recurso do usuário**. Quando um thread está esperando por um recurso que é potencialmente controlado por um aplicativo de usuário, o recurso é considerado como externo ou recurso de usuário e é tratado como um bloqueio.  
  
    -   **Mutex da sessão**. As tarefas que estão sendo executadas em uma sessão são intercaladas, ou seja, apenas uma tarefa pode ser executada na sessão em um determinado momento. Antes de a tarefa ser executada, deve ter acesso exclusivo ao mutex de sessão.  
  
    -   **Mutex de transação**. Todas as tarefas que estão sendo executadas em uma transação são intercaladas, ou seja, somente uma tarefa pode ser executada na transação em um determinado momento. Antes da tarefa ser executada, deve ter acesso exclusivo ao mutex de transação.  
  
     Para que uma tarefa seja executada em MARS, ela deve adquirir o mutex da sessão. Se a tarefa estiver sendo executada em uma transação, deverá adquirir o mutex de transação. Isso garante que apenas uma tarefa esteja ativa em um determinado momento, sessão e transação. Quando os mutexes solicitados forem adquiridos, a tarefa poderá ser executada. Quando a tarefa termina, ou está no meio da solicitação, primeiro ela libera o mutex de transação e, depois, o mutex de sessão em ordem reversa de aquisição. Porém, podem ocorrer deadlocks com esses recursos. No exemplo de código a seguir, duas tarefas, solicitação de usuário U1 e solicitação de usuário U2, estão sendo executadas na mesma sessão.  
  
    ```  
    U1:    Rs1=Command1.Execute("insert sometable EXEC usp_someproc");  
    U2:    Rs2=Command2.Execute("select colA from sometable");  
    ```  
  
     O procedimento armazenado que está sendo executado na solicitação U1 adquiriu o mutex de sessão. Se o procedimento armazenado levar muito tempo para ser executado, o [!INCLUDE[ssDE](../includes/ssde-md.md)] presumirá que o procedimento armazenado está esperando uma entrada do usuário. A solicitação de usuário U2 está esperando pelo mutex de sessão, enquanto o usuário está esperando pelo conjunto de resultados de U2, e U1 está esperando por um recurso de usuário. Esse estado de deadlock é logicamente ilustrado como:  
  
 ![Diagrama lógico mostrando deadlock de processo do usuário.](media/udb9-logicflowexamplec.gif "Diagrama lógico mostrando deadlock de processo do usuário.")  
  
##### <a name="deadlock-detection"></a>Detecção de deadlock  

 Todos os recursos listados na seção anterior participam do esquema de detecção de deadlock [!INCLUDE[ssDE](../includes/ssde-md.md)]. A detecção de deadlock é executada por um thread de monitor de bloqueio que periodicamente inicia uma pesquisa por todas as tarefas em uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)]. Os seguintes pontos descrevem o processo de pesquisa:  
  
-   O intervalo padrão é de 5 segundos.  
  
-   Se o thread de monitor de bloqueio localizar deadlocks, o intervalo de detecção de deadlock diminuirá de 5 segundos para até 100 milissegundos, dependendo da frequência de deadlocks.  
  
-   Se o thread de monitor de bloqueio parar de localizar deadlocks, o [!INCLUDE[ssDE](../includes/ssde-md.md)] aumentará os intervalos entre pesquisas para 5 segundos.  
  
-   Se um deadlock tiver sido detectado há pouco tempo, presume-se que os próximos threads que precisarem esperar por um bloqueio estejam entrando no ciclo de deadlock. O primeiro par de esperas de bloqueio, após a detecção de um deadlock, dispara imediatamente uma pesquisa de deadlock em vez de aguardar pelo próximo intervalo de detecção de deadlock. Por exemplo, se o intervalo atual for de 5 segundos, e um deadlock tiver sido detectado há pouco tempo, a próxima espera de bloqueio iniciará o detector de deadlock imediatamente. Se essa espera de bloqueio fizer parte de um deadlock, será detectada imediatamente em vez de durante a próxima pesquisa de deadlock.  
  
 Normalmente, o [!INCLUDE[ssDE](../includes/ssde-md.md)] executa somente a detecção periódica de deadlock. Como o número de deadlocks encontrado no sistema geralmente é pequeno, a detecção periódica de deadlock ajuda a reduzir a sobrecarga de detecção de deadlock no sistema.  
  
 Quando o monitor de bloqueio inicia a pesquisa de deadlock para um determinado thread, ele identifica o recurso em que o thread está esperando. O monitor de bloqueio localiza o proprietário desse recurso em particular e, recursivamente, continua a pesquisa de deadlock para esses threads até encontrar um ciclo. Um ciclo identificado dessa maneira forma um deadlock.  
  
 Depois que um deadlock é detectado, o [!INCLUDE[ssDE](../includes/ssde-md.md)] encerra esse deadlock escolhendo um dos threads como uma vítima de deadlock. O [!INCLUDE[ssDE](../includes/ssde-md.md)] encerra o lote atual que está sendo executado para o thread, reverte a transação da vítima de deadlock e retorna um erro 1205 para o aplicativo. A reversão da transação da vítima de deadlock libera todos os bloqueios mantidos pela transação. Isso permite que as transações dos outros threads sejam desbloqueadas e prossigam. O erro 1205 da vítima de deadlock registra informações sobre os threads e recursos envolvidos em um deadlock no log de erros.  
  
 Por padrão, o [!INCLUDE[ssDE](../includes/ssde-md.md)] escolhe a sessão que está executando a transação mais fácil de ser revertida como a vítima de deadlock. Alternativamente, um usuário pode especificar a prioridade de sessões em uma situação de deadlock usando a instrução SET DEADLOCK_PRIORITY. O DEADLOCK_PRIORITY pode ser definida como LOW, NORMAL ou HIGH ou, alternativamente, pode ser definido como qualquer valor de inteiro no intervalo (-10 a 10). A prioridade de deadlock assume NORMAL como padrão. Se duas sessões tiverem prioridades de deadlock diferentes, a sessão com a prioridade mais baixa será escolhida como a vítima de deadlock. Se ambas as sessões tiverem a mesma prioridade de deadlock, a sessão com a transação menos dispendiosa para ser revertida será escolhida. Se as sessões envolvidas no ciclo de deadlock tiverem a mesma prioridade de deadlock e o mesmo custo, a vítima será escolhida aleatoriamente.  
  
 Ao trabalhar com CLR, o monitor de deadlock detecta automaticamente um deadlock para recursos de sincronização (monitores, bloqueio de leitura/gravação ou junção de thread) acessados dentro dos procedimentos gerenciados. Entretanto, o deadlock é resolvido ao se lançar uma exceção no procedimento selecionado como a vítima de deadlock. É importante entender que a exceção não libera automaticamente os recursos pertencentes à vítima; os recursos devem ser liberados explicitamente. Em consonância com o comportamento de exceção, a exceção usada para identificar uma vítima de deadlock pode ser capturada e ignorada.  
  
##### <a name="deadlock-information-tools"></a>Ferramentas de informações sobre deadlock  

 Para exibir informações sobre deadlock, o [!INCLUDE[ssDE](../includes/ssde-md.md)] fornece ferramentas de monitoração na forma de dois sinalizadores de rastreamento e o evento gráfico de deadlock no [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)].  
  
###### <a name="trace-flag-1204-and-trace-flag-1222"></a>Sinalizadores de rastreamento 1204 e 1222  

 Quando acontecem deadlocks, os sinalizadores de rastreamento 1204 e 1222 retornam informações captadas no log de erros [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. O sinalizador de rastreamento 1204 relata informações de deadlock formatadas por cada nó envolvido no deadlock. O sinalizador de rastreamento 1222 formata informações de deadlock, primeiro por processos e depois por recursos. É possível permitir que ambos os sinalizadores de rastreamento obtenham duas representações do mesmo evento de deadlock.  
  
 Além de definir as propriedades dos sinalizadores de rastreamento 1204 e 1222, a tabela a seguir também mostra suas semelhanças e diferenças.  
  
|Propriedade|Sinalizadores de rastreamento 1204 e 1222|Apenas sinalizador de rastreamento 1204|Apenas sinalizador de rastreamento 1222|  
|--------------|-----------------------------------------|--------------------------|--------------------------|  
|Formato da saída|A saída captada no log de erros do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|Focado nos nós envolvidos no deadlock. Cada nó tem uma seção dedicada e a seção final descreve a vítima de deadlock.|Retorna informações em um formato parecido com XML que não está em conformidade com uma definição de esquema XML (XSD). O formato tem três seções principais. A primeira seção declara a vítima de deadlock. A segunda seção descreve cada processo envolvido no deadlock. A terceira seção descreve os recursos que são sinônimos com os nós no sinalizador de rastreamento 1204.|  
|Identificando atributos|**SPID: \<x> ECID: \<x> .** Identifica o thread de ID de processo de sistema em casos de processos paralelos. A entrada `SPID:<x> ECID:0` , onde \<x> é substituída pelo valor SPID, representa o thread principal. A entrada `SPID:<x> ECID:<y>` , em que \<x> é substituída pelo valor SPID e \<y> maior que 0, representa os subthreads para o mesmo SPID.<br /><br /> **BatchID** (**sbid** para sinalizador de rastreamento 1222). Identifica o lote do qual a execução de código está solicitando ou mantendo um bloqueio. Quando vários conjuntos de resultados ativos (MARS) estão desabilitados, o valor BatchID é 0. Quando MARS está habilitado, o valor para lotes ativos é 1 para *n*. Se não houver lotes ativos na sessão, BatchID será 0.<br /><br /> **Modo**. Especifica o tipo de bloqueio de um determinado recurso que é solicitado, concedido ou aguardado por um thread. O modo pode ser IS (Intencional Compartilhado), S (Compartilhado), U (Atualização), IX (Intencional Exclusivo), SIX (Compartilhado com Intenção Exclusiva) e X (Exclusivo).<br /><br /> **Nº de linha** (**linha** para o sinalizador de rastreamento 1222). Lista o número de linha no lote atual de instruções que estava sendo executado quando o deadlock aconteceu.<br /><br /> **Input Buf** (**inputbuf** para o sinalizador de rastreamento 1222). Lista todas as instruções no lote atual.|**Nó**. Representa o número de entrada na cadeia de deadlock.<br /><br /> **Lista**. O proprietário do bloqueio pode fazer parte destas listas:<br /><br /> **Lista de Concessões**. Enumera os proprietários atuais do recurso.<br /><br /> **Lista de Conversão**. Enumera os proprietários atuais que estão tentando converter seus bloqueios em um nível mais alto.<br /><br /> **Lista de Espera**. Enumera as novas solicitações de bloqueio do recurso.<br /><br /> **Tipo de Instrução**. Descreve o tipo de instrução DML (SELECT, INSERT, UPDATE ou DELETE) em que os threads têm permissões.<br /><br /> **Proprietário do Recurso Vítima**. Especifica o thread participante que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] escolhe como a vítima para quebrar o ciclo de deadlock. O thread escolhido e todos os sub-threads existentes são encerrados.<br /><br /> **Próximo Branch**. Representa os dois ou mais sub-threads do mesmo SPID envolvidos no ciclo de deadlock.|**vítima do deadlock**. Representa o endereço de memória física da tarefa (consulte [os_tasks &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql)) que foi selecionada como vítima de deadlock. Pode ser 0 (zero) no caso de um deadlock não resolvido. Uma tarefa que está sendo revertida não pode ser escolhida como vítima de deadlock.<br /><br /> **executionstack**. Representa o código [!INCLUDE[tsql](../includes/tsql-md.md)] que está sendo executado no momento em que o deadlock ocorre.<br /><br /> **prioridade**. Representa a prioridade do deadlock. Em determinados casos, o [!INCLUDE[ssDE](../includes/ssde-md.md)] pode optar por alterar a prioridade de deadlock para uma duração curta para obter uma simultaneidade melhor.<br /><br /> **logused**. Espaço de log usado pela tarefa.<br /><br /> **ID do proprietário**. A ID da transação que tem o controle da solicitação.<br /><br /> **status**. O estado da tarefa. Pode ser um dos seguintes valores:<br /><br /> >> **pendente**. Esperando por um thread de trabalho.<br /><br /> >> **executável**. Pronto para ser executado, mas esperando por um quantum.<br /><br /> >> **em execução**. Atualmente em execução no agendador.<br /><br /> >> **suspenso**. A execução está suspensa.<br /><br /> >> **concluído**. A tarefa foi concluída.<br /><br /> >> **spinloop**. Esperando que um spinlock seja liberado.<br /><br /> **waitresource**. O recurso exigido pela tarefa.<br /><br /> **waittime**. O tempo em milissegundos de espera pelo recurso.<br /><br /> **schedulerid**. O agendador associado à essa tarefa. Veja [sys.dm_os_schedulers &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql).<br /><br /> **nome do host**. O nome da estação de trabalho.<br /><br /> **IsolationLevel**. O nível de isolamento da transação atual.<br /><br /> **Xactid**. A ID da transação que tem controle da solicitação.<br /><br /> **CurrentDb**. A ID do banco de dados.<br /><br /> **lastbatchstarted**. A última vez em que um processo cliente iniciou uma execução em lote.<br /><br /> **lastbatchcompleted**. A última vez em que um processo cliente concluiu uma execução em lote.<br /><br /> **clientoption1 e clientoption2**. Defina as opções nessa conexão de cliente. Esse é um bitmask que inclui informações sobre opções normalmente controladas por instruções SET, como SET NOCOUNT e SET XACTABORT.<br /><br /> **associatedObjectId**. Representa a ID de HoBT (heap ou árvore B).|  
|Atributos do recurso|**RID**. Identifica a única linha dentro de uma tabela na qual um bloqueio é mantido ou solicitado. RID é representado como RID: *db_id:file_id:page_no:row_no*. Por exemplo, `RID: 6:1:20789:0`.<br /><br /> **Objeto**. Identifica a tabela na qual um bloqueio é mantido ou solicitado. OBJECT é representado como OBJECT: *db_id:object_id*. Por exemplo, `TAB: 6:2009058193`.<br /><br /> **Chave**. Identifica o intervalo de chave dentro de um índice em que um bloqueio é mantido ou solicitado. KEY é representado como KEY: *db_id:hobt_id* (*o valor de hash da chave de índice*). Por exemplo, `KEY: 6:72057594057457664 (350007a4d329)`.<br /><br /> **PAG**. Identifica o recurso de página no qual um bloqueio é mantido ou solicitado. PAG é representado como PAG: *db_id:file_id:page_no*. Por exemplo, `PAG: 6:1:20789`.<br /><br /> **Ext**. Identifica a estrutura de extensão. EXT é representado como EXT: *db_id:file_id:extent_no*. Por exemplo, `EXT: 6:1:9`.<br /><br /> **DB**. Identifica o bloqueio de banco de dados. **DB é representado de um dos seguintes modos:**<br /><br /> DB: *db_id*<br /><br /> DB: *db_id*[BULK-OP-DB], que identifica o bloqueio de banco de dados feito pelo banco de dados de backup.<br /><br /> DB: *db_id*[BULK-OP-LOG], que identifica o bloqueio feito pelo log de backup daquele banco de dados específico.<br /><br /> **Aplicativo**. Identifica o bloqueio feito por um recurso de aplicativo. APP é representado por APP: *lock_resource*. Por exemplo, `APP: Formf370f478`.<br /><br /> **Metadados**. Representa os recursos de metadados envolvidos em um deadlock. Como METADATA tem muitos sub-recursos, o valor retornado depende do sub-recurso envolvido no deadlock. Por exemplo, metadados. USER_TYPE retorna `user_type_id =` \<*integer_value*> . Para obter mais informações sobre os recursos e sub-recursos METADATA, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql).<br /><br /> **HoBT**. Representa um heap ou árvore B envolvida em um deadlock.|Nenhum exclusivo para esse sinalizador de rastreamento.|Nenhum exclusivo para esse sinalizador de rastreamento.|  
  
###### <a name="trace-flag-1204-example"></a>Exemplo do sinalizador de rastreamento 1204  

 O exemplo a seguir mostra a saída quando o sinalizador de rastreamento 1204 é ativado. Neste caso, a tabela em Node 1 é um heap sem índices, e a tabela em Node 2 é um heap com índices não clusterizados. A chave de índice em Node 2 é atualizada quando o deadlock ocorre.  
  
```  
Deadlock encountered .... Printing deadlock information  
Wait-for graph  
  
Node:1  
  
RID: 6:1:20789:0               CleanCnt:3 Mode:X Flags: 0x2  
 Grant List 0:  
   Owner:0x0315D6A0 Mode: X          
     Flg:0x0 Ref:0 Life:02000000 SPID:55 ECID:0 XactLockInfo: 0x04D9E27C  
   SPID: 55 ECID: 0 Statement Type: UPDATE Line #: 6  
   Input Buf: Language Event:   
BEGIN TRANSACTION  
   EXEC usp_p2  
 Requested By:   
   ResType:LockOwner Stype:'OR'Xdes:0x03A3DAD0   
     Mode: U SPID:54 BatchID:0 ECID:0 TaskProxy:(0x04976374) Value:0x315d200 Cost:(0/868)  
  
Node:2  
  
KEY: 6:72057594057457664 (350007a4d329) CleanCnt:2 Mode:X Flags: 0x0  
 Grant List 0:  
   Owner:0x0315D140 Mode: X          
     Flg:0x0 Ref:0 Life:02000000 SPID:54 ECID:0 XactLockInfo: 0x03A3DAF4  
   SPID: 54 ECID: 0 Statement Type: UPDATE Line #: 6  
   Input Buf: Language Event:   
     BEGIN TRANSACTION  
       EXEC usp_p1  
 Requested By:   
   ResType:LockOwner Stype:'OR'Xdes:0x04D9E258   
     Mode: U SPID:55 BatchID:0 ECID:0 TaskProxy:(0x0475E374) Value:0x315d4a0 Cost:(0/380)  
  
Victim Resource Owner:  
 ResType:LockOwner Stype:'OR'Xdes:0x04D9E258   
     Mode: U SPID:55 BatchID:0 ECID:0 TaskProxy:(0x0475E374) Value:0x315d4a0 Cost:(0/380)  
```  
  
###### <a name="trace-flag-1222-example"></a>Exemplo do sinalizador de rastreamento 1222  

 O exemplo a seguir mostra a saída quando o sinalizador de rastreamento 1222 é ativado. Neste caso, uma tabela é um heap sem índices, e a outra tabela é um heap com um índice não clusterizado. Na segunda tabela, a chave de índice é atualizada quando o deadlock ocorre.  
  
```  
deadlock-list  
 deadlock victim=process689978  
  process-list  
   process id=process6891f8 taskpriority=0 logused=868   
   waitresource=RID: 6:1:20789:0 waittime=1359 ownerId=310444   
   transactionname=user_transaction   
   lasttranstarted=2005-09-05T11:22:42.733 XDES=0x3a3dad0   
   lockMode=U schedulerid=1 kpid=1952 status=suspended spid=54   
   sbid=0 ecid=0 priority=0 transcount=2   
   lastbatchstarted=2005-09-05T11:22:42.733   
   lastbatchcompleted=2005-09-05T11:22:42.733   
   clientapp=Microsoft SQL Server Management Studio - Query   
   hostname=TEST_SERVER hostpid=2216 loginname=DOMAIN\user   
   isolationlevel=read committed (2) xactid=310444 currentdb=6   
   lockTimeout=4294967295 clientoption1=671090784 clientoption2=390200  
    executionStack  
     frame procname=AdventureWorks2012.dbo.usp_p1 line=6 stmtstart=202   
     sqlhandle=0x0300060013e6446b027cbb00c69600000100000000000000  
     UPDATE T2 SET COL1 = 3 WHERE COL1 = 1;       
     frame procname=adhoc line=3 stmtstart=44   
     sqlhandle=0x01000600856aa70f503b8104000000000000000000000000  
     EXEC usp_p1       
    inputbuf  
      BEGIN TRANSACTION  
       EXEC usp_p1  
   process id=process689978 taskpriority=0 logused=380   
   waitresource=KEY: 6:72057594057457664 (350007a4d329)     
   waittime=5015 ownerId=310462 transactionname=user_transaction   
   lasttranstarted=2005-09-05T11:22:44.077 XDES=0x4d9e258 lockMode=U   
   schedulerid=1 kpid=3024 status=suspended spid=55 sbid=0 ecid=0   
   priority=0 transcount=2 lastbatchstarted=2005-09-05T11:22:44.077   
   lastbatchcompleted=2005-09-05T11:22:44.077   
   clientapp=Microsoft SQL Server Management Studio - Query   
   hostname=TEST_SERVER hostpid=2216 loginname=DOMAIN\user   
   isolationlevel=read committed (2) xactid=310462 currentdb=6   
   lockTimeout=4294967295 clientoption1=671090784 clientoption2=390200  
    executionStack  
     frame procname=AdventureWorks2012.dbo.usp_p2 line=6 stmtstart=200   
     sqlhandle=0x030006004c0a396c027cbb00c69600000100000000000000  
     UPDATE T1 SET COL1 = 4 WHERE COL1 = 1;       
     frame procname=adhoc line=3 stmtstart=44   
     sqlhandle=0x01000600d688e709b85f8904000000000000000000000000  
     EXEC usp_p2       
    inputbuf  
      BEGIN TRANSACTION  
        EXEC usp_p2      
  resource-list  
   ridlock fileid=1 pageid=20789 dbid=6 objectname=AdventureWorks2012.dbo.T2   
   id=lock3136940 mode=X associatedObjectId=72057594057392128  
    owner-list  
     owner id=process689978 mode=X  
    waiter-list  
     waiter id=process6891f8 mode=U requestType=wait  
   keylock hobtid=72057594057457664 dbid=6 objectname=AdventureWorks2012.dbo.T1   
   indexname=nci_T1_COL1 id=lock3136fc0 mode=X   
   associatedObjectId=72057594057457664  
    owner-list  
     owner id=process6891f8 mode=X  
    waiter-list  
     waiter id=process689978 mode=U requestType=wait  
```  
  
###### <a name="profiler-deadlock-graph-event"></a>Evento gráfico de deadlock de designer de perfil  

 Este é um evento do [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] que apresenta uma representação gráfica das tarefas e recursos envolvidos em um deadlock. O exemplo a seguir mostra a saída do [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] quando o evento de gráfico de deadlock é ativado.  
  
 ![Diagrama de fluxo lógico mostrando deadlock de processo do usuário.](media/udb9-profilerdeadlockgraphc.gif "Diagrama de fluxo lógico mostrando deadlock de processo do usuário.")  
  
 Para obter mais informações sobre como executar o [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] grafo de deadlock, consulte [salvar grafos de deadlock &#40;SQL Server Profiler&#41;](../relational-databases/performance/save-deadlock-graphs-sql-server-profiler.md).  
  
#### <a name="handling-deadlocks"></a>Manipulando deadlocks  

 Quando uma instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] escolhe uma transação como vítima do deadlock, ela encerra o lote atual, reverte a transação e retorna a mensagem de erro 1205 ao aplicativo.  
  
 `Your transaction (process ID #52) was deadlocked on {lock | communication buffer | thread} resources with another process and has been chosen as the deadlock victim. Rerun your transaction.`  
  
 Como qualquer aplicativo que envia consultas [!INCLUDE[tsql](../includes/tsql-md.md)] pode ser escolhido como vítima de deadlock, os aplicativos deverão ter um manipulador de erros que possa interceptar a mensagem de erro 1205. Se um aplicativo não interceptar o erro, o aplicativo poderá prosseguir sem saber que sua transação foi revertida e que erros podem ocorrer.  
  
 A implementação de um manipulador de erros que intercepte a mensagem de erro 1205 permite que um aplicativo manipule a situação de deadlock e tome uma ação paliativa (por exemplo, enviar automaticamente de novo a consulta que estava envolvida no deadlock). Ao enviar a consulta novamente de forma automática, o usuário não precisa saber que ocorreu um deadlock.  
  
 O aplicativo deveria pausar brevemente antes de enviar novamente a consulta. Isso dá a outra transação envolvida no deadlock uma chance para completar e liberar seus bloqueios que formaram parte do ciclo de deadlock. Isso minimiza a probabilidade do deadlock ocorrer novamente quando a consulta reenviada solicitar seus bloqueios.  
  
#### <a name="minimizing-deadlocks"></a>Minimizando deadlocks  

 Embora deadlocks não possam ser completamente evitados, seguir certas convenções de codificação pode minimizar a chance de gerar um deadlock. Minimizar deadlocks pode aumentar a taxa de transferência da transação e pode reduzir a sobrecarga do sistema pois poucas transações são:  
  
-   Revertidas, desfazendo todo o trabalho executado pela transação.  
  
-   Reenviadas por aplicativos pois elas foram revertidas quando bloqueadas.  
  
 Para ajudar a minimizar deadlocks:  
  
-   Acesse objetos na mesma ordem.  
  
-   Evite a interação de usuário durante as transações.  
  
-   Mantenha as transações curtas e em um lote.  
  
-   Use um nível de isolamento inferior.  
  
-   Use um nível de isolamento com base em controle de versão de linha  
  
    -   Configure a opção de banco de dados READ_COMMITTED_SNAPSHOT em ON, para habilitar que as transações de leitura confirmada utilizem controle de versão de linha.  
  
    -   Use transação de isolamento de instantâneo  
  
-   Use associações de saída.  
  
##### <a name="access-objects-in-the-same-order"></a>Acesse objetos na mesma ordem.  

 Se todas as transações simultâneas acessarem objetos na mesma ordem, haverá menos chance de ocorrerem deadlocks. Por exemplo, se duas transações simultâneas obtiverem um bloqueio na tabela **Supplier** e depois na tabela **Part**, uma transação será bloqueada na tabela **Supplier** até que a outra transação seja concluída. Após a primeira transação ser confirmada ou revertida, a segunda continua e um deadlock não acontece. Usar procedimentos armazenados para todas as modificações de dados pode padronizar a ordem de acesso dos objetos.  
  
 ![Diagrama mostrando impedimento do deadlock de transação](media/dedlck2.gif "Diagrama mostrando impedimento do deadlock de transação")  
  
##### <a name="avoid-user-interaction-in-transactions"></a>Evite usar interação nas transações  

 Evite escrever transações que incluam interação de usuário, pois a velocidade de lotes executados sem intervenção de usuário é muito mais rápida que a velocidade que um usuário deve responder manualmente às consultas, como por exemplo, responder a um prompt para um parâmetro solicitado por um aplicativo. Por exemplo, se uma transação estiver esperando por entrada de usuário e o usuário sai para almoçar ou vai para casa durante o fim de semana, esse mesmo usuário atrasa o término da transação. Isto degrada a taxa de transferência do sistema, pois quaisquer bloqueios mantidos pela transação somente são liberados quando a transação é confirmada ou revertida. Até mesmo se uma situação de deadlock não surgir, outras transações que acessem os mesmos recursos serão bloqueadas enquanto esperam pela conclusão da transação.  
  
##### <a name="keep-transactions-short-and-in-one-batch"></a>Mantenha as transações curtas e em um lote.  

 Um deadlock ocorre tipicamente quando várias transações demoradas são executadas simultaneamente no mesmo banco de dados. Quanto mais longa a transação, por mais tempo as atualizações e bloqueios exclusivos são mantidos, bloqueando outras atividades, e levando à possíveis situações de deadlock.  
  
 Manter as transações em um lote minimiza as viagens de ida-e-volta de rede durante uma transação, reduzindo possíveis retardos ao completar a transação e liberando bloqueios.  
  
##### <a name="use-a-lower-isolation-level"></a>Use um nível inferior de isolamento  

 Determine se uma transação pode ser executada em um nível inferior de isolamento. Implementar confirmação por leitura permite que uma transação leia dados lidos anteriormente (não modificados) por outra transação, sem esperar pela conclusão da primeira transação. Usar um nível de isolamento inferior, como a leitura confirmada, mantém bloqueios compartilhados por uma período mais curto que um nível de isolamento maior, como o serializável. Isto reduz a contenção de bloqueio.  
  
##### <a name="use-a-row-versioning-based-isolation-level"></a>Use um nível de isolamento com base em controle de versão de linha  

 Quando a opção READ_COMMITTED_SNAPSHOT do banco de dados é configurada em ON, uma transação em execução sob o nível de isolamento de leitura confirmada utiliza controle de versão de linha em vez de bloqueios compartilhados durante operações de leitura.  
  
> [!NOTE]  
>  Alguns aplicativos dependem de um comportamento de bloqueio e desbloqueio de isolamento confirmado por leitura. Para estes aplicativos, algumas alterações são necessárias antes que essa opção possa ser habilitada.  
  
 O isolamento de instantâneo também usa controle de versão de linha, o qual não usa bloqueios compartilhados durante operações de leitura. Antes que uma transação possa ser executada sob um isolamento de instantâneo, a opção ALLOW_SNAPSHOT_ISOLATION do banco de dados deve ser configurada em ON.  
  
 Implemente estes níveis de isolamento para minimizar deadlocks, que podem ocorrer entre as operações de leitura e gravação.  
  
##### <a name="use-bound-connections"></a>Use associações de saída.  

 Usar associações de saída usando, faz com que duas ou mais conexões abertas pelo mesmo aplicativo possam cooperar entre si. Qualquer bloqueio adquirido pelas conexões secundárias é mantido como se tivessem sido adquiridos pela conexão primária, e vice-versa. Portanto, eles não bloqueiam um ao outro.  
  
### <a name="lock-partitioning"></a>Particionamento de bloqueio  

 Para os grandes sistemas de computador, bloqueios em objetos que são referenciados com frequência podem se tornar um gargalo de desempenho, uma vez que a aquisição e liberação de bloqueios produz contenções em recursos de bloqueios internos. O particionamento de bloqueio melhora o desempenho do bloqueio dividindo um único recurso de bloqueio em vários recursos de bloqueio. Esse recurso só está disponível para sistemas com 16 ou mais CPUs, é habilitado automaticamente e não pode ser desabilitado. Apenas os bloqueios de objeto podem ser particionados. Os bloqueios de objeto que têm um subtipo não são particionados. Para obter mais informações, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql).  
  
#### <a name="understanding-lock-partitioning"></a>Compreendendo o particionamento de bloqueio  

 As tarefas de bloqueio acessam vários recursos compartilhados, dois dos quais são otimizados através de particionamento de bloqueio:  
  
-   **Spinlock**. Controla o acesso a um recurso de bloqueio, como uma linha ou uma tabela.  
  
     Sem particionamento de bloqueio, um spinlock gerencia todas as solicitações de bloqueio para um único recurso de bloqueio. Em sistemas que têm um grande volume de atividade, a contenção pode acontecer enquanto as solicitações de bloqueio esperam que o spinlock fique disponível. Nessa situação, adquirir bloqueios pode se converter em um gargalo e ter um impacto negativo no desempenho.  
  
     Para reduzir a contenção em um único recurso de bloqueio, o particionamento de bloqueio divide um único recurso de bloqueio em vários recursos de bloqueio para distribuir a carga através de vários spinlocks.  
  
-   **Memória**. É usada para armazenar as estruturas de recurso de bloqueio.  
  
     Depois que o spinlock é adquirido, são armazenadas estruturas de bloqueio na memória, que então são acessadas e eventualmente modificadas. Distribuir acesso de bloqueio através de vários recursos ajuda eliminar a necessidade de transferir blocos de memória entre CPUs, que ajudará melhorar o desempenho.  
  
#### <a name="implementing-and-monitoring-lock-partitioning"></a>Implementando e monitorando o particionamento de bloqueio  

 O particionamento de bloqueio é ativado por padrão para sistemas com 16 ou mais CPUs. Quando o particionamento de bloqueio é habilitado, uma mensagem informativa é registrada no log de erros do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Ao adquirir bloqueios em um recurso particionado:  
  
-   Só os modos de bloqueio NL, SCH-S, IS, IU e IX modos são adquiridos em uma única partição.  
  
-   Bloqueios S (Shared), X (Exclusive) e outros bloqueios em modos diferentes de NL, SCH-S, IS, IU e IX em todas as partições iniciando com partição ID 0 e seguindo na partição a ordem de ID. Esses bloqueios em um recurso particionado usarão mais memória que os bloqueios, no mesmo modo, em um recurso não particionado, desde que cada partição seja efetivamente um bloqueio separado. O aumento de memória é determinado pelo número de partições. Os contadores de bloqueio do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Monitor de Desempenho do Windows exibirão informações sobre a memória usada em bloqueios particionados e não particionados.  
  
 Uma transação é atribuída a uma partição quando a transação inicia. Para a transação, todas as solicitações de bloqueio que podem ser particionadas usam a partição atribuída a essa transação. Por esse método, o acesso para bloquear recursos do mesmo objeto através de transações diferentes é distribuído através de diferentes partições.  
  
 A coluna resource_lock_partition no sys.dm_tran_locks da Exibição de Gerenciamento Dinâmico fornece o ID da partição de bloqueio para um recurso de bloqueio particionado. Para obter mais informações, consulte [sys.DM tran_locks &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql).  
  
 A coluna de BigintData1 fornece o ID da partição de bloqueio para o recurso de bloqueio particionado no evento de Bloqueios do [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)].  
  
#### <a name="working-with-lock-partitioning"></a>Trabalhando com particionamento de bloqueio  

 Os exemplos de código a seguir ilustram o particionamento de bloqueio. Nos exemplos, são executadas duas transações em duas sessões diferentes para mostrar o comportamento de particionamento de bloqueio em um sistema de computador com 16 CPUs.  
  
 Estas instruções [!INCLUDE[tsql](../includes/tsql-md.md)] criam objetos de teste que são usados nos exemplos a seguir.  
  
```  
-- Create a test table.  
CREATE TABLE TestTable  
    (col1        int);  
GO  
  
-- Create a clustered index on the table.  
CREATE CLUSTERED INDEX ci_TestTable   
    ON TestTable (col1);  
GO  
  
-- Populate the table.  
INSERT INTO TestTable VALUES (1);  
GO  
```  
  
##### <a name="example-a"></a>Exemplo A  

 Sessão 1:  
  
 Uma instrução `SELECT` é executada em uma transação. Devido à dica de bloqueio `HOLDLOCK`, essa instrução adquirirá e reterá um bloqueio IS (Intencional compartilhado) na tabela (para efeitos de ilustração, são ignorados os bloqueios de linha e de página). O bloqueio IS só será adquirido na partição atribuída à transação. Para este exemplo, supõe-se que o bloqueio IS é adquirido na ID 7 da partição.  
  
```  
-- Start a transaction.  
BEGIN TRANSACTION  
    -- This SELECT statement will acquire an IS lock on the table.  
    SELECT col1  
        FROM TestTable  
        WITH (HOLDLOCK);  
```  
  
 Sessão 2:  
  
 Uma transação é iniciada e a instrução `SELECT` que executa sob essa transação adquirirá e reterá um bloqueio S (compartilhado) na tabela. O bloqueio S será adquirido em todas as partições que resultem em vários bloqueios de tabela, um para cada partição. Por exemplo, em um sistema com 16 CPUs, 16 bloqueios S serão emitidos através de os IDs de partição 0-15. Como o bloqueio S é compatível com o bloqueio de IS, que é mantido na ID 7 da partição pela transação na sessão 1, não há nenhum bloqueio entre as transações.  
  
```  
BEGIN TRANSACTION  
    SELECT col1  
        FROM TestTable  
        WITH (TABLOCK, HOLDLOCK);  
```  
  
 Sessão 1:  
  
 A instrução `SELECT` a seguir é executada na transação que ainda estiver ativa na sessão 1. Devido a dica de bloqueio de tabela exclusivo, a transação tentará adquirir um bloqueio X na tabela . Entretanto, o bloqueio S que está sendo mantido pela transação na sessão 2 bloqueará o bloqueio X na ID 0 da partição.  
  
```  
SELECT col1  
    FROM TestTable  
    WITH (TABLOCKX);  
```  
  
##### <a name="example-b"></a>Exemplo B  

 Sessão 1:  
  
 Uma instrução `SELECT` é executada em uma transação. Devido à dica de bloqueio `HOLDLOCK`, essa instrução adquirirá e reterá um bloqueio IS (Intencional compartilhado) na tabela (para efeitos de ilustração, são ignorados os bloqueios de linha e de página). O bloqueio IS só será adquirido na partição atribuída à transação. Para este exemplo, supõe-se que o bloqueio IS é adquirido na ID 6 da partição.  
  
```  
-- Start a transaction.  
BEGIN TRANSACTION  
    -- This SELECT statement will acquire an IS lock on the table.  
    SELECT col1  
        FROM TestTable  
        WITH (HOLDLOCK);  
```  
  
 Sessão 2:  
  
 Uma instrução `SELECT` é executada em uma transação. Devido a dica de bloqueio `TABLOCKX`, a transação tenta adquirir um bloqueio X (exclusivo) na tabela. Lembre-se que o bloqueio X deve ser adquirido em todas as partições começando com o ID de partição 0. Entretanto, o bloqueio X será adquirido em todos os IDs de partição 0-5 pelo bloqueio IS que é adquirido no ID de partição 6.  
  
 Nos IDs de partição 7-15 que o bloqueio X ainda não atingiu, outras transações podem continuar adquirindo bloqueios.  
  
```  
BEGIN TRANSACTION  
    SELECT col1  
        FROM TestTable  
        WITH (TABLOCKX, HOLDLOCK);  
```  
  
 ![Ícone de seta usado com o link voltar ao início](media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [neste guia](#Top)  
  
##  <a name="row-versioning-based-isolation-levels-in-the-database-engine"></a><a name="Row_versioning"></a>Níveis de isolamento baseados em controle de versão de linha no Mecanismo de Banco de Dados  

 Com o SQL Server 2005, o mecanismo de banco de dados passou a oferecer a implementação do nível de isolamento de uma transação existente, a leitura confirmada, que fornece um instantâneo de nível de instrução usando o controle de versão de linha. O mecanismo de banco de dados do SQL Server também oferece um nível de isolamento da transação, o instantâneo, que fornece um instantâneo de nível de transação e que também usa o controle de versão de linha.  
  
 O controle de versão de linha é uma estrutura geral no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que chama um mecanismo de gravação de cópia quando uma linha é modificada ou excluída. Enquanto a transação está sendo executada, ele requer que a versão anterior da linha esteja disponível para transações que exigem um estado transacional consistente anterior. O controle de versão de linha é usado para:  
  
-   Compilar as tabelas **inseridas** e **excluídas** em gatilhos. Qualquer linha modificada pelo gatilho tem controle de versão. Isso inclui as linhas modificadas pela instrução que iniciou o gatilho, bem como quaisquer modificações de dados feitas pelo gatilho.  
  
-   Oferecer suporte a vários conjuntos de resultados ativos (MARS) Se uma sessão MARS emitir uma instrução de modificação de dados (como INSERT, UPDATE ou DELETE) cada vez que houver um conjunto de resultados ativos, as linhas afetadas pela instrução de modificação terão controle de versão.  
  
-   Oferecer suporte a operações de índice que especificam a opção ONLINE.  
  
-   Oferecer suporte a níveis de isolamento de transações com base em controle de versão de linha:  
  
    -   Uma nova implementação de nível de isolamento de leitura confirmada que utiliza o controle de versão de linha para fornecer a consistência de leitura em nível de instrução.  
  
    -   Um novo nível de isolamento, instantâneo, para fornecer a consistência de leitura em nível de transações.  
  
 O banco de dados `tempdb` deve ter espaço suficiente para o armazenamento de versão. Quando `tempdb` está cheio, as operações de atualização param de gerar versões e continuam a ter êxito, mas as operações de leitura podem falhar porque uma versão de linha específica necessária não existe mais. Isto afeta operações como gatilhos, MARS e indexação online.  
  
 O uso de controle de versão de linha para transações de leitura confirmada e de instantâneo é um processo em duas etapas:  
  
1.  Defina uma ou ambas as opções de banco de dados READ_COMMITTED_SNAPSHOT e ALLOW_SNAPSHOT_ISOLATION como ON.  
  
2.  Defina o nível de isolamento da transação apropriado em um aplicativo:  
  
    -   Quando a opção de banco de dados READ_COMMITTED_SNAPSHOT for ON, as transações que configuram o nível de isolamento da leitura confirmada usarão o controle de versão de linha.  
  
    -   Quando a opção de banco de dados ALLOW_SNAPSHOT_ISOLATION for ON, as transações poderão definir o nível de isolamento do instantâneo.  
  
 Quando a opção de banco de dados READ_COMMITTED_SNAPSHOT ou ALLOW_SNAPSHOT_ISOLATION for ON, o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] atribuirá um número de sequência da transação (XSN) para cada transação que manipular dados usando o controle de versão de linha. As transações iniciam quando uma instrução BEGIN TRANSACTION é executada. Porém, o número de sequência da transação inicia com a primeira operação de leitura ou gravação depois da instrução BEGIN TRANSACTION. O número de sequência da transação é incrementado um por vez sempre que é atribuído.  
  
 Quando as opções de banco de dados READ_COMMITTED_SNAPSHOT ou ALLOW_SNAPSHOT_ISOLATION forem ON, as cópias lógicas (versões) serão mantidas para todas as modificações de dados executadas no banco de dados. Sempre que uma linha é modificada por uma transação específica, a instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] armazena uma versão da imagem confirmada anteriormente da linha em `tempdb`. Cada versão é marcada com o número de sequência de transação da transação que fez a alteração. As versões das linhas modificadas são encadeadas usando uma lista de links. O valor da linha mais recente sempre é armazenado no banco de dados atual e encadeado às linhas com controle de versão armazenadas em `tempdb`.  
  
> [!NOTE]  
>  Para a modificação de LOBs (objetos grandes), somente o fragmento alterado é copiado para o armazenamento de versão em `tempdb`.  
  
 As versões da linha são mantidas por tempo suficiente para atender os requisitos das transações executadas em níveis de isolamento com base em controle de versão de linha. O [!INCLUDE[ssDE](../includes/ssde-md.md)] localiza o número útil mais antigo de sequência da transação e exclui periodicamente todas as versões da linha carimbadas com números de sequência da transação inferiores ao número útil mais antigo da sequência.  
  
 Quando ambas as opções do banco de dados estão definidas como OFF, somente as linhas modificadas por gatilhos ou sessões MARS, ou lidas por operações de índice ONLINE, têm controle de versão. Essas versões de linha são liberadas quando já não são necessárias. Um thread em segundo plano é periodicamente executado para remover versões obsoletas da linha.  
  
> [!NOTE]  
>  Para transações de execução curta, uma versão de uma linha modificada pode ficar armazenada em cache no pool de buffers sem ser gravada nos arquivos de disco do banco de dados `tempdb`. Se a necessidade da linha com controle de versão for de curta duração, a linha será simplesmente retirada do pool de buffers sem necessariamente gerar uma sobrecarga de E/S.  
  
### <a name="behavior-when-reading-data"></a>Comportamento durante a leitura de dados  

 Quando as transações são executadas em dados de leitura de isolamento com base em controle de versão de linha, as operações de leitura não adquirem bloqueios compartilhados (S) nos dados que estão sendo lidos, portanto, não bloqueiam transações que estão modificando dados. A sobrecarga de recursos de bloqueio também é minimizada conforme o número de bloqueios adquirido é reduzido. O isolamento de leitura confirmada que usa controle de versão de linha e isolamento de instantâneo é desenvolvido para fornecer consistências de leitura em nível de transação e instrução de dados com controle de versão.  
  
 Todas as consultas, incluindo as transações executadas em níveis de isolamento com base em controle de versão de linha, adquirem bloqueios Sch-S (estabilidade do esquema) durante a compilação e a execução. Por causa disso, as consultas são bloqueadas quando uma transação simultânea mantém um bloqueio Sch-M (modificação de esquema) na tabela. Por exemplo, uma operação DDL (Linguagem de Definição de Dados) adquire um bloqueio Sch-M antes de modificar as informações do esquema da tabela. As transações de consulta, incluindo aquelas executadas em nível de isolamento com base em controle de versão de linha, são bloqueadas ao tentar adquirir um bloqueio Sch-S. Da mesma forma, uma consulta que mantém um bloqueio Sch-S bloqueará uma transação simultânea que tentar adquirir um bloqueio Sch-M.  
  
 Quando uma transação que usa o nível de isolamento do instantâneo é iniciada, a instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] registra todas as transações ativas no momento. Quando a transação de instantâneo lê uma linha que tem uma cadeia de versão, o [!INCLUDE[ssDE](../includes/ssde-md.md)] segue a cadeia e recupera a linha em que o número de sequência da transação:  
  
-   Está mais próxima, mas inferior ao número de sequência da transação de instantâneo que está lendo a linha.  
  
-   Não está na lista das transações ativas quando a transação de instantâneo é iniciada.  
  
 As operações de leitura executadas por uma transação de instantâneo recuperam a última versão de cada linha confirmada quando a transação de instantâneo foi iniciada. Isso fornece um instantâneo transacional consistente dos dados, da mesma forma como existiam no início da transação.  
  
 As transações de leitura confirmada que usam controle de versão de linha funcionam praticamente do mesmo modo. A diferença é que a transação de leitura confirmada não usa o seu próprio número de sequência da transação ao escolher versões de linha. Cada vez que uma instrução é iniciada, a transação de leitura confirmada lê o último número de sequência da transação emitido para aquela instância do [!INCLUDE[ssDE](../includes/ssde-md.md)]. Esse é o número de sequência da transação usado para selecionar as versões de linha corretas para aquela instrução. Isso permite que as transações de leitura confirmada veja um instantâneo dos dados como ele era no início de cada instrução.  
  
> [!NOTE]  
>  Embora as transações de leitura confirmada que usam controle de versão de linha forneçam uma exibição transacional consistente dos dados em um nível de instrução, as versões de linha geradas ou acessadas por esse tipo de transação são mantidas até a conclusão da transação.  
  
### <a name="behavior-when-modifying-data"></a>Comportamento durante a modificação de dados  

 Em uma transação de leitura confirmada que usa o controle de versão de linha, a seleção de linhas a serem atualizadas é feita usando uma verificação de bloqueio em que um bloqueio de atualização (U) é feito na linha de dados conforme os valores dos dados são lidos. Isso é igual à transação de leitura confirmada que não usa controle de versão de linha. Se a linha de dados não atender os critérios de atualização, o bloqueio de atualização será liberado naquela linha e a próxima linha será fechada e verificada.  
  
 As transações executadas em isolamento de instantâneo usam uma abordagem otimista para modificação de dados adquirindo bloqueios em dados antes de executar a modificação somente para impor restrições. Do contrário, os bloqueios não são adquiridos em dados até que os dados sejam modificados. Quando uma linha de dados atende os critérios de atualização, a transação de instantâneo verifica se a linha de dados não foi modificada por uma transação simultânea que foi confirmada depois do início da transação de instantâneo. Se a linha de dados tiver sido modificada fora da transação de instantâneo, ocorrerá um conflito de atualização e a transação de instantâneo será finalizada. O conflito de atualização é controlado pelo [!INCLUDE[ssDE](../includes/ssde-md.md)] e não há como desabilitar a detecção de conflito de atualização.  
  
> [!NOTE]  
>  As operações de atualização executadas em isolamento de instantâneo são internamente executadas em isolamento de leitura confirmada quando a transação de instantâneo acessa qualquer um dos seguintes itens:  
>   
>  Uma tabela com uma restrição FOREIGN KEY.  
>   
>  Uma tabela referenciada na restrição FOREIGN KEY de outra tabela.  
>   
>  Uma exibição indexada referenciando mais de uma tabela.  
>   
>  Porém, mesmo de acordo com essas condições, a operação de atualização continuará verificando se os dados não foram modificados por outra transação. Se os dados tiverem sido modificados por outra transação, a transação de instantâneo encontrará um conflito de atualização e será finalizada.  
  
### <a name="behavior-in-summary"></a>Resumo do comportamento  

 A tabela a seguir resume as diferenças entre o isolamento de instantâneo e o isolamento de leitura confirmada usando o controle de versão de linha.  
  
|Propriedade|Nível de isolamento de leitura confirmada usando o controle de versão de linha|Nível de isolamento do instantâneo|  
|--------------|----------------------------------------------------------|------------------------------|  
|A opção de banco de dados que deve ser definida como ON para habilitar o suporte exigido.|READ_COMMITTED_SNAPSHOT|ALLOW_SNAPSHOT_ISOLATION|  
|Como uma sessão solicita o tipo específico de controle de versão de linha.|Use o nível padrão de isolamento de leitura confirmada ou execute a instrução SET TRANSACTION ISOLATION LEVEL para especificar o nível de isolamento READ COMMITTED. Isso pode ser feito depois do início da transação.|Exige a execução de SET TRANSACTION ISOLATION LEVEL para especificar o nível de isolamento SNAPSHOT antes do início da transação.|  
|A versão dos dados lidos por instruções.|Todos os dados que foram confirmados antes do início de cada instrução.|Todos os dados que foram confirmados antes do início de cada transação.|  
|Como as atualizações são controladas.|Faz a reversão de versões de linha a dados reais para selecionar as linhas que devem ser atualizadas e usa os bloqueios de atualização nas linhas de dados selecionadas. Adquire bloqueios exclusivos em linhas de dados atuais a serem modificadas. Nenhuma detecção de conflito de atualização.|Usa versões de linha para selecionar linhas a serem atualizadas. Tenta adquirir um bloqueio exclusivo na linha de dados reais a ser modificada e, se os dados tiverem sido modificados por outra transação, ocorrerá um conflito de atualização e a transação de instantâneo será finalizada.|  
|Atualização de detecção de conflito.|Nenhum.|Suporte integrado. Não pode ser desabilitado.|  
  
### <a name="row-versioning-resource-usage"></a>Uso do recurso de controle de versão de linha  

 A estrutura de controle de versão de linha dá suporte aos seguintes recursos disponíveis no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   Gatilhos  
  
-   MARS (vários conjuntos de resultados ativos)  
  
-   Indexação online  
  
 A estrutura de controle de versão de linha também dá suporte aos seguintes níveis de isolamento da transação baseada no controle de versão de linha que, por padrão, não estão habilitados:  
  
-   Quando a opção de banco de dados READ_COMMITTED_SNAPSHOT for ON, as transações READ_COMMITTED fornecerão consistência de leitura no nível da instrução usando o controle de versão de linha.  
  
-   Quando a opção de banco de dados ALLOW_SNAPSHOT_ISOLATION for ON, as transações SNAPSHOT fornecerão consistência de leitura no nível da transação usando o controle de versão de linha.  
  
 Os níveis de isolamento com base no controle de versão de linha reduzem o número de bloqueios adquiridos pela transação eliminando o uso de bloqueios compartilhados em operações de leitura. Isso aumenta o desempenho do sistema reduzindo os recursos usados para gerenciar bloqueios. O desempenho também é aumentado pela redução do número de vezes em que uma transação fica bloqueada por bloqueios adquiridos por outras transações.  
  
 Os níveis de isolamento com base no controle de versão de linha aumentam os recursos necessários pelas modificações de dados. Habilitar essas opções faz com que todas as modificações de dados no banco de dados sejam controladas por versão. Uma cópia dos dados antes da modificação é armazenada em tempdb, mesmo quando não há transações ativas que usam o isolamento com base em controle de versão de linha. Os dados após a modificação incluem um ponteiro para os dados controlados por versão armazenados em tempdb. Para objetos grandes, apenas parte do objeto alterado é copiada em tempdb.  
  
#### <a name="space-used-in-tempdb"></a>Espaço usado no tempdb  

 Para cada instância do [!INCLUDE[ssDE](../includes/ssde-md.md)], o tempdb deve ter espaço suficiente para manter as versões de linha geradas para cada banco de dados na instância. O administrador de banco do dados deve garantir que tempdb tem espaço suficiente para oferecer suporte ao armazenamento da versão. Há dois armazenamentos de versão em tempdb:  
  
-   O repositório de versão de compilação de índices online é usado para compilações de índices online em todos os bancos de dados.  
  
-   O repositório da versão comum é usado para todas as outras operações de modificação de dados em todos os bancos de dados.  
  
 As versões de linha devem ser armazenadas enquanto uma transação ativa precisar acessá-las. Uma vez a cada minuto, um thread em segundo plano remove as versões de linha que não são mais necessárias e libera o espaço da versão no tempdb. Uma transação de longa execução impedirá que o espaço do repositório de versão seja liberado, se as seguintes condições forem encontradas:  
  
-   Ela usa isolamento com base em controle de versão de linha.  
  
-   Ela usa gatilhos, MARS ou operações de compilação de índices online.  
  
-   Ela gera versões de linha.  
  
> [!NOTE]  
>  Quando um gatilho é acionado em uma transação, são mantidas as versões de linha criadas pelo gatilho até o término da transação, mesmo quando as versões de linha não forem mais necessárias após o gatilho ser concluído. Isso também se aplica a transações de leitura confirmada que usam controle de versão de linha. Com esse tipo de transação, uma exibição consistente de maneira transacional do banco de dados é necessária apenas para cada instrução na transação. Isso significa que as versões de linha criadas para uma instrução na transação não são necessárias depois que a instrução é concluída. Porém, as versões de linha criadas por cada instrução na transação são mantidas até que a transação seja concluída.  
  
 Quando o espaço no tempdb for insuficiente, o [!INCLUDE[ssDE](../includes/ssde-md.md)] reduzirá os armazenamentos da versão. Durante o processo de redução, as transações mais longas que estiverem sendo executadas e que ainda não geraram versões de linha serão marcadas como vítimas. Uma mensagem 3967 é gerada no log de erros para cada transação vítima. Se uma transação for marcada como uma vítima, não poderá ler as versões de linha no armazenamento da versão. Ao tentar ler versões de linhas, a mensagem 3966 é gerada e a transação é revertida. Se o processo de redução for executado com êxito, haverá espaço disponível em tempdb. Caso contrário, o tempdb ficará sem espaço e ocorrerá o seguinte:  
  
-   As operações de gravação continuarão a ser executadas, mas não gerarão versões. Uma mensagem informativa (3959) será exibida no log de erros, mas a transação que grava dados não será afetada.  
  
-   As transações que tentam acessar versões de linha que não foram geradas devido a uma reversão completa de tempdb serão encerradas com um erro 3958.  
  
#### <a name="space-used-in-data-rows"></a>Espaço usado em linhas de dados  

 Cada linha de banco de dados pode usar até 14 bytes ao término da linha para obter informações sobre o controle de versão de linha. As informações sobre o controle de versão de linha contêm o número de sequência da transação que confirmou a versão e o ponteiro da linha controlada por versão. Esses 14 bytes são adicionados na primeira vez em que a linha é modificada, ou quando uma nova linha é inserida, em qualquer uma destas condições:  
  
-   A opção READ_COMMITTED_SNAPSHOT ou ALLOW_SNAPSHOT_ISOLATION está ON.  
  
-   A tabela tem um gatilho.  
  
-   Os MARS (conjuntos de resultados ativos múltiplos) estão sendo usados.  
  
-   As operações de compilação de índices online estão sendo executadas atualmente na tabela.  
  
 Esses 14 bytes são removidos da linha do banco de dados na primeira vez em que a linha é modificada nestas condições:  
  
-   As opções READ_COMMITTED_SNAPSHOT e ALLOW_SNAPSHOT_ISOLATION estão OFF.  
  
-   O gatilho não existe mais na tabela.  
  
-   Os MARS não estão sendo usados.  
  
-   As operações de compilação de índices online não estão sendo executadas no momento.  
  
 Se você usar qualquer um dos recursos de controle de versão de linha, poderá ser necessário alocar espaço em disco adicional para o banco de dados para acomodar a linha de 14 bytes por banco de dados. A adição das informações de controle de versão de linha poderá causar a divisão da página de índice ou a alocação de uma nova página de dados se não houver espaço disponível suficiente na página atual. Por exemplo, se o comprimento médio da linha for 100 bytes, os 14 bytes adicionais farão com que uma tabela existente cresça até 14%.  
  
 Reduzir o [fator de preenchimento](../relational-databases/indexes/specify-fill-factor-for-an-index.md) pode ajudar a impedir ou diminuir a fragmentação de páginas de índice. Para exibir informações de fragmentação dos dados e índices de uma tabela ou exibição, você pode usar [DBCC SHOWCONTIG](/sql/t-sql/database-console-commands/dbcc-showcontig-transact-sql).  
  
#### <a name="space-used-in-large-objects"></a>Espaço usado em objetos grandes  

 O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] dá suporte a seis tipos de dados que podem manter grandes cadeias de caracteres com até 2 GB (gigabytes) de comprimento: `nvarchar(max)`, `varchar(max)`, `varbinary(max)`, `ntext`, `text` e `image`. Grandes cadeias de caracteres armazenadas que usam esses tipos de dados são armazenadas em uma série de fragmentos de dados vinculados à linha de dados. As informações de controle de versão de linha estão armazenadas em cada fragmento usado para armazenar grandes cadeias de caracteres. Os fragmentos de dados são uma coleção de páginas dedicadas a objetos grandes em uma tabela.  
  
 Conforme novos valores grandes forem adicionados a um banco de dados, eles serão alocados com o máximo de 8040 bytes de dados por fragmento. Versões anteriores do [!INCLUDE[ssDE](../includes/ssde-md.md)] armazenavam até 8080 bytes de dados `ntext`, `text` ou `image` por fragmento.  
  
 O dados de LOB (Objeto Grande) `ntext`, `text` e `image` existentes não são atualizados para criar espaço para as informações de controle de versão de linha quando um banco de dados é atualizado para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de uma versão anterior do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Porém, a primeira vez em que os dados de LOB são modificados, eles são atualizados dinamicamente para habilitar o armazenamento de informações de controle de versão. Isso acontecerá até mesmo se não forem geradas versões de linha. Depois que os dados de LOB são atualizados, o número máximo de bytes armazenados por fragmento é reduzido de 8080 bytes para 8040 bytes. O processo de atualização é equivalente a excluir o valor LOB e reinserir o mesmo valor. Os dados de LOB são atualizados mesmo quando apenas um byte é modificado. Essa é uma operação única para cada coluna `ntext`, `text` ou `image`, mas cada operação pode gerar uma grande quantidade de alocações de página e atividade de E/S dependendo do tamanho dos dados de LOB. Isso também poderá gerar uma grande quantidade de atividade de registro se a modificação for totalmente registrada. As operações WRITETEXT e UPDATETEXT serão registradas minimamente se o modo de recuperação do banco de dados não for definido como FULL.  
  
 Os tipos de dados `nvarchar(max)`, `varchar(max)` e `varbinary(max)` não estão disponíveis nas versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Portanto, eles não têm nenhum problema de atualização.  
  
 Deve ser alocado espaço em disco suficiente para acomodar esse requisito.  
  
#### <a name="monitoring-row-versioning-and-the-version-store"></a>Monitorando o controle de versão de linha e o armazenamento da versão  

 Para monitorar os processos de controle de versão de linha, armazenamento de versão e isolamento de instantâneo quanto ao desempenho e aos problemas, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornece ferramentas na forma de DMVs (Exibições de Gerenciamento Dinâmico) e contadores de desempenho no Windows System Monitor.  
  
##### <a name="dmvs"></a>DMVs  

 As DMVs a seguir fornecem informações sobre o estado atual do sistema de tempdb e o armazenamento da versão, bem como sobre as transações que usam controle de versão de linha.  
  
 sys.dm_db_file_space_usage. Retorna informações de uso do espaço de cada arquivo no banco de dados. Para obter mais informações, veja [sys.dm_db_file_space_usage &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql).  
  
 sys.dm_db_session_space_usage. Retorna a alocação de páginas e a atividade de desalocação por sessão do banco de dados. Para obter mais informações, veja [sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql).  
  
 sys.dm_db_task_space_usage. Retorna a alocação de páginas e a atividade de desalocação por tarefa do banco de dados. Para obter mais informações, veja [sys.dm_db_task_space_usage &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql).  
  
 sys.dm_tran_top_version_generators. Retorna uma tabela virtual para os objetos que produzem a maioria das versões no repositório de versão. Agrupa os 256 maiores registros agregados por database_id e rowset_id. Use essa função para localizar os maiores usuários do repositório de versão. Para obter mais informações, veja [sys.DM tran_top_version_generators &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-top-version-generators-transact-sql).  
  
 sys.dm_tran_version_store. Retorna uma tabela virtual que exibe todos os registros de versão no repositório de versão comum. Para obter mais informações, veja [sys.dm_tran_version_store &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-version-store-transact-sql).  
  
> [!NOTE]  
>  sys.dm_tran_top_version_generators e sys.dm_tran_version_store são funções cuja execução é potencialmente muito dispendiosa, uma vez que ambas consultam todo o armazenamento de versão, que pode ser muito grande.  
  
 sys.dm_tran_active_snapshot_database_transactions. Retorna uma tabela virtual para todas as transações ativas em todos os bancos de dados dentro da instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que usam controle de versão de linha. As transações de sistema não são exibidas nessa DMV. Para obter mais informações, veja [sys.dm_tran_active_snapshot_database_transactions &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql).  
  
 sys.dm_tran_transactions_snapshot. Retorna uma tabela virtual que exibe instantâneos tirados por cada transação. O instantâneo contém o número de sequência das transações ativas que usam controle de versão de linha. Para obter mais informações, veja [sys.dm_tran_transactions_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-transactions-snapshot-transact-sql).  
  
 sys.dm_tran_current_transaction. Retorna uma única linha que exibe informações de estado relacionadas ao controle de versão de linha da transação na sessão atual. Para obter mais informações, veja [sys.dm_tran_current_transaction &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-current-transaction-transact-sql).  
  
 sys.dm_tran_current_snapshot. Retorna uma tabela virtual que exibe todas as transações ativas no momento em que a transação de isolamento do instantâneo atual é iniciada. Se a transação atual estiver usando um isolamento de instantâneo, essa função não retornará nenhuma linha. sys.dm_tran_current_snapshot é semelhante a sys.dm_tran_transactions_snapshot, exceto pelo fato de que retorna apenas as transações ativas para o instantâneo atual. Para obter mais informações, veja [sys.DM tran_current_snapshot &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-current-snapshot-transact-sql).  
  
##### <a name="performance-counters"></a>Contadores de desempenho  

 Os contadores de desempenho do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornecem informações sobre o desempenho do sistema afetado por processos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Os contadores de desempenho a seguir monitoram tempdb e o armazenamento de versão, bem como transações que usam controle de versão de linha. Os contadores de desempenho estão contidos no objeto de desempenho SQLServer:Transactions.  
  
 **Espaço livre em tempdb (KB)**. Monitora a quantidade, em KB (kilobytes), de espaço livre no banco de dados tempdb. Deve haver espaço livre suficiente em tempdb para processar o repositório de versão que dá suporte ao isolamento de instantâneo.  
  
 A fórmula a seguir fornece uma estimativa aproximada do tamanho do armazenamento de versão. Para transações de longa execução, pode ser útil monitorar a taxa de geração e limpeza para calcular o tamanho máximo de armazenamento de versão.  
  
 [tamanho do repositório de versão comum] = 2 * [dados de repositório de versão gerados por minuto] \* [maior tempo de execução (minutos) da transação]  
  
 O tempo de execução mais longo das transações não deve incluir as compilações de índices online. Como essas operações podem demorar muito tempo em tabelas muito grandes, as compilações de índices online usam um armazenamento de versão separado. O tamanho aproximado do repositório de versão de compilação de índices online é igual à quantidade de dados modificados na tabela, incluindo todos os índices, enquanto a compilação de índices online estiver ativa.  
  
 **Tamanho do Repositório de Versão (KB)**. Monitora o tamanho em KB de todos os armazenamentos de versão. Essas informações ajudam a determinar a quantidade de espaço necessária no banco de dados tempdb para o armazenamento de versão. O monitoramento desse contador durante um determinado tempo fornece uma estimativa útil do espaço adicional necessário para tempdb.  
  
 `Version Generation rate (KB/s)`. Monitora a taxa de geração de versão, em KB por segundo, em todos os repositórios de versão.  
  
 `Version Cleanup rate (KB/s)`. Monitora a taxa de limpeza de versão, em KB por segundo, em todos os repositórios de versão.  
  
> [!NOTE]  
>  As informações da Taxa de Geração de Versão (KB/s) e da Taxa de Limpeza de Versão (KB/s) podem ser usadas para prever os requisitos de espaço de tempdb.  
  
 **Contagem de unidades de repositório de versão**. Monitora a contagem de unidades do repositório de versão.  
  
 **Criação da unidade do repositório de versão**. Monitora o número total de unidades de repositório de versão criadas para armazenar versões de linha depois que a instância tiver sido iniciada.  
  
 **Truncamento de unidade de repositório de versão**. Monitora o número total de unidades de repositório de versão truncadas depois que a instância tiver sido iniciada. Uma unidade de repositório de versão é truncada quando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] determina que nenhuma das linhas de versão armazenadas na unidade de armazenamento de versão é necessária para a execução de transações ativas.  
  
 **Taxa de conflito de atualização**. Monitora a taxa de transação de instantâneo de atualização com conflitos de atualização para o número total de transações de instantâneo de atualização.  
  
 **Tempo de execução da transação mais longa**. Monitora o tempo de execução mais longo em segundos de qualquer transação que usa controle de versão de linha. Pode ser usado para determinar se alguma transação está sendo executada por uma quantidade de tempo excessiva.  
  
 **Transações**. Monitora o número total de transações ativas. Não inclui as transações de sistema.  
  
 `Snapshot Transactions`. Monitora o número total de transações de instantâneo ativas.  
  
 `Update Snapshot Transactions`. Monitora o número total de transações de instantâneo ativas que executam operações de atualização.  
  
 `NonSnapshot Version Transactions`. Monitora o número total de transações de não instantâneo ativas que geram registros de versão.  
  
> [!NOTE]  
>  A soma de Transações de Instantâneo de Atualização e Transações de Versão Não Instantâneo representa o número total de transações que participam da geração de versão. A diferença de Transações de Instantâneo e Transações de Instantâneo de Atualização informa o número de transações de instantâneo somente leitura.  
  
### <a name="row-versioning-based-isolation-level-example"></a>Exemplo de nível de isolamento com base em controle de versão de linha  

 Os exemplos a seguir mostram as diferenças de comportamento entre transações de isolamento de instantâneo e transações de leitura confirmada que usam controle de versão de linha.  
  
#### <a name="a-working-with-snapshot-isolation"></a>A. Trabalhando com isolamento de instantâneo  

 Neste exemplo, uma transação sendo executada sob um isolamento de instantâneo lê dados que são então modificados por outra transação. A transação de instantâneo não bloqueia a operação de atualização executada pela outra transação, e continua lendo dados do controle de versão de linha, ao mesmo tempo em que ignora a modificação de dados. Porém, quando a transação de instantâneo tentar modificar os dados que já foram modificados pela outra transação, a transação de instantâneo gera um erro e é terminada.  
  
 Na sessão 1:  
  
```  
USE AdventureWorks2012;  -- Or the 2008 or 2008R2 version of the AdventureWorks database.  
GO  
  
-- Enable snapshot isolation on the database.  
ALTER DATABASE AdventureWorks2012  
    SET ALLOW_SNAPSHOT_ISOLATION ON;  
GO  
  
-- Start a snapshot transaction  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
GO  
  
BEGIN TRANSACTION;  
    -- This SELECT statement will return  
    -- 48 vacation hours for the employee.  
    SELECT BusinessEntityID, VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
```  
  
 Sessão 2:  
  
```  
USE AdventureWorks2012;  
GO  
  
-- Start a transaction.  
BEGIN TRANSACTION;  
    -- Subtract a vacation day from employee 4.  
    -- Update is not blocked by session 1 since  
    -- under snapshot isolation shared locks are  
    -- not requested.  
    UPDATE HumanResources.Employee  
        SET VacationHours = VacationHours - 8  
        WHERE BusinessEntityID = 4;  
  
    -- Verify that the employee now has 40 vacation hours.  
    SELECT VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
```  
  
 Na sessão 1:  
  
```  
    -- Reissue the SELECT statement - this shows  
    -- the employee having 48 vacation hours.  The  
    -- snapshot transaction is still reading data from  
    -- the versioned row.  
    SELECT BusinessEntityID, VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
```  
  
 Sessão 2:  
  
```  
-- Commit the transaction; this commits the data  
-- modification.  
COMMIT TRANSACTION;  
GO  
```  
  
 Na sessão 1:  
  
```  
    -- Reissue the SELECT statement - this still   
    -- shows the employee having 48 vacation hours  
    -- even after the other transaction has committed  
    -- the data modification.  
    SELECT BusinessEntityID, VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
  
    -- Because the data has been modified outside of the  
    -- snapshot transaction, any further data changes to   
    -- that data by the snapshot transaction will cause   
    -- the snapshot transaction to fail. This statement   
    -- will generate a 3960 error and the transaction will   
    -- terminate.  
    UPDATE HumanResources.Employee  
        SET SickLeaveHours = SickLeaveHours - 8  
        WHERE BusinessEntityID = 4;  
  
-- Undo the changes to the database from session 1.   
-- This will not undo the change from session 2.  
ROLLBACK TRANSACTION  
GO  
```  
  
#### <a name="b-working-with-read-committed-using-row-versioning"></a>B. Trabalhando com leituras confirmadas com o controle de versão de linha  

 Neste exemplo, uma transação de leitura confirmada que usa o controle de versão de linha é executada ao mesmo tempo que outra transação. A transação de leitura confirmada se comporta diferentemente de uma transação de instantâneo. Como uma transação de instantâneo, a transação de leitura confirmada lerá controles de versão de linhas, mesmo após a outra transação ter modificado os dados. Entretanto, diferentemente de uma transação de instantâneo, a transação de leitura confirmada:  
  
-   Lerá os dados modificados depois que a outra transação confirmar as mudanças de dados.  
  
-   Poderá atualizar os dados modificados pela outra transação onde a transação de instantâneo não pôde.  
  
 Na sessão 1:  
  
```  
USE AdventureWorks2012;  -- Or any earlier version of the AdventureWorks database.  
GO  
  
-- Enable READ_COMMITTED_SNAPSHOT on the database.  
-- For this statement to succeed, this session  
-- must be the only connection to the AdventureWorks2012  
-- database.  
ALTER DATABASE AdventureWorks2012  
    SET READ_COMMITTED_SNAPSHOT ON;  
GO  
  
-- Start a read-committed transaction  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;  
GO  
  
BEGIN TRANSACTION;  
    -- This SELECT statement will return  
    -- 48 vacation hours for the employee.  
    SELECT BusinessEntityID, VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
  
```  
  
 Sessão 2:  
  
```  
USE AdventureWorks2012;  
GO  
  
-- Start a transaction.  
BEGIN TRANSACTION;  
    -- Subtract a vacation day from employee 4.  
    -- Update is not blocked by session 1 since  
    -- under read-committed using row versioning shared locks are  
    -- not requested.  
    UPDATE HumanResources.Employee  
        SET VacationHours = VacationHours - 8  
        WHERE BusinessEntityID = 4;  
  
    -- Verify that the employee now has 40 vacation hours.  
    SELECT VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
  
```  
  
 Na sessão 1:  
  
```  
    -- Reissue the SELECT statement - this still shows  
    -- the employee having 48 vacation hours.  The  
    -- read-committed transaction is still reading data   
    -- from the versioned row and the other transaction   
    -- has not committed the data changes yet.  
    SELECT BusinessEntityID, VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
  
```  
  
 Sessão 2:  
  
```  
-- Commit the transaction.  
COMMIT TRANSACTION;  
GO  
  
```  
  
 Na sessão 1:  
  
```  
    -- Reissue the SELECT statement which now shows the   
    -- employee having 40 vacation hours.  Being   
    -- read-committed, this transaction is reading the   
    -- committed data. This is different from snapshot  
    -- isolation which reads from the versioned row.  
    SELECT BusinessEntityID, VacationHours  
        FROM HumanResources.Employee  
        WHERE BusinessEntityID = 4;  
  
    -- This statement, which caused the snapshot transaction   
    -- to fail, will succeed with read-committed using row versioning.  
    UPDATE HumanResources.Employee  
        SET SickLeaveHours = SickLeaveHours - 8  
        WHERE BusinessEntityID = 4;  
  
-- Undo the changes to the database from session 1.   
-- This will not undo the change from session 2.  
ROLLBACK TRANSACTION;  
GO  
```  
  
### <a name="enabling-row-versioning-based-isolation-levels"></a>Habilitando os níveis de isolamento baseados em controle de versão de linha  

 Os administradores de banco de dados controlam as configurações no nível de banco de dados para controle de versão de linha usando as opções de banco de dados READ_COMMITTED_SNAPSHOT e ALLOW_SNAPSHOT_ISOLATION na instrução ALTER DATABASE.  
  
 Quando a opção de banco de dados READ_COMMITTED_SNAPSHOT está definida como ON, são ativados os mecanismos usados para oferece suporte à opção imediatamente. Ao definir a opção READ_COMMITTED_SNAPSHOT, só a conexão que executa o comando ALTER DATABASE é permitida no banco de dados. Não deve haver nenhuma outra conexão aberta no banco de dados até que ALTER DATABASE esteja concluído. O banco de dados não precisa estar no modo do usuário único.  
  
 A seguinte instrução [!INCLUDE[tsql](../includes/tsql-md.md)] habilita READ_COMMITTED_SNAPSHOT:  
  
```  
ALTER DATABASE AdventureWorks2012  
    SET READ_COMMITTED_SNAPSHOT ON;  
```  
  
 Quando a opção banco de dados ALLOW_SNAPSHOT_ISOLATION está definida como ON, a instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] não gera versões de linhas para os dados modificados até que todas as transações ativas que modificaram os dados no banco de dados estejam concluídas. Se houver transações de modificação ativas, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] definirá o estado da opção como PENDING_ON. Depois que todas as modificações de transações estiverem concluídas, o estado da opção é alterado para ON. Os usuários não podem iniciar uma transação de instantâneo nesse banco de dados até que a opção esteja completamente ON. O banco de dados passa por um estado de PENDING_OFF quando o administrador de banco de dados define a opção ALLOW_SNAPSHOT_ISOLATION como OFF.  
  
 A instrução [!INCLUDE[tsql](../includes/tsql-md.md)] a seguir habilitará ALLOW_SNAPSHOT_ISOLATION:  
  
```  
ALTER DATABASE AdventureWorks2012  
    SET ALLOW_SNAPSHOT_ISOLATION ON;  
```  
  
 A tabela a seguir relaciona e descreve os estados da opção ALLOW_SNAPSHOT_ISOLATION. Usar a opção ALTER DATABASE com a opção ALLOW_SNAPSHOT_ISOLATION não bloqueará os usuários que estiverem acessando os dados do banco de dados no momento.  
  
|Estado da estrutura de isolamento de instantâneo para banco de dados atual|Descrição|  
|----------------------------------------------------------------|-----------------|  
|OFF|O suporte para as transações de isolamento de instantâneo não está ativado. Não é permitida nenhuma transação de isolamento de instantâneo.|  
|PENDING_ON|O suporte para as transações de isolamento de instantâneo está em estado de transição (de OFF para ON). As transações abertas precisam ser concluídas.<br /><br /> Não é permitida nenhuma transação de isolamento de instantâneo.|  
|ATIVADO|O suporte para as transações de isolamento de instantâneo está ativado.<br /><br /> São permitidas transações de instantâneo.|  
|PENDING_OFF|O suporte para as transações de isolamento de instantâneo está em estado de transição (de ON para OFF).<br /><br /> As transações de instantâneo iniciadas depois dessa hora não poderão acessar este banco de dados. Atualizar transações ainda paga o custo de controle de versão neste banco de dados. As transações de instantâneo existentes ainda podem acessar este banco de dados sem problemas. O estado PENDING_OFF não se torna OFF até que todas as transações de instantâneo, que estavam ativas quando o estado de isolamento de instantâneo do banco de dados era ON, forem concluídas.|  
  
 Use as exibições do catálogo sys.databases para determinar o estado de ambas as opções do banco de dados de controle de versão de linha.  
  
 Todas as atualizações para tabelas de usuário e algumas tabelas do sistema armazenados no mestre e no msdb geram versões de linha.  
  
 A opção ALLOW_SNAPSHOT_ISOLATION é definida automaticamente como ON nos bancos de dados mestre e msdb e não pode ser desabilitada.  
  
 Os usuários não podem definir a opção READ_COMMITTED_SNAPSHOT como ON no mestre, no tempdb ou no msdb.  
  
### <a name="using-row-versioning-based-isolation-levels"></a>Usando níveis de isolamento com base em controle de versão de linha  

 A estrutura de controle de versão de linha permanece sempre habilitada no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e é usada por vários recursos. Além de fornecer níveis de isolamento com base em controle de versão de linha, ela é usada para oferecer suporte a modificações feitas em gatilhos e em sessões MARS (Multiple Active Result Sets), e para oferecer suporte à leitura de dados de operações de índice ONLINE.  
  
 Os níveis de isolamento com base em controle de versão de linha são habilitados no banco de dados. Todos os aplicativos que acessam os objetos de bancos de dados habilitados podem executar consultas usando os seguintes níveis de isolamento:  
  
-   Leitura confirmada que usa controle de versão de linha pela definição da opção de banco de dados `READ_COMMITTED_SNAPSHOT` como `ON`, como mostrado no seguinte exemplo de código:  
  
    ```  
    ALTER DATABASE AdventureWorks2012  
        SET READ_COMMITTED_SNAPSHOT ON;  
    ```  
  
     Quando o banco de dados está habilitado para READ_COMMITTED_SNAPSHOT, todas as consultas no nível de isolamento confirmado para leitura usam controle de versão de linha, o que significa que as operações de leitura não bloqueiam as operações de atualização.  
  
-   Isolamento do instantâneo através da definição da opção de banco de dados `ALLOW_SNAPSHOT_ISOLATION` como `ON`, como mostrado no exemplo de código seguinte:  
  
    ```  
    ALTER DATABASE AdventureWorks2012  
        SET ALLOW_SNAPSHOT_ISOLATION ON;  
    ```  
  
     Uma transação executada em isolamento de instantâneo pode acessar tabelas do banco de dados habilitadas para instantâneo. Para acessar tabelas que não foram habilitadas para instantâneo, é preciso alterar o nível de isolamento. Por exemplo, o exemplo de código a seguir mostra uma instrução `SELECT` que une duas tabelas durante a execução de uma transação de instantâneo. Uma das tabelas pertence a um banco de dados no qual o isolamento de instantâneo não está habilitado. Quando a instrução `SELECT` for executada no isolamento de instantâneo, não será executada com êxito.  
  
    ```  
    SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
    BEGIN TRAN  
        SELECT t1.col5, t2.col5  
            FROM Table1 as t1  
            INNER JOIN SecondDB.dbo.Table2 as t2  
                ON t1.col1 = t2.col2;  
    ```  
  
     O exemplo de código a seguir mostra a mesma instrução `SELECT` que foi modificada para alterar o nível de isolamento da transação para leitura confirmada. Em razão dessa mudança, a instrução `SELECT` será executada com êxito.  
  
    ```  
    SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
    BEGIN TRAN  
        SELECT t1.col5, t2.col5  
            FROM Table1 as t1  
            WITH (READCOMMITTED)  
            INNER JOIN SecondDB.dbo.Table2 as t2  
                ON t1.col1 = t2.col2;  
    ```  
  
#### <a name="limitations-of-transactions-using-row-versioning-based-isolation-levels"></a>Limitações de transações usando níveis de isolamento com base em controle de versão de linha  

 Considere as limitações a seguir ao trabalhar com níveis de isolamento baseados em controle de versão de linha:  
  
-   READ_COMMITTED_SNAPSHOT não pode ser habilitada em tempdb, msdb, nem em master.  
  
-   As tabelas temporárias globais são armazenadas em tempdb. Ao acessar tabelas temporárias globais em uma transação de instantâneo, uma das seguintes ações deve ocorrer:  
  
    -   Defina a opção de banco de dados ALLOW_SNAPSHOT_ISOLATION como ON em tempdb.  
  
    -   Use uma dica de isolamento para alterar o nível de isolamento da instrução.  
  
-   Transações de instantâneo falham quando:  
  
    -   O banco de dados é transformado em somente leitura após o início da transação de instantâneo, mas antes que a transação de instantâneo acesse o banco de dados.  
  
    -   Se objetos forem acessados em vários bancos de dados, um estado de banco de dados terá sido alterado de tal modo que a recuperação do banco de dados ocorrerá após o início da transação de instantâneo, mas antes que a transação de instantâneo acesse o banco de dados. Por exemplo: o banco de dados foi definido como OFFLINE e depois como ONLINE; o banco de dados fecha automaticamente e se abre ou o banco de dados é desanexado e anexado.  
  
-   Não há suporte para transações distribuídas, inclusive consultas em bancos de dados particionados distribuídos em isolamento de instantâneo.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não mantém versões múltiplas de metadados de sistema. As instruções DDL (Linguagem de Definição de Dados) em tabelas e em outros objetos de banco de dados (índices, exibições, tipos de dados, procedimentos armazenados e funções CLR (Common Language Runtime)) alteram metadados. Se uma instrução DDL modificar um objeto, qualquer referência simultânea ao objeto em isolamento de instantâneo fará com que a transação de instantâneo falhe. Transações de leitura confirmada não têm essa limitação quando a opção de banco de dados READ_COMMITTED_SNAPSHOT é ON.  
  
     Por exemplo, um administrador de banco de dados executa a instrução `ALTER INDEX` a seguir.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER INDEX AK_Employee_LoginID  
        ON HumanResources.Employee REBUILD;  
    GO  
    ```  
  
     Qualquer transação de instantâneo que esteja ativa quando a instrução `ALTER INDEX` for executada receberá um erro, caso ela tente fazer referência à tabela `HumanResources.Employee` após a execução da instrução `ALTER INDEX`. As transações de leitura confirmada que usam controle de versão de linha não são afetadas.  
  
    > [!NOTE]  
    >  As operações BULK INSERT podem causar alterações a metadados da tabela de destino (por exemplo, ao desabilitar verificações de restrição). Quando isso ocorre, as transações de isolamento de instantâneo simultâneas que acessam tabelas inseridas em massa falham.  
  
 ![Ícone de seta usado com o link voltar ao início](media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [neste guia](#Top)  
  
## <a name="customizing-locking-and-row-versioning"></a>Personalizando bloqueio e controle de versão de linha  
  
### <a name="customizing-the-lock-time-out"></a>Personalizando tempo limite de bloqueio  

 Quando uma instância do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] não pode conceder um bloqueio a uma transação porque outra transação já possui um bloqueio conflitante no recurso, a primeira transação se torna bloqueada aguardando a liberação do bloqueio existente. Por padrão, não existe período obrigatório de tempo limite e nenhuma forma para testar se um recurso está bloqueado antes de bloqueá-lo, exceto a tentativa de acessar os dados (e potencialmente ser bloqueado indefinidamente).  
  
> [!NOTE]  
>  No [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], use a exibição de gerenciamento dinâmico **sys.dm_os_waiting_tasks** para determinar se um processo está sendo bloqueado e quem o está bloqueando. Em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], use o procedimento armazenado do sistema **sp_who**.  
  
 A configuração LOCK_TIMEOUT permite que um aplicativo defina um tempo máximo que uma instrução espera um recurso bloqueado. Quando uma instrução espera por mais tempo do que a configuração LOCK_TIMEOUT, a instrução bloqueada é cancelada automaticamente e a mensagem de erro 1222 (`Lock request time-out period exceeded`) é retornada ao aplicativo. Porém, qualquer transação que contém a instrução não é revertida ou cancelada pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Portanto, o aplicativo deve ter um identificador de erro que possa interceptar a mensagem de erro 1222. Se um aplicativo não interceptar o erro, o aplicativo poderá continuar sem reconhecer que uma instrução individual dentro de uma transação foi cancelada, e poderão ocorrer erros porque as instruções posteriores da transação podem depender da instrução que nunca foi executada.  
  
 A implementação de um identificador de erro que intercepte a mensagem de erro 1222 permite que um aplicativo possa lidar com a situação de tempo limite e execute uma ação para corrigir a situação, como: automaticamente enviar novamente a instrução que estava bloqueada ou reverter toda a transação.  
  
 Para determinar a configuração atual de LOCK_TIMEOUT, execute a @LOCK_TIMEOUT função @:  
  
```  
SELECT @@lock_timeout;  
GO  
```  
  
### <a name="customizing-transaction-isolation-level"></a>Personalizando o nível de isolamento da transação  

 READ COMMITTED é o nível de isolamento padrão para o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] . Se um aplicativo precisar operar em um nível de isolamento diferente, poderá usar os seguintes métodos para definir o nível de isolamento:  
  
-   Executar a instrução [SET TRANSACTION ISOLATION LEVEL](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql).  
  
-   Aplicativos ADO.NET que usam o SqlClient namespace gerenciado podem especificar uma opção *IsolationLevel* usando o método SqlConnection.BeginTransaction.  
  
-   Aplicativos que usam ADO podem definir a propriedade `Autocommit Isolation Levels`.  
  
-   Ao iniciar uma transação, os aplicativos que usam OLE DB podem chamar ITransactionLocal::StartTransaction com *isoLevel* definido como o nível desejado de isolamento da transação. Ao especificar o nível de isolamento em modo de confirmação automática, os aplicativos que usam OLE DB podem definir a propriedade DBPROPSET_SESSION DBPROP_SESS_AUTOCOMMITISOLEVELS como o nível desejado de isolamento da transação.  
  
-   Aplicativos que usam ODBC podem definir o atributo SQL_COPT_SS_TXN_ISOLATION usando SQLSetConnectAttr.  
  
 Quando o nível de isolamento é especificado, o comportamento de bloqueio de todas as consultas e instruções de DML (linguagem de manipulação de dados) na sessão [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] opera nesse nível de isolamento. O nível de isolamento permanece em vigor até o término da sessão ou até que o nível de isolamento seja definido como outro nível.  
  
 O exemplo seguinte define o nível de isolamento `SERIALIZABLE`:  
  
```  
USE AdventureWorks2012;  
GO  
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;  
GO  
BEGIN TRANSACTION;  
SELECT BusinessEntityID  
    FROM HumanResources.Employee;  
GO  
```  
  
 O nível de isolamento pode ser substituído por uma consulta individual ou instruções DML, se necessário, especificando uma dica no nível de tabela. A especificação de uma dica no nível de tabela não afeta outras instruções na sessão. Recomendamos que as dicas no nível de tabela sejam usadas para alterar o comportamento padrão apenas quando absolutamente necessário.  
  
 O [!INCLUDE[ssDE](../includes/ssde-md.md)] talvez tenha que adquirir bloqueios ao ler metadados mesmo quando o nível de isolamento é definido como um nível em que os bloqueios de compartilhamento não são solicitados durante a leitura de dados. Por exemplo, uma transação em execução no nível de isolamento de leitura não confirmada não adquire bloqueios de compartilhamento ao ler dados, mas pode solicitar bloqueios ao ler uma exibição de catálogo do sistema. Isso significa que é possível que uma transação de leitura não confirmada cause o bloqueio ao consultar uma tabela quando uma transação simultânea estiver modificando os metadados dessa tabela.  
  
 Para determinar o nível de isolamento da transação definido atualmente, use a instrução `DBCC USEROPTIONS`, como mostrado no exemplo a seguir. O conjunto de resultados pode ser diferente do conjunto de resultados em seu sistema.  
  
```  
USE AdventureWorks2012;  
GO  
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;  
GO  
DBCC USEROPTIONS;  
GO  
```  
  
 [!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
 `Set Option                   Value`  
  
 `---------------------------- -------------------------------------------`  
  
 `textsize                     2147483647`  
  
 `language                     us_english`  
  
 `dateformat                   mdy`  
  
 `datefirst                    7`  
  
 `...                          ...`  
  
 `Isolation level              repeatable read`  
  
 ``  
  
 `(14 row(s) affected)`  
  
 ``  
  
 `DBCC execution completed. If DBCC printed error messages, contact your system administrator.`  
  
### <a name="locking-hints"></a>Dicas de bloqueio  

 Dicas de bloqueio podem ser especificadas para referências de tabela individuais nas instruções SELECT, INSERT, UPDATE e DELETE. As dicas especificam o tipo de bloqueio ou controle de versão de linha da instância que o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] usa para dados de tabela. Dicas de bloqueio de tabelas podem ser usadas quando é necessário um controle mais refinado dos tipos de bloqueios adquiridos em um objeto. Essas dicas de bloqueio substituem o nível de isolamento da transação atual na sessão.  
  
 Para obter mais informações sobre as dicas de bloqueio específicas e seus comportamentos, veja [Dicas de tabela&#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-table).  
  
> [!NOTE]  
>  O otimizador de consulta [!INCLUDE[ssDE](../includes/ssde-md.md)] quase sempre escolhe o nível de bloqueio correto. É recomendável que as dicas de bloqueio no nível de tabela sejam usadas para alterar o comportamento de bloqueio padrão apenas quando necessário. Não permitir um nível de bloqueio pode afetar adversamente a simultaneidade.  
  
 O [!INCLUDE[ssDE](../includes/ssde-md.md)] talvez tenha que adquirir bloqueios ao ler metadados, mesmo quando está processando uma seleção com uma dica de bloqueio, que impede solicitações para bloqueios de compartilhamento durante a leitura de dados. Por exemplo, SELECT usando a dica NOLOCK não adquire bloqueios de compartilhamento ao ler dados, mas pode solicitar bloqueios ao ler uma exibição de catálogo do sistema. Isso significa que é possível uma instrução SELECT usando NOLOCK ser bloqueada.  
  
 Como é mostrado no exemplo a seguir, se o nível de isolamento da transação for configurado para `SERIALIZABLE`, e a dica de bloqueio em nível de tabela `NOLOCK` for usada com a instrução `SELECT`, bloqueios de intervalo de chaves usados para manter transações serializáveis não são aceitos.  
  
```  
USE AdventureWorks2012;  
GO  
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;  
GO  
BEGIN TRANSACTION;  
GO  
SELECT JobTitle  
    FROM HumanResources.Employee WITH (NOLOCK);  
GO  
  
-- Get information about the locks held by   
-- the transaction.  
SELECT    
        resource_type,   
        resource_subtype,   
        request_mode  
    FROM sys.dm_tran_locks  
    WHERE request_session_id = @@spid;  
  
-- End the transaction.  
ROLLBACK;  
GO  
```  
  
 O único bloqueio aceito que referencia `HumanResources.Employee` é um bloqueio de estabilidade (Sch-S) de esquema. Nesse caso, a seriabilidade não é mais garantida.  
  
 No [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)], a opção LOCK_ESCALATION de ALTER TABLE pode não favorecer bloqueios de tabela e ativar bloqueios HoBT em tabelas particionadas. Essa opção não é uma dica de bloqueio, mas pode ser usada para reduzir o escalonamento do bloqueio. Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
###  <a name="customizing-locking-for-an-index"></a><a name="Customize"></a> Personalizando bloqueio de um índice  

 O [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] usa uma estratégia de bloqueio dinâmico que escolhe automaticamente a melhor granularidade de bloqueio para as consultas, na maioria dos casos. É recomendável substituir os níveis de bloqueio padrão que têm bloqueio de página e de linha ativado, a não ser que os padrões de acesso a tabela e ao índice sejam bem compreendidos e consistentes e haja um problema de contenção de recursos a ser resolvida. Substituir um nível de bloqueio pode impedir significativamente o acesso simultâneo a uma tabela ou índice. Por exemplo, a especificação de apenas bloqueios em nível de tabela em uma tabela grande que os usuários acessam excessivamente pode provocar gargalos, porque os usuários precisam esperar que o bloqueio em nível de tabela seja liberado para acessar a tabela.  
  
 Há alguns casos em que a desabilitação do bloqueio de página ou de linha poderá ser benéfico, se os padrões de acesso forem bem-entendidos e consistentes. Por exemplo, um aplicativo de banco de dados usa uma tabela de pesquisa que é atualizada semanalmente em um processo em lotes. Leitores simultâneos acessam a tabela com um bloqueio compartilhado (S) e a atualização em lotes semanal acessa a tabela com um bloqueio exclusivo (X). A desativação do bloqueio de página e de linha na tabela reduz a sobrecarga do bloqueio durante a semana permitindo que os leitores acessem a tabela simultaneamente por meio de bloqueios de tabelas compartilhado. Quando o trabalho em lotes é executado, ele pode concluir a atualização de maneira eficiente porque obtém um bloqueio de tabela exclusivo.  
  
 A desativação do bloqueio de página e de linha pode ou não ser aceitável porque a atualização semanal em lotes bloqueia o acesso dos leitores simultâneos à tabela enquanto a atualização está em execução. Se o trabalho em lotes só alterar algumas linhas ou páginas, você poderá alterar o nível de bloqueio para permitir bloqueio em nível de linha ou de página, o que permite que outras seções leiam a tabela sem bloqueio. Se o trabalho em lotes tiver um grande número de atualizações, obter um bloqueio exclusivo na tabela poderá ser a melhor maneira de garantir que o trabalho em lotes seja concluído de maneira eficiente.  
  
 Ocasionalmente um deadlock ocorre quando duas operações concorrentes adquirirem bloqueios de linha na mesma tabela e então bloqueiam a página porque ambas precisam bloquear a página. A desabilitação de bloqueios de linha força uma operação a esperar, evitando o deadlock.  
  
 A granularidade de bloqueio usada em um índice pode ser definida usando as instruções CREATE INDEX e ALTER INDEX. As configurações de bloqueio se aplicam a páginas de índice e a páginas de tabela. Além disso, podem ser usadas as instruções CREATE TABLE e ALTER TABLE para definir a granularidade de bloqueio nas restrições PRIMARY KEY e UNIQUE. Para compatibilidade com versões anteriores, o procedimento armazenado do sistema **sp_indexoption** também pode definir a granularidade. Para exibir a opção atual de bloqueio para um determinado índice, use a função INDEXPROPERTY. Podem não ser permitidos bloqueios no nível de página, no nível de linha ou uma combinação de bloqueios no nível de página e no nível de linha, para um determinado índice.  
  
|Bloqueios não permitidos|Índice acessado por|  
|----------------------|-----------------------|  
|Nível de página|Bloqueios no nível de linha e no nível de tabela|  
|Nível de linha|Bloqueios no nível de página e no nível de tabela|  
|Nível de página e nível de linha|Bloqueio no nível de tabela|  
  
 ![Ícone de seta usado com o link voltar ao início](media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [neste guia](#Top)  
  
##  <a name="advanced-transaction-information"></a><a name="Advanced"></a> Informações sobre transações avançadas  
  
### <a name="nesting-transactions"></a>Aninhando transações  

 Transações explícitas podem ser aninhadas. Isso serve basicamente para dar suporte a transações em procedimentos armazenados que possam ser chamados de um processo já presente em uma transação ou de processos que não tenham nenhuma transação ativa.  
  
 O exemplo a seguir mostra o uso planejado de transações aninhadas. O procedimento `TransProc` obriga sua transação independentemente do modo de transação de qualquer processo que o execute. Se `TransProc` for chamado quando uma transação estiver ativa, a transação aninhada em `TransProc` será amplamente ignorada e suas instruções INSERT serão confirmadas ou revertidas com base na ação final tomada para a transação externa. Se `TransProc` for executado por um processo que não tenha uma transação pendente, o COMMIT TRANSACTION ao término do procedimento confirmará efetivamente as instruções INSERT.  
  
```  
SET QUOTED_IDENTIFIER OFF;  
GO  
SET NOCOUNT OFF;  
GO  
CREATE TABLE TestTrans(Cola INT PRIMARY KEY,  
               Colb CHAR(3) NOT NULL);  
GO  
CREATE PROCEDURE TransProc @PriKey INT, @CharCol CHAR(3) AS  
BEGIN TRANSACTION InProc  
INSERT INTO TestTrans VALUES (@PriKey, @CharCol)  
INSERT INTO TestTrans VALUES (@PriKey + 1, @CharCol)  
COMMIT TRANSACTION InProc;  
GO  
/* Start a transaction and execute TransProc. */  
BEGIN TRANSACTION OutOfProc;  
GO  
EXEC TransProc 1, 'aaa';  
GO  
/* Roll back the outer transaction, this will  
   roll back TransProc's nested transaction. */  
ROLLBACK TRANSACTION OutOfProc;  
GO  
EXECUTE TransProc 3,'bbb';  
GO  
/* The following SELECT statement shows only rows 3 and 4 are   
   still in the table. This indicates that the commit  
   of the inner transaction from the first EXECUTE statement of  
   TransProc was overridden by the subsequent rollback. */  
SELECT * FROM TestTrans;  
GO  
```  
  
 A confirmação de transações internas é ignorada pelo [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]. A transação é confirmada ou revertida com base na ação tomada no término da transação mais externa. Se a transação externa for confirmada, as transações aninhadas internas também serão confirmadas. Se a transação externa for revertida, então todas as transações internas também serão revertidas, sem considerar se as transações internas estavam individualmente confirmadas ou não.  
  
 Cada chamada para COMMIT TRANSACTION ou COMMIT WORK se aplica a última BEGIN TRANSACTION executada. Se as instruções de BEGIN TRANSACTION forem aninhadas, então uma instrução COMMIT só se aplicará à última transação aninhada que é a transação interna. Mesmo que uma instrução COMMIT TRANSACTION *transaction_name* em uma transação aninhada se refere ao nome da transação externa, a confirmação se aplica somente à transação mais interna.  
  
 Não é válido para o parâmetro *transaction_name* de uma instrução ROLLBACK TRANSACTION para se referir às transações internas de um conjunto de transações aninhadas nomeadas. *transaction_name* pode se referir apenas ao nome da transação mais externa. Se uma instrução de ROLLBACK TRANSACTION *transaction_name* que usa o nome da transação externa for executada em qualquer nível de um conjunto de transações aninhadas, todas as transações aninhadas serão revertidas. Se uma instrução ROLLBACK WORK ou ROLLBACK TRANSACTION sem um parâmetro *transaction_name* for executada em qualquer nível de um conjunto de transações aninhadas, ela reverterá todas as transações aninhadas, incluindo a transação externa.  
  
 A @TRANCOUNT função @ registra o nível de aninhamento da transação atual. Cada instrução de BEGIN TRANSACTION incrementa @ @TRANCOUNT por um. Cada instrução COMMIT transação ou confirmar trabalho diminui @ @TRANCOUNT por um. Um trabalho de reversão ou uma instrução ROLLBACK TRANSACTION que não tem um nome de transação reverte todas as transações aninhadas e decrementa @ @TRANCOUNT para 0. Uma transação de reversão que usa o nome da transação da transação mais externa em um conjunto de transações aninhadas reverte todas as transações aninhadas e decrementa @ @TRANCOUNT para 0. Quando você não tiver certeza se já está em uma transação, selecione @ @TRANCOUNT para determinar se ela é 1 ou mais. Se @ @TRANCOUNT for 0, você não estará em uma transação.  
  
### <a name="using-bound-sessions"></a>Usando sessões associadas  

 As sessões associadas facilitam a coordenação de ações em várias sessões no mesmo servidor. As sessões associadas permitem que duas ou mais sessões compartilhem a mesma transação e bloqueios e trabalhem nos mesmos dados sem conflitos de bloqueio. Essas seções podem ser criadas a partir de várias sessões dentro do mesmo aplicativo ou de vários aplicativos com sessões separadas.  
  
 Para participar de uma sessão associada, uma sessão chama **sp_getbindtoken** ou **srv_getbindtoken** (por meio de serviços de dados abertos) para obter um token de associação. Um token de ligação é uma cadeia de caracteres que identifica exclusivamente cada transação associada. O token de ligação é enviado às outras sessões a serem associadas à sessão atual. As outras sessões associam a transação chamando **sp_bindsession**, usando o token de associação recebido da primeira sessão.  
  
> [!NOTE]  
>  Uma sessão deve ter uma transação de usuário ativa para que **sp_getbindtoken** ou **srv_getbindtoken** seja realizada com sucesso.  
  
 Os tokens de ligação devem ser transmitidos a partir do código do aplicativo que faz a primeira sessão para o código de aplicativo que associa subsequentemente suas sessões à primeira sessão. Não há nenhuma instrução [!INCLUDE[tsql](../includes/tsql-md.md)] ou função de API que um aplicativo pode usar para obter o token de ligação para uma transação iniciada por outro processo. Alguns dos métodos que podem ser usados para transmitir um token de ligação incluem o seguinte:  
  
-   Se todas as sessões forem iniciadas do mesmo processo de aplicativo, os tokens de ligação poderão ser armazenados na memória global ou passados em funções como um parâmetro.  
  
-   Se as sessões forem feitas a partir de processos de aplicativo separados, os tokens de ligação poderão ser transmitidos usando a comunicação entre processos (IPC), como uma chamada de procedimento remoto (RPC) ou troca dinâmica de dados (DDE).  
  
-   Os tokens de ligação podem ser armazenados em uma tabela em uma instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] que possa ser lida pelos processos que desejam se associar à primeira sessão.  
  
 Somente uma sessão em um conjunto de sessões associadas pode estar ativa a qualquer momento. Se uma sessão estiver executando uma instrução na instância ou tiver resultados pendentes da instância, nenhuma outra sessão associada a ela poderá acessar a instância até que a sessão atual termine o processamento ou cancele a instrução atual. Se a instância estiver ocupada processando uma instrução de outras sessões associadas, ocorrerá um erro indicando que o espaço de transação está em uso e a sessão deverá tentar novamente posteriormente.  
  
 Quando você associa as sessões, cada sessão retém sua configuração de nível de isolamento. O uso de SET TRANSACTION ISOLATION LEVEL para alterar a configuração de nível de isolamento de uma sessão não afeta a configuração de nenhuma outra sessão associada a ela.  
  
#### <a name="types-of-bound-sessions"></a>Tipos de sessões associadas  

 Os dois tipos de sessões associadas são local e distribuído.  
  
-   Sessão associada local  
  
     Permite que as sessões associadas compartilhem o espaço de transação de uma única transação em uma instância única do [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
-   Sessão associada distribuída  
  
     Permite que as sessões associadas compartilhem a mesma transação em duas ou mais instâncias até que toda a transação seja confirmada ou revertida usando o MS DTC (Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../includes/msconame-md.md)]).  
  
 As sessões associadas distribuídas não são identificadas por um token de ligação de cadeia de caracteres; elas são identificadas por meio de números de identificação da transação distribuída. Se uma sessão associada estiver envolvida em uma transação local e executar uma RPC em um servidor remoto com SET REMOTE_PROC_TRANSACTIONS ON, a transação associada local será promovida automaticamente a uma transação associada distribuída por MS DTC e uma sessão MS DTC será iniciada.  
  
#### <a name="when-to-use-bound-sessions"></a>Quando usar sessões associadas  

 Nas versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], as sessões associadas eram usadas principalmente no desenvolvimento de procedimentos armazenados estendidos que precisavam executar instruções [!INCLUDE[tsql](../includes/tsql-md.md)] a favor do processo que as chamava. A passagem do processo de chamada por um token de ligação como um parâmetro do procedimento armazenado estendido permite que o procedimento seja associado ao espaço de transação do processo de chamada, integrando o procedimento armazenado estendido ao processo de chamada.  
  
 No [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)], os procedimentos armazenados gravados que usam CLR são mais seguros, evolutivos e estáveis que os procedimentos armazenados estendidos. Os procedimentos armazenados em CLR usam o objeto **SqlContext** para ingressar no contexto da sessão de chamada, não **sp_bindsession**.  
  
 As sessões associadas podem ser usadas para desenvolver aplicativos de três camadas nos quais a lógica empresarial está incorporada em programas separados que trabalham cooperativamente em uma única transação empresarial. Esses programas devem ser codificados para coordenar seu acesso cuidadosamente a um banco de dados. Como as duas sessões compartilham os mesmos bloqueios, os dois programas não devem tentar modificar os mesmos dados ao mesmo tempo. Em qualquer point-in-time, apenas uma sessão pode trabalhar como parte da transação; não pode haver execução paralela. A transação pode ser alternada apenas entre sessões em pontos bem definidos, como quando todas as instruções DML forem concluídas e seus resultados forem recuperados.  
  
### <a name="coding-efficient-transactions"></a>Codificando transações eficientes  

 É importante manter as transações tão curtas quanto possível. Quando uma transação é iniciada, um DBMS (Sistema de administração de banco de dados), deve manter muitos recursos, até o término da transação, para proteger as propriedades (ACID) de atomicidade, consistência, isolamento e durabilidade da transação. Se os dados forem modificados, as linhas modificadas devem ser protegidas com bloqueios exclusivos que evitem a leitura das linhas por qualquer outra transação, e os bloqueios exclusivos devem ser mantidos até que a transação seja confirmada ou revertida. Dependendo das configurações de nível de isolamento da transação, as instruções SELECT podem obter bloqueios que devem ser mantidos até que a transação esteja confirmada ou revertida. Especialmente em sistemas com muitos usuários, as transações devem ser mantidas tão curtas quanto possível para reduzir a contenção de bloqueios de recursos em conexões simultâneas. Transações longas e ineficazes podem não causar problemas com um número pequeno de usuários, mas são intoleráveis em um sistema com milhares de usuários. Começando com o [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], há compatibilidade com transações duráveis atrasadas. As transações duráveis atrasadas não garantem a durabilidade. Consulte o tópico [Durabilidade da Transação](../relational-databases/logs/control-transaction-durability.md) para obter mais informações.  
  
#### <a name="coding-guidelines"></a>Codificando diretrizes  

 Estas são diretrizes para codificar transações eficazes:  
  
-   Não solicite entradas de usuários durante a transação.  
  
     Obtenha todas as entradas necessárias da parte dos usuários antes do início de uma transação. Sendo necessária uma entrada adicional de usuário durante uma transação, reverta a transação atual e reinicie a transação depois que a entrada do usuário for fornecida. Mesmo que os usuários respondam imediatamente, a reação humana é muito mais lenta que a velocidade do computador. Todos os recursos mantidos pela transação são retidos por um tempo extremamente longo, criando potencial para causar problemas de bloqueio. Se os usuários não responderem, a transação permanecerá ativa, bloqueando recursos críticos até que eles respondam, o que pode não acontecer por vários minutos ou até mesmo horas.  
  
-   Não abra uma transação enquanto estiver navegando pelos dados, se possível.  
  
     As transações não devem ser iniciadas até que toda a análise preliminar de dados tenha terminado.  
  
-   Mantenha a transação tão curta quanto possível.  
  
     Depois de saber quais são as modificações que precisam ser feitas, inicie uma transação, execute as instruções de modificação e, em seguida, confirme ou reverta imediatamente. Só abra a transação quando for necessário.  
  
-   Para reduzir o bloqueio, considere usar um nível de isolamento de linha baseado em controle de versão de linha para consultas somente leitura.  
  
-   Utilize bem os níveis de isolamento de transação inferiores.  
  
     Muitos aplicativos podem ser prontamente codificados para usar um nível de isolamento de transação de leitura confirmada. Nem todas as transações requerem nível de isolamento de transação serializável.  
  
-   Utilize bem as opções inferiores de simultaneidade de cursor, como opções de simultaneidade otimista.  
  
     Em um sistema com pouca probabilidade de atualizações simultâneas, a sobrecarga de lidar com um erro ocasional quando "alguém altera seus dados depois que você os leu" pode ser muito inferior à sobrecarga de sempre bloquear linhas à medida que são lidas.  
  
-   Acesse a menor quantidade de dados possível enquanto estiver em uma transação.  
  
     Isso reduz o número de linhas bloqueadas, reduzindo, portanto, a contenção entre transações.  
  
#### <a name="avoiding-concurrency-and-resource-problems"></a>Evitando problemas de simultaneidade e de recurso  

 Para impedir problemas de simultaneidade e de recurso, gerencie cuidadosamente as transações implícitas. Ao usar transações implícitas, a próxima instrução do [!INCLUDE[tsql](../includes/tsql-md.md)] após COMMIT ou ROLLBACK iniciará automaticamente uma nova transação. Isso pode fazer com que uma nova transação seja aberta enquanto o aplicativo navega pelos dados, ou até mesmo quando solicita entradas da parte do usuário. Depois de completar a última transação necessária à proteção contra modificações de dados, desative as transações implícitas até que a transação seja novamente necessária para proteger as modificações de dados. Esse processo deixa o [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] usar o modo autocommit enquanto o aplicativo navega pelos dados e obtém entradas do usuário.  
  
 Além disso, quando o nível de isolamento do instantâneo estiver habilitado, embora uma nova transação não vá reter bloqueios, uma transação de execução longa impedirá a remoção de versões antigas de `tempdb`.  
  
### <a name="managing-long-running-transactions"></a>Gerenciando transações demoradas  

 Uma *transação de execução longa* é uma transação ativa que não foi confirmada nem revertida em tempo hábil. Por exemplo, se o início e o término de uma transação forem controlados pelo usuário, uma causa típica de uma transação de longa execução será um usuário iniciar uma transação e sair enquanto a transação espera por uma resposta dele.  
  
 Uma transação de execução longa pode causar sérios problemas para um banco de dados, como:  
  
-   Se uma instância de servidor for desligada depois que uma transação ativa tiver realizado muitas modificações não confirmadas, a fase de recuperação da reinicialização subsequente poderá demorar muito mais do que o tempo especificado pela opção de configuração de servidor de **intervalo de recuperação** ou pelo ALTER DATABASE... Defina TARGET_RECOVERY_TIME opção. Essas opções controlam a frequência de pontos de verificação ativos e indiretos, respectivamente. Para obter mais informações sobre os tipos de pontos de verificação, veja [Pontos de verificação de bancos de dados &#40;SQL Server&#41;](../relational-databases/logs/database-checkpoints-sql-server.md).  
  
-   É importante ressaltar que, embora uma transação em espera possa gerar um log muito pequeno, ela reterá o truncamento de log indefinidamente, fazendo com que o log da transação aumente bastante e seja completamente preenchido. Se o log da transação for completamente preenchido, o banco de dados não fará mais atualizações. Para obter mais informações, consulte [solucionar problemas de um log de transações completo &#40;SQL Server erro 9002&#41;](../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)e [o Log de transações &#40;](../relational-databases/logs/the-transaction-log-sql-server.md)SQL Server&#41;.  
  
#### <a name="discovering-long-running-transactions"></a>Descobrindo transações demoradas  

 Para procurar transações demoradas, use um dos seguintes:  
  
-   **sys.dm_tran_database_transactions**  
  
     Essa exibição de gerenciamento dinâmico retorna informações sobre as transações no banco de dados. Para uma transação de longa execução, as colunas de interesse específico incluem a hora do primeiro registro de log (**database_transaction_begin_time**), o estado atual da transação (**database_transaction_state**) e o LSN (número de sequência de log) do registro de início no log de transações (**database_transaction_begin_lsn**).  
  
     Para obter mais informações, consulte [sys.DM tran_database_transactions &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql).  
  
-   DBCC OPENTRAN  
  
     Essa instrução permite identificar a ID do proprietário da transação, de modo que seja possível localizar potencialmente a origem da transação para um término mais ordenado (confirmar, em vez de revertê-la). Para obter mais informações, consulte [DBCC OPENTRAN &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-opentran-transact-sql).  
  
#### <a name="stopping-a-transaction"></a>Parando uma transação  

 Talvez seja necessário usar a instrução KILL. Use essa instrução com muito cuidado, porém, especialmente quando houver processos importantes em processamento. Para obter mais informações, consulte [KILL &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/kill-transact-sql).  
  
 ![Ícone de seta usado com o link voltar ao início](media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [neste guia](#Top)  
  
## <a name="see-also"></a>Consulte Também  

 [Isolamento de transação com base no controle de versão de linha SQL Server 2005](https://msdn.microsoft.com/library/ms345124(v=sql.90).aspx)   
 [Sobrecarga de controle de versão de linha](https://blogs.msdn.com/b/sqlserverstorageengine/archive/2008/03/30/overhead-of-row-versioning.aspx)   
 [Como criar uma transação autônoma no SQL Server 2008](https://blogs.msdn.com/b/sqlprogrammability/archive/2008/08/22/how-to-create-an-autonomous-transaction-in-sql-server-2008.aspx)  
  
  

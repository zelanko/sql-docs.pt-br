---
title: 'Início Rápido: Eventos estendidos no SQL Server | Microsoft Docs'
ms.custom: ''
ms.date: 05/28/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xevents
ms.topic: quickstart
ms.assetid: 7bb78b25-3433-4edb-a2ec-c8b2fa58dea1
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4bad2f6cf7f36141b4f5a1d42f648c1631175d36
ms.sourcegitcommit: c426c7ef99ffaa9e91a93ef653cd6bf3bfd42132
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/10/2019
ms.locfileid: "72251538"
---
# <a name="quickstart-extended-events-in-sql-server"></a>Início Rápido: Eventos estendidos no SQL Server

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


Este artigo visa ajudar o desenvolvedor SQL que não está familiarizado com eventos estendidos e que deseja criar uma sessão de evento em apenas alguns minutos. Usando os eventos estendidos, é possível ver detalhes sobre as operações internas do sistema SQL e de seu aplicativo. Quando você cria uma sessão de eventos estendidos, você informa o sistema:

- Das ocorrências que lhe interessam.
- Como você deseja que o sistema relate os dados para você.


Este artigo faz o seguinte:

- Usa as capturas de tela para ilustrar os cliques em SSMS.exe que cria uma sessão de evento.
- Correlaciona as capturas de tela a instruções Transact-SQL equivalentes.
- Explica detalhadamente os termos e conceitos por trás dos cliques e do T-SQL nas sessões de evento.
- Demonstra como testar sua sessão de evento.
- Descreve as alternativas em relação aos resultados:
  - Captura de armazenamento dos resultados.
  - Resultados brutos versus processados.
  - Ferramentas para exibir os resultados de diferentes maneiras e em escalas de tempo diferentes.
- Mostra como você pode procurar e descobrir todos os eventos disponíveis.
- Fornece a chave primária e as relações de chave estrangeira implícitas entre as DMVs (exibições de gerenciamento dinâmico) para eventos estendidos.
- Descreve outras informações de interesse em artigos relacionados.


Blogs e outras conversas informais, às vezes, referem-se aos eventos estendidos pela abreviação *xevents*.


> [!NOTE]
> Para obter informações sobre as diferenças de eventos estendidos entre o Microsoft SQL Server e o banco de dados SQL do Azure, veja [Eventos estendidos no Banco de Dados SQL](https://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/).


## <a name="preparations-before-demo"></a>Preparações antes da demonstração


As etapas preliminares a seguir serão necessárias para a realização real da próxima demonstração.

1. [Baixar o SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx)
  - Todos os meses, é necessário instalar a atualização mais recente mensal do SSMS.
2. Faça logon no Microsoft SQL Server 2014 ou superior, ou em um Banco de Dados SQL do Azure em que `SELECT @@version` retorna um valor cujo primeiro nó é 12 ou superior.
3. Verifique se sua conta tem a [permissão de servidor](../../t-sql/statements/grant-server-permissions-transact-sql.md) de **ALTER ANY EVENT SESSION**.
  - Se estiver interessado, veja mais detalhes sobre segurança e permissões relacionadas aos eventos estendidos ao final deste artigo no [Apêndice](#appendix1).




## <a name="demo-of-ssms-integration"></a>Demonstração da integração do SSMS


SSMS.exe fornece uma interface do usuário excelente para eventos estendidos. A interface do usuário é tão boa que muitos usuários não veem a necessidade de interagir com os eventos estendidos usando o Transact-SQL ou as DMVs (exibições de gerenciamento dinâmico) voltadas para eventos estendidos.

Nesta seção, é possível ver as etapas da interface do usuário para criação de um evento estendido e ver os dados que ele relata. Após as etapas, você pode ler sobre os conceitos envolvidos nas etapas para obter uma compreensão mais profunda.


### <a name="steps-of-demo"></a>Etapas de demonstração


Você pode entender as etapas mesmo se optar por não realizá-las. A demonstração inicia a caixa de diálogo **Nova Sessão** . Processamos suas quatro páginas chamadas:

- Geral
- Eventos
- Armazenamento de Dados
- Avançado


O texto e as capturas de tela de suporte podem não ser exatas quando a interface do usuário do SSMS é ajustada em meses ou anos. Apesar disso, as capturas de tela ainda serão válidas para explicação se as discrepâncias forem pequenas.


1. Conecte-se ao SSMS.

2. No Pesquisador de Objetos, clique em **Gerenciamento** > **Eventos Estendidos** > **Nova Sessão**. A caixa de diálogo **Nova Sessão** é preferível a **Assistente de Nova Sessão**, embora as duas sejam semelhantes.

3. No canto superior esquerdo, clique na página **Geral** . Digite *YourSession*ou qualquer nome que desejar na caixa de texto **Nome da sessão** . *Não* pressione o botão **OK** ainda, que aparece apenas ao final da demonstração.

    ![Nova Sessão > Geral > Nome da sessão](../../relational-databases/extended-events/media/xevents-session-newsessions-10-general-ssms-yoursessionnode.png)

4. No canto superior esquerdo, clique na página **Eventos** e no botão **Selecionar** .

    ![Nova Sessão > Eventos > Selecionar > Biblioteca de eventos, Eventos selecionados](../../relational-databases/extended-events/media/xevents-session-newsessions-14-events-ssms-rightclick-not-wizard.png)

5. Na área **Biblioteca de eventos**, na lista suspensa, escolha **Somente nomes de evento**.
    - Na caixa de texto, digite **sql**, que filtra e reduz a longa lista de eventos disponíveis usando um operador *contains* .
    - Role e clique no evento chamado **sql_statement_completed**.
    - Clique no botão de seta para a direita **>** para mover o evento para a caixa **Eventos selecionados** .

6. Na página **Eventos** , clique no botão **Configurar** à extrema direita.
    - Com o lado esquerdo cortado para melhor exibição, na captura de tela a seguir, é possível ver a área **Opções de configuração de evento**.

    ![Nova Sessão > Eventos > Configurar > Filtro (Predicado) > Campo](../../relational-databases/extended-events/media/xevents-session-newsessions-20b-events-ssms-yoursessionnode.png)

7. Clique na guia **Filtro (Predicado)** . Em seguida, clique em **Clique aqui para adicionar uma cláusula**para capturar todas as instruções SQL SELECT que têm uma cláusula HAVING.

8. No lista suspensa **Campo** , escolha **sqlserver.sql_text**.
   - Em **Operador** , escolha um operador LIKE.
   - Em **Valor** , digite **%SELECT%HAVING%** .

    > [!NOTE]
    > Neste nome de duas partes, *sqlserver* é o nome do pacote e *sql_text* é o nome do campo. O evento anterior que escolhemos, *sql_statement_completed* , deve estar no mesmo pacote que o campo escolhido.

9. No canto superior esquerdo, clique na página **Armazenamento de Dados** .

10. Na área **Destinos**, clique em **Clique aqui para adicionar um destino**.
    - Na lista suspensa **Tipo** , escolha **event_file**.
    - Isso significa que os dados de evento serão armazenados em um arquivo que pode ser exibido.

    ![Nova Sessão > Armazenamento de Dados > Destinos > Tipo > event_file](../../relational-databases/extended-events/media/xevents-session-newsessions-30-datastorage-ssms-yoursessionnode.png)

11. Na área **Propriedades** , digite um nome de arquivo e caminho completo na caixa de texto **Nome de arquivo no servidor** .
    - A extensão de nome de arquivo deve ser *.xel*.
    - Nosso pequeno teste precisará de um tamanho do arquivo inferior a 1 MB.

    ![Nova Sessão > Avançado > Latência máxima de expedição > OK](../../relational-databases/extended-events/media/xevents-session-newsessions-40-advanced-ssms-yoursessionnode.png)

12. No canto superior esquerdo, clique na página **Avançado**.
    - Reduza a **Latência máxima de expedição** até 3 segundos.
    - Por fim, clique no botão **OK** na parte inferior.

13. De volta ao **Pesquisador de Objetos**, expanda **Gerenciamento** > **Sessões** e veja o novo nó de **YourSession**.

    ![O nó da nova *event session* chamado YourSession, no Pesquisador de Objetos, em Gerenciamento > Eventos Estendidos > Sessões](../../relational-databases/extended-events/media/xevents-session-newsessions-50-objectexplorer-ssms-yoursessionnode.png)


#### <a name="edit-your-event-session"></a>Editar a sessão de evento


No **Pesquisador de Objetos**do SSMS, é possível editar a sessão de evento clicando com o botão direito do mouse em seu nó e clicando em **Propriedades**. A mesma caixa de diálogo com várias páginas é exibida.


### <a name="corresponding-t-sql-for-your-event-session"></a>T-SQL correspondente da sessão de evento


Você usou a interface do usuário do SSMS para gerar um script T-SQL que criou a sessão de evento. É possível ver o script gerado da seguinte maneira:

- Clique com o botão direito do mouse no nó da sessão, clique em **Gerar Script da Sessão como** > **CRIAR para** > **Área de Transferência**.
- Cole em qualquer editor de texto.


Veja a seguir a instrução T-SQL CREATE EVENT SESSION para *YourSession*, que foi gerada por cliques na interface do usuário:


```sql
CREATE EVENT SESSION [YourSession]
    ON SERVER 
    ADD EVENT sqlserver.sql_statement_completed
    (
        ACTION(sqlserver.sql_text)
        WHERE
        ( [sqlserver].[like_i_sql_unicode_string]([sqlserver].[sql_text], N'%SELECT%HAVING%')
        )
    )
    ADD TARGET package0.event_file
    (SET
        filename = N'C:\Junk\YourSession_Target.xel',
        max_file_size = (2),
        max_rollover_files = (2)
    )
    WITH (
        MAX_MEMORY = 2048 KB,
        EVENT_RETENTION_MODE = ALLOW_MULTIPLE_EVENT_LOSS,
        MAX_DISPATCH_LATENCY = 3 SECONDS,
        MAX_EVENT_SIZE = 0 KB,
        MEMORY_PARTITION_MODE = NONE,
        TRACK_CAUSALITY = OFF,
        STARTUP_STATE = OFF
    );
GO
```


> [!NOTE]
> Para o Banco de Dados SQL do Azure, na instrução anterior CREATE EVENT SESSION, a cláusula ON SERVER será ON DATABASE.
> 
> Para obter mais informações sobre as diferenças de eventos estendidos entre o Microsoft SQL Server e o banco de dados SQL do Azure, veja [Eventos estendidos no Banco de Dados SQL](https://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/).


#### <a name="pre-drop-of-the-event-session"></a>Pré-DROP da sessão de evento


Antes da instrução CREATE EVENT SESSION, você talvez queira emitir condicionalmente um DROP EVENT SESSION caso o nome já exista.


```sql
IF EXISTS (SELECT *
      FROM sys.server_event_sessions    -- If Microsoft SQL Server.
    --FROM sys.database_event_sessions  -- If Azure SQL Database in the cloud.
      WHERE name = 'YourSession')
BEGIN
    DROP EVENT SESSION YourSession
          ON SERVER;    -- If Microsoft SQL Server.
        --ON DATABASE;  -- If Azure SQL Database.
END
go
```


#### <a name="alter-to-start-and-stop-the-event-session"></a>ALTER para iniciar e interromper a sessão de evento


Quando você cria uma sessão de evento, o padrão é que ela não inicie a execução automaticamente. Você pode iniciar ou interromper a sessão de evento a qualquer momento, usando a instrução T-SQL ALTER EVENT SESSION a seguir.


```sql
ALTER EVENT SESSION [YourSession]
      ON SERVER
    --ON DATABASE
    STATE = START;   -- STOP;
```


Você tem a opção de informar a sessão de evento para ser iniciada automaticamente quando a instância do SQL Server é iniciada. Veja a palavra-chave **STARTUP STATE = ON** em CREATE EVENT SESSION.

- A interface do usuário do SSMS oferece uma caixa de seleção correspondente na página **Nova Sessão** > **Geral** .


## <a name="test-your-event-session"></a>Testar sua sessão de evento


Teste sua sessão de evento com estas etapas simples:

1. No **Pesquisador de Objetos**do SSMS, clique com o botão direito do mouse no nó da sessão de evento e clique em **Iniciar Sessão**.
2. Execute a instrução `SELECT...HAVING` a seguir algumas vezes.
    - O ideal é que você possa alterar o valor `HAVING Count` entre as duas execuções, ativando/desativando entre 2 e 3. Isso permite que você veja as diferenças nos resultados.
3. Clique com o botão direito do mouse no nó da sessão e clique em **Interromper Sessão**.
4. Leia a próxima subseção sobre [como usar SELECT e exibir os resultados](#select-the-full-results-xml-37).



```sql
SELECT
        c.name,
        Count(*)  AS [Count-Per-Column-Repeated-Name]
    FROM
             sys.syscolumns  AS c
        JOIN sys.sysobjects  AS o
    
            ON o.id = c.id
    WHERE
        o.type = 'V'
        AND
        c.name like '%event%'
    GROUP BY
        c.name
    HAVING
        Count(*) >= 3   --2     -- Try both values during session.
    ORDER BY
        c.name;
```


Apenas para fins de exatidão, esta é a saída aproximada da instrução SELECT...HAVING anterior.


```
/*** Approximate output, 6 rows, all HAVING Count >= 3:
name                   Count-Per-Column-Repeated-Name
---------------------  ------------------------------
event_group_type       4
event_group_type_desc  4
event_session_address  5
event_session_id       5
is_trigger_event       4
trace_event_id         3
***/
```



<a name="select-the-full-results-xml-37"/>

### <a name="select-the-full-results-as-xml"></a>Selecionar os resultados completos como XML


No SSMS, execute a instrução T-SQL SELECT a seguir para retornar resultados em que cada linha fornece os dados sobre a ocorrência de um evento. CAST AS XML facilita a exibição dos resultados.


> [!NOTE]
> O sistema de eventos sempre acrescenta um número longo ao nome de arquivo de *.xel* event_file especificado. Antes de executar a instrução SELECT a seguir por meio do arquivo, copie o nome completo fornecido pelo sistema e cole-o em SELECT.


```sql
SELECT
        object_name,
        file_name,
        file_offset,
        event_data,
        'CLICK_NEXT_CELL_TO_BROWSE_XML RESULTS!'
                AS [CLICK_NEXT_CELL_TO_BROWSE_XML_RESULTS],
    
        CAST(event_data AS XML) AS [event_data_XML]
                -- TODO: In ssms.exe results grid, double-click this xml cell!
    FROM
        sys.fn_xe_file_target_read_file(
            'C:\Junk\YourSession_Target_0_131085363367310000.xel',
            null, null, null
        );
```


A cláusula SELECT anterior oferece duas maneiras de exibir os resultados completos de qualquer linha de evento específica:

- Execute SELECT no SSMS e clique em uma célula da coluna **event_data_XML** . Isso é muito útil.
- Copie a cadeia de caracteres longa de XML de uma célula na coluna **event_data** . Cole em qualquer editor de texto simples como Notepad.exe e salve a cadeia de caracteres em um arquivo com a extensão .XML. Em seguida, abra o arquivo .XML com um navegador.


#### <a name="display-of-results-for-one-event"></a>Exibição de resultados de um evento


Em seguida, vemos uma parte dos resultados, que estão em formato XML. Esse XML é editado aqui para torná-lo mais curto para exibição. Observe que `<data name="row_count">` exibe um valor de `6`, que corresponde às nossas seis linhas de resultados exibidas anteriormente. Além disso, podemos ver a instrução SELECT inteira.


```xml
<event name="sql_statement_completed" package="sqlserver" timestamp="2016-05-24T04:06:08.997Z">
  <data name="duration">
    <value>111021</value>
  </data>
  <data name="cpu_time">
    <value>109000</value>
  </data>
  <data name="physical_reads">
    <value>0</value>
  </data>
  <data name="last_row_count">
    <value>6</value>
  </data>
  <data name="offset">
    <value>0</value>
  </data>
  <data name="offset_end">
    <value>584</value>
  </data>
  <data name="statement">
    <value>SELECT
        c.name,
        Count(*)  AS [Count-Per-Column-Repeated-Name]
    FROM
             sys.syscolumns  AS c
        JOIN sys.sysobjects  AS o

            ON o.id = c.id
    WHERE
        o.type = 'V'
        AND
        c.name like '%event%'
    GROUP BY
        c.name
    HAVING
        Count(*) &gt;= 3   --2     -- Try both values during session.
    ORDER BY
        c.name</value>
  </data>
</event>
```


## <a name="ssms-to-display-results"></a>SSMS para exibir os resultados


Há vários recursos avançados da interface do usuário do SSMS que podem ser usados para exibir os dados capturados de um evento estendido. Os detalhes estão em:

- [Exibição avançada de dados de destino dos Eventos Estendidos no SQL Server](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)


Os conceitos básicos começam com as opções do menu de contexto rotuladas **Exibir Dados de Destino** e **Inspecionar Dados Dinâmicos**.


### <a name="view-target-data"></a>Exibir Dados de Destino


No **Pesquisador de Objetos**do SSMS, é possível clicar com o botão direito do mouse no nó de destino que está sob o nó da sessão de evento. No menu de contexto, clique em **Exibir Dados de Destino**. O SSMS exibe os dados.

A exibição não é atualizada conforme novos dados são reportados pelo evento. Mas você pode clicar em **Exibir Dados de Destino** novamente.


![Exibir Dados de Destino, no SSMS, Gerenciamento > Eventos Estendidos > Sessões > YourSession > package0.event_file, clique com o botão direito do mouse](../../relational-databases/extended-events/media/xevents-viewtargetdata-ssms-targetnode-61.png)


### <a name="watch-live-data"></a>Inspecionar Dados Dinâmicos


No **Pesquisador de Objetos**do SSMS, é possível clicar com o botão direito do mouse no nó da sessão de evento. No menu de contexto, clique em **Inspecionar Dados Dinâmicos**. O SSMS exibe dados de entrada conforme sua chegada em tempo real.


![Inspecionar Dados Dinâmicos, no SSMS, Gerenciamento > Eventos Estendidos > Sessões > YourSession > clique com o botão direito do mouse](../../relational-databases/extended-events/media/xevents-watchlivedata-ssms-yoursessionnode-63.png)


## <a name="scenarios"></a>Cenários


Há inúmeros cenários para o uso efetivo dos eventos estendidos. Os artigos a seguir fornecem exemplos de cenários que envolvem os bloqueios usados durante as consultas.


Cenários específicos de sessões de evento destinadas à avaliação de bloqueios são descritos nos artigos a seguir. Os artigos também mostram algumas técnicas avançadas, como o uso de **\@dbid** e de `EXECUTE (@YourSqlString)` dinâmico:

- [Localizar os objetos que detêm a maioria dos bloqueios](../../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)
  - Esse cenário usa o destino package0.histogram, que processa os dados brutos de evento antes de exibi-los para você.
- [Determinar quais consultas estão mantendo bloqueios](../../relational-databases/extended-events/determine-which-queries-are-holding-locks.md)
  - Esse cenário usa o [destino package0.pair_matching](https://msdn.microsoft.com/library/3c87dcfb-543a-4bd8-a73d-1390bdf4ffa3), em que o par de eventos é sqlserver.lock_acquire e lock_release.


## <a name="terms-and-concepts-in-extended-events"></a>Termos e conceitos nos eventos estendidos


A tabela a seguir lista os termos usados para eventos estendidos e descreve seus significados.


| Termo | Descrição |
| :--- | :---------- |
| sessão de evento | Um constructo centrado em torno de um ou mais eventos, além de itens de suporte como ações, são destinos. A instrução CREATE EVENT SESSION constrói cada sessão de evento. Você pode usar ALTER em uma sessão de evento para iniciá-la e interrompê-la quando desejar. <br/> <br/> Às vezes, uma sessão de evento é chamada de apenas uma *sessão*, quando o contexto esclarece que ela indica uma *sessão de evento*. <br/> <br/> Mais detalhes sobre as sessões de evento são descritos em: [Sessões de eventos estendidos do SQL Server](../../relational-databases/extended-events/sql-server-extended-events-sessions.md). |
| event | Uma ocorrência específica no sistema que é inspecionada por uma sessão de eventos ativos. <br/> <br/> Por exemplo, o evento *sql_statement_completed* representa o momento em que se conclui qualquer instrução T-SQL. O evento pode relatar sua duração e outros dados. |
| target | Um item que recebe os dados de saída de um evento capturado. O destino exibe os dados para você. <br/> <br/> Alguns exemplos incluem o *event_file*, e sua prima leve e útil, a memória *ring_buffer*. O destino *histogram* mais elaborado executa algum processamento de seus dados antes de exibi-los. <br/> <br/> Qualquer destino pode ser usado para qualquer sessão de evento. Para obter detalhes, consulte [Destinos de eventos estendidos no SQL Server](../../relational-databases/extended-events/targets-for-extended-events-in-sql-server.md). |
| action | Um campo conhecido para o evento. Os dados do campo são enviados para o destino. O campo de ação está intimamente relacionado ao *filtro de predicado*. |
| filtro de predicado | Um teste de dados em um campo de evento, usado de forma que apenas um subconjunto interessante de ocorrências de eventos sejam enviados para o destino. <br/> <br/> Por exemplo, um filtro pode incluir somente as ocorrências de eventos *sql_statement_completed* em que a instrução T-SQL contém a cadeia de caracteres *HAVING*. |
| pacote | Um qualificador de nome anexado a cada item em um conjunto de itens centrado em torno de um núcleo de eventos. <br/> <br/> Por exemplo, um pacote pode ter eventos sobre o texto T-SQL. Um evento pode tratar de todo o T-SQL em um lote delimitado por GO. Enquanto isso, outro evento mais estreito designa instruções T-SQL individuais. Além disso, para qualquer instrução T-SQL, há eventos de início e concluídos. <br/> <br/> Os campos apropriados para os eventos também estão no pacote com os eventos. A maioria dos destinos está em *package0* e é usada com eventos de vários outros pacotes. |


## <a name="how-to-discover-the-available-events-in-packages"></a>Como descobrir os eventos disponíveis em pacotes


O T-SQL SELECT a seguir retorna uma linha para cada evento disponível cujo nome contém a cadeia de caracteres de três “sql”. Obviamente, você pode editar o valor LIKE para procurar nomes de eventos diferentes. As linhas também dão nome ao pacote que contém o evento.


```sql
SELECT   -- Find an event you want.
        p.name         AS [Package-Name],
        o.object_type,
        o.name         AS [Object-Name],
        o.description  AS [Object-Descr],
        p.guid         AS [Package-Guid]
    FROM
              sys.dm_xe_packages  AS p
        JOIN  sys.dm_xe_objects   AS o
    
                ON  p.guid = o.package_guid
    WHERE
        o.object_type = 'event'   --'action'  --'target'
        AND
        p.name LIKE '%'
        AND
        o.name LIKE '%sql%'
    ORDER BY
        p.name, o.object_type, o.name;
```


A exibição a seguir mostra a linha retornada, editada aqui no formato de nome de coluna = valor. Os dados referem-se ao evento *sql statement_completed* usado nas etapas anteriores do exemplo. A frase para a coluna Object-Descr é particularmente útil.


```  
Package-Name = sqlserver
object_type  = event
Object-Name  = sql_statement_completed
Object-Descr = Occurs when a Transact-SQL statement has completed.
Package-Guid = 655FD93F-3364-40D5-B2BA-330F7FFB6491
```


#### <a name="ssms-ui-for-search"></a>Interface do usuário do SSMS para pesquisa


Outra opção de pesquisa é usar a interface do usuário do SSMS da caixa de diálogo **Nova Sessão** > **Eventos** > **Biblioteca de Eventos** , mostrada em uma captura de tela anterior.



#### <a name="sql-trace-event-classes-with-extended-events"></a>Classes de evento de Rastreamento do SQL, com eventos estendidos


Uma descrição de como usar eventos estendidos com colunas e classes de evento de Rastreamento do SQL está disponível em: [Exibir os Eventos Estendidos equivalentes às classes de rastreamento de eventos do SQL](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)



#### <a name="event-tracing-for-windows-etw-with-extended-events"></a>ETW (Rastreamento de Eventos para Windows), com os eventos estendidos


Descrições de como usar os eventos estendidos com o ETW (Rastreamento de Eventos para Windows) estão disponíveis em:

- [Destino do rastreamento de eventos do Windows](../../relational-databases/extended-events/event-tracing-for-windows-target.md)
- [Monitorar a atividade do sistema usando Eventos Estendidos](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)



Os eventos ETW não estão disponíveis nos eventos estendidos do Banco de Dados SQL do Azure.



## <a name="additional-items"></a>Itens adicionais


Esta seção apresenta brevemente alguns itens diversos.


### <a name="event-sessions-installed-with-sql-server"></a>Sessões de evento instaladas com o SQL Server


O SQL Server é fornecido com alguns eventos estendidos já criados. Todos são configurados para serem iniciados sempre que o sistema SQL é iniciado. Essas sessões de evento coletam dados que podem ser úteis em caso de erro do sistema. Como todos os eventos estendidos, eles consomem apenas uma pequena quantidade de recursos, e a Microsoft recomenda que sejam executados sozinhos.

Você pode ver essas sessões de evento no SSMS **Pesquisador de Objetos** em **Gerenciamento** > **Eventos Estendidos** > **Sessões**.  A partir de junho de 2016, a lista dessas sessões de evento instaladas é:

- AlwaysOn_health
- system_health
- telemetry_events



### <a name="powershell-provider-for-extended-events"></a>Provedor do PowerShell para eventos estendidos


Você pode gerenciar os eventos estendidos do SQL Server usando o provedor do PowerShell do SQL Server. Os detalhes estão em: [Usar o provedor do PowerShell para Eventos Estendidos](../../relational-databases/extended-events/use-the-powershell-provider-for-extended-events.md)


### <a name="system-views-for-extended-events"></a>Exibições do sistema para eventos estendidos


As exibições do sistema para os eventos estendidos incluem:

- *Exibições de catálogo:* para obter informações sobre as sessões de evento definidas por CREATE EVENT SESSION.

- *DMVs (exibições de gerenciamento dinâmico):* para obter informações sobre as sessões de evento atualmente em execução.


[SELECTs and JOINs From System Views for Extended Events in SQL Server (SELECTs e JOINs das exibições do sistema para eventos estendidos no SQL Server)](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md) –fornece informações sobre:


- Como unir as exibições entre si.


- Várias SELECTs úteis nas exibições.


- A correlação entre:
    - As colunas da exibição.
    - Cláusulas CREATE EVENT SESSION.
    - Os controles da interface do usuário do SSMS.

## <a name="code-examples-can-differ-for-azure-sql-database"></a>Os exemplos de código podem ser diferentes no Banco de Dados SQL do Azure

[!INCLUDE[sql-on-premises-vs-azure-similar-sys-views-include.](../../includes/paragraph-content/sql-on-premises-vs-azure-similar-sys-views-include.md)]

## <a name="appendix1"></a> Apêndice: SELECTs para determinar o proprietário da permissão com antecedência

As permissões mencionadas neste artigo são:

- ALTER ANY EVENT SESSION
- VIEW SERVER STATE
- CONTROL SERVER

As instruções SELECT do Transact-SQL podem relatar quem tem essas permissões.


#### <a name="union-direct-permissions-plus-role-derived-permissions"></a>Permissões diretas UNION e permissões derivadas de função


A instrução SELECT...UNION ALL a seguir retorna linhas que mostram quem tem as permissões necessárias para criar sessões de evento e consultar as exibições de catálogo do sistema em busca de eventos estendidos.


```sql
-- Ascertain who has the permissions listed in the ON clause.
-- 'CONTROL SERVER' permission includes the permissions
-- 'ALTER ANY EVENT SESSION' and 'VIEW SERVER STATE'.
SELECT
        'Owner-is-Principal'  AS [Type-That-Owns-Permission],
        NULL                  AS [Role-Name],
        prin.name             AS [Owner-Name],

        perm.permission_name
            COLLATE Latin1_General_CI_AS_KS_WS
            AS [Permission-Name]
    FROM
             sys.server_permissions  AS perm
        JOIN sys.server_principals   AS prin

            ON prin.principal_id = perm.grantee_principal_id
    WHERE
        perm.permission_name IN
            ('ALTER ANY EVENT SESSION',
            'VIEW SERVER STATE',
            'CONTROL SERVER')
UNION ALL

-- Plus check for members of the 'sysadmin' fixed server role,
-- because 'sysadmin' includes the 'CONTROL SERVER' permission.
SELECT
        'Owner-is-Role',
        prin.name,  -- [Role-Name]

        CAST( (IsNull(pri2.name, N'No members'))
            AS nvarchar(128)),

        NULL
    FROM
                         sys.server_role_members  AS rolm
        RIGHT OUTER JOIN sys.server_principals    AS prin

            ON prin.principal_id = rolm.role_principal_id

        LEFT OUTER JOIN sys.server_principals     AS pri2

            ON rolm.member_principal_id = pri2.principal_id
    WHERE
        prin.name = 'sysadmin'
    ORDER BY
        1,2,3,4;
```


#### <a name="has_perms_by_name-function"></a>função HAS_PERMS_BY_NAME


A instrução SELECT a seguir relata as permissões. Ela utiliza a função interna [HAS_PERMS_BY_NAME](../../t-sql/functions/has-perms-by-name-transact-sql.md).

Além disso, se você tem autoridade para temporariamente *representar* outras contas, é possível remover a marca de comentário de [EXECUTE AS LOGIN](../../t-sql/statements/execute-as-transact-sql.md) e as instruções REVERT, para saber mais sobre outras contas.


```sql
--EXECUTE AS LOGIN = 'AccountNameHere';
SELECT HAS_PERMS_BY_NAME(
    null, null,
    'ALTER ANY EVENT SESSION'
    );
--REVERT;
```


#### <a name="security-links"></a>Links de segurança

Estes são os links para a documentação relacionada a essas instruções SELECT e às permissões:

- Detalhes da função interna [HAS_PERMS_BY_NAME (Transact-SQL)](../../t-sql/functions/has-perms-by-name-transact-sql.md)
- [sys.fn_my_permissions (Transact-SQL)](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md)
- [Permissões de servidor GRANT (Transact-SQL)](../../t-sql/statements/grant-server-permissions-transact-sql.md)
- [sys.server_principals (Transact-SQL)](https://msdn.microsoft.com/library/ms188786.aspx)
- Especialmente, para o Banco de Dados SQL do Azure [database_principals (Transact-SQL)](https://msdn.microsoft.com/library/ms187328.aspx)
- Blog: [Effective Database Engine Permissions](https://social.technet.microsoft.com/wiki/contents/articles/15180.effective-database-engine-permissions.aspx) (Permissões eficientes do Mecanismo de Banco de Dados)
- [Cartaz](https://aka.ms/sql-permissions-poster)que permite zoom, como um PDF, que exibe a hierarquia de todas as permissões do SQL Server.



## <a name="links-to-supporting-information"></a>Links para informações de suporte


- [sys.fn_xe_file_target_read_file (Transact-SQL)](../../relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql.md)



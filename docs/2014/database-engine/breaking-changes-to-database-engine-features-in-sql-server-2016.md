---
title: Recursos no SQL Server 2014 do mecanismo de alterações significativas ao banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], what's new
- breaking changes [SQL Server]
ms.assetid: 47edefbd-a09b-4087-937a-453cd5c6e061
caps.latest.revision: 143
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: db9392c92568442a17c4683b2c8a25a5487f59d4
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40392463"
---
# <a name="breaking-changes-to-database-engine-features-in-sql-server-2014"></a>Alterações em recursos do Mecanismo de Banco de Dados que causam interrupção no SQL Server 2014
  Este tópico descreve as últimas alterações no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)] e versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Essas alterações podem danificar aplicativos, scripts ou funcionalidades baseados em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Talvez você tenha esses problemas ao atualizar. Para obter mais informações, consulte [Use Upgrade Advisor to Prepare for Upgrades](../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
##  <a name="SQL14"></a> Últimas alterações do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 Nenhum novo problema.  
  
##  <a name="Denali"></a> Últimas alterações do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="transact-sql"></a>Transact-SQL  
  
|Recurso|Description|  
|-------------|-----------------|  
|Selecionando a partir de colunas ou tabelas denominadas NEXT|As sequências usam a função NEXT VALUE FOR do padrão ANSI. Se uma tabela ou uma coluna for nomeada NEXT e a tabela ou coluna é um alias como valor, e se o padrão ANSI AS for omitida, a instrução resultante poderá causar um erro. Para obter uma solução alternativa, inclua a palavra-chave AS do padrão ANSI. Por exemplo, `SELECT NEXT VALUE FROM Table` deveria ser reescrito como `SELECT NEXT AS VALUE FROM Table` e `SELECT Col1 FROM NEXT VALUE` deveria ser reescrito como `SELECT Col1 FROM NEXT AS VALUE`.|  
|operador PIVOT|O operador PIVOT não é permitido em uma consulta CTE (expressão de tabela comum) recursiva quando o nível de compatibilidade do banco de dados é definido como 110. Escreva a consulta novamente ou altere o nível de compatibilidade para 100 ou menos. O uso de PIVOT e uma consulta CTE recursiva produz resultados incorretos quando há mais de uma única linha por agrupamento.|  
|sp_setapprole e sp_unsetapprole|O parâmetro `OUTPUT` de cookie para `sp_setapprole` é documentado atualmente como `varbinary(8000)` que é o comprimento máximo correto. No entanto, a implementação atual retorna `varbinary(50)`. Os aplicativos devem continuar a reservar `varbinary(8000)` para que o aplicativo continue a operar corretamente se o tamanho de retorno do cookie aumentar em uma versão futura. Para obter mais informações, veja [sp_setapprole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-setapprole-transact-sql).|  
|EXECUTE AS|O parâmetro OUTPUT de cookie para EXECUTE AS está documentado atualmente como `varbinary(8000)`, que tem o comprimento máximo correto. No entanto, a implementação atual retorna `varbinary(100)`. Os aplicativos devem continuar a reservar `varbinary(8000)` para que o aplicativo continue a operar corretamente se o tamanho de retorno do cookie aumentar em uma versão futura. Para obter mais informações, veja [EXECUTE AS &#40;Transact-SQL&#41;](/sql/t-sql/statements/execute-as-transact-sql).|  
|função sys.fn_get_audit_file|Duas colunas adicionais (**user_defined_event_id** e **user_defined_information**) foram adicionados para dar suporte a eventos de auditoria definido pelo usuário. Aplicativos que não selecionam colunas por nome podem retornar mais colunas do que o esperado. Selecione as colunas por nome ou ajuste o aplicativo para aceitar essas colunas adicionais.|  
|Palavra-chave reservada WITHIN|Agora, WITHIN é uma palavra-chave reservada. As referências a colunas ou objetos denominados 'within' falharão. Renomeie a coluna ou o objeto ou delimite o nome usando colchetes ou aspas.  Por exemplo, `SELECT * FROM [within]`.|  
|Operações CAST e CONVERT em colunas computadas do tipo `time` ou `datetime2`|Nas versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], o estilo padrão de operações CAST e CONVERT nos tipos de dados `time` e `datetime2` é 121, exceto quando um dos tipos é usado em uma expressão de coluna computada. Para colunas computadas, o estilo padrão é 0. Esse comportamento afeta as colunas computadas quando são criadas, usadas em consultas que envolvam parametrização automática ou usadas em definições de restrição.<br /><br /> No nível de compatibilidade 110, o estilo padrão das operações CAST e CONVERT nos tipos de dados `time` e `datetime2` sempre é 121. Se a sua consulta depender do comportamento antigo, use um nível de compatibilidade inferior a 110 ou especifique explicitamente o estilo 0 na consulta afetada.<br /><br /> A atualização do banco de dados para o nível de compatibilidade 110 não alterará os dados de usuário que foram armazenados em disco. Você deve corrigir esses dados manualmente conforme apropriado. Por exemplo, se você usou SELECT INTO para criar uma tabela com base em uma fonte que continha uma expressão de coluna computada descrita acima, os dados (usando o estilo 0) serão armazenados, em vez da própria definição de coluna computada. Você precisará atualizar manualmente esses dados para que coincidam com o estilo 121.|  
|ALTER TABLE|A instrução ALTER TABLE permite apenas nomes de tabela de duas partes (schema.object). Especificar um nome de tabela usando os formatos a seguir agora falhará em tempo de compilação com o erro 117:<br /><br /> server.database.schema.table<br /><br /> .database.schema.table<br /><br /> ..schema.table<br /><br /> As versões anteriores que especificam que o formato server.database.schema.table retornaram o erro 4902. A especificação do formato .database.schema.table ou do formato ..schema.table foi bem-sucedida. Para resolver o problema, remova o uso de um prefixo de 4 partes.|  
|Navegando em metadados|Consultar uma exibição usando FOR BROWSE ou SET NO_BROWSETABLE ON agora retorna os metadados da exibição, não os metadados do objeto subjacente. Esse comportamento agora corresponde a outros métodos de navegação em metadados.|  
|SOUNDEX|No nível de compatibilidade de banco de dados 110, a função SOUNDEX implementa novas regras que podem fazer com que os valores computados pela função sejam diferentes dos valores computados sob os níveis de compatibilidade anteriores. Após a atualização para o nível de compatibilidade 110, talvez seja necessário recriar os índices, os heaps ou as restrições CHECK que usam a função SOUNDEX. Para obter mais informações, consulte [SOUNDEX &#40;Transact-SQL&#41;](/sql/t-sql/functions/soundex-transact-sql)
 para obter informações sobre a ferramenta de configuração e recursos adicionais.|  
|Mensagem de contagem de linhas para instruções DML com falha|No [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], o [!INCLUDE[ssDE](../includes/ssde-md.md)] enviará consistentemente o token TDS DONE com RowCount: 0 aos clientes quando uma instrução DML falhar. Nas versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], um valor incorreto de -1 é enviado ao cliente quando a instrução DML que falha está contida em um bloco TRY-CATCH é parametrizada automaticamente pelo [!INCLUDE[ssDE](../includes/ssde-md.md)] ou o bloco TRY-CATCH não está no mesmo nível da instrução que falhou. Por exemplo, se um bloco TRY-CATCH chamar um procedimento armazenado e uma instrução DML no procedimento falhar, o cliente receberá incorretamente um valor -1.<br /><br /> Os aplicativos que confiarem nesse comportamento incorreto falharão.|  
|SERVERPROPERTY (‘Edition’)|Edição instalada do produto da instância do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. Use o valor dessa propriedade para determinar os recursos e os limites, como o número máximo de CPUs que têm suporte do produto instalado.<br /><br /> Com base na edição instalada do Enterprise, pode retornar ‘Enterprise Edition’ ou ‘Enterprise Edition: licenciamento baseado em núcleo’. As edições Enterprise são diferenciadas com base na capacidade de computação máxima por uma única instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter mais informações sobre limites de capacidade de computação na [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], consulte [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).|  
|CREATE LOGIN|O `CREATE LOGIN WITH PASSWORD = '` *senha* `' HASHED` opção não pode ser usada com os hashes criados pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 7 ou anterior.|  
|Operações CAST e CONVERT para `datetimeoffset`|Os únicos estilos que têm suporte ao serem convertidos de tipos de data e hora para `datetimeoffset` são 0 ou 1. Todos os outros estilos de conversão retornam erro 9809. Por exemplo, o seguinte código retorna um erro 9809.<br /><br /> `SELECT CONVERT(date, CAST('7070-11-25 16:25:01.00986 -02:07' as datetimeoffset(5)), 107);`|  
  
### <a name="dynamic-management-views"></a>Exibições de gerenciamento dinâmico  
  
|Exibição|Description|  
|----------|-----------------|  
|sys.dm_exec_requests|As alterações de coluna de comando de `nvarchar(16)` para `nvarchar(32)`.|  
|sys.dm_os_memory_cache_counters|As seguintes colunas foram renomeadas:<br /><br /> single_pages_kb agora é: <br />                          pages_kb<br /><br /> multi_pages_kb<br />                           Agora é: pages_in_use_kb|  
|sys.dm_os_memory_cache_entries|A coluna pages_allocated_count coluna foi renomeada pages_kb.|  
|sys.dm_os_memory_clerks|A coluna multi_pages_kb foi removido.<br /><br /> A coluna single_pages_kb coluna foi renomeada pages_kb.|  
|sys.dm_os_memory_nodes|As seguintes colunas foram renomeadas:<br /><br /> single_pages_kb agora é: <br />                            pages_kb<br /><br /> multi_pages_kb agora é: <br />                            foreign_committed_kb|  
|sys.dm_os_memory_objects|As colunas a seguir foram renomeadas.<br /><br /> pages_allocated_count agora é:<br />                            pages_in_bytes<br /><br /> max_pages_allocated_count agora é: max_pages_in_bytes|  
|sys.dm_os_sys_info|As seguintes colunas foram renomeadas:<br /><br /> physical_memory_in_bytes agora é: <br />                            physical_memory_kb<br /><br /> bpool_commit_target agora é: <br />                            committed_target_kb<br /><br /> Agora, bpool_visible é: <br />                            visible_target_kb<br /><br /> virtual_memory_in_bytes agora é: <br />                            virtual_memory_kb<br /><br /> bpool_commited agora é:<br />                            committed_kb|  
|sys.dm_os_workers|A coluna de localidade foi removida.|  
  
### <a name="catalog-views"></a>Exibições do catálogo  
  
|Exibição|Description|  
|----------|-----------------|  
|sys.data_spaces<br /><br /> sys.partition_schemes<br /><br /> sys.filegroups<br /><br /> sys.partition_functions|Uma nova coluna, is_system, foi adicionada a sys.data_spaces e sys.partition_functions. (sys.partition_schemes e sys.filegroups herdam as colunas de sys.data_spaces.)<br /><br /> Um valor de 1 nessa coluna indica que o objeto foi usado para fragmentos de índice de texto completo.<br /><br /> Em sys.partition_functions, sys.partition_schemes e sys.filegroups, a nova coluna não é a última coluna. Revise as consultas existentes que confiam na ordem das colunas retornadas dessas exibições de catálogo.|  
  
### <a name="sql-clr-data-types-geometry-geography-and-hierarchyid"></a>Tipos de dados de SQL CLR (geometria, geografia e hierarchyid)  
 O assembly **Types**, que contém os tipos de dados espaciais e o tipo hierarchyid, foi atualizado da versão 10.0 para a versão 11.0. Aplicativos personalizados que referenciam esse assembly poderão falhar quando as condições a seguir forem verdadeiras.  
  
-   Quando você move um aplicativo personalizado de um computador no qual [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] tiver sido instalado em um computador no qual apenas [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] é instalado, o aplicativo falhará porque a versão referenciada 10.0 do **SqlTypes** assembly não está presente. Talvez você receba esta mensagem de erro: `“Could not load file or assembly 'Microsoft.SqlServer.Types, Version=10.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91' or one of its dependencies. The system cannot find the file specified.”`  
  
-   Quando você faz referência a **SqlTypes** assembly versão 11.0 e a versão 10.0 também estiver instalada, você poderá ver esta mensagem de erro: `“System.InvalidCastException: Unable to cast object of type 'Microsoft.SqlServer.Types.SqlGeometry' to type 'Microsoft.SqlServer.Types.SqlGeometry'.”`  
  
-   Quando você faz referência a **SqlTypes** assembly versão 11.0 de um aplicativo personalizado que tem como alvo o .NET 3.5, 4 ou 4.5, o aplicativo falhará porque o SqlClient por design carrega a versão 10.0 do assembly. Essa falha ocorre quando o aplicativo chama um dos seguintes métodos:  
  
    -   O método `GetValue` da classe `SqlDataReader`  
  
    -   O método `GetValues` da classe `SqlDataReader`  
  
    -   operador de índice de colchete [] da classe `SqlDataReader`  
  
    -   O método `ExecuteScalar` da classe `SqlCommand`  
  
 Você pode contornar esse problema usando um dos seguintes métodos:  
  
-   Você pode contornar esse problema no seu código chamando o método `GetSqlBytes`, em vez dos métodos Get listados acima, para recuperar tipos de sistema CLR do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], conforme mostrado no exemplo a seguir:  
  
    ```csharp  
    string query = "SELECT [SpatialColumn] FROM [SpatialTable]";  
          using (SqlConnection conn = new SqlConnection("..."))  
          {  
                SqlCommand cmd = new SqlCommand(query, conn);  
  
                conn.Open();  
                SqlDataReader reader = cmd.ExecuteReader();  
  
                while (reader.Read())  
                {  
                      // In version 11.0 only  
                      SqlGeometry g =   
    SqlGeometry.Deserialize(reader.GetSqlBytes(0));  
  
                      // In version 10.0 or 11.0  
                      SqlGeometry g2 = new SqlGeometry();  
                      g.Read(new BinaryReader(reader.GetSqlBytes(0).Stream));  
                }  
          }  
    ```  
  
-   Você pode contornar esse problema usando redirecionamento de assembly no arquivo de configuração de aplicativo, conforme mostrado no seguinte exemplo:  
  
    ```xml  
    <runtime>  
    <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
        ...  
        <dependentAssembly>  
            <assemblyIdentity name="Microsoft.SqlServer.Types" publicKeyToken="89845dcd8080cc91" culture="neutral" />  
            <bindingRedirect oldVersion="10.0.0.0" newVersion="11.0.0.0" />  
        </dependentAssembly>  
        ...  
    </assemblyBinding>  
    <runtime>  
    ```  
  
-   Você pode contornar esse problema na sua cadeia de conexão especificando um valor "SQL Server 2012" para o atributo "Type System Version" para forçar o SqlClient a carregar a versão 11.0 do assembly. Esse atributo de cadeia de conexão está disponível apenas no .NET 4.5 e versões superiores.  
  
-   A marca `assemblyBinding` deve ser encapsulada na marca `runtime`.  
  
### <a name="support-for-awe"></a>Suporte para AWE  
 O suporte ao recurso AWE (Address Windowing Extensions) de 32 bits foi descontinuado. Isso poderá resultar em desempenho mais lento em sistemas operacionais de 32 bits. Para instalações que usam quantidades de memória grandes, migre para um sistema operacional de 64 bits.  
  
### <a name="xquery-functions-are-surrogate-aware"></a>As funções XQuery reconhecem substituições  
 A recomendação W3C para funções e operadores XQuery requer que eles considerem um par substituto que representa um caractere Unicode no intervalo alto como um glifo único na codificação UTF-16. No entanto, nas versões do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssSQL11](../includes/sssql11-md.md)], as funções de cadeia de caracteres não reconheciam pares substitutos como um caracteres único. Algumas operações de cadeia de caracteres – como cálculos de comprimento da cadeia de caracteres e extrações de subcadeia de caracteres – retornavam resultados incorretos. Agora, o [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] oferece suporte para UTF-16 e para a manipulação correta de pares substitutos.  
  
 O tipo de dados XML no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] permite apenas pares substitutos bem formados. No entanto, algumas funções ainda podem retornar resultados indefinidos ou inesperados em certas circunstâncias, pois é possível passar pares substitutos inválidos ou parciais para funções XQuery como valores de cadeia de caracteres. Considere os seguintes métodos para gerar valores da cadeia de caracteres ao usar XQuery no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   Forneça um valor da cadeia de caracteres constante como um valor binário. Durante o uso desse método, continua sendo possível passar pares substitutos inválidos ou parciais.  
  
-   Forneça um valor da cadeia de caracteres constante fornecendo entidades de caractere. Durante o uso desse método, não é possível passar pares substitutos inválidos ou parciais. As funções XQuery requerem uma entidade de caractere único para o caracteres de alto nível. Essas funções gerarão um erro se as entidades de caracteres para os caracteres de pares substitutos forem fornecidas.  
  
-   Importar valores externos por meio **SQL: Column** ou **SQL: Variable**. Durante o uso desses métodos, continua sendo possível introduzir pares substitutos inválidos ou parciais.  
  
#### <a name="affected-xquery-functions-and-operators"></a>Funções e operadores XQuery afetados  
 Agora, as seguintes funções e operadores XQuery manipulam pares substitutos UTF-16 corretamente no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]:  
  
-   **Fn: string-comprimento**. No entanto, se um par alternativo inválido ou parcial for passado como um argumento, o comportamento de **comprimento de cadeia de caracteres** é indefinido.  
  
-   **Fn: substring**.  
  
-   **Fn: contém**. No entanto, se um par substituto parcial for passado como um valor **contém** podem retornar resultados inesperados, pois pode encontrar o par substituto parcial contido no par substituto bem formado.  
  
-   **Fn: concat**. No entanto, se um par substituto parcial for passado como um valor **concat** pode produzir pares substitutos incorretos ou parciais.  
  
-   Operadores de comparação e o **Ordenar por** cláusula. Operadores de comparação incluem +, \<, >, \<=, > =, `eq`, `lt`, `gt`, `le`, e `ge`.  
  
#### <a name="distributed-query-calls-to-a-system-procedure"></a>Chamadas de consulta distribuída a um procedimento de sistema  
 Chamadas de consulta distribuída por `OPENQUERY` para alguns procedimentos de sistema que falharão quando chamadas de um servidor [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] para outro. Isto ocorre quando o [!INCLUDE[ssDE](../includes/ssde-md.md)] não pode descobrir metadados para um procedimento. Por exemplo, `SELECT * FROM OPENQUERY(..., 'EXEC xp_loginfo')`.  
  
#### <a name="isolation-level-and-spresetconnection"></a>nível de isolamento e sp_reset_connection  
 O nível de isolamento para conexões é tratado da seguinte maneira pelos drivers de cliente:  
  
-   Todos os drivers nativos (SNAC, MDAC, ODBC) definem o nível de isolamento (com base na configuração de aplicativo) ao sp_reset_connection.  
  
-   Para ADO.NET, você basicamente terá um nível de isolamento aleatório, dependendo da conexão que você obtém do pool (e se o aplicativo usa o nível de isolamento diferente). Como o pool ADO.NET pode reciclar conexões internamente e de forma transparente, você não poderá prever o que ocorrerá fora do pool.  
  
-   Para o driver JDBC, você obtém o mesmo comportamento que o ADO.NET  
  
     O aplicativo deve sempre definir o nível de isolamento explicitamente depois de abrir a conexão para obter o que ele deseja.  
  
     A conexão JDBC pode ser agrupada para que o aplicativo possa obter um nível de isolamento aleatório e não souber sobre ele.  
  
 Para preservar a compatibilidade com versões anteriores, esse novo comportamento se aplica somente a clientes recentes começando com TDS 7.4.  
  
#### <a name="backward-compatibility"></a>Backward Compatibility  
 **Novo comportamento depende do nível de compatibilidade**  
  
 As seguintes funções e operadores demonstram o novo comportamento descrito acima somente quando o nível de compatibilidade é 110 ou superior:  
  
-   **Fn: contém**.  
  
-   **Fn: concat**.  
  
-   operadores de comparação e **Ordenar por** cláusula  
  
 **Novo comportamento depende do URI de namespace padrão para funções**  
  
 As funções a seguir demonstram o novo comportamento descrito acima somente quando o URI do namespace padrão corresponde ao namespace na recomendação final, ou seja, [ http://www.w3.org/2005/xpath-functions ](http://www.w3.org/2005/xpath-functions). Quando o nível de compatibilidade é 110 ou superior, por padrão, o [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] associa o namespace da função padrão a esse namespace. No entanto, essas funções demonstram o novo comportamento quando esse namespace é usado, independentemente do nível de compatibilidade.  
  
-   **Fn: string-comprimento**  
  
-   **Fn: substring**  
  
##  <a name="KJKatmai"></a> Alterações recentes no SQL Server 2008/SQL Server 2008 R2  
 Esta seção contém as últimas alterações introduzidas no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Nenhuma alteração foi introduzida no [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)].  
  
### <a name="collations"></a>Agrupamentos  
  
|Recurso|Description|  
|-------------|-----------------|  
|Novos agrupamentos|O [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] introduz novos agrupamentos totalmente alinhados aos agrupamentos fornecidos pelo Windows Server 2008. Esses 80 novos agrupamentos melhoraram a exatidão linguística e foram indicados por referências à versão *_100. Se você escolher um agrupamento novo para o servidor ou para o banco de dados, lembre-se de que o agrupamento pode não ser reconhecido pelos clientes com drivers de clientes mais antigos. Agrupamentos não reconhecidos podem fazer com que o aplicativo retorne erros e apresente falhas. Considere as seguintes soluções:<br /><br /> Atualize o sistema operacional do cliente para que os agrupamentos de sistemas subjacentes sejam atualizados.<br /><br /> Se houver um software cliente do banco de dados instalado no cliente, considere a possibilidade de aplicar uma atualização de serviço ao software cliente do banco de dados.<br /><br /> Escolha um agrupamento existente, mapeado para uma página de código no cliente.|  
  
### <a name="common-language-runtime-clr"></a>CLR (Common Language Runtime)  
  
|Recurso|Description|  
|-------------|-----------------|  
|Assemblies CLR|Quando um banco de dados é atualizado para [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], o assembly do `Microsoft.SqlServer.Types` para dar suporte a novos tipos de dados é instalado automaticamente. As regras do Supervisor de Atualização detectam qualquer tipo de usuário ou assemblies de usuário com nomes conflitantes. O Supervisor de Atualização aconselhará renomear qualquer assembly em conflito, bem como qualquer tipo em conflito, ou usar nomes de duas partes no código para fazer referência a esse tipo de usuário preexistente.<br /><br /> Se uma atualização de banco de dados detectar um assembly de usuário com um nome conflitante, ele o renomeará automaticamente e o colocará no banco de dados em modo de suspeição.<br /><br /> Se um tipo de usuário com nome conflitante existir durante a atualização, nenhuma etapa especial será efetuada. Depois da atualização, existirão ambos os tipos de usuário, antigo e novo. O tipo de usuário só estará disponível através de nomes de duas partes.|  
|Assemblies CLR|O [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] instala o .NET Framework 3.5 SP1, que atualiza bibliotecas no GAC (cache de assembly global). Se você tiver bibliotecas sem-suporte registradas em um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], o aplicativo do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] poderá parar de funcionar após a atualização para o [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Isso ocorre porque o serviço de reparo ou a atualização de bibliotecas no GAC não atualiza os assemblies dentro do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se um assembly existir tanto em um banco de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como no GAC, as duas cópias do assembly deverão ser exatamente iguais. Caso isso não aconteça, ocorrerá um erro quando o assembly for usado pela integração CLR do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [suporte para bibliotecas do .NET Framework](../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).<br /><br /> Depois de atualizar o banco de dados, mantenha ou atualize a cópia do assembly dentro dos bancos de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com a instrução ALTER ASSEMBLY. Para obter mais informações, consulte [artigo 949080 da Base de dados de Conhecimento](http://go.microsoft.com/fwlink/?LinkId=154563).<br /><br /> Para detectar se você está usando uma biblioteca do .NET Framework sem-suporte no aplicativo, execute a seguinte consulta no banco de dados.<br /><br /> `SELECT name FROM sys.assemblies WHERE clr_name LIKE '%publickeytoken=b03f5f7f11d50a3a,%';`|  
|Rotinas CLR|O uso da representação dentro de funções CLR definidas pelo usuário, de agregações definidas pelo usuário ou de UDTs (tipos definidos pelo usuário) pode causar o erro 6522 no aplicativo após a atualização para o [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Os cenários a seguir são executados com êxito no [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], mas falham no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. São apresentadas resoluções para cada cenário.<br /><br /> Uma função CLR definida pelo usuário, uma agregação definida pelo usuário ou um método UDT que utiliza representação tem um parâmetro do tipo `nvarchar(max)`, `varchar(max)`, `varbinary(max)`, `ntext`, `text`, `image`, ou um UDT grande e não tiver o  **DataAccessKind. Read** atributo no método. Para resolver esse problema, adicione a **DataAccessKind. Read** de atributo no método, recompile o assembly e reimplante a rotina e o assembly.<br /><br /> Uma função CLR com valor de tabela que tem um **Init** método que executa representação. Para resolver este problema, adicione a **DataAccessKind. Read** de atributo no método, recompile o assembly e reimplante a rotina e o assembly.<br /><br /> Uma função CLR com valor de tabela que tem um **FillRow** método que executa representação. Para resolver esse problema, remova a representação do **FillRow** método. Acesse recursos externos usando o **FillRow** método. Em vez disso, acessar recursos externos do **Init** método.|  
  
### <a name="dynamic-management-views"></a>Exibições de gerenciamento dinâmico  
  
|Exibição|Description|  
|----------|-----------------|  
|sys.dm_os_sys_info|Foram removidas as colunas cpu_ticks_in_ms e sqlserver_start_time_cpu_ticks.|  
|sys.dm_exec_query_resource_semaphoressys.dm_exec_query_memory_grants|A coluna resource_semaphore_id não é uma ID exclusiva no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Essa alteração pode afetar a execução de consulta de solução de problemas. Para obter mais informações, consulte [DM exec_query_resource_semaphores &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-resource-semaphores-transact-sql).|  
  
### <a name="errors-and-events"></a>Erros e eventos  
  
|Recurso|Description|  
|-------------|-----------------|  
|Erros de logon|No [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], o erro 18452 é retornado quando um logon do SQL é usado para conexão a um servidor configurado para usar somente a Autenticação do Windows. No [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], o erro 18456 é retornado.|  
  
### <a name="showplan"></a>Plano de Execução  
  
|Recurso|Description|  
|-------------|-----------------|  
|Esquema XML do plano de execução|Uma nova **SeekPredicateNew** elemento é adicionado ao esquema Showplan XML e a sequência de xsd delimitador (**SqlPredicatesType**) é convertido em um  **\<xsd: choice >** item. Em vez de um ou mais **SeekPredicate** elementos, um ou mais **SeekPredicateNew** elementos podem aparecer agora no Showplan XML. Os dois elementos são mutuamente exclusivos. **SeekPredicate** é mantido no esquema XML Showplan para versões anteriores compatibilidade; no entanto, planos de consulta criados no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] pode conter o **SeekPredicateNew** elemento. Aplicativos que esperam recuperar somente os **SeekPredicate** filho do nó ShowPlanXML/BatchSequence/lote/instruções/StmtSimple/QueryPlan/RelOp/IndexScan/SeekPredicates poderá falhar se o  **SeekPredicate** o elemento não existe. Reescreva o aplicativo para esperar o a **SeekPredicate** ou **SeekPredicateNew** elemento neste nó. Para obter mais informações, consulte .|  
|Esquema XML do plano de execução|Uma nova **IndexKind** atributo é adicionado para o **ObjectType** tipo complexo no esquema de Showplan XML. Haverá falha nos aplicativos que validam estritamente os planos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em relação ao esquema do [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)].|  
  
### <a name="transact-sql"></a>Transact-SQL  
  
|Recurso|Description|  
|-------------|-----------------|  
|Evento DDL ALTER_AUTHORIZATION_DATABASE|Na [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], quando o evento DDL ALTER_AUTHORIZATION_DATABASE é acionado, o valor 'object' é retornado na **ObjectType** elemento do xml EVENTDATA para esse evento quando o tipo de entidade do protegível na definição de dados operação DDL (linguagem) é um objeto. No [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], o tipo real (por exemplo, 'table' ou 'function') é retornado.|  
|CONVERT|Se um estilo inválido for passado para a função CONVERT, será retornado um erro quando o tipo de conversão for de binário em caractere ou de caractere em binário. Em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], o estilo inválido era definido como o estilo padrão para conversões de binário em caractere e de caractere em binário.|  
|GRANT/DENY/REVOKE EXECUTE em assemblies|A permissão EXECUTE não pode ser concedida, negada ou revogada para assemblies. Essa permissão não tem nenhum efeito e agora provoca um erro. Em vez disso, conceda, negue ou revogue a permissão EXECUTE nos procedimentos armazenados ou nas funções que fazem referência ao método de assembly.|  
|Permissões GRANT/DENY/REVOKE em tipos de sistema|As permissões não podem ser concedidas, negadas ou revogadas para tipos de sistema. Em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], essas instruções tinham êxito, mas não tinham nenhum efeito. No [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], um erro é retornado.|  
|GROUP BY|A cláusula GROUP BY não pode conter uma subconsulta em uma expressão que é usada pela lista group by. Em versões anteriores do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], isso era permitido. No [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)], o erro 144 é retornado.<br /><br /> Por exemplo, o código a seguir terá êxito no SQL Server 2005 e falhará no SQL Server 2008.<br /><br /> `DECLARE @Test TABLE(a int NOT NULL);` <br /> `INSERT INTO @Test SELECT 1 union ALL SELECT 2;` <br /> `SELECT COUNT(*)` <br /> `FROM @Test` <br /> `GROUP BY CASE WHEN a IN (SELECT t.a FROM @Test AS t)` <br /> `THEN 1 ELSE 0` <br /> `END;`|  
|cláusula OUTPUT|Para evitar comportamento não determinístico, a cláusula OUTPUT não pode fazer referência a uma coluna de uma exibição ou função com valor de tabela embutida quando essa coluna é definida por um dos seguintes métodos:<br /><br /> Uma subconsulta.<br /><br /> Uma função definida pelo usuário que executa acesso a dados de usuário ou de sistema ou que supostamente executa tal acesso.<br /><br /> Uma coluna computada que contém em sua definição uma função definida pelo usuário que executa acesso a dados de usuário ou de sistema.<br /><br /> <br /><br /> Quando [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] detectar tal coluna na cláusula OUTPUT, ocorrerá o erro 4186. Para obter mais informações, consulte [MSSQLSERVER_4186](../relational-databases/errors-events/mssqlserver-4186-database-engine-error.md).|  
|Cláusula OUTPUT INTO|A tabela de destino da cláusula OUTPUT INTO não pode ter gatilhos habilitados.|  
|Opção no nível de servidor classificação pré-computada|Esta opção não tem suporte no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]. Modifique os aplicativos que usam esse recurso o mais rápido possível.|  
|dica de tabela READPAST|Você não pode especificar a dica READPAST em Isolamento de Instantâneo.<br /><br /> A dica READPAST é ignorada quando a opção de banco de dados READ_COMMITED_SNAPSHOT ou ALLOW_SNAPSHOT_ISOLATION é configurada como ON. No entanto, se você combinar a dica READPAST com READCOMMITTEDLOCK, o comportamento de READPAST é igual ao do bloqueio da dica READCOMMITTED.|  
|sp_helpuser|Os seguintes nomes de coluna são retornados no conjunto de resultados do procedimento armazenado sp_helpuser foram alterados:<br /><br /> Agora é o nome do grupo:<br />                            RoleName<br /><br /> Group_name agora é:<br />                            Role_name<br /><br /> Group_id agora é:<br />                            Role_id<br /><br /> Users_in_group agora é:<br />                            Users_in_role|  
|Criptografia de Dados Transparente|A criptografia transparente de dados (TDE) é executada no nível de E/S: a estrutura da página é descriptografada na memória e criptografada somente quando a página é gravada no disco. Os arquivos de banco de dados e os arquivos de log são criptografados. Os aplicativos de terceiros que ignoram o mecanismo regular do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para acessar páginas (por exemplo, verificando os dados ou os arquivos de log diretamente), falharão quando um banco de dados usar TDE porque os dados estão criptografados nos arquivos. Esses aplicativos podem aproveitar a API Criptográfica do Windows para desenvolver uma solução para descriptografar os dados fora do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
  
### <a name="xquery"></a>XQuery  
  
|Recurso|Description|  
|-------------|-----------------|  
|Suporte à data/hora|Na [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], os tipos de dados `xs:time`, `xs:date`, e `xs:dateTime` não têm suporte de fuso horário. Os dados de fuso horário são mapeados para o fuso horário de UTC. O [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] fornece comportamento de conformidade padrão, o que resulta nas seguintes alterações:<br /><br /> Os valores sem fuso horário são validados.<br /><br /> O fuso horário fornecido ou a ausência de um fuso horário é preservada.<br /><br /> A representação de armazenamento interna é modificada.<br /><br /> A resolução de valores armazenados é aumentada.<br /><br /> Anos negativos não são permitidos.<br /><br /> <br /><br /> Observação: Modificar aplicativos e as expressões XQuery para levar em conta os novos valores de tipo.|  
|Expressões XQuery e Xpath|No [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], as etapas em uma expressão XQuery ou XPath que começam com dois-pontos (': ') são permitidos. Por exemplo, a instrução a seguir contém um teste de nome (`CTR02)` dentro da expressão de caminho que começa com um dois pontos.<br /><br /> `SELECT FileContext.query('for n$ in //CTR return <C>{data )(n$/:CTR02)} </C>) AS Files FROM dbo.MyTable;`<br /><br /> No [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] esse uso não é permitido porque não está de acordo com os padrões XML. O erro 9341 é retornado. Remova o dois-pontos à esquerda ou especifique um prefixo para o teste de nome, por exemplo, (n$/CTR02) ou (n$/p1:CTR02).|  
  
### <a name="connecting"></a>Connecting  
  
|Recurso|Description|  
|-------------|-----------------|  
|Estabelecendo conexão a partir do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client usando SSL|Na conexão com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client, os aplicativos que usam "SERVER=shortname; FORCE ENCRYPTION=true" com certificado cujos Assuntos especificam FQDNs (nomes de domínios totalmente qualificados) antes se conectavam devido à validação reduzida. O SQL Server 2008 R2 aprimora a segurança impondo assuntos de FQDN para certificados. Os aplicativos que dependem de validação reduzida devem executar uma das seguintes ações:<br /><br /> Use o FQDN na cadeia de caracteres de conexão.<br /><br /> -Esta opção não exigirá recompilação do aplicativo se a palavra-chave do servidor da cadeia de caracteres de conexão for configurada fora do aplicativo.<br /><br /> -Esta opção não funciona para aplicativos que têm as cadeias de caracteres de conexão embutidas no código.<br /><br /> -Esta opção não funciona para aplicativos que usam o espelhamento de banco de dados desde o servidor espelhado responde com um nome simples.|  
||Adicione um alias para o nome curto mapear para o FQDN.<br /><br /> -Esta opção funciona mesmo para aplicativos que têm as cadeias de caracteres de conexão embutidas no código.<br /><br /> -Esta opção não funciona para aplicativos que usam o espelhamento de banco de dados, pois os provedores não procuram aliases para nomes de parceiro de failover recebidos.|  
||Tenha um certificado emitido para nome curto.<br /><br /> -Esta opção funciona para todos os aplicativos.|  
  
##  <a name="Yukon"></a> Alterações recentes no SQL Server 2005  
 Para obter uma lista das últimas alterações introduzidas no [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], consulte [alterações recentes em recursos do mecanismo de banco de dados no SQL Server 2005](breaking-changes-to-database-engine-features-in-sql-server-2016.md).  
  
## <a name="see-also"></a>Consulte também  
 [Recursos do mecanismo de banco de dados preteridos no SQL Server 2014](deprecated-database-engine-features-in-sql-server-2016.md)   
 [Alterações no comportamento de recursos do mecanismo de banco de dados no SQL Server 2014](../../2014/database-engine/behavior-changes-to-database-engine-features-in-sql-server-2014.md)   
 [Funcionalidade do mecanismo de banco de dados descontinuada no SQL Server 2014](discontinued-database-engine-functionality-in-sql-server-2016.md)   
 [Compatibilidade com versões anteriores do Mecanismo de Banco de Dados do SQL Server](sql-server-database-engine-backward-compatibility.md)   
 [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
  

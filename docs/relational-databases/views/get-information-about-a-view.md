---
title: Obter informações sobre uma exibição | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql13.swb.viewproperties.general.f1
helpviewer_keywords:
- views [SQL Server], status information
- metadata [SQL Server], views
- dependencies [SQL Server], views
- displaying view information
- views [SQL Server], metadata
- viewing view information
- status information [SQL Server], views
- view dependencies
ms.assetid: 05a73e33-8f85-4fb6-80c1-1b659e753403
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 95611ab79850954506150785b4a4e26c50efe126
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87396435"
---
# <a name="get-information-about-a-view"></a>Obter informações sobre uma exibição
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  Você pode obter informações sobre a definição ou as propriedades de uma exibição no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Talvez seja necessário observar a definição da exibição para entender como seus dados são derivados das tabelas de origem, ou consultar os dados definidos pela exibição.  
  
> [!IMPORTANT]  
>  Se você alterar o nome de um objeto referenciado por uma exibição, deverá modificar a exibição, de modo que seu texto reflita o novo nome. Portanto, antes de renomear um objeto, exiba primeiramente as dependências do objeto para determinar se as exibições foram afetadas pela mudança proposta.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para obter informações sobre uma exibição usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Usar `sp_helptext` para retornar a definição de uma exibição exige associação à função **pública** . Usar `sys.sql_expression_dependencies` para localizar todas as dependências em uma exibição exige a permissão VIEW DEFINITION no banco de dados e a permissão SELECT em `sys.sql_expression_dependencies` para o banco de dados. As definições de objeto de sistema, como as retornadas em SELECT OBJECT_DEFINITION, são publicamente visíveis.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="get-view-properties-by-using-object-explorer"></a>Obter as propriedades da exibição usando o Pesquisador de Objetos  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição ao lado do banco de dados que contém a exibição na qual você deseja ver as propriedades e clique no sinal de adição para expandir a pasta **Exibições** .  
  
2.  Clique com o botão direito do mouse na exibição da qual você deseja ver as propriedades e selecione **Propriedades**.  

     As propriedades a seguir aparecem na caixa de diálogo **Propriedades da Exibição** .  
  
     **Backup de banco de dados**  
     Nome do banco de dados que contém esta exibição.  
  
     **Servidor**  
     O nome da instância do servidor atual.  
  
     **Usuário**  
     Nome do usuário desta conexão.  
  
     **Data da criação**  
     Exibe a data em que a exibição foi criada.  
  
     **Nome**  
     Nome da exibição atual.  
  
     **Esquema**  
     Exibe o esquema que possui a exibição.  
  
     **Objeto do sistema**  
     Indica se a exibição é um objeto do sistema. Os valores são True e False.  
  
     **ANSI NULLs**  
     Indica se o objeto foi criado com a opção ANSI NULLs.  
  
     **Criptografado**  
     Indica se a exibição é criptografada. Os valores são True e False.  
  
     **Identificador entre aspas**  
     Indica se o objeto foi criado com a opção de identificador entre aspas.  
  
     **Ligado a esquema**  
     Indica se a exibição é ligada ao esquema. Os valores são True e False. Para obter informações sobre exibições ligadas ao esquema, consulte a parte SCHEMABINDING de [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
#### <a name="getting-view-properties-by-using-the-view-designer-tool"></a>Obtendo as propriedades da exibição usando a ferramenta Designer de Exibição  
  
1.  No **Pesquisador de Objetos**, expanda o banco de dados que contém a exibição da qual você ver as propriedades e expanda a pasta **Exibições** .  
  
2.  Clique com o botão direito do mouse na exibição da qual você deseja ver as propriedades e selecione **Design**.  
  
3.  Clique com o botão direito do mouse no espaço em branco no painel Diagrama e clique em **Propriedades**.  
  
     As propriedades a seguir aparecem no painel **Propriedades** .  
  
     **(Nome)**  
     Nome da exibição atual.  
  
     **Database Name**  
     Nome do banco de dados que contém esta exibição.  
  
     **Descrição**  
     Uma breve descrição da exibição atual.  
  
     **Esquema**  
     Exibe o esquema que possui a exibição.  
  
     **Nome do servidor**  
     O nome da instância do servidor atual.  
  
     **Associar a Esquema**  
     Impede os usuários de modificar os objetos subjacentes que contribuem com essa exibição de qualquer forma que invalide a definição de exibição.  
  
     **Determinística**  
     Mostra se o tipo de dados da coluna selecionada pode ser determinado com certeza.  
  
     **Valores distintos**  
     Especifica se a consulta filtrará duplicatas na exibição. Essa opção é útil quando você estiver usando apenas algumas das colunas de uma tabela e essas colunas podem conter valores duplicados ou, quando o processo de junção de duas ou mais tabelas produz linhas duplicadas no conjunto de resultados. Escolher essa opção equivale a inserir a palavra-chave DISTINCT na instrução no painel do SQL.  
  
     **Extensão GROUP BY**  
     Especifica de as opções adicionais de exibições com base em consultas de agregação estão disponíveis.  
  
     **Todas as Colunas de Saída**  
     Mostra se todas as colunas são retornadas pela exibição selecionada. Isso é definido no momento em que a exibição é criada.  
  
     **Comentário SQL**  
     Mostra uma descrição das instruções SQL. Para ver a descrição inteira ou editá-la, clique nela e, em seguida, clique nas reticências **(…)** à direita da propriedade. Os comentários podem incluir informações como quem usa a exibição e quando ela é usada.  
  
     **Especificação de Top**  
     Expande para mostrar as propriedades **Top**, **Expression**, **Percent**e **With Ties** .  
  
     **(Top)**  
     Especifica se a exibição incluirá uma cláusula TOP, que retorna apenas as primeiras linhas n ou primeiro percentual n de linhas no conjunto de resultados. O padrão é que a exibição retorne as primeiras 10 linhas no conjunto de resultados. Use para alterar o número de linhas para retornar ou especificar uma porcentagem diferente.  
  
     **Expression**  
     Mostra que porcentagem (se **Percent** for definida como **Sim**) ou registros (se **Percent** for definida como **Não**) a exibição retornará.  
  
     **Percent**  
     Especifica se a consulta incluirá uma cláusula **TOP** , que retorna apenas o primeiro n percentual de linhas no conjunto de resultados  
  
     **With Ties**  
     Especifica se a exibição incluirá uma cláusula **WITH TIES** . **WITH TIES** é útil se uma exibição incluir uma cláusula **ORDER BY** e uma cláusula **TOP** com base na porcentagem. Se essa opção for determinada, e se a porcentagem de corte se encontrar no meio de um conjunto de linhas com valores idênticos na cláusula **ORDER BY** , a exibição será estendida para incluir todas essas linhas.  
  
     **Especificação de atualização**  
     Expande para mostrar as propriedades de **Atualizar Usando Regras de Exibição** e **Verificar Opção** .  
  
     **(Atualizar Usando Regras de Exibição)**  
     Indica que todas as atualizações e inserções da exibição serão convertidas pelo MDAC (Microsoft Data Access Components) em instruções SQL que fazem referência à exibição, e não em instruções SQL que fazem referência diretamente às tabelas base da exibição.  
  
     Em alguns casos, o MDAC manifesta as operações de atualização de exibição e inserção de exibição como atualizações e inserções de acordo com as tabelas base subjacentes da exibição. Selecionando **Atualizar Usando Regras de Exibição**, você pode assegurar que o MDAC gere operações de atualização e inserção na própria exibição.  
  
     **Verificar Opção**  
     Indica que quando você abrir essa exibição e modificar o painel **Resultados** , a fonte de dados verificará se os dados adicionados ou modificados estão de acordo com a cláusula **WHERE** da definição de exibição. Se sua modificação não estiver de acordo com a cláusula **WHERE** , você verá um erro com mais informações.  
  
#### <a name="to-get-dependencies-on-the-view"></a>Para obter as dependências da exibição  
  
1.  No **Pesquisador de Objetos**, expanda o banco de dados que contém a exibição da qual você ver as propriedades e expanda a pasta **Exibições** .  
  
2.  Clique com o botão direito do mouse na exibição da qual você deseja ver as propriedades e selecione **Dependências da Exibição**.  
  
3.  Selecione **Objetos que dependem de [nome da exibição]** para ver os objetos que fazem referência à exibição.  
  
4.  Selecione **Objetos dos quais [nome da exibição] depende** para ver os objetos que são referenciados pela exibição.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-get-the-definition-and-properties-of-a-view"></a>Para obter a definição e as propriedades de uma exibição  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole um dos exemplos a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT definition, uses_ansi_nulls, uses_quoted_identifier, is_schema_bound  
    FROM sys.sql_modules  
    WHERE object_id = OBJECT_ID('HumanResources.vEmployee');   
    GO  
    ```  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    SELECT OBJECT_DEFINITION (OBJECT_ID('HumanResources.vEmployee')) AS ObjectDefinition;   
    GO  
    ```  
  
    ```  
    EXEC sp_helptext 'HumanResources.vEmployee';  
    ```  
  
 Para obter mais informações, veja [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md), [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md) e [sp_helptext &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helptext-transact-sql.md).  
  
#### <a name="to-get-the-dependencies-of-a-view"></a>Para obter as dependências de uma exibição  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT OBJECT_NAME(referencing_id) AS referencing_entity_name,   
        o.type_desc AS referencing_desciption,   
        COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
        referencing_class_desc, referenced_class_desc,  
        referenced_server_name, referenced_database_name, referenced_schema_name,  
        referenced_entity_name,   
        COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,  
        is_caller_dependent, is_ambiguous  
    FROM sys.sql_expression_dependencies AS sed  
    INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
    WHERE referencing_id = OBJECT_ID(N'Production.vProductAndDescription');  
    GO  
    ```  
  
 Para obter mais informações, veja [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) e [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).  
  
  

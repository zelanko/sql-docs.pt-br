---
title: Atualizado — Documentos de bancos de dados relacionais | Microsoft Docs
description: Exibir trechos de conteúdo atualizado para documentação de Bancos de Dados Relacionais alterada recentemente.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: relational-databases
ms.date: 04/28/2018
ms.openlocfilehash: a885befe2411a76dc8c68bf2a7b543a838a52877
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-relational-databases-docs"></a>Novos e recém-atualizados: documentos de Bancos de Dados Relacionais



Quase todos os dias a Microsoft atualiza alguns de seus artigos existentes no site de documentação [Docs.Microsoft.com](http://docs.microsoft.com/). Este artigo exibe trechos de artigos atualizados recentemente. Links para novos artigos também podem ser listados.

Este artigo é gerado por um programa que é reexecutado periodicamente. Ocasionalmente, um trecho pode aparecer com formatação imperfeita ou como markdown do artigo de origem. Imagens nunca são exibidas aqui.

Atualizações recentes são relatadas para o intervalo de datas e o assunto a seguir:



- *Intervalo de datas das atualizações:* &nbsp; **03-02-2018** &nbsp; até &nbsp; **28-04-2018**
- *Área de assunto:* &nbsp; **Bancos de dados relacionais**.




&nbsp;

## <a name="new-articles-created-recently"></a>Novos artigos criados recentemente

Os links a seguir direcionam para novos artigos que foram adicionados recentemente.


1. [Joins (SQL Server)](performance/joins.md)
2. [Subconsultas (SQL Server)](performance/subqueries.md)
3. [Configurar o banco de dados de distribuição de replicação no grupo de disponibilidade Always On](replication/configure-distribution-availability-group.md)
4. [Descoberta e classificação de dados SQL](security/sql-data-discovery-and-classification.md)
5. [Guia de Controle de Versão de Linha e Bloqueio de Transações](sql-server-transaction-locking-and-row-versioning-guide.md)
6. [sys.dm_os_job_object (Banco de Dados SQL do Microsoft Azure)](system-dynamic-management-views/sys-dm-os-job-object-transact-sql.md)
7. [Procedimentos armazenados de fluxo de arquivos e FileTable (Transact-SQL)](system-stored-procedures/filestream-and-filetable-system-stored-procedures.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artigo atualizado com trechos

Esta seção exibe os trechos de atualizações coletados de artigos que passaram por uma atualização extensa recentemente.

Os trechos exibidos aqui aparecerão separados de seu contexto de semântico apropriado. Além disso, às vezes um trecho é separado da sintaxe de markdown importante que circunda no artigo real. Portanto, esses trechos servem apenas como orientações gerais. Os trechos só mostram a você se vale a pena clicar e visitar o artigo real conforme seus interesses.

Por essas e outras razões, não copie o código desses trechos, nem considere-os como verdade exata. Em vez disso, visite o artigo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta dos artigos atualizados recentemente

Essa lista compacta fornece links para todos os artigos atualizados listados na seção Trechos.

1. [Usar um arquivo de formato para ignorar uma coluna de tabela (SQL Server)](#TitleNum_1)
2. [Dados JSON no SQL Server](#TitleNum_2)
3. [Guia de arquitetura de processamento de consultas](#TitleNum_3)
4. [Tutorial: Preparar o SQL Server para replicação – Editor, Distribuidor, Assinante](#TitleNum_4)
5. [Tutorial: Configurar a replicação entre dois servidores totalmente conectados (Transacional)](#TitleNum_5)
6. [Tutorial: Configurar a replicação entre um servidor e clientes móveis (Mesclagem)](#TitleNum_6)
7. [Consulta com pesquisa de texto completo](#TitleNum_7)
8. [Transparent Data Encryption com suporte a Bring Your Own Key para o Data Warehouse e Banco de Dados SQL do Azure](#TitleNum_8)
9. [PowerShell e CLI: habilitar a Transparent Data Encryption usando sua própria chave no Azure Key Vault](#TitleNum_9)
10. [Sobre o change data capture (SQL Server)](#TitleNum_10)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-use-a-format-file-to-skip-a-table-column-sql-serverimport-exportuse-a-format-file-to-skip-a-table-column-sql-servermd"></a>1. &nbsp; [Usar um arquivo de formato para ignorar uma coluna de tabela (SQL Server)](import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)

*Atualizado: 13-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Próximo](#TitleNum_2))

<!-- Source markdown line 221.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 167916d79c5de1e7f13990cb7acc41ceb541b9a7 cb92eb201292294e3397879c98f353fba45f1c1c  (PR=0  ,  Filename=use-a-format-file-to-skip-a-table-column-sql-server.md  ,  Dirpath=docs\relational-databases\import-export\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**Como usar OPENROWSET(BULK...)**


Para usar um arquivo de formato XML para ignorar uma coluna de tabela usando `OPENROWSET(BULK...)`, é necessário fornecer uma lista de colunas explícita na lista de seleção e também na tabela de destino, como segue:

```
    INSERT ...<column_list> SELECT <column_list> FROM OPENROWSET(BULK...)
```

O exemplo a seguir usa o provedor de conjunto de linhas em massa `OPENROWSET` e o arquivo de formato `myTestSkipCol2.xml` . O exemplo importa em massa o arquivo de dados `myTestSkipCol2.dat` para a tabela `myTestSkipCol` . A instrução contém uma lista explícita de colunas na lista de seleção e também na tabela de destino, como exigido.

No SSMS, execute o seguinte código. Atualize os caminhos do sistema de arquivos do local dos arquivos de exemplo em seu computador.

```
USE WideWorldImporters;
GO
INSERT INTO myTestSkipCol
  (Col1,Col3)
    SELECT Col1,Col3
      FROM  OPENROWSET(BULK  'C:\myTestSkipCol2.Dat',
      FORMATFILE='C:\myTestSkipCol2.Xml'
       ) as t1 ;
GO
```



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-json-data-in-sql-serverjsonjson-data-sql-servermd"></a>2. &nbsp; [Dados JSON no SQL Server](json/json-data-sql-server.md)

*Atualizado: 13-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_1) | [Próximo](#TitleNum_3))

<!-- Source markdown line 145.  ms.author= "jovanpop".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 19e276637a463b412f2c29a84f9fb7d0b0f5fcc5 e2f2e8b4732779b3f24561cc0c4da3a958f4edbb  (PR=0  ,  Filename=json-data-sql-server.md  ,  Dirpath=docs\relational-databases\json\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



Os documentos JSON podem ter subelementos e dados hierárquicos que não podem ser mapeados diretamente nas colunas relacionais padrão. Nesse caso, você poderá mesclar a hierarquia JSON unindo a entidade pai às submatrizes.

No exemplo a seguir, o segundo objeto na matriz tem uma submatriz que representa as habilidades da pessoa. Cada subobjeto pode ser analisado usando uma chamada adicional à função `OPENJSON`:

```
DECLARE @json NVARCHAR(MAX)
SET @json =
N'[
       { "id" : 2,"info": { "name": "John", "surname": "Smith" }, "age": 25 },
       { "id" : 5,"info": { "name": "Jane", "surname": "Smith", "skills": ["SQL", "C#", "Azure"] }, "dob": "2005-11-04T12:00:00" }
 ]'

SELECT *
FROM OPENJSON(@json)
  WITH (id int 'strict $.id',
        firstName nvarchar(50) '$.info.name', lastName nvarchar(50) '$.info.surname',
        age int, dateOfBirth datetime2 '$.dob',
    skills nvarchar(max) '$.skills' as json)
    outer apply openjson( a.skills )
                     with ( skill nvarchar(8) '$' ) as b
```
A matriz **skills** é retornada no primeiro `OPENJSON` como um fragmento de texto JSON original e passada para outra função `OPENJSON` usando o operador `APPLY`. A segunda função `OPENJSON` analisará a matriz JSON e retornará valores de cadeia de caracteres como um único conjunto de linhas de coluna que será associado ao resultado do primeiro `OPENJSON`.
O resultado dessa consulta é mostrado na seguinte tabela:

**Resultados**

|id|firstName|lastName|age|dateOfBirth|skill|
|--------|---------------|--------------|---------|-----------------|----------|
|2|John|Smith|25|||
|5|Jane|Smith||2005-11-04T12:00:00|SQL|
|5|Jane|Smith||2005-11-04T12:00:00|C#|
|5|Jane|Smith||2005-11-04T12:00:00|Azure|

`OUTER APPLY OPENJSON` unirá a entidade de primeiro nível à submatriz e retornará um conjunto de resultados mesclado. Devido ao uso de JOIN, a segunda linha será repetida para cada habilidade.




&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-query-processing-architecture-guidequery-processing-architecture-guidemd"></a>3. &nbsp; [Guia de arquitetura de processamento de consultas](query-processing-architecture-guide.md)

*Atualizado: 13-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_2) | [Próximo](#TitleNum_4))

<!-- Source markdown line 34.  ms.author= "jroth".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 96d91b39acdb2f32aaff323e374e92d6f229d241 2c1d2f8585632ada174388399782dc3ed2721dba  (PR=0  ,  Filename=query-processing-architecture-guide.md  ,  Dirpath=docs\relational-databases\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**Precedência de operador lógico**


Quando mais de um operador lógico é usado em uma instrução, `NOT` é avaliado primeiro, em seguida, `AND` e, finalmente, `OR`. Operadores aritméticos e bit a bit são tratados antes dos operadores lógicos. Para saber mais, confira Operator Precedence (Precedência de operador).

No exemplo a seguir, a condição de cor pertence ao modelo de produto 21 e não ao modelo de produto 20, porque `AND` tem precedência em relação a `OR`.

```
SELECT ProductID, ProductModelID
FROM Production.Product
WHERE ProductModelID = 20 OR ProductModelID = 21
  AND Color = 'Red';
GO
```

Você pode alterar o significado da consulta adicionando parênteses para forçar a avaliação de  `OR` primeiro. A consulta a seguir só encontra produtos nos modelos 20 e 21 que são vermelhos.

```
SELECT ProductID, ProductModelID
FROM Production.Product
WHERE (ProductModelID = 20 OR ProductModelID = 21)
  AND Color = 'Red';
GO
```

Usar parênteses, até mesmo quando eles não são necessários, pode melhorar a legibilidade das consultas e reduzir a chance de cometer um erro sutil devido à precedência do operador. Não há penalidade de desempenho significativa usando parênteses. O exemplo a seguir é mais legível que o exemplo original, embora eles sejam sintaticamente semelhantes.

```
SELECT ProductID, ProductModelID
FROM Production.Product
WHERE ProductModelID = 20 OR (ProductModelID = 21
  AND Color = 'Red');
GO
```




&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-tutorial-prepare-sql-server-for-replication---publisher-distributor-subscriberreplicationtutorial-preparing-the-server-for-replicationmd"></a>4. &nbsp; [Tutorial: Preparar o SQL Server para replicação – Editor, Distribuidor, Assinante](replication/tutorial-preparing-the-server-for-replication.md)

*Atualizado: 13-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_3) | [Próximo](#TitleNum_5))

<!-- Source markdown line 56.  ms.author= "mathoma".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6e5caedacff193ce79bdd98708ae1b9dc91f0a8f 9f7af4d3f8b1cffd048db2a5b29fc9e6013f5ed2  (PR=0  ,  Filename=tutorial-preparing-the-server-for-replication.md  ,  Dirpath=docs\relational-databases\replication\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



- Instalar o [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Instalar o [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- Baixar [Bancos de dados de exemplo do AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases). Para obter instruções sobre como restaurar um banco de dados no SSMS, consulte [Restaurando um banco de dados](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms).

>[!NOTE]
> - Não há suporte para replicação em SQL Servers que têm um intervalo de mais de duas versões. Para obter mais informações, consulte [Versões do SQL compatíveis na topologia de replicação](https://blogs.msdn.microsoft.com/repltalk/2016/08/12/suppported-sql-server-versions-in-replication-topology/).
> - No *{Included-Content-Goes-Here}* , você deve se conectar ao Editor e ao Assinante usando um logon que seja membro da função de servidor fixa **sysadmin**. Para obter mais informações sobre a função sysadmin, consulte [Funções de nível de servidor](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/server-level-roles).


**Tempo estimado para concluir este tutorial: 30 minutos**

**Criar contas do Windows para replicação**

Nesta seção, você criará contas do Windows para executar os agentes de replicação. Você criará uma conta de Windows separada no servidor local para os seguintes agentes:

|Agente|Local|Nome da conta|
|---------|------------|----------------|
|Snapshot Agent|Publicador|<*machine_name*>\repl_snapshot|



&nbsp;

&nbsp;

---

<a name="TitleNum_5"/>

### <a name="5-nbsp-tutorial-configure-replication-between-two-fully-connected-servers-transactionalreplicationtutorial-replicating-data-between-continuously-connected-serversmd"></a>5. &nbsp; [Tutorial: Configurar a replicação entre dois servidores totalmente conectados (Transacional)](replication/tutorial-replicating-data-between-continuously-connected-servers.md)

*Atualizado: 13-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_4) | [Próximo](#TitleNum_6))

<!-- Source markdown line 162.  ms.author= "mathoma".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0d74f984d0ffc01cce0376837e6d94df3c5654d7 4ecf4d724286130927dd43687d6845059af6f9b7  (PR=0  ,  Filename=tutorial-replicating-data-between-continuously-connected-servers.md  ,  Dirpath=docs\relational-databases\replication\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**Criar uma assinatura na publicação Transacional**

Nesta seção, você adicionará um assinante à Publicação criada anteriormente. Este tutorial usa um assinante remoto (NODE2\SQL2016), mas uma assinatura também pode ser adicionada localmente ao editor.

**Para criar a assinatura**


1.  Conecte-se ao Publicador no *{Included-Content-Goes-Here}*, expanda o nó de servidor e depois expanda a pasta **Replicação**.

2.  Na pasta **Publicações Locais**, clique com o botão direito do mouse na publicação **AdvWorksProductTrans** e, em seguida, selecione **Novas Assinaturas**.  O Assistente para Nova Assinatura é iniciado:

    Nova Assinatura

3.  Na página Publicação, selecione **AdvWorksProductTrans** e, em seguida, **Avançar**:

    Selecionar o Publicador Tran

4.  Na página Local do Agente de Distribuição, selecione **Executar todos os agentes no Distribuidor** e, em seguida, selecione **Avançar**.  Para obter mais informações sobre assinaturas pull e push, consulte [Assinar publicações](https://docs.microsoft.com/sql/relational-databases/replication/subscribe-to-publications):

    Executar agentes em Dist

5.  Na página Assinantes, se o nome da instância de Assinante não for exibido, selecione **Adicionar Assinante** e, em seguida, **Adicionar Assinante do SQL Server** na lista suspensa. Isso iniciará a caixa de diálogo **Conectar ao Servidor**. Insira o nome da instância de Assinante e, em seguida, selecione **Conectar**.



&nbsp;

&nbsp;

---

<a name="TitleNum_6"/>

### <a name="6-nbsp-tutorial-configure-replication-between-a-server-and-mobile-clients-mergereplicationtutorial-replicating-data-with-mobile-clientsmd"></a>6. &nbsp; [Tutorial: Configurar a replicação entre um servidor e clientes móveis (Mesclagem)](replication/tutorial-replicating-data-with-mobile-clients.md)

*Atualizado: 13-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_5) | [Próximo](#TitleNum_7))

<!-- Source markdown line 93.  ms.author= "mathoma".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0eed78dfe83c88358c030539a2b25d11ef5ec2d3 79b2a3f32c940fede94b11ad2a3ef8a00b911a39  (PR=0  ,  Filename=tutorial-replicating-data-with-mobile-clients.md  ,  Dirpath=docs\relational-databases\replication\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



A tabela Employee contém uma coluna (OrganizationNode) que tem o tipo de dados hierarchyid, compatível apenas com a replicação no SQL 2017. Se estiver usando um build inferior ao SQL 2017, você verá uma mensagem na parte inferior da tela notificando da potencial perda de dados com o uso dessa coluna na replicação bidirecional. Para fins deste tutorial, essa mensagem pode ser ignorada. No entanto, esse tipo de dados não deve ser replicado em um ambiente de produção, a menos que você esteja usando um build compatível. Para obter mais informações sobre como replicar o tipo de dados hierarchyid, consulte [Usando colunas hierarchyid na replicação](https://docs.microsoft.com/sql/t-sql/data-types/hierarchyid-data-type-method-reference#using-hierarchyid-columns-in-replicated-tables)


-  Na página Filtrar Linhas da Tabela, selecione **Adicionar** e, em seguida, **Adicionar Filtro**.

-  Na caixa de diálogo **Adicionar Filtro**, selecione **Funcionário (HumanResources)** em **Selecionar a tabela a ser filtrada**. Selecione a coluna **LoginID**, selecione a seta para a direita para adicionar a coluna à cláusula WHERE da consulta de filtro e modifique a cláusula WHERE da seguinte maneira:

    ```
    WHERE [LoginID] = HOST_NAME()
    ```

    A. Selecione **Uma linha desta tabela vai para apenas uma assinatura** e **OK**:

    Adicionar Filtro



- Na página **Filtrar Linhas da Tabela**, selecione **Funcionário (Recursos Humanos)**, **Adicionar** e, em seguida, **Adicionar Junção para Estender o Filtro Selecionado**.

    A. Na caixa de diálogo **Adicionar Junção**, selecione **Sales.SalesOrderHeader** em **Tabela unida**. Selecione **Gravar a instrução de junção manualmente** e conclua a instrução de junção da seguinte maneira:



&nbsp;

&nbsp;

---

<a name="TitleNum_7"/>

### <a name="7-nbsp-query-with-full-text-searchsearchquery-with-full-text-searchmd"></a>7. &nbsp; [Consulta com pesquisa de texto completo](search/query-with-full-text-search.md)

*Atualizado: 13-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_6) | [Próximo](#TitleNum_8))

<!-- Source markdown line 247.  ms.author= "douglasl".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5ec67b56aa0a6eadadbcfa8b73b6726e75eca2bb 4eb108b202d3dd035a312bac7872cf02bcf31cfa  (PR=0  ,  Filename=query-with-full-text-search.md  ,  Dirpath=docs\relational-databases\search\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**Mais informações sobre pesquisas de termo de geração**


As *formas flexionadas* são os diferentes tempos e conjugações de um verbo ou as formas singular e plural de um substantivo.

Por exemplo, pesquise a forma flexionada da palavra "dirigir". Se várias linhas da tabela contivessem as palavras "dirigir", "dirige", "dirigiu", "dirigindo" e "dirigido", todas elas fariam parte do conjunto de resultados, pois cada uma delas seria uma flexão gerada da palavra dirigir.

Por padrão,FREETEXT e FREETEXTTABLE procuram termos flexionados de todas as palavras especificadas. CONTAINS e CONTAINSTABLE são compatíveis com um argumento `INFLECTIONAL` opcional.

**Pesquisar sinônimos de uma palavra específica**


Um *dicionário de sinônimos* define sinônimos especificados pelo usuário para os termos. Para saber mais sobre arquivos de dicionário de sinônimos, veja [Configurar e gerenciar arquivos do dicionário de sinônimos na pesquisa de texto completo].

Por exemplo, se uma entrada "{carro, automóvel, caminhão, van}" for adicionada ao dicionário de sinônimos, será possível pesquisar o sinônimo da palavra "carro". Todas as linhas da tabela consultada que contiverem as palavras "automóvel", "caminhão", "van" ou "carro" serão exibidas no conjunto de resultados, pois cada uma dessas palavras pertence a um conjunto de expansão de sinônimos contendo a palavra "carro".

FREETEXT e FREETEXTTABLE usam o dicionário de sinônimos por padrão. CONTAINS e CONTAINSTABLE são compatíveis com um argumento `THESAURUS` opcional.



&nbsp;

&nbsp;

---

<a name="TitleNum_8"/>

### <a name="8-nbsp-transparent-data-encryption-with-bring-your-own-key-support-for-azure-sql-database-and-data-warehousesecurityencryptiontransparent-data-encryption-byok-azure-sqlmd"></a>8. &nbsp; [Transparent Data Encryption com suporte a Bring Your Own Key para o Data Warehouse e Banco de Dados SQL do Azure](security/encryption/transparent-data-encryption-byok-azure-sql.md)

*Atualizado: 24-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_7) | [Próximo](#TitleNum_9))

<!-- Source markdown line 110.  ms.author= "aliceku".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 9527658848d430bf0148be84474a75b232cbd112 70ed2a129c580962384f808e8526673957f00d2c  (PR=5662  ,  Filename=transparent-data-encryption-byok-azure-sql.md  ,  Dirpath=docs\relational-databases\security\encryption\  ,  MergeCommitSha40=91a9c812739a1c9a6ec9e7b8cda71ee1f5adae3d) -->



**Como configurar a recuperação de desastres geográfica com o Azure Key Vault**


Para manter a alta disponibilidade de Protetores TDE para bancos de dados criptografados, é necessário configurar Azure Key Vaults redundantes com base nos grupos de failover ou instâncias de replicação geográfica ativas do Banco de Dados SQL desejado ou existente.  Cada servidor com replicação geográfica requer um cofre de chaves separado, que deve estar colocalizado com o servidor na mesma região do Azure. Caso um banco de dados primário se torne inacessível devido a uma interrupção em uma região e um failover seja acionado, o banco de dados secundário é capaz de assumir usando o cofre de chaves secundário.

Para bancos de dados SQL do Azure com replicação geográfica, é necessária a seguinte configuração do Azure Key Vault:
- Um banco de dados primário com um cofre de chaves na região e um banco de dados secundário com um cofre de chaves na região.
- Pelo menos um secundário é necessário; há suporte para até quatro secundários.
- Não há suporte para secundários de secundários (encadeamento).

A seção a seguir apresentará as etapas de instalação e de configuração em mais detalhes.

**Etapas de configuração do Azure Key Vault**


- Instalar o [PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-5.6.0)
- Crie dois Azure Key Vaults em duas regiões diferentes usando o [PowerShell para habilitar a propriedade de "exclusão reversível"](https://docs.microsoft.com/azure/key-vault/key-vault-soft-delete-powershell) nos cofres de chaves (essa opção ainda não está disponível no Portal do AKV – mas é obrigatória no SQL).
- Ambos os Azure Key Vaults devem estar localizados nas duas regiões disponíveis na mesma Área Geográfica do Azure para que o backup e a restauração de chaves funcione.  Se precisar que os dois cofres de chaves estejam localizados em áreas geográficas diferentes para atender aos requisitos de Geo-DR do SQL, siga o [Processo BYOK](https://docs.microsoft.com/azure/key-vault/key-vault-hsm-protected-keys) que permite a importação das chaves de um HSM local.



&nbsp;

&nbsp;

---

<a name="TitleNum_9"/>

### <a name="9-nbsp-powershell-and-cli-enable-transparent-data-encryption-using-your-own-key-from-azure-key-vaultsecurityencryptiontransparent-data-encryption-byok-azure-sql-configuremd"></a>9. &nbsp; [PowerShell e CLI: habilitar a Transparent Data Encryption usando sua própria chave no Azure Key Vault](security/encryption/transparent-data-encryption-byok-azure-sql-configure.md)

*Atualizado: 24-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_8) | [Próximo](#TitleNum_10))

<!-- Source markdown line 196.  ms.author= "aliceku".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a0e00f5701d9a493f503a477c69097ce65aba174 721e8fb856a55ee1e8e9e7fc06036a03adab647b  (PR=5662  ,  Filename=transparent-data-encryption-byok-azure-sql-configure.md  ,  Dirpath=docs\relational-databases\security\encryption\  ,  MergeCommitSha40=91a9c812739a1c9a6ec9e7b8cda71ee1f5adae3d) -->



**Pré-requisitos para a CLI**


- Você deve ter uma assinatura do Azure e ser um administrador na assinatura.
- [Recomendado, mas opcional] Ter um HSM (módulo de segurança de hardware) ou repositório de chaves local para criar uma cópia local do material da chave do Protetor de TDE.
- Interface de linha de comando versão 2.0 ou posterior. Para instalar a versão mais recente e conectar-se à sua assinatura do Azure, consulte [Instalar e configurar a Interface de linha de comando de plataforma cruzada do Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).
- Criar um Azure Key Vault e uma chave para usar para a TDE.
   - [Gerenciar o Key Vault usando a CLI 2.0](https://docs.microsoft.com/azure/key-vault/key-vault-manage-with-cli2)
   - [Instruções para usar um HSM (módulo de segurança de hardware) e o Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-get-started#a-idhsmaif-you-want-to-use-a-hardware-security-module-hsm)
 - O cofre de chaves deve ter as seguintes propriedades para ser usado para TDE:
   - [exclusão reversível](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-soft-delete)
   - [Como usar a exclusão reversível do Key Vault com a CLI](https://docs.microsoft.com/azure/key-vault/key-vault-soft-delete-cli)
- A chave deve ter os seguintes atributos para ser usada para TDE:
   - Nenhuma data de expiração
   - Não estar desabilitada
   - Ser capaz de executar as operações *get*, *wrap key* e *unwrap key*

**Etapa: Criar um servidor e atribuir uma identidade do Microsoft Azure AD ao seu servidor**

      cli
      # create server (with identity) and database



&nbsp;

&nbsp;

---

<a name="TitleNum_10"/>

### <a name="10-nbsp-about-change-data-capture-sql-servertrack-changesabout-change-data-capture-sql-servermd"></a>10. &nbsp; [Sobre o change data capture (SQL Server)](track-changes/about-change-data-capture-sql-server.md)

*Atualizado: 17-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_9))

<!-- Source markdown line 112.  ms.author= "jroth".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 588bff652adefd719e799e9777a416b70184c5f8 77ebdbb1b98b24054d5c5afbb3f1d40e94d1e6bc  (PR=5574  ,  Filename=about-change-data-capture-sql-server.md  ,  Dirpath=docs\relational-databases\track-changes\  ,  MergeCommitSha40=bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68) -->



**Como trabalhar com as diferenças de agrupamento de banco de dados e de tabela**


É importante estar ciente de uma situação em que há diferentes agrupamentos entre o banco de dados e as colunas de uma tabela configurada para a captura de dados de alterações. A CDA usa um armazenamento provisório para popular tabelas laterais. Se uma tabela tiver colunas CHAR ou VARCHAR com agrupamentos diferentes do agrupamento de banco de dados e se essas colunas armazenarem caracteres não ASCII (como caracteres DBCS de byte duplo), a CDA não poderá persistir os dados alterados de maneira consistente com os dados nas tabelas base. Isso se deve ao fato de que as variáveis do armazenamento provisório não podem ter agrupamentos associados a elas.

Considere uma das seguintes abordagens para garantir que os dados capturados da alteração sejam consistentes com as tabelas base:

- Use o tipo de dados NCHAR ou NVARCHAR para colunas que contêm dados não ASCII.

- Ou use o mesmo agrupamento para colunas e para o banco de dados.

Por exemplo, se você tiver um banco de dados que usa um agrupamento SQL_Latin1_General_CP1_CI_AS, considere a seguinte tabela:

```
CREATE TABLE T1(
     C1 INT PRIMARY KEY,
     C2 VARCHAR(10) collate Chinese_PRC_CI_AI)
```

A CDA poderá não capturar os dados binários para a coluna C2, porque seu agrupamento é diferente (Chinese_PRC_CI_AI). Use NVARCHAR para evitar esse problema:

```
CREATE TABLE T1(
     C1 INT PRIMARY KEY,
     C2 NVARCHAR(10) collate Chinese_PRC_CI_AI --Unicode data type, CDC works well with this data type)
```







## <a name="similar-articles-about-new-or-updated-articles"></a>Artigos semelhantes sobre artigos novos ou atualizados

Esta seção lista artigos muito semelhantes a artigos atualizados recentemente em outras áreas de assunto, em nosso repositório público GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Áreas de assunto que *têm* artigos novos ou atualizados recentemente

- [Novo + Atualizado (11+6): &nbsp;documentos sobre a&nbsp; **Análise Avançada para SQL** ](../advanced-analytics/new-updated-advanced-analytics.md)
- [Novo + Atualizado (18+0): &nbsp; documentos sobre o &nbsp;**Analysis Services para SQL** ](../analysis-services/new-updated-analysis-services.md)
- [Novo + Atualizado (218+14): documentos sobre a **Conexão ao SQL** ](../connect/new-updated-connect.md)
- [Novo + Atualizado (14+0): &nbsp;documentos sobre o&nbsp; **Mecanismo de Banco de Dados para SQL** ](../database-engine/new-updated-database-engine.md)
- [Novo + Atualizado (3+2): &nbsp;documentos sobre o&nbsp; **Integration Services para SQL** ](../integration-services/new-updated-integration-services.md)
- [Novo + Atualizado (3+3): &nbsp;documentos sobre o&nbsp; **Linux para SQL** ](../linux/new-updated-linux.md)
- [Novo + Atualizado (7+10): &nbsp;documentos sobre o&nbsp; **Bancos de Dados Relacionais para SQL** ](../relational-databases/new-updated-relational-databases.md)
- [Novo + Atualizado (0+2): &nbsp;documentos sobre o&nbsp; **Reporting Services para SQL** ](../reporting-services/new-updated-reporting-services.md)
- [Novo + Atualizado (1+3): &nbsp;documentos sobre o&nbsp; **SQL Operations Studio** ](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Novo + Atualizado (2+3): &nbsp;documentos sobre o&nbsp; **Microsoft SQL Server** ](../sql-server/new-updated-sql-server.md)
- [Novo + Atualizado (1+1): &nbsp;documentos sobre o&nbsp; **SSDT (SQL Server Data Tools)** ](../ssdt/new-updated-ssdt.md)
- [Novo + Atualizado (5+2): &nbsp;documentos sobre o&nbsp; **SSMS (SQL Server Management Studio)** ](../ssms/new-updated-ssms.md)
- [Novo + Atualizado (0+2): &nbsp;documentos sobre o&nbsp; **Transact-SQL** ](../t-sql/new-updated-t-sql.md)
- [Novo + Atualizado (1+1): &nbsp;documentos sobre as&nbsp; **Ferramentas para SQL** ](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Áreas de assunto que *não* têm nenhum artigo novo ou atualizado recentemente

- [Novo + Atualizado (0+0): documentos sobre o **Sistema de Plataforma Analítica para SQL** ](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Novo + atualizado (0 + 0): documentos do **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Novo + atualizado (0 + 0): documentos de **Extensões DMX (Data Mining) para SQL**](../dmx/new-updated-dmx.md)
- [Novo + Atualizado (0+0): documentos sobre o **MDS (Master Data Services) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Novo + atualizado (0 + 0): documentos de **Expressão MDX para SQL**](../mdx/new-updated-mdx.md)
- [Novo + atualizado (0 + 0): documentos do **ODBC (Open Database Connectivity) para SQL**](../odbc/new-updated-odbc.md)
- [Novo + atualizado (0 + 0): documentos do **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Novo + atualizado (0 + 0): documentos de **Exemplos para SQL**](../samples/new-updated-samples.md)
- [Novo + atualizado (0 + 0): documentos do **SSMA (SQL Server Migration Assistant)**](../ssma/new-updated-ssma.md)
- [Novo + atualizado (0 + 0): documentos do **XQuery para SQL**](../xquery/new-updated-xquery.md)


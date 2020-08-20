---
description: Exportando um inventário de acesso (AccessToSQL)
title: Exportando um inventário de acesso (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Access databases
- Access databases, exporting metadata
- exporting
- exporting Access metadata
- exporting, Access metadata
- exporting, querying exported metadata
- inventories of Access databases
- querying exported metadata
ms.assetid: 7e1941fb-3d14-4265-aff6-c77a4026d0ed
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 112452e9e6c31810dbf26d9aa1e7b36959c192d5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488329"
---
# <a name="exporting-an-access-inventory-accesstosql"></a>Exportando um inventário de acesso (AccessToSQL)
Se você tiver vários bancos de dados do Access e não tiver certeza sobre quais deles serão migrados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , poderá exportar um inventário de todos os bancos de dados do Access em um projeto do. Em seguida, você pode examinar e consultar os metadados de inventário para determinar quais bancos de dados e objetos nesses bancos de dados migram. Esse inventário permite que você encontre rapidamente respostas para perguntas, como as seguintes:  
  
-   Quais são os maiores bancos de dados?  
  
-   Quem possui a maioria dos bancos de dados?  
  
-   Quais bancos de dados contêm as mesmas tabelas?  
  
-   Quais bancos de dados não foram modificados nos últimos seis meses?  
  
-   Quais bancos de dados contêm informações particulares?  
  
Exemplos de consulta que são usados para responder a essas perguntas são fornecidos no final deste tópico.  
  
## <a name="exported-metadata"></a>Metadados exportados  
O SSMA exporta metadados sobre bancos de dados do Access, tabelas, colunas, índices, chaves estrangeiras, consultas, relatórios, formulários, macros e módulos. Os metadados sobre cada uma dessas categorias de itens são exportados para uma tabela separada. Para esquemas dessas tabelas, consulte esquemas de [inventário de acesso](access-inventory-schemas-accesstosql.md).  
  
## <a name="exporting-inventory-data"></a>Exportando dados de inventário  
Para exportar um inventário de acesso, você deve primeiro abrir ou criar um projeto do SSMA e, em seguida, adicionar o banco de dados do Access que deseja analisar. Depois de adicionar bancos de dados a um projeto do SSMA, você exporta metadados sobre esses bancos de dados para um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquema e um banco de dados especificados. Se necessário, o SSMA cria tabelas para armazenar os metadados. Em seguida, o SSMA adiciona os metadados sobre os bancos de dados do Access ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados.  
  
> [!NOTE]  
> Um banco de dados do Access pode ser dividido em vários arquivos: um banco de dados back-end que contém tabelas e bancos de dados front-end que contêm consultas, formulários, relatórios, macros, módulos e atalhos. Se você quiser migrar um banco de dados de divisão para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, adicione o banco de dados front-end ao SSMA.  
  
As instruções a seguir descrevem como criar um projeto do, adicionar bancos de dados ao projeto, conectar-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, em seguida, exportar o inventário.  
  
**Para criar um projeto**  
  
1.  Abra o SSMA para acesso.  
  
2.  No menu **Arquivo**, selecione **Novo Projeto**.  
  
    A caixa de diálogo **Novo Projeto** aparecerá.  
  
3.  Na caixa **nome** , insira um nome para o seu projeto.  
  
4.  Na caixa **local** , insira ou selecione uma pasta para o projeto.  
  
5.  Na caixa **migrar para** combinação, selecione a versão de destino para a qual você deseja migrar e clique em **OK**.  
  
Para obter mais informações sobre como criar projetos, consulte [criando e gerenciando projetos](creating-and-managing-projects-accesstosql.md).  
  
**Para localizar e adicionar bancos de dados**  
  
1.  No menu **arquivo** , clique em **Localizar bancos de dados**.  
  
2.  No assistente localizar bancos de dados, insira a unidade, o caminho do arquivo ou o caminho UNC que você deseja pesquisar. Como alternativa, clique em **procurar** para selecionar a unidade ou a pasta de rede.  
  
3.  Clique em **Adicionar** para adicionar o local à caixa de listagem.  
  
    Repita as duas etapas anteriores para adicionar locais de pesquisa adicionais.  
  
4.  Opcionalmente, adicione critérios de pesquisa para refinar a lista de bancos de dados que são retornados.  
  
    > [!IMPORTANT]  
    > A caixa de texto **tudo ou parte do nome do arquivo** não oferece suporte a caracteres curinga.  
  
5.  Clique em **Verificar**.  
  
    A página verificação é exibida. Isso mostra os bancos de dados que foram encontrados e o progresso da pesquisa. Para interromper a pesquisa, clique em **parar**.  
  
6.  Na página Selecionar arquivos, selecione cada banco de dados que você deseja adicionar ao projeto.  
  
    Você pode usar os botões **selecionar tudo** e **desmarcar todos** na parte superior da lista para selecionar ou limpar todos os bancos de dados. Você também pode manter a tecla CTRL pressionada para selecionar várias linhas ou manter a tecla SHIFT pressionada para selecionar um intervalo de linhas.  
  
7.  Clique em **Avançar**.  
  
8.  Na página verificar, clique em **concluir**.  
  
Para obter mais informações sobre como adicionar bancos de dados a projetos, consulte [adicionando e removendo arquivos de banco de dados do Access](adding-and-removing-access-database-files-accesstosql.md).  
  
**Para se conectar ao SQL Server**  
  
1.  No menu **arquivo** , selecione **conectar-se a SQL Server**.  
  
2.  Na caixa de diálogo conexão, digite ou selecione o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   Se você estiver se conectando à instância padrão no computador local, poderá inserir **localhost** ou um ponto (**.**).  
  
    -   Se você estiver se conectando à instância padrão em outro computador, insira o nome do computador.  
  
    -   Se você estiver se conectando a uma instância nomeada, insira o nome do computador, uma barra invertida e o nome da instância. Por exemplo: MyServer\MyInstance.  
  
3.  Na caixa **banco de dados** , digite o nome do banco de dados de destino para metadados exportados.  
  
4.  Se sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver configurada para aceitar conexões em uma porta não padrão, insira o número da porta que é usado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexões na caixa **porta do servidor** . Para a instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o número da porta padrão é 1433. Para instâncias nomeadas, o SSMA tenta obter o número da porta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço navegador.  
  
5.  No menu suspenso **autenticação** , selecione o tipo de autenticação a ser usado para a conexão. Para usar a conta atual do Windows, selecione **autenticação do Windows**. Para usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon, selecione **SQL Server autenticação**e, em seguida, forneça um nome de usuário e uma senha.  
  
Para obter mais informações sobre como se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [conectando-se a SQL Server &#40;AccessToSQL&#41;](../../ssma/access/connecting-to-sql-server-accesstosql.md).  
  
**Para exportar informações de inventário**  
  
1.  No Gerenciador de metadados do Access, expanda **Access-metabase**.  
  
2.  Marque a caixa de seleção ao lado de **bancos de dados**.  
  
    Para omitir bancos de dados individuais ou objetos de banco de dados, expanda a pasta **databases** e desmarque a caixa de seleção ao lado do banco de dados ou objeto de banco de dados.  
  
3.  Clique com o botão direito do mouse em **bancos de dados** e selecione **Exportar esquema**.  
  
4.  Na caixa de diálogo **selecionar esquema para exportação** , selecione o esquema de destino para os metadados exportados e clique em **OK**.  
  
Cada vez que você exporta metadados, o SSMA anexa os dados ao inventário. Os dados existentes no inventário não são atualizados ou excluídos.  
  
## <a name="querying-the-exported-metadata"></a>Consultando os metadados exportados  
Depois de exportar metadados sobre bancos de dados do Access, você pode consultar os metadados. As instruções a seguir descrevem como usar a janela do editor de consultas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para executar consultas.  
  
**Para consultar metadados**  
  
1.  No menu **Iniciar** , aponte para **todos os programas**, aponte para **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005** ou para **o Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008** ou para **o Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012**e clique em **SQL Server Management Studio**.  
  
2.  Na caixa de diálogo **conectar ao servidor** , verifique as configurações e clique em **conectar**.  
  
3.  Na barra de ferramentas Management Studio, clique em **nova consulta** para abrir o editor de consultas.  
  
4.  Na janela Editor de consultas, insira uma consulta. Alguns exemplos são mostrados na seção a seguir.  
  
5.  Pressione a tecla F5 para executar a consulta.  
  
## <a name="query-examples"></a>Exemplos de consulta  
Antes de executar qualquer uma das consultas a seguir, você deve executar uma consulta de *database_name* de uso para garantir que as consultas sejam executadas no banco de dados que contém os metadados exportados. Por exemplo, se você exportou metadados para um banco de dados chamado MyAccessMetadata, você adicionaria o seguinte no início do [!INCLUDE[tsql](../../includes/tsql-md.md)] código:  
  
```  
USE MyAccessMetadata;  
GO  
```  
Todos os exemplos a seguir usam o esquema **dbo** . Se você exportou os metadados para outro esquema, certifique-se de alterar o esquema ao executar essas consultas.  
  
### <a name="what-tables-and-columns-are-in-these-databases"></a>Quais tabelas e colunas estão nesses bancos de dados?  
A consulta a seguir une as tabelas que contêm os metadados de coluna, tabela e banco de dados e, em seguida, retorna os nomes de todas as colunas, tabelas e dados classificados por nome de coluna:  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D.DatabaseId  
ORDER BY ColumnName;  
```  
  
### <a name="what-are-the-largest-databases"></a>Quais são os maiores bancos de dados?  
A consulta a seguir retorna o nome do banco de dados, o tamanho do arquivo e o número de tabelas em cada banco de dados do Access, classificados por tamanho do arquivo:  
  
```  
SELECT DatabaseName, FileSize, TablesCount  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileSize DESC;  
```  
  
### <a name="who-is-the-owner-of-most-of-the-databases"></a>Quem é o proprietário da maioria dos bancos de dados?  
A consulta a seguir retorna o nome do banco de dados e o proprietário de cada banco de dados do Access, classificados por proprietário.  
  
```  
SELECT DatabaseName, FileOwner  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileOwner;  
```  
  
### <a name="which-databases-contain-the-same-tables"></a>Quais bancos de dados contêm as mesmas tabelas?  
A consulta a seguir usa uma subconsulta para localizar todos os nomes de tabela que aparecem mais de uma vez na lista de tabelas e, em seguida, usa essa lista de tabelas para obter o nome do banco de dados. Os resultados são retornados como o nome do banco de dados e, em seguida, o nome da tabela e são classificados por nome de tabela.  
  
```  
SELECT DatabaseName, TableName   
FROM dbo.SSMA_Access_InventoryTables T  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON D.DatabaseId = T.DatabaseId  
WHERE TableName IN (  
SELECT TableName   
FROM dbo.SSMA_Access_InventoryTables  
GROUP BY TableName   
HAVING count(*)>1  
)  
ORDER BY TableName;  
```  
  
### <a name="which-databases-were-not-modified-in-the-last-six-months"></a>Quais bancos de dados não foram modificados nos últimos seis meses?  
A consulta a seguir obtém a data atual, obtém o valor de mês há seis meses e, em seguida, retorna uma lista de bancos de dados com uma data de modificação superior a seis meses atrás.  
  
```  
SELECT DatabaseName, DateModified  
FROM dbo.SSMA_Access_InventoryDatabases  
WHERE DATEDIFF(month, DateModified, GETDATE()) > 6  
ORDER BY DateModified;  
```  
  
### <a name="which-databases-contain-private-information"></a>Quais bancos de dados contêm informações particulares?  
Seus bancos de dados do Access podem conter informações confidenciais ou pessoais. Talvez você queira mover esses bancos de dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para tirar proveito de seus recursos de segurança. Se você sabe que as colunas que contêm dados confidenciais têm um nome específico ou contêm caracteres específicos, você pode usar uma consulta para localizar todas as colunas que contêm essas informações. Por exemplo, você pode encontrar todas as colunas que incluem a cadeia de caracteres "salário".  Em seguida, a consulta retorna o nome do banco de dados, o nome da tabela e o nome da coluna.  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D. DatabaseId  
WHERE ColumnName LIKE '%salary%';  
```  
Se você não souber o nome da coluna, poderá escrever uma consulta para retornar todas as colunas. Para fazer isso, remova a cláusula WHERE da consulta anterior.  
  
## <a name="see-also"></a>Consulte Também  
[Preparando bancos de dados do Access para migração](preparing-access-databases-for-migration-accesstosql.md)  
  

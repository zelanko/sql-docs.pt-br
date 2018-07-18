---
title: Exportando um inventário do Access (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: 18
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 8a6c94a1335c8ee20aa7f42e179cd924b6661f55
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38980668"
---
# <a name="exporting-an-access-inventory-accesstosql"></a>Exportando um inventário do Access (AccessToSQL)
Se você tiver vários bancos de dados do Access e não tiver certeza quais para migrar para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], você pode exportar um inventário de todos os bancos de dados do Access em um projeto. Você pode revisar e consultar os metadados de inventário para determinar quais bancos de dados e objetos dentro desses bancos de dados para migrar. Esse inventário permite que você realize rapidamente encontrar respostas para perguntas, como o seguinte:  
  
-   Quais são os maiores bancos de dados?  
  
-   Quem possui a maioria dos bancos de dados?  
  
-   Quais bancos de dados contém as mesmas tabelas?  
  
-   Quais bancos de dados não foram modificados nos últimos seis meses?  
  
-   Quais bancos de dados contêm informações privadas?  
  
Exemplos de consultas que são usados para responder a essas perguntas são fornecidos no final deste tópico.  
  
## <a name="exported-metadata"></a>Metadados exportados  
O SSMA exporta os metadados sobre acesso bancos de dados, tabelas, colunas, índices, chaves estrangeiras, consultas, relatórios, formulários, macros e módulos. Metadados sobre cada uma dessas categorias de itens é exportado para uma tabela separada. Para esquemas dessas tabelas, consulte [esquemas de inventário do Access](http://msdn.microsoft.com/fdd3cff2-4d62-4395-8acf-71ea8f17f524).  
  
## <a name="exporting-inventory-data"></a>Exportar dados de inventário  
Para exportar um inventário do Access, você deve abrir pela primeira vez ou criar um projeto do SSMA e, em seguida, adicione o banco de dados que você deseja analisar. Depois de adicionar os bancos de dados a um projeto do SSMA, exportar metadados sobre esses bancos de dados para um especificados [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados e esquema. Se necessário, o SSMA cria tabelas para armazenar os metadados. O SSMA, em seguida, adiciona os metadados sobre os bancos de dados do Access para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] banco de dados.  
  
> [!NOTE]  
> Um banco de dados pode ser dividido em vários arquivos: um banco de dados de back-end que contém tabelas e bancos de dados front-end que contêm consultas, formulários, relatórios, macros, módulos e atalhos. Se você quiser migrar um banco de dados divisão [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], adicione o banco de dados front-end para o SSMA.  
  
As instruções a seguir descrevem como criar um projeto, adicionar bancos de dados ao projeto, conecte-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]e, em seguida, exportar dados de inventário.  
  
**Para criar um projeto**  
  
1.  Abra o SSMA para Access.  
  
2.  No menu **Arquivo**, selecione **Novo Projeto**.  
  
    A caixa de diálogo **Novo Projeto** será exibida.  
  
3.  No **nome** , digite um nome para seu projeto.  
  
4.  No **local** caixa, digite ou selecione uma pasta para o projeto.  
  
5.  No **migrar para** caixa de combinação, selecione a versão de destino ao qual você deseja migrar e, em seguida, clique em **Okey**.  
  
Para obter mais informações sobre como criar projetos, consulte [criando e gerenciando projetos](http://msdn.microsoft.com/f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7).  
  
**Para localizar e adicionar bancos de dados**  
  
1.  Sobre o **arquivo** menu, clique em **localizar bancos de dados**.  
  
2.  No assistente localizar bancos de dados, insira a unidade, caminho do arquivo ou caminho UNC que você deseja pesquisar. Como alternativa, clique em **procurar** para selecionar a unidade ou pasta de rede.  
  
3.  Clique em **adicionar** para adicionar o local para a caixa de listagem.  
  
    Repita as duas etapas anteriores para adicionar locais de pesquisa adicionais.  
  
4.  Opcionalmente, adicione os critérios de pesquisa para refinar a lista de bancos de dados que são retornados.  
  
    > [!IMPORTANT]  
    > O **todo ou parte do nome do arquivo** caixa de texto não oferece suporte a caracteres curinga.  
  
5.  Clique em **Scan**.  
  
    A página de verificação aparece. Isso mostra os bancos de dados que foram localizados e o progresso da pesquisa. Para parar a pesquisa, clique em **parar**.  
  
6.  Na página Selecionar arquivos, selecione cada banco de dados que você deseja adicionar ao projeto.  
  
    Você pode usar o **Selecionar tudo** e **Limpar tudo** botões na parte superior da lista para selecionar ou desmarcar todos os bancos de dados. Você também mantenha a tecla CTRL pressionada para selecionar várias linhas, ou mantenha a tecla SHIFT pressionada para baixo para selecionar um intervalo de linhas.  
  
7.  Clique em **Avançar**.  
  
8.  Na página verificar, clique em **concluir**.  
  
Para obter mais informações sobre como adicionar bancos de dados para projetos, consulte [adicionando e removendo arquivos de banco de dados do Access](http://msdn.microsoft.com/e944c740-4c8a-4bc1-b0ed-be57bc06dced).  
  
**Para se conectar ao SQL Server**  
  
1.  Sobre o **arquivo** menu, selecione **conectar ao SQL Server**.  
  
2.  Na caixa de diálogo de conexão, insira ou selecione o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
    -   Se você estiver se conectando à instância padrão no computador local, você pode inserir **localhost** ou um ponto (**.**).  
  
    -   Se você estiver se conectando à instância padrão em outro computador, digite o nome do computador.  
  
    -   Se você estiver se conectando a uma instância nomeada, digite o nome do computador, uma barra invertida e o nome da instância. Por exemplo: MyServer\MyInstance.  
  
3.  No **banco de dados** , digite o nome do banco de dados de destino para os metadados exportados.  
  
4.  Se sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] está configurado para aceitar conexões em uma porta não padrão, insira o número da porta que é usado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] conexões na **porta do servidor** caixa. Para a instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], o número da porta padrão é 1433. Para instâncias nomeadas, o SSMA tenta obter o número da porta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] serviço localizador.  
  
5.  No **autenticação** menu suspenso, selecione o tipo de autenticação a ser usado para a conexão. Para usar a conta atual do Windows, selecione **autenticação do Windows**. Para usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] login, selecione **autenticação do SQL Server**e, em seguida, forneça um nome de usuário e senha.  
  
Para obter mais informações sobre como se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], consulte [conectando ao SQL Server &#40;AccessToSQL&#41;](../../ssma/access/connecting-to-sql-server-accesstosql.md).  
  
**Para exportar informações de inventário**  
  
1.  No Gerenciador de metadados de acesso, expanda **metabase acesso**.  
  
2.  Marque a caixa de seleção ao lado **bancos de dados**.  
  
    Para omitir os bancos de dados individuais ou objetos de banco de dados, expanda o **bancos de dados** pasta e desmarque a caixa de seleção ao lado do banco de dados ou objeto de banco de dados.  
  
3.  Clique com botão direito **bancos de dados** e selecione **exportar esquema**.  
  
4.  No **selecionar o esquema para exportação** caixa de diálogo, selecione o esquema de destino para os metadados exportados e, em seguida, clique em **Okey**.  
  
Cada vez que você exportar metadados, o SSMA acrescenta os dados para o inventário. Os dados existentes no inventário não são atualizados ou excluídos.  
  
## <a name="querying-the-exported-metadata"></a>Consultando os metadados exportados  
Depois de exportar metadados sobre bancos de dados de acesso, você pode consultar os metadados. As instruções a seguir descrevem para usar a janela do Editor de consultas no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] para executar consultas.  
  
**Para consultar metadados**  
  
1.  Do **inicie** , aponte para **todos os programas**, aponte para **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2005** ou **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2008**ou a **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012**e, em seguida, clique em **SQL Server Management Studio**.  
  
2.  No **conectar ao servidor** caixa de diálogo, verifique as configurações e, em seguida, clique em **Connect**.  
  
3.  Na barra de ferramentas do Management Studio, clique em **nova consulta** para abrir o Editor de consultas.  
  
4.  Na janela do Editor de consultas, insira uma consulta. Alguns exemplos são mostrados na seção a seguir.  
  
5.  Pressione a tecla F5 para executar a consulta.  
  
## <a name="query-examples"></a>Exemplos de consulta  
Antes de executar qualquer uma das consultas a seguir, você deve executar um uso *database_name* consulta para garantir que as consultas são executadas no banco de dados que contém os metadados exportados. Por exemplo, se você exportou os metadados para um banco de dados denominado MyAccessMetadata, você adicionaria o seguinte no início do [!INCLUDE[tsql](../../includes/tsql_md.md)] código:  
  
```  
USE MyAccessMetadata;  
GO  
```  
Os seguintes exemplos usam todos os **dbo** esquema. Se você exportou os metadados para outro esquema, certifique-se de alterar o esquema quando você executar essas consultas.  
  
### <a name="what-tables-and-columns-are-in-these-databases"></a>Quais tabelas e colunas são nesses bancos de dados?  
A consulta a seguir une as tabelas que contêm metadados de banco de dados, tabela e coluna e, em seguida, retorna os nomes de todos os bancos de dados, tabelas e colunas, classificadas por nome de coluna:  
  
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
A consulta a seguir retorna o nome do banco de dados, o tamanho do arquivo e o número de tabelas em cada banco de dados do Access, classificado pelo tamanho do arquivo:  
  
```  
SELECT DatabaseName, FileSize, TablesCount  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileSize DESC;  
```  
  
### <a name="who-is-the-owner-of-most-of-the-databases"></a>Quem é o proprietário da maioria dos bancos de dados?  
A consulta a seguir retorna o nome do banco de dados e o proprietário de cada banco de dados do Access, classificado pelo proprietário.  
  
```  
SELECT DatabaseName, FileOwner  
FROM dbo.SSMA_Access_InventoryDatabases  
ORDER BY FileOwner;  
```  
  
### <a name="which-databases-contain-the-same-tables"></a>Quais bancos de dados contém as mesmas tabelas?  
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
A consulta a seguir obtém a data atual, obtém o valor do mês por seis meses atrás e, em seguida, retorna uma lista de bancos de dados com uma data de modificação de mais de seis meses atrás.  
  
```  
SELECT DatabaseName, DateModified  
FROM dbo.SSMA_Access_InventoryDatabases  
WHERE DATEDIFF(month, DateModified, GETDATE()) > 6  
ORDER BY DateModified;  
```  
  
### <a name="which-databases-contain-private-information"></a>Quais bancos de dados contêm informações privadas?  
Seus bancos de dados do Access podem conter informações confidenciais ou pessoais. Você talvez queira mover esses bancos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] para tirar proveito de seus recursos de segurança. Se você souber que colunas que contêm dados confidenciais têm um nome específico, ou contêm caracteres específicos, você pode usar uma consulta para localizar todas as colunas que contêm essas informações. Por exemplo, você pode encontrar todas as colunas que incluem a cadeia de caracteres "salário".  A consulta, em seguida, retorna o nome do banco de dados, o nome da tabela e o nome da coluna.  
  
```  
SELECT DatabaseName, TableName, ColumnName   
FROM dbo.SSMA_Access_InventoryColumns C  
JOIN dbo.SSMA_Access_InventoryTables T  
ON C.TableId = T.TableId  
JOIN dbo.SSMA_Access_InventoryDatabases D  
ON T.DatabaseId = D. DatabaseId  
WHERE ColumnName LIKE '%salary%';  
```  
Se você não souber o nome da coluna, você pode escrever uma consulta para retornar todas as colunas. Para fazer isso, remova a cláusula WHERE da consulta anterior.  
  
## <a name="see-also"></a>Consulte também  
[Preparar bancos de dados de acesso para a migração](http://msdn.microsoft.com/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
  

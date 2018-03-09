---
title: Adicionando e removendo o acesso a arquivos (AccessToSQL) do banco de dados | Microsoft Docs
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssma-access
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- Access databases
- adding Access files
- adding and removing Access databases
- browsing Access metadata
- browsing metadata, Access databases
- connecting, Access databases
- databases
- files, adding and removing
- finding Access databases
- finding database files
- locating database files
- metadata
- metadata, browsing
- metadata, refreshing
- refreshing metadata
- removing Access files
- scanning for database files
- searching for database files
ms.assetid: e944c740-4c8a-4bc1-b0ed-be57bc06dced
caps.latest.revision: "15"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 64e1bc5dd6b78df1f24ee03b65cfdf6b796c0e39
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="adding-and-removing-access-database-files-accesstosql"></a>Adicionando e removendo arquivos de banco de dados do Access (AccessToSQL)
Para migrar dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, você deve adicionar um ou mais bancos de dados do Access para o projeto SSMA. Esses bancos de dados devem ser Access 97 ou posterior. Se você tiver bancos de dados de uma versão anterior do Access, você deve converter os bancos de dados em uma versão mais recente. Você pode fazer isso abrindo e salvando os bancos de dados do Access 97 ou posterior antes de adicioná-los para o SSMA.  
  
## <a name="what-happens-when-you-add-access-database-files"></a>O que acontece quando você adicionar arquivos de banco de dados de acesso?  
Quando você adiciona um banco de dados a um projeto do SSMA, SSMA lê os metadados de banco de dados e, em seguida, adiciona esses metadados ao arquivo de projeto. Esses metadados descrevem o banco de dados e seus objetos. O SSMA usa os metadados ao converter objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou sintaxe de SQL Azure, e quando ele migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Você pode procurar esses metadados no Gerenciador de metadados de acesso e revisar as propriedades dos objetos de banco de dados individuais.  
  
> [!NOTE]  
> Um banco de dados pode ser dividido em vários arquivos: um banco de dados de back-end que contém tabelas e bancos de dados front-end que contêm consultas, formulários, relatórios, macros, módulos e atalhos. Se você deseja migrar um banco de dados de divisão para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure, adicione o banco de dados front-end para o SSMA.  
  
## <a name="permissions-that-are-required-by-ssma"></a>Permissões necessárias para o SSMA  
Para migrar um banco de dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, o grupo de usuários e o usuário administrador devem ter permissões de administrador. Para obter informações sobre como migrar bancos de dados com proteção do grupo de trabalho, consulte [Preparar bancos de dados para migração](http://msdn.microsoft.com/en-us/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
  
## <a name="selecting-databases-to-add"></a>Selecionar bancos de dados para adicionar  
Se você deseja adicionar um ou mais bancos de dados a um projeto do SSMA, e os arquivos estão em um local conhecido, você pode adicionar os arquivos usando o procedimento a seguir.  
  
**Para adicionar arquivos de banco de dados individual**  
  
1.  Sobre o **arquivo** menu, clique em **adicionar bancos de dados**.  
  
2.  No **abrir** caixa de diálogo caixa, localize a pasta que contém o arquivo de banco de dados ou arquivos.  
  
3.  Selecione os arquivos que você deseja adicionar e, em seguida, clique em **abrir**.  
  
## <a name="finding-databases-to-add"></a>Localizando bancos de dados para adicionar  
Se você deseja adicionar vários bancos de dados de acesso de pastas diferentes para um projeto do SSMA, ou você deseja adicionar um único arquivo, mas tem que localizar o arquivo, você pode seguir estas etapas para localizar um mais arquivos e adicioná-los ao projeto.  
  
**Para localizar e adicionar bancos de dados**  
  
1.  Sobre o **arquivo** menu, clique em **localizar bancos de dados**.  
  
2.  No Assistente de bancos de dados de localização, digite o nome da unidade, caminho do arquivo ou caminho UNC que você deseja pesquisar. Como alternativa, clique em **procurar** para localizar a unidade ou pasta de rede.  
  
3.  Clique em **adicionar** para adicionar o local na lista.  
  
    Repita as duas etapas anteriores para adicionar mais locais de pesquisa.  
  
4.  Opcionalmente, adicione os critérios de pesquisa para refinar a lista de bancos de dados que são retornados.  
  
    > [!IMPORTANT]  
    > O **todo ou parte do nome do arquivo** caixa de texto não oferece suporte a caracteres curinga.  
  
5.  Clique em **verificação**.  
  
    A página de verificação é exibida. Isso mostra os bancos de dados que foram encontrados e o andamento da pesquisa. Para interromper a pesquisa, clique em **parar**.  
  
6.  Na página Selecionar arquivos, selecione os bancos de dados que você deseja adicionar ao projeto.  
  
    Você pode usar o **Selecionar tudo** e **Limpar tudo** botões na parte superior da lista para selecionar ou desmarcar todos os bancos de dados. Você pode mantenha a tecla CTRL pressionada para selecionar vários bancos de dados, ou mantenha pressionada a tecla SHIFT para baixo para selecionar um intervalo de bancos de dados.  
  
7.  Clique em **Avançar**.  
  
8.  Na página de verificação, clique em **concluir**.  
  
## <a name="browsing-access-metadata"></a>Navegando em metadados de acesso  
Depois de adicionar um banco de dados a um projeto, os metadados do projeto é exibido no Gerenciador de metadados de acesso. Você pode procurar a hierarquia de bancos de dados e objetos de banco de dados no Gerenciador.  
  
**Para procurar os metadados**  
  
1.  No Gerenciador de metadados de acesso, expanda **acesso metabase**e, em seguida, expanda **bancos de dados**.  
  
2.  Expanda o banco de dados que você deseja analisar e, em seguida, expanda **consultas**.  
  
    Observe a lista de consultas. Se você selecionar uma consulta, um **SQL** guia e um **propriedades** guia aparecerá no painel direito.  
  
3.  Expanda **tabelas** e, em seguida, selecione uma tabela.  
  
    Observe que são exibidos em quatro guias: **tabela**, **mapeamento de tipo**, **propriedades**, e **dados**.  
  
4.  Expanda uma tabela, **chaves**e, em seguida, selecione uma chave.  
  
    As propriedades de chave são exibidas no painel direito.  
  
5.  Expanda **índices**e, em seguida, selecione um índice.  
  
    As propriedades do índice são exibidas no painel direito.  
  
## <a name="refreshing-databases"></a>Atualizando bancos de dados  
Se um banco de dados do Access for alterado depois que você adicionar seu arquivo, você pode atualizar metadados do banco de dados do Access.  
  
**Para atualizar os metadados de acesso**  
  
-   No Gerenciador de metadados de acesso, o banco de dados e, em seguida, selecione **de atualização do banco de dados**.  
  
## <a name="removing-databases"></a>Removendo bancos de dados  
Você pode remover um banco de dados de um projeto seguindo estas etapas.  
  
**Para remover um banco de dados de um projeto**  
  
1.  No Gerenciador de metadados de acesso, expanda **acesso metabase**e, em seguida, expanda **bancos de dados**.  
  
2.  O banco de dados e, em seguida, selecione **remover banco de dados**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração é [conectar ao SQL Server](http://msdn.microsoft.com/en-us/bb8c4bde-cfc2-4636-92ae-5dd24abe9536).  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[Criando e gerenciando projetos](http://msdn.microsoft.com/en-us/f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7)  
  

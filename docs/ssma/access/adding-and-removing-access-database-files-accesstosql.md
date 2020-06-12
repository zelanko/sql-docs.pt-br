---
title: Adicionando e removendo arquivos de banco de dados do Access (AccessToSQL) | Microsoft Docs
description: Saiba como adicionar ou Remover bancos de dados do Access de ou para o projeto do SSMA a fim de migrar para o Access data para o SQL Server ou para o Azure SQL Database.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
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
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 6806792fa828a5ebb4ea3a7a5a7e813626bff523
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293683"
---
# <a name="adding-and-removing-access-database-files-accesstosql"></a>Adicionando e removendo arquivos de banco de dados do Access (AccessToSQL)
Para migrar dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o ou SQL Azure, você deve adicionar um ou mais bancos de dado do Access ao projeto do SSMA. Esses bancos de dados devem ter o Access 97 ou versões posteriores. Se você tiver bancos de dados de uma versão anterior do Access, deverá converter os bancos de dados em uma versão mais recente. Você faz isso abrindo e salvando os bancos de dados no Access 97 ou em uma versão posterior antes de adicioná-los ao SSMA.  
  
## <a name="what-happens-when-you-add-access-database-files"></a>O que acontece quando você adiciona arquivos de banco de dados do Access?  
Quando você adiciona um banco de dados do Access a um projeto do SSMA, o SSMA lê os metadados do banco de dados e, em seguida, adiciona esses metadados ao arquivo do projeto. Esses metadados descrevem o banco de dados e seus objetos. O SSMA usa os metadados ao converter objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure sintaxe e ao migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Você pode procurar esses metadados no Gerenciador de metadados do Access e examinar as propriedades de objetos de banco de dados individuais.  
  
> [!NOTE]  
> Um banco de dados do Access pode ser dividido em vários arquivos: um banco de dados back-end que contém tabelas e bancos de dados front-end que contêm consultas, formulários, relatórios, macros, módulos e atalhos. Se você quiser migrar um banco de dados de divisão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, adicione o banco de dados front-end ao SSMA.  
  
## <a name="permissions-that-are-required-by-ssma"></a>Permissões exigidas pelo SSMA  
Para migrar um banco de dados do Access para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, o grupo usuários e o usuário administrador devem ter permissões de administrador. Para obter informações sobre como migrar bancos de dados com a proteção de grupo de trabalho, consulte [preparando bancos de dados do Access para migração](preparing-access-databases-for-migration-accesstosql.md).  
  
## <a name="selecting-databases-to-add"></a>Selecionando bancos de dados a serem adicionados  
Se você quiser adicionar um ou mais bancos de dados a um projeto do SSMA e os arquivos estiverem todos em um único local conhecido, você poderá adicionar os arquivos usando o procedimento a seguir.  
  
**Para adicionar arquivos de banco de dados individuais**  
  
1.  No menu **arquivo** , clique em **Adicionar bancos de dados**.  
  
2.  Na caixa de diálogo **abrir** , localize a pasta que contém o arquivo ou arquivos de banco de dados.  
  
3.  Selecione os arquivos que você deseja adicionar e clique em **abrir**.  
  
## <a name="finding-databases-to-add"></a>Localizando bancos de dados a serem adicionados  
Se você quiser adicionar vários bancos de dados do Access de pastas diferentes a um projeto do SSMA ou desejar adicionar um único arquivo, mas precisar localizá-lo, siga estas etapas para localizar um ou mais arquivos e adicioná-los ao projeto.  
  
**Para localizar e adicionar bancos de dados**  
  
1.  No menu **arquivo** , clique em **Localizar bancos de dados**.  
  
2.  No Assistente para localizar bancos de dados, insira o nome da unidade, o caminho do arquivo ou o caminho UNC que você deseja pesquisar. Como alternativa, clique em **procurar** para localizar a unidade ou a pasta de rede.  
  
3.  Clique em **Adicionar** para adicionar o local à lista.  
  
    Repita as duas etapas anteriores para adicionar mais locais de pesquisa.  
  
4.  Opcionalmente, adicione critérios de pesquisa para refinar a lista de bancos de dados que são retornados.  
  
    > [!IMPORTANT]  
    > A caixa de texto **tudo ou parte do nome do arquivo** não oferece suporte a caracteres curinga.  
  
5.  Clique em **Verificar**.  
  
    A página verificação é exibida. Isso mostra os bancos de dados que foram encontrados e o progresso da pesquisa. Para interromper a pesquisa, clique em **parar**.  
  
6.  Na página Selecionar arquivos, selecione os bancos de dados que você deseja adicionar ao projeto.  
  
    Você pode usar os botões **selecionar tudo** e **desmarcar todos** na parte superior da lista para selecionar ou limpar todos os bancos de dados. Você pode manter a tecla CTRL pressionada para selecionar vários bancos de dados ou manter a tecla SHIFT pressionada para selecionar um intervalo de bancos de dados.  
  
7.  Clique em **Próximo**.  
  
8.  Na página verificar, clique em **concluir**.  
  
## <a name="browsing-access-metadata"></a>Procurando metadados de acesso  
Depois de adicionar um banco de dados do Access a um projeto, os metadados do projeto aparecerão no Gerenciador de metadados do Access. Você pode procurar a hierarquia de bancos de dados e objetos de banco de dados no Gerenciador.  
  
**Para procurar metadados**  
  
1.  No Gerenciador de metadados do Access, expanda **acesso-metabase**e expanda **bancos de dados**.  
  
2.  Expanda o banco de dados que você deseja examinar e, em seguida, expanda **consultas**.  
  
    Observe a lista de consultas. Se você selecionar uma consulta, uma guia **SQL** e uma guia **Propriedades** aparecerão no painel direito.  
  
3.  Expanda **tabelas** e selecione uma tabela.  
  
    Observe que são exibidas quatro guias: **tabela**, **mapeamento de tipo**, **Propriedades**e **dados**.  
  
4.  Expanda uma tabela, expanda **chaves**e selecione uma chave.  
  
    As propriedades de chave aparecem no painel direito.  
  
5.  Expanda **índices**e selecione um índice.  
  
    As propriedades do índice aparecem no painel direito.  
  
## <a name="refreshing-databases"></a>Atualizando bancos de dados  
Se um banco de dados do Access for alterado depois que você adicionar seu arquivo, você poderá atualizar os metadados do banco de dados do Access.  
  
**Para atualizar metadados de acesso**  
  
-   No Gerenciador de metadados do Access, clique com o botão direito do mouse no banco de dados e selecione **Atualizar do banco de dados**.  
  
## <a name="removing-databases"></a>Removendo bancos de dados  
Você pode remover um banco de dados do Access de um projeto seguindo estas etapas.  
  
**Para remover um banco de dados de um projeto**  
  
1.  No Gerenciador de metadados do Access, expanda **acesso-metabase**e expanda **bancos de dados**.  
  
2.  Clique com o botão direito do mouse no banco de dados e selecione **remover banco de dados**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa do processo de migração é [conectar-se a SQL Server](https://msdn.microsoft.com/bb8c4bde-cfc2-4636-92ae-5dd24abe9536).  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados do Access para SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[Criando e Gerenciando Projetos](creating-and-managing-projects-accesstosql.md)  
  

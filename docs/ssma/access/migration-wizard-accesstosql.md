---
title: Assistente de migração (AccessToSQL) | Microsoft Docs
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
- Migration Wizard dialog box
- Migration Wizard, adding Access databases
- Migration Wizard, Connect to SQL Azure
- Migration Wizard, Connect to SQL Server
- Migration Wizard, Link Tables
- Migration Wizard, Migration status
- Migration Wizard, New Project
- Migration Wizard, Selecting objects to migrate
ms.assetid: 5bab5914-b2ae-4795-8cf5-83e42d64bef2
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 52e29fb03a3bcc0436f69447caa4e96fc146c3a7
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38985488"
---
# <a name="migration-wizard-accesstosql"></a>Assistente de migração (AccessToSQL)
O Migration Wizard orienta a migração de um ou mais bancos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Usando o assistente, você cria um projeto, adicionar bancos de dados para o projeto, selecione objetos para migrar e se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Você também irá converter, carregar e migrar dados e esquemas de acesso. Opcionalmente, você pode vincular a tabelas do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tabelas ou do SQL Azure.  
  
A maioria das páginas do Assistente de migração contém as mesmas opções de caixas de diálogo do SSMA existentes. Portanto, as páginas do assistente são descritas aqui e, em seguida, os links são fornecidos para que você pode aprender mais sobre as opções individuais. Se uma página contém opções exclusivas, eles estão documentados aqui.  
  
## <a name="starting-the-migration-wizard"></a>Iniciando o Assistente de migração  
Por padrão, o Migration Wizard é exibida quando você inicia o SSMA. Você também pode iniciar o assistente no **arquivo** menu selecionando **Assistente de migração**.  
  
## <a name="welcome-page"></a>Página de boas-vindas  
A página de boas-vinda introduz o Assistente de migração e fornece a opção a seguir para iniciar o assistente.  
  
**Inicie esse assistente na inicialização.**  
Por padrão, o SSMA iniciará o Assistente de migração quando você inicia o SSMA. Para impedir a inicialização automática do assistente, desmarque essa caixa de seleção.  
  
## <a name="create-new-project-page"></a>Criar nova página do projeto  
A página Criar novo projeto é onde você pode inserir o arquivo nome, local e migração projeto tipo de projeto (a versão de destino usado para a migração do SQL Server). Para obter mais informações, consulte [novo projeto (SSMA)](http://msdn.microsoft.com/ca294f6d-eeb5-42ca-9306-156281a3f0f3)  
  
## <a name="add-access-databases-page"></a>Adicionar página de acesso a bancos de dados  
A página Adicionar bancos de dados do Access é onde você adicionar um ou mais bancos de dados do Access para o projeto. Você pode adicionar bancos de dados individuais, clicando **adicionar bancos de dados**e, em seguida, selecionando os bancos de dados de **aberto** janela. Ou, você pode encontrar os bancos de dados usando o **localizar bancos de dados** botão. Para obter mais informações, consulte os tópicos a seguir:  
  
-   [Adicionando e removendo arquivos de banco de dados do Access](http://msdn.microsoft.com/e944c740-4c8a-4bc1-b0ed-be57bc06dced)  
  
-   [Localizar o Assistente de bancos de dados (selecione os locais)](http://msdn.microsoft.com/00b2d32a-998b-47a7-b25c-589b5bd6777a)  
  
-   [Localizar o Assistente de bancos de dados (selecione os arquivos)](http://msdn.microsoft.com/2f574a34-4bab-40a4-89a8-ad4907ffc3fd)  
  
-   [Assistente Localizar Bancos de Dados (verifique a seleção)](http://msdn.microsoft.com/62e20e03-50cc-4ac8-8072-524d194d2ec3)  
  
## <a name="select-objects-to-migrate-page"></a>Selecionar objetos a serem migrados de página  
Os objetos Selecione a página de migração, você seleciona objetos a ser convertida. Você pode selecionar todos os objetos, grupos de objetos ou objetos individuais.  
  
**Para selecionar objetos**  
  
1.  Expandir **acesso metabase**e, em seguida, expanda **bancos de dados**.  
  
2.  Siga um ou mais destes procedimentos:  
  
    -   Para converter todos os bancos de dados, selecione a caixa de seleção ao lado **bancos de dados**.  
  
    -   Para converter ou omitir os bancos de dados individuais, marque ou desmarque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para converter ou omitir consultas, expanda o banco de dados e, em seguida, marque ou desmarque a **consultas** caixa de seleção.  
  
    -   Para converter ou omitir tabelas individuais, expanda o banco de dados, expanda **tabelas**e, em seguida, selecione ou desmarque a caixa de seleção ao lado da tabela.  
  
Se você tiver muitos objetos, talvez você queira usar o **seleção de objeto avançado** objetos de banco de dados de opções no painel à direita para filtrar o acesso. Por exemplo, se você selecionar **tabelas** no painel esquerdo, em seguida, você pode filtrar a lista de tabelas inserindo cadeias de caracteres na **filtro** caixa. Em seguida, você pode selecionar ou limpar as tabelas filtradas para a migração usando os botões na parte superior do painel.  
  
Para obter mais informações sobre filtragem, consulte a seção de opções de [objeto seleção avançada (SSMA comuns)](http://msdn.microsoft.com/f53b0c79-5473-410a-a0dc-d8f544f7a63c).  
  
## <a name="connect-to-sql-server-page"></a>Conectar-se à página do SQL Server  
Em conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] página, você especificar as propriedades de conexão e, em seguida, conecte-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obter mais informações, consulte [conectar-se ao SQL Server](http://msdn.microsoft.com/00e0432e-ec26-4ab4-af64-c9ca760e3541)  
  
> [!IMPORTANT]  
> Assim que a conexão for bem-sucedida, você encontrará **vincular tabelas** página onde você tem a opção de vincular as tabelas. Clique em **próxima** e inicia a migração.  
  
## <a name="connect-to-sql-azure-page"></a>Conectar-se ao SQL Azure página  
Na página conectar a SQL Azure, especifique as propriedades de conexão e, em seguida, conecte-se ao SQL Azure. Para criar um novo banco de dados do azure, você pode fazer isso usando **criar banco de dados do Azure** opção que aparece em clique **procurar** botão. Para obter mais informações, consulte [conectar-se ao SQL Azure](http://msdn.microsoft.com/bf44b236-d9be-41ae-a5fd-bd73038e505f)  
  
> [!IMPORTANT]  
> Assim que a conexão for bem-sucedida, você encontrará **vincular tabelas** página onde você tem a opção de vincular as tabelas. Clique em **próxima** botão na página de Links para iniciar a migração.  
  
## <a name="link-tables-page"></a>Página de tabelas de link  
A página de vincular tabelas permite vincular suas tabelas originais do Access para o migrado [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou tabelas do SQL Azure. Vinculando tabelas modifica seu banco de dados do Access de modo que suas páginas de acesso de consultas, formulários, relatórios e dados de usarem os dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados do SQL Azure em vez dos dados em seu banco de dados do Access.  
  
**Vincular tabelas**  
Selecione o **vincular tabelas** caixa de seleção para vincular a tabelas do Access para o migrado [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou tabelas do SQL Azure. Para iniciar a migração, você deve clicar **próxima** botão.  
  
## <a name="migration-status-page"></a>Página de Status de migração  
A página de Status de migração mostra o andamento de converter os esquemas de acesso à [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou os esquemas do SQL Azure, carregando os esquemas convertidos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, e, em seguida, a migração de dados.  
  
Para obter mais informações sobre essa página, consulte [converter, carregar e migrar](http://msdn.microsoft.com/4ec83e96-88a5-4b7b-8d5a-f3429d9a936b)  
  
## <a name="see-also"></a>Consulte também  
[Introdução ao Assistente de migração do SQL Server para acesso &#40;AccessToSQL&#41;](../../ssma/access/getting-started-with-sql-server-migration-assistant-for-access-accesstosql.md)  
[Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[Reference(Access) de Interface do usuário](http://msdn.microsoft.com/af24c303-4a41-449b-9c86-d6558a97e839)  
  

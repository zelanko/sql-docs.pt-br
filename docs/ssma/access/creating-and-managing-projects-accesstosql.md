---
title: Criando e gerenciando projetos (AccessToSQL) | Microsoft Docs
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- creating projects
- new projects
- opening projects
- projects
- projects, creating and managing
- saving metadata
- saving projects
ms.assetid: f2d1f0b0-5394-4adb-b3f3-abd71eb68ca7
caps.latest.revision: 22
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bc89d40afd125aef5c874c4578bb153cdfcf6993
ms.contentlocale: pt-br
ms.lasthandoff: 08/02/2017

---
# <a name="creating-and-managing-projects-accesstosql"></a>Criando e gerenciando projetos (AccessToSQL)
Para migrar bancos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, você deve primeiro criar um projeto SSMA. O projeto é um arquivo que contém metadados sobre os bancos de dados de acesso que você deseja migrar para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure, metadados sobre a instância de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure que receberá os dados, e os objetos migrados [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] informações de conexão e as configurações do projeto.  
  
## <a name="reviewing-default-project-settings"></a>Revisando parâmetros de projeto padrão  
O SSMA contém várias opções de conversão e sincronização de objetos de banco de dados e para conversão de dados. A configuração padrão para essas opções é apropriada para muitos usuários. No entanto, antes de criar um novo projeto SSMA, examine as opções e, se você quiser alterar as configurações padrão que serão usadas para todos os seus projetos novos.  
  
**Para examinar as configurações de projeto padrão**  
  
1.  Sobre o **ferramentas** menu, selecione **configurações de projeto padrão**.  
  
2.  Selecione o tipo de projeto em **versão de destino de migração** lista suspensa para quais configurações devem ser exibidos / alterado e clique **geral** guia.  
  
3.  No painel esquerdo, clique em **conversão**.  
  
4.  No painel direito, revise as opções. Para obter mais informações sobre essas opções, consulte [configurações do projeto (conversão)](http://msdn.microsoft.com/en-us/bcebc635-c638-4ddb-924c-b9ccfef86388).  
  
5.  Altere as opções conforme necessário.  
  
6.  Repita as etapas anteriores para o **migração**, **GUI**, e **mapeamento de tipo** páginas.  
  
    -   Para obter informações sobre opções de migração, consulte [configurações do projeto (migração)](http://msdn.microsoft.com/en-us/4caebc9c-8680-4b99-a8fa-89c43161c95d).  
  
    -   Para obter informações sobre as opções de interface de usuário, consulte [configurações de projeto (GUI)](http://msdn.microsoft.com/en-us/cf06baf1-8714-48a3-95dc-781f6ca53693).  
  
    -   Para obter mais informações sobre configurações de mapeamento de tipo de dados, consulte [configurações do projeto (tipo de mapeamento)](http://msdn.microsoft.com/en-us/b87b9683-abed-4677-8c50-18bdba704655).  
  
    -   Para obter informações sobre as configurações do SQL Azure, consulte [configurações do projeto (SQL Azure)](http://msdn.microsoft.com/en-us/bbb8a204-d0e4-4f0b-9709-271feb1f136e).  
  
**Observação** as configurações do SQL Azure estará disponíveis somente quando você seleciona a migração para o SQL Azure ao criar um projeto.  
  
## <a name="creating-new-projects"></a>Criar novos projetos  
O SSMA é iniciado sem carregar um projeto padrão. Para migrar dados de bancos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou SQL Azure, você deve criar um projeto.  
  
**Para criar um novo projeto**  
  
1.  No menu **Arquivo**, selecione **Novo Projeto**.  
  
    A caixa de diálogo **Novo Projeto** será exibida.  
  
2.  No **nome** , digite um nome para seu projeto.  
  
3.  No **local** caixa, digite ou selecione uma pasta para o projeto  
  
4.  O descarte de migração para baixo, selecione um SQL Server 2005 / SQL Server 2008 / SQL Server 2012 / SQL Server 2014 / 2016 / Azure SQL DB do SQL Server e, em seguida, clique em **Okey**.  
  
O SSMA cria o arquivo de projeto. Agora você pode executar a próxima etapa do [adicionando um ou mais bancos de dados do Access](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced).  
  
## <a name="customizing-project-settings"></a>Personalizando configurações de projeto  
Além de definir as configurações do projeto padrão, que se aplicam a todos os novos projetos do SSMA, você também pode personalizar as configurações para cada projeto. Para obter mais informações, consulte [conversão de configuração e opções de migração](http://msdn.microsoft.com/en-us/0a7304df-2f35-4453-96ef-7ac83dea1167).  
  
Quando você personalizar mapeamentos de tipo de dados entre bancos de dados de origem e de destino, você pode definir mapeamentos no projeto, no banco de dados ou no nível de objeto. Para obter mais informações sobre o mapeamento de tipo, consulte [tipos de dados de destino e origem do mapeamento de](http://msdn.microsoft.com/en-us/b362a075-16e7-423f-b63f-e1e9f02844a9).  
  
## <a name="saving-projects"></a>Salvando projetos  
Quando você salvar um projeto, o SSMA persiste as configurações do projeto e, opcionalmente, os metadados do banco de dados, para o arquivo de projeto.  
  
**Para salvar um projeto**  
  
-   Sobre o **arquivo** menu, selecione **Salvar projeto**.  
  
    Se bancos de dados dentro do projeto foram alteradas ou não tem sido convertidos, SSMA solicitará que você salve os metadados para o projeto. Salvar metadados permite trabalhar offline. Ele também permite enviar um arquivo de projeto completo para outras pessoas, incluindo a equipe de suporte técnico. Se você for solicitado a salvar metadados, faça o seguinte:  
  
    1.  Para cada banco de dados que mostra um status de **metadados ausentes**, marque a caixa de seleção ao lado do nome do banco de dados.  
  
        Salvar metadados pode levar vários minutos. Se você não quiser salvar metadados neste momento, não selecione todas as caixas de seleção.  
  
    2.  Clique em **Salvar**.  
  
        O SSMA analisará os esquemas de acesso e salve os metadados para o arquivo de projeto.  
  
## <a name="opening-projects"></a>Abrindo projetos  
Quando você abre um projeto, ele é desconectado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Isso lhe permite trabalhar offline. Para atualizar objetos de banco de dados de carregamento de metadados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure. Para migrar os dados, você deve reconectar para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do SQL Azure.  
  
**Para abrir um projeto**  
  
1.  Use um dos procedimentos a seguir:  
  
    -   Sobre o **arquivo** , aponte para **projetos recentes**e, em seguida, selecione o projeto que você deseja abrir.  
  
    -   Sobre o **arquivo** menu, selecione **Abrir projeto**, localize o arquivo de projeto .a2ssproj, selecione o arquivo e, em seguida, clique em **abrir**.  
  
2.  Para reconectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], no **arquivo** menu, selecione **reconectar-se ao SQL Server**.  
  
3.  Para reconectar-se ao SQL Azure, no **arquivo** menu, selecione **reconectar-se ao SQL Azure.**  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa no processo de migração é [adicionar um ou mais bancos de dados do Access](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced).  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/en-us/76a3abcf-2998-4712-9490-fe8d872c89ca)  
[Adicionando e removendo arquivos de banco de dados do Access](http://msdn.microsoft.com/en-us/e944c740-4c8a-4bc1-b0ed-be57bc06dced)  
  


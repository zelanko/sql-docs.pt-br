---
title: "Introdução ao Assistente de migração do SQL Server para Access | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 08/15/2017
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
- error list pane
- getting started
- menus
- metadata explorers
- output pane
- toolbars
- user interface
- user interface overview
ms.assetid: 462a731f-08f1-44e1-9eeb-4deac6d2f6c5
caps.latest.revision: 24
author: Shamikg
ms.author: Shamikg
manager: murato
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 846d08c9226e6a34e0d0b3bbd5efab8c2548a469
ms.contentlocale: pt-br
ms.lasthandoff: 09/07/2017

---
# <a name="getting-started-with-sql-server-migration-assistant-for-access-accesstosql"></a>Introdução ao SQL Server Migration Assistant para acesso (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SSMA (Migration Assistant) para acesso permite que você converta rapidamente os objetos de banco de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou objetos de banco de dados de SQL do Azure, carregue os objetos resultantes em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure, e migrar dados de acesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure. Se necessário, também é possível vincular tabelas de acesso para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou tabelas de banco de dados do Azure SQL para que você pode continuar a usar seus aplicativos front-end do Access existentes com [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure.  
  
Este tópico apresenta o processo de instalação e ajuda a se familiarizar com a interface de usuário do SSMA.  
  
## <a name="installing-ssma"></a>Instalando o SSMA  
Para usar o SSMA, primeiro instale o programa de cliente do SSMA em um computador que possa acessar os bancos de dados você deseja migrar e a instância de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure. Para obter instruções de instalação, consulte [instalar o SQL Server Migration Assistant para acesso &#40; AccessToSQL &#41; ](../../ssma/access/installing-sql-server-migration-assistant-for-access-accesstosql.md).  
  
Para iniciar o SSMA, clique em **iniciar**, aponte para **todos os programas**, aponte para **SQL Server Migration Assistant para acesso**e, em seguida, selecione **SQL Server Migration Assistant para acesso**.  
  
## <a name="using-ssma"></a>Usando o SSMA  
Depois de instalar o SSMA, ele ajuda a se familiarizar com a interface de usuário do SSMA antes de usar a ferramenta para migrar bancos de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure. A interface de usuário do SSMA, incluindo os gerenciadores de metadados, metadados, barras de ferramentas, painel de saída e painel de lista de erros são mostrados no diagrama a seguir:  
  
![SSMA para Interface gráfica do usuário de acesso](../../ssma/access/media/ssmaforaccessgui.gif "SSMA para Interface gráfica do usuário de acesso")  
  
Para iniciar uma migração, crie um novo projeto e, em seguida, adicionar bancos de dados de acesso ao Gerenciador de metadados de acesso. Você pode, em seguida, clique com botão direito objetos no Gerenciador de metadados de acesso para executar tarefas como:
- Exportando um inventário dos objetos de banco de dados do Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure.
- Criar relatórios que avaliam conversões para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure.
- Convertendo esquemas de acesso para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou esquemas de banco de dados de SQL do Azure.

Você também pode executar essas tarefas usando os menus e barras de ferramentas.  
  
Você também deve se conectar a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Após uma conexão bem-sucedida, uma hierarquia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bancos de dados aparece na [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados. Depois de converter esquemas de acesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquemas, você pode selecionar esses esquemas convertidos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados e, em seguida, carregar os esquemas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Se você selecionou o banco de dados do Azure SQL de migração para a lista suspensa na caixa de diálogo Novo projeto, você deve se conectar ao banco de dados de SQL do Azure. Após uma conexão bem-sucedida, a hierarquia de bancos de dados do banco de dados do Azure SQL aparece no Gerenciador de metadados de banco de dados de SQL do Azure. Depois de converter esquemas de acesso para esquemas de banco de dados de SQL do Azure, você pode selecionar esses esquemas convertidos no Gerenciador de metadados de banco de dados de SQL do Azure e, em seguida, carregar os esquemas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Depois de carregar esquemas convertidas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure, você pode retornar ao Gerenciador de metadados de acesso e migrar dados de bancos de dados do Access em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou bancos de dados do banco de dados de SQL do Azure. Se necessário, também é possível vincular tabelas de acesso para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou tabelas de banco de dados de SQL do Azure.  
  
Para obter mais informações sobre essas tarefas e como executá-los, consulte os tópicos a seguir:  
  
-   [Preparar bancos de dados do Access para a migração](http://msdn.microsoft.com/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
  
-   [Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
-   [Vinculando a aplicativos de acesso ao SQL Server](http://msdn.microsoft.com/82374ad2-7737-4164-a489-13261ba393d4)  
  
As seções a seguir descrevem os recursos da interface de usuário do SSMA.  
  
### <a name="metadata-explorers"></a>Gerenciadores de metadados  
O SSMA contém dois gerenciadores de metadados que você pode usar para procurar e executar ações em acesso e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou bancos de dados do banco de dados de SQL do Azure.  
  
#### <a name="access-metadata-explorer"></a>Acessar Gerenciador de metadados  
Gerenciador de metadados de acesso mostra informações sobre os bancos de dados do Access que foram adicionados ao projeto. Quando você adiciona um banco de dados, o SSMA recupera metadados sobre esse banco de dados, os metadados que está disponível no Gerenciador de metadados de acesso.  
  
Você pode usar o Gerenciador de metadados de acesso para executar as seguintes tarefas:  
  
-   Procure tabelas em cada banco de dados do Access.  
  
-   Selecionar objetos para a conversão e converter os objetos a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxe. Para obter mais informações, consulte [converter objetos de banco de dados do Access](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c).  
  
-   Selecionar objetos para a migração de dados e migrar os dados desses objetos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obter mais informações, consulte [migrando dados do Access para SQL Server](http://msdn.microsoft.com/f3b18af7-1af0-499d-a00d-a0af94895625).  
  
-   Vincular e desvincular acesso e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tabelas.  
  
#### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server ou o Gerenciador de metadados do banco de dados SQL do Azure  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]ou o Gerenciador de metadados de banco de dados de SQL Azure mostra informações sobre uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure. Quando você se conectar a uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure, o SSMA recupera metadados sobre essa instância e o armazena no arquivo de projeto.  
  
Você pode usar o SQL Server ou o Gerenciador de metadados de banco de dados do Azure SQL para selecionar objetos de banco de dados do Access convertidos e carregar (synchronize) os objetos na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure.  
  
Para obter mais informações, consulte [carregar objetos de banco de dados convertidos para o SQL Server](http://msdn.microsoft.com/4e854eee-b10c-4f0b-9d9e-d92416e6f2ba).  
  
### <a name="metadata"></a>Metadados  
À direita de cada Gerenciador de metadados são guias que descrevem o objeto selecionado. Por exemplo, se você selecionar uma tabela no Gerenciador de metadados de acesso, quatro guias são exibidas: **tabela**, **mapeamento de tipo**, **propriedades**, e **dados**. Se você selecionar uma tabela em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados, três guias são exibidas: **tabela**, **SQL**, e **dados**.  
  
A maioria das configurações de metadados são somente leitura. No entanto, você pode alterar os metadados a seguir:  
  
-   No Gerenciador de metadados de acesso, você pode alterar os mapeamentos de tipo. Certifique-se de fazer essas alterações antes de criar relatórios ou converter esquemas.  
  
-   Em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Gerenciador de metadados, você pode alterar as propriedades de tabela e índice no **tabela** guia. Fazer essas alterações antes de carregar os esquemas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obter mais informações, consulte [converter objetos de banco de dados do Access](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c).  
  
### <a name="toolbars"></a>Barras de Ferramentas  
O SSMA tem duas barras de ferramentas: uma barra de ferramentas do projeto e uma barra de ferramentas de migração.  
  
#### <a name="the-project-toolbar"></a>A barra de ferramentas do projeto  
O projeto contém botões para trabalhar com projetos, adicionando arquivos de banco de dados do Access e conectar-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure. Esses botões lembram os comandos no **arquivo** menu.  
  
#### <a name="the-migration-toolbar"></a>A barra de ferramentas de migração  
A barra de ferramentas de migração contém os seguintes comandos:  
  
|Botão|Função|  
|----------|------------|  
|**Converter, carregar e migrar**|Converte os bancos de dados do Access, carregará objetos convertidos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure, e migra dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou do Azure SQL DB, tudo em uma única etapa.|  
|**Criar relatório**|Converte o esquema de acesso selecionado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou sintaxe de banco de dados de SQL do Azure e, em seguida, cria um relatório que mostra a conversão foi como bem-sucedida.<br /><br />Este comando está disponível somente quando os objetos selecionados no Gerenciador de metadados de acesso.|  
|**Converter esquema**|Converte o esquema selecionado acesso [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou esquemas de banco de dados de SQL do Azure.<br /><br />Este comando está disponível somente quando os objetos selecionados no Gerenciador de metadados de acesso.|  
|**Migrar dados**|Migra os dados do banco de dados Access para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure. Antes de executar esse comando, você deve converter os esquemas de acesso à [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou esquemas de banco de dados de SQL do Azure e, em seguida, carregue os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure.<br /><br />Este comando está disponível somente quando os objetos selecionados no Gerenciador de metadados de acesso.|  
|**Parar**|Interrompe o processo atual, como a conversão de objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou sintaxe de banco de dados de SQL do Azure.|  
  
### <a name="menus"></a>Menus  
O SSMA contém os seguintes menus:  
  
|Menu|Description|  
|--------|---------------|  
|**Arquivo**|Contém comandos para o Assistente de migração, trabalhando com projetos, adicionando e removendo arquivos de banco de dados do Access e conectar-se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou banco de dados de SQL do Azure.|  
|**Editar**|Contém comandos para localizar e trabalhar com texto nas páginas de detalhes, como copiar [!INCLUDE[tsql](../../includes/tsql_md.md)] do painel de detalhes do SQL. Para abrir o **gerenciar indicadores** caixa de diálogo, no menu Editar, clique em Gerenciar indicadores. Na caixa de diálogo, você verá uma lista de indicadores. Você pode usar os botões à direita da caixa de diálogo para gerenciar os indicadores.|  
|**Exibir**|Contém o **sincronizar metadados de pesquisadores** comando. Isso sincroniza os objetos entre o Gerenciador de metadados de acesso e [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ou Gerenciador de metadados de banco de dados de SQL do Azure. Também contém comandos para exibir e ocultar o **saída** e **lista de erros** painéis e uma opção **Layouts** para gerenciar com os Layouts.|  
|**Ferramentas**|Contém comandos para criar relatórios, exportar dados, migrar objetos e dados, tabelas e fornece acesso global e configurações de projeto de caixas de diálogo.|  
|**Ajuda**|Fornece acesso para ajudar o SSMA e para o **sobre** caixa de diálogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Painel de saída e o painel de lista de erros  
O **exibição** menu fornece comandos para alternar a visibilidade do painel de saída e o painel de lista de erros:  
  
-   O painel de saída mostra mensagens de status do SSMA durante a conversão do objeto de sincronização de objetos e migração de dados.  
  
-   O painel de lista de erros mostra erro, aviso e mensagens informativas em uma lista que você pode classificar.  
  
## <a name="see-also"></a>Consulte também  
[Migrando bancos de dados do Access para o SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  


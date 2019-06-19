---
title: Introdução ao SSMA para DB2 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 48ca32fc-1830-4d1f-add7-480ba5ad02e8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 86a931c9132a23d9ceb3d46b48fbdce23bf76f92
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63298860"
---
# <a name="getting-started-with-ssma-for-db2-db2tosql"></a>Introdução ao SSMA para DB2 (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) para DB2 permite que você rapidamente os esquemas de banco de dados do DB2 para converter [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas, carregar os esquemas resultantes em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e migrar dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Este tópico apresenta o processo de instalação e, em seguida, ajuda você a se familiarizar com a interface de usuário do SSMA.  
  
## <a name="installing-ssma"></a>Instalar o SSMA  
Para usar o SSMA, você primeiro deve instalar o programa cliente SSMA em um computador que pode acessar o banco de dados do DB2 de origem e a instância de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Provedores OLE DB do DB2 no computador que está executando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esses componentes oferecem suporte a migração de dados e a emulação de funções de sistema do DB2. Para obter instruções de instalação, consulte [instalar o SSMA para DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md).  
  
Para iniciar o SSMA, clique em **inicie**, aponte para **todos os programas**, aponte para  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant for DB2**e, em seguida, clique em  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Assistente de migração para o DB2**.  
  
## <a name="ssma-for-db2-user-interface"></a>SSMA para Interface de usuário do DB2  
Depois que o SSMA é instalado, você pode usar o SSMA para migrar bancos de dados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ele ajuda a se familiarizar com a interface de usuário do SSMA antes de começar. O diagrama a seguir mostra a interface do usuário para o SSMA, incluindo os gerenciadores de metadados, metadados, barras de ferramentas, painel de saída e painel de lista de erros:  
  
![Interface de usuário do SSMA](../../ssma/db2/media/ssma_db2_ui.png "Interface de usuário do SSMA")  
  
Para iniciar uma migração, você deve primeiro criar um novo projeto. Em seguida, você se conectar a um banco de dados do DB2. Após uma conexão bem-sucedida, os esquemas do DB2 serão exibido no Gerenciador de metadados do DB2. Você pode então objetos do botão direito do mouse no Gerenciador de metadados do DB2 para executar tarefas como criar relatórios que avaliam as conversões para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você também pode executar essas tarefas usando os menus e barras de ferramentas.  
  
Você também deve se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Após uma conexão bem-sucedida, uma hierarquia do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados aparecerão no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados. Depois de converter esquemas do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas, selecione as esquemas convertidas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados e, em seguida, sincronizar os esquemas com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Depois de sincronizar esquemas convertidas com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você pode retornar ao Gerenciador de metadados do DB2 e migrar dados de esquemas do DB2 em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados.  
  
Para obter mais informações sobre essas tarefas e como realizá-las, consulte [migrando bancos de dados do DB2 para o SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md).  
  
As seções a seguir descrevem os recursos da interface do usuário do SSMA.  
  
### <a name="metadata-explorers"></a>Metadata Explorers  
O SSMA contém dois gerenciadores de metadados para procurar e executar ações no DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados.  
  
#### <a name="db2-metadata-explorer"></a>DB2 Metadata Explorer  
Gerenciador de metadados de DB2 mostra informações sobre esquemas do DB2. Usando o Gerenciador de metadados do DB2, você pode executar as seguintes tarefas:  
  
-   Procure os objetos em cada esquema.  
  
-   Selecionar objetos para a conversão e, em seguida, converter os objetos a serem [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe. Para obter mais informações, consulte [converter esquemas do DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md).  
  
-   Selecionar tabelas para migração de dados e, em seguida, migrar os dados dessas tabelas para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [migrando bancos de dados do DB2 para o SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md).  
  
#### <a name="sql-server-metadata-explorer"></a>Gerenciador de metadados do SQL Server  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados mostra informações sobre uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando você se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], SSMA recupera metadados sobre essa instância e o armazena no arquivo de projeto.  
  
Você pode usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados para selecionar objetos de banco de dados convertidos do DB2 e, em seguida, sincronizar esses objetos com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="metadata"></a>Metadados  
À direita de cada Gerenciador de metadados são guias que descrevem o objeto selecionado. Por exemplo, se você selecionar uma tabela no Gerenciador de metadados do DB2, seis guias serão exibida: **Tabela**, **SQL**, **tipo de mapeamento, o relatório**, **propriedades**, e **dados**. O **relatório** guia contém informações somente depois de criar um relatório que contém o objeto selecionado. Se você selecionar uma tabela no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, três guias serão exibida: **Tabela**, **SQL**, e **dados**.  
  
A maioria das configurações de metadados são somente leitura. No entanto, você pode alterar os metadados a seguir:  
  
-   No Gerenciador de metadados do DB2, você pode alterar procedimentos e mapeamentos de tipo. Para converter os procedimentos alterados e mapeamentos de tipo, faça as alterações antes de converter esquemas.  
  
-   Na [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, você pode alterar o [!INCLUDE[tsql](../../includes/tsql-md.md)] para procedimentos armazenados. Para ver essas alterações nas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], faça essas alterações antes de carregar os esquemas em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
As alterações feitas em um Gerenciador de metadados são refletidas nos metadados do projeto, não nos bancos de dados de origem ou destino.  
  
### <a name="toolbars"></a>Barras de Ferramentas  
O SSMA tem duas barras de ferramentas: uma barra de ferramentas do projeto e uma barra de ferramentas de migração.  
  
#### <a name="the-project-toolbar"></a>A barra de ferramentas do projeto  
O projeto contém botões para trabalhar com projetos, conectar ao DB2 e conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esses botões se parecer com os comandos na **arquivo** menu.  
  
#### <a name="migration-toolbar"></a>Barra de ferramentas de migração  
A tabela a seguir mostra a migração de comandos da barra de ferramentas:  
  
|Botão|Função|  
|------|--------|  
|**Criar relatório**|Converte os objetos selecionados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe e, em seguida, cria um relatório que mostra a conversão foi bem-sucedida como.<br /><br />Este comando está desabilitado, a menos que os objetos selecionados no Gerenciador de metadados do DB2.|  
|**Converter esquema**|Converte os objetos selecionados do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos.<br /><br />Este comando está desabilitado, a menos que os objetos selecionados no Gerenciador de metadados do DB2.|  
|**Migrar dados**|Migra dados do banco de dados DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Antes de executar esse comando, você deve converter os esquemas do DB2 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas e, em seguida, carregue os objetos em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].<br /><br />Este comando está desabilitado, a menos que os objetos selecionados no Gerenciador de metadados do DB2.|  
|**Parar**|Interrompe o processo atual.|  
  
### <a name="menus"></a>Menus  
A tabela a seguir mostra os menus do SSMA.  
  
|Menu|Descrição|  
|----|-----------|  
|**File**|Contém comandos para trabalhar com projetos, conectar ao DB2 e conectar-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Editar**|Contém comandos para localizar e trabalhar com texto nas páginas de detalhes, como copiar [!INCLUDE[tsql](../../includes/tsql-md.md)] do painel de detalhes do SQL. Também contém o **gerenciar indicadores** opção, onde você poderá ver uma lista de indicadores atuais. Você pode usar os botões no lado direito da caixa de diálogo para gerenciar os indicadores.|  
|**Exibir**|Contém o **sincronizar metadados Explorers** comando. Que sincroniza os objetos entre o Gerenciador de metadados do DB2 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados. Também contém comandos para mostrar e ocultar os **saída** e **lista de erros** painéis e uma opção **Layouts** para gerenciar os Layouts.|  
|**Ferramentas**|Contém comandos para criar relatórios e migrar dados e objetos. Também fornece acesso para o **configurações globais** e **configurações do projeto** caixas de diálogo.|  
|**Ajuda**|Fornece acesso para ajudar a SSMA e para o **sobre** caixa de diálogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Painel de saída e o painel de lista de erros  
O **exibição** menu fornece comandos para alternar a visibilidade do painel de saída e o painel de lista de erros:  
  
-   O painel de saída mostra mensagens de status do SSMA durante a conversão do objeto de sincronização de objetos e migração de dados.  
  
-   O painel de lista de erros mostra o erro, aviso e mensagens informativas em uma lista classificável.  
  
## <a name="see-also"></a>Consulte também  
[Migrando dados do DB2 para o SQL Server &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
[Referência da Interface do usuário &#40;DB2ToSQL&#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  

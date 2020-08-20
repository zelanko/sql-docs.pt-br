---
description: Carregar objetos de banco de dados convertidos no SQL Server (SybaseToSQL)
title: Carregando objetos de banco de dados convertidos em SQL Server (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Loading Converted Database Objects
ms.assetid: 4c59256f-99a8-4351-9559-a455813dbd06
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 8cf1c6af1a526efe771ccbd3b0f02f35670a1130
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88492158"
---
# <a name="loading-converted-database-objects-into-sql-server-sybasetosql"></a>Carregar objetos de banco de dados convertidos no SQL Server (SybaseToSQL)
Depois de converter objetos de banco de dados ASE (Sybase Adaptive Server Enterprise) no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, você pode carregar os objetos de banco de dados resultantes no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Você pode fazer com que o SSMA crie os objetos, ou pode criar o script dos objetos e executar os scripts por conta própria. Além disso, o SSMA permite que você atualize os metadados de destino com o conteúdo real do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do banco de dados SQL do Azure.  
  
## <a name="choosing-between-synchronization-and-scripts"></a>Escolhendo entre a sincronização e os scripts  
Se você quiser carregar os objetos de banco de dados convertidos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure sem modificação, poderá fazer com que o SSMA crie ou recrie os objetos de banco de dados diretamente. Esse método é rápido e fácil, mas não permite a personalização do [!INCLUDE[tsql](../../includes/tsql-md.md)] código que define os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos ou SQL Azure, além de procedimentos armazenados.  
  
Se você quiser modificar o [!INCLUDE[tsql](../../includes/tsql-md.md)] que é usado para criar os objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, ou se quiser mais controle sobre quando e como os objetos são criados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, use o SSMA para criar [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts. Em seguida, você pode modificar esses scripts, criar cada objeto individualmente e até mesmo usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure agente para agendar a criação desses objetos.  
  
## <a name="using-ssma-to-load-objects-into-sql-server-or-sql-azure"></a>Usando o SSMA para carregar objetos em SQL Server ou SQL Azure  
Para usar o SSMA para criar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou objetos de banco de dados SQL do Azure, você seleciona os objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure Gerenciador de metadados e, em seguida, sincroniza os objetos com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, conforme mostrado no procedimento a seguir. Por padrão, se os objetos já existirem no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure, e se os metadados do SSMA tiverem algumas alterações locais ou atualizações na definição desses objetos, o SSMA alterará as definições de objeto no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure. Você pode alterar o comportamento padrão editando **as configurações do projeto**.  
  
> [!NOTE]  
> Você pode selecionar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] objetos existentes ou do banco de dados SQL do Azure que não foram convertidos de bancos de dados ASE. No entanto, esses objetos não serão recriados ou alterados pelo SSMA.  
  
**Para sincronizar objetos com SQL Server ou SQL Azure**  
  
1.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure Gerenciador de metadados, expanda o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nó superior ou SQL Azure e, em seguida, expanda **bancos de dados**.  
  
2.  Selecione os objetos a serem processados:  
  
    -   Para sincronizar um banco de dados completo, marque a caixa de seleção ao lado do nome do banco de dados.  
  
    -   Para sincronizar ou omitir objetos individuais ou categorias de objetos, marque ou desmarque a caixa de seleção ao lado do objeto ou da pasta.  
  
3.  Depois de selecionar os objetos a serem processados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou SQL Azure o Gerenciador de metadados, clique com o botão direito do mouse em **bancos**de dados e clique em **sincronizar com o Database**.  
  
    Você também pode sincronizar objetos individuais ou categorias de objetos clicando com o botão direito do mouse no objeto ou em sua pasta pai e clicando em  **sincronizar com o banco de dados**.  
  
    Depois disso, o SSMA exibirá a caixa de diálogo **sincronizar com o banco de dados** , onde você poderá ver dois grupos de itens. No lado esquerdo, o SSMA mostra os objetos de banco de dados selecionados representados em uma árvore. No lado direito, você pode ver uma árvore que representa os mesmos objetos em metadados do SSMA. Você pode expandir a árvore clicando no botão à direita ou à esquerda ' + '. A direção da sincronização é mostrada na coluna ação colocada entre as duas árvores.  
  
    Um sinal de ação pode estar em três Estados:  
  
    -   Uma seta para a esquerda significa que o conteúdo dos metadados será salvo no banco de dados (o padrão).  
  
    -   Uma seta para a direita significa que o conteúdo do banco de dados substituirá os metadados do SSMA.  
  
    -   Um sinal cruzado significa que nenhuma ação será executada.  
  
Clique no sinal de ação para alterar o estado. A sincronização real será executada quando você clicar no botão **OK** da caixa de diálogo **sincronizar com Banco de dados** .  
  
## <a name="scripting-objects"></a>Objetos de script  
Se você quiser salvar as [!INCLUDE[tsql](../../includes/tsql-md.md)] definições dos objetos de banco de dados convertidos ou desejar alterar as definições de objeto e executar scripts por conta própria, poderá salvar as definições de objeto de banco de dados convertido em [!INCLUDE[tsql](../../includes/tsql-md.md)] scripts.  
  
**Para salvar objetos como scripts**  
  
1.  Depois de selecionar os objetos a serem salvos em um script, clique com o botão direito do mouse em **bancos de dados**e selecione **salvar como script**.  
  
    Você também pode criar scripts de objetos individuais ou categorias de objetos clicando com o botão direito do mouse no objeto ou na pasta que o contém e, em seguida, selecionando **Salvar script**.  
  
2.  Na caixa de diálogo **salvar como** , localize a pasta onde você deseja salvar o script, insira um nome de arquivo na caixa **nome do arquivo** e clique em **OK**.  
  
    O SSMA acrescentará a extensão de nome de arquivo. Sql.  
  
### <a name="modifying-scripts"></a>Modificando scripts  
Depois de salvar as [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definições de objeto do ou do SQL Azure como um ou mais scripts, você pode usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o para exibir e modificar os scripts.  
  
**Para modificar um script**  
  
1.  No menu [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Arquivo** , aponte para **Abrir**e clique em **Arquivo**.  
  
2.  Na caixa de diálogo **abrir** , navegue até o arquivo de script e selecione-o e clique em **OK**.  
  
3.  Edite e o arquivo de script usando o editor de consultas.  
  
    Para obter mais informações sobre o editor de consultas, consulte "comandos e recursos de conveniência do editor" nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] manuais online do.  
  
4.  Para salvar o script, no menu arquivo, selecione **salvar**.  
  
### <a name="running-scripts"></a>Executando scripts  
Você pode executar um script, ou instruções individuais, no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
**Para executar um script**  
  
1.  No menu [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **Arquivo** , aponte para **Abrir**e clique em **Arquivo**.  
  
2.  Na caixa de diálogo **abrir** , navegue até o arquivo de script e selecione-o e clique em **OK**.  
  
3.  Para executar o script completo, pressione a tecla **F5** .  
  
4.  Para executar um conjunto de instruções, selecione as instruções na janela do editor de consultas e pressione a tecla **F5** .  
  
Para obter mais informações sobre como usar o editor de consultas para executar scripts, consulte " [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] consultar" nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] manuais online do.  
  
Você também pode executar scripts na linha de comando usando o utilitário **sqlcmd** e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para obter mais informações sobre o **sqlcmd**, consulte o "utilitário sqlcmd" nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] manuais online do. Para obter mais informações sobre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, consulte "automatizando tarefas administrativas ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente)" nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] manuais online do.  
  
## <a name="securing-objects-in-sql-server"></a>Protegendo objetos no SQL Server  
Depois de carregar os objetos de banco de dados convertidos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você pode conceder e negar permissões nesses objetos. É uma boa ideia fazer isso antes de migrar dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter informações sobre como ajudar a proteger objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte "considerações de segurança para bancos de dados e aplicativos de banco de dados" nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] manuais online do.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa do processo de migração é [migrar dados de ase do Sybase para SQL Server/SQL Azure (SybaseToSQL)](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811).  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados do Sybase ASE para o SQL Server-banco de SybaseToSQL SQL do Azure &#40;o&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  

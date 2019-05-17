---
title: 'Como fazer: alterar a plataforma de destino e publicar um projeto de banco de dados | Microsoft Docs'
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- sql.data.tools.publish.dialog
- sql.data.tools.publishdacproject
ms.assetid: 6012e120-5f72-4f4f-ae6e-f9a57ae1dea7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 3a95768fd863c7584c98a5135dccef826fabbc56
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65090100"
---
# <a name="how-to-change-target-platform-and-publish-a-database-project"></a>Como fazer: Alterar a plataforma de destino e publicar um projeto de banco de dados
Você pode alterar a versão do SQL Server de destino do projeto de banco de dados SSDT (Ferramentas de dados do SQL Server) para qualquer instância com suporte do SQL Server (SQL Server 2005, 2008, 2008 R2, Microsoft SQL Server 2012 ou SQL Azure). Ao fazer isso, você pode centralizar seu desenvolvimento de banco de dados em um único projeto, mas publicá-lo em várias instâncias do SQL Server de acordo com a necessidade.  
  
O SSDT também simplifica essa tarefa reconhecendo a plataforma de destino e detectando automaticamente qualquer erro no código (por exemplo, quando você está usando recursos sem suporte para um projeto que será publicado no SQL Azure).  
  
> [!WARNING]  
> Os procedimentos a seguir utilizam entidades criadas em procedimentos anteriores nas seções [Desenvolvimento de banco de dados conectado](../ssdt/connected-database-development.md) e [Desenvolvimento de banco de dados offline orientado a projetos](../ssdt/project-oriented-offline-database-development.md).  
  
### <a name="to-change-a-projects-target-platform"></a>Para alterar a plataforma de destino de um projeto  
  
1.  Clique com o botão direito no seu projeto no **Gerenciador de Soluções** e selecione **Propriedades**. Clique na guia **Configurações do Projeto** à esquerda para acessar a página de propriedades **Configurações do Projeto** .  
  
2.  A lista suspensa **Plataforma de destino** nesta página contém todas as plataformas de SQL Server com suporte para as quais um projeto de banco de dados pode ser publicado. Para este procedimento, selecione o **SQL Azure**.  
  
### <a name="to-use-platform-validation-when-editing-scripts"></a>Para usar a validação de plataforma ao editar scripts  
  
1.  Clique com o botão direito do mouse na tabela **Produtos** no Gerenciador de Soluções e selecione **Exibir Código** para abri-lo no Editor Transact\-SQL.  
  
2.  Acrescente `ON [PRIMARY]` ao final da instrução `CREATE TABLE` .  
  
3.  Observe que o erro a seguir aparece no painel **Lista de Erros**:  SQL70015: Não há suporte para 'Esquema de particionamento e referência de grupo de arquivos' no SQL Azure...  
  
    O SSDT valida automaticamente seu script com base na plataforma de destino. Neste caso, como o grupo de arquivos não tem suporte no SQL Azure, o SSDT retorna um erro. Para obter uma lista de instruções do Transact\-SQL sem suporte no SQL Azure, confira [Instruções Transact-SQL com suporte parcial (Banco de Dados SQL do Microsoft Azure)](https://msdn.microsoft.com/library/ee336267.aspx).  
  
4.  Remova a cláusula `ON` . Observe que o erro desaparece imediatamente da **Lista de Erros**.  
  
### <a name="to-publish-a-database-project"></a>Para publicar um projeto de banco de dados  
  
1.  Se você tiver acesso a uma instância do SQL Azure, poderá saltar para a próxima etapa. Caso contrário, clique com o botão direito do mouse no projeto **TradeDev** no **Gerenciador de Soluções** e selecione **Propriedades** para acessar a página de propriedades **Configurações de Projeto**. Use a lista suspensa **Plataforma de destino** para selecionar a plataforma SQL Server na qual você deseja publicar o projeto.  
  
2.  Clique com o botão direito do mouse no projeto **TradeDev** no **Gerenciador de Soluções** e selecione **Publicar**. O SSDT começará a compilar seu projeto. Se não houver nenhum erro de compilação, a caixa de diálogo **Publicar Banco de Dados** será exibida.  
  
3.  Na caixa de diálogo **Publicar Banco de Dados** , clique em **Editar** para editar a Conexão do banco de dados de destino.  
  
4.  Na caixa de diálogo **Propriedades de Conexão**, insira o nome da instância do SQL Server e suas credenciais para autenticação. Em **Conectar a um banco de dados**, insira **NewTrade**. Isso tentará publicar seu projeto de banco de dados em um novo banco de dados. Você também pode escolher um banco de dados existente para o qual publicar. Por exemplo, se você escolher o banco de dados **TradeDev** existente, todas as alterações que você fez nos objetos (como scripts) no projeto **TradeDev** offline serão propagadas para o banco de dados **TradeDev** online.  
  
    Se você tiver permissão para fazer qualquer alteração no banco de dados no qual você deseja publicar, pressione o botão **Publicar** . Porém, se você não tiver acesso para gravação em um banco de dados de produção, poderá clicar no botão **Gerar Script** para produzir um script de publicação do Transact\-SQL, que poderá ser entregue a um DBA. O DBA pode executar o script para atualizar o servidor de produção, de modo que seu esquema esteja sincronizado com o projeto de banco de dados.  
  
5.  A janela **Operações de Ferramentas de Dados**  mostrará o progresso de suas operações de publicação, e o notificará se ocorrerem erros. Nessa nova janela, você também pode optar por exibir a visualização da implantação, o script gerado ou os resultados completos da publicação, se desejado.  
  
6.  Você também pode salvar as configurações de publicação em um perfil, de modo que você possa reutilizar as mesmas configurações para operações de publicação futuras. Para fazer isso, clique no botão **Salvar Perfil como** , na caixa de diálogo **Publicar Banco de Dados** . No futuro, você poderá clicar no botão **Carregar Perfil** quando desejar recarregar configurações existentes.  
  
7.  Observe as mensagens na janela **Operações de Ferramentas de Dados** . Clique no link “Exibir Visualização” à direita de **Criando visualização de publicação...** Isso abrirá o relatório de visualização da implantação. Se a plataforma de destino do seu projeto não for idêntica ao servidor de banco de dados em que o projeto foi publicado, o SSDT emitirá um aviso neste relatório.  Por exemplo, se a plataforma de destino do projeto for o Microsoft SQL Server 2012 e você estiver tentando publicar o projeto em uma instância do servidor SQL Server 2008 R2, você verá o seguinte aviso na janela de **Saída**:  
  
**Um projeto que especifica o Microsoft SQL Server 2012 como a plataforma de destino pode enfrentar problemas de compatibilidade com o SQL Server 2008**   Se tal projeto contiver entidades (por exemplo, um objeto Sequence) introduzidas no Microsoft SQL Server 2012, a operação de publicação falhará.  
  
    The deployment will fail if object predicates use **CONTAINS** or **FREETEXT** over a newly created full-text index and transactional scripts are used. If the option to include transactional scripts is enabled during deployment, then procedures and views are defined inside a transaction while a full-text index is defined outside of a transaction at the end of the deploy script. Because of this ordering in the script, procedures or views using CONTAINS or FREETEXT will not be resolved against the full-text index, resulting in a deployment error.  
  

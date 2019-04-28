---
title: Conceitos dos objetos de gerenciamento de replicação | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- replication [SQL Server], RMO
- programming interfaces [SQL Server replication]
- replication [SQL Server], how-to topics
- RMO [SQL Server]
- Replication Management Objects
- programming [SQL Server replication], RMO
ms.assetid: 37476d50-fb47-49e3-9504-3b163ac381d8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2cbc3571aa26728fa94957bb0c2f207ff769f4c4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721788"
---
# <a name="replication-management-objects-concepts"></a>Replication Management Objects Concepts
  O RMO (Replication Management Objects) é um assembly de código gerenciado que encapsula funcionalidades de replicação para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O RMO é implementado pelo namespace <xref:Microsoft.SqlServer.Replication>.  
  
 Os tópicos das seções a seguir descrevem como você pode usar o RMO para controlar as tarefas de replicação de forma programática.  
  
 [Configurar Distribuição](../configure-distribution.md)  
 Os tópicos desta seção mostram como usar o RMO para configurar a publicação e a distribuição.  
  
 [Create a Publication](../publish/create-a-publication.md)  
 Os tópicos desta seção mostram como usar o RMO para criar, excluir e modificar publicações e artigos.  
  
 [Assinar publicações](../subscribe-to-publications.md)  
 Os tópicos desta seção mostram como usar o RMO para criar, excluir e modificar assinaturas.  
  
 [Proteger uma topologia de replicação](../security/view-and-modify-replication-security-settings.md)  
 Os tópicos desta seção mostram como usar o RMO para exibir e modificar configurações de segurança.  
  
 [Sincronizar assinaturas &#40;replicação&#41;](../synchronize-data.md)  
 Os tópicos desta seção mostram como sincronizar assinaturas.  
  
 [Monitorando a Replicação](../monitoring-replication.md)  
 Os tópicos desta seção mostram como monitorar uma topologia de replicação programaticamente.  
  
## <a name="introduction-to-rmo-programming"></a>Introdução à programação RMO  
 O RMO é criado para a programação de todos os aspectos da replicação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O namespace RMO é <xref:Microsoft.SqlServer.Replication> e é implementado pelo Microsoft.SqlServer.Rmo.dll, um assembly [!INCLUDE[msCoName](../../../includes/msconame-md.md)] do .NET Framework. O assembly Microsoft.SqlServer.Replication.dll, que também pertence ao namespace <xref:Microsoft.SqlServer.Replication>, implementa uma interface de código gerenciado para a programação de vários agentes de replicação (Snapshot Agent, Distribution Agent e Merge Agent). Suas classes podem ser acessadas do RMO para a sincronização de assinaturas. As classes do namespace <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>, implementadas pelo assembly Microsoft.SqlServer.Replication.BusinessLogicSupport.dll, são usadas na criação de lógica de negócios personalizada para replicação de mesclagem. Esse assembly é independente do RMO.  
  
## <a name="deploying-applications-based-on-rmo"></a>Implantando aplicativos baseados em RMO  
 O RMO depende dos componentes de replicação e de conectividade de cliente incluídos em todas as versões do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], exceto no SQL Server Compact. Para implantar um aplicativo baseado em RMO, instale uma versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que inclui componentes de replicação e de conectividade de cliente no computador em que o aplicativo será executado.  
  
## <a name="getting-started-with-rmo"></a>Introdução ao RMO  
 Esta seção descreve como começar um projeto simples de RMO usando o Visual Studio do [!INCLUDE[msCoName](../../../includes/msconame-md.md)].  
  
#### <a name="to-create-a-new-microsoft-visual-c-project"></a>Para criar um novo projeto do Microsoft Visual C#  
  
1.  Inicie o Visual Studio.  
  
2.  No menu **Arquivo**, clique em **NewProject.** A caixa de diálogo **Novo Projeto** será exibida.  
  
3.  Na caixa de diálogo **Tipos de Projeto**, selecione **Projetos do Visual C#**. No painel **Modelos**, selecione **Aplicativos do Windows**.  
  
4.  (Opcional) Em **Nome**, digite o nome do novo aplicativo.  
  
5.  Clique em **OK** para carregar o modelo do Windows do Visual C#.  
  
6.  No menu **Projeto**, selecione o item **Adicionar Referência**. A caixa de diálogo **Adicionar Referência** é exibida.  
  
7.  Selecione os assemblies a seguir na lista da guia **.NET** e clique em **OK**.  
  
    -   Interface de programação .NET Microsoft.SqlServer.Replication  
  
    -   Microsoft.SqlServer.ConnectionInfo  
  
    -   Biblioteca de agentes de replicação  
  
    > [!NOTE]  
    >  Use a tecla CTRL para selecionar mais de um arquivo.  
  
8.  (Opcional) Repita a etapa 6. Clique na guia **Procurar**, navegue para [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM, selecione Microsoft.SqlServer.Replication.BusinessLogicSupport.dll e clique em **OK**.  
  
9. No menu **Exibir** , clique em **Código**.  
  
10. No código, antes da instrução do namespace, digite as instruções `using` a seguir para qualificar os tipos nos namespaces RMO:  
  
    ```  
    // These namespaces are required.  
    using Microsoft.SqlServer.Replication;  
    using Microsoft.SqlServer.Management.Common;  
    // This namespace is only used when creating custom business  
    // logic for merge replication.  
    using Microsoft.SqlServer.Replication.BusinessLogicSupport;   
    ```  
  
#### <a name="to-create-a-new-microsoft-visual-basic-net-project"></a>Para criar um novo projeto do Microsoft Visual Basic .NET  
  
1.  Inicie o Visual Studio.  
  
2.  No menu **Arquivo**, selecione **Novo Projeto**. A caixa de diálogo **Novo Projeto** será exibida.  
  
3.  No painel Tipos de Projeto, selecione **Visual Basic**. No painel Modelos, selecione **Aplicativos do Windows**.  
  
4.  (Opcional) Na caixa **Nome**, digite o nome do novo aplicativo.  
  
5.  Clique em **OK** para carregar o modelo do Windows do Visual Basic.  
  
6.  No menu **Projeto**, selecione **Adicionar Referência**. A caixa de diálogo **Adicionar Referência** é exibida.  
  
7.  Selecione os assemblies a seguir na lista da guia **.NET** e clique em **OK**.  
  
    -   Interface de programação .NET Microsoft.SqlServer.Replication  
  
    -   Microsoft.SqlServer.ConnectionInfo  
  
    -   Biblioteca de agentes de replicação  
  
    > [!NOTE]  
    >  Use a tecla CTRL para selecionar mais de um arquivo.  
  
8.  (Opcional) Repita a etapa 6. Clique na guia **Procurar**, navegue para [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM, selecione Microsoft.SqlServer.Replication.BusinessLogicSupport.dll e clique em **OK**.  
  
9. No menu **Exibir** , clique em **Código**.  
  
10. No código, antes de qualquer instrução, digite as instruções `Imports` a seguir para qualificar os tipos nos namespaces RMO.  
  
    ```  
    ' These namespaces are required.  
    Imports Microsoft.SqlServer.Replication  
    Imports Microsoft.SqlServer.Management.Common  
    ' This namespace is only used when creating custom business  
    ' logic for merge replication.  
    Imports Microsoft.SqlServer.Replication.BusinessLogicSupport   
    ```  
  
## <a name="connecting-to-a-replication-server"></a>Conectando a um servidor de replicação  
 Os objetos de programação RMO exigem que uma conexão a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] seja feita por meio de uma instância da classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. Essa conexão ao servidor é feita de forma independente de qualquer objeto da programação RMO. Então, ela é passada para o objeto RMO, seja durante a criação da instância, seja pela atribuição à propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> do objeto. Dessa maneira, um objeto de programação de RMO e as instâncias de objeto de conexão podem ser criados e gerenciados separadamente, e um único objeto de conexão pode ser reutilizado com vários objetos de programação de RMO. As regras a seguir se aplicam a conexões com um servidor de replicação:  
  
-   Todas as propriedades da conexão são definidas para um determinado objeto de <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
-   Uma conexão com cada instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] precisa ter seu próprio objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
-   O objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> é atribuído à propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> do objeto da programação RMO criado ou acessado no servidor.  
  
-   O método <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A> abre a conexão ao servidor. Esse método deve ser chamado antes da chamada a qualquer método que acesse o servidor em qualquer objeto da programação RMO que usa a conexão.  
  
-   Como o RMO e o SMO do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usam a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> para conexões ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a mesma conexão poderá ser usada por objetos RMO e SMO. Para obter mais informações, consulte [Conectando a uma instância do SQL Server](../../server-management-objects-smo/create-program/connecting-to-an-instance-of-sql-server.md).  
  
-   Todas as informações sobre autenticação para estabelecer com êxito a conexão e o logon no servidor são fornecidas no objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>.  
  
-   A Autenticação do Windows é o padrão. Para usar a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.LoginSecure%2A> deve ser definido como `false` e <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Login%2A> e <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.Password%2A> deve ser definido como um logon e uma senha do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] válidos. As credenciais de segurança sempre deverão ser armazenadas e manipuladas com segurança, além de serem fornecidas em tempo de execução quando possível.  
  
-   Para aplicativos multithreaded, um objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> separado deveria ser usado em cada thread.  
  
 Chame o método <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> no objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> para fechar conexões de servidor ativas usadas por objetos RMO.  
  
## <a name="setting-rmo-properties"></a>Definindo propriedades RMO  
 As propriedades de objetos da programação RMO representam as propriedades desses objetos de replicação no servidor. Durante a criação de novos objetos de replicação no servidor, serão usadas propriedades RMO em sua definição. Para objetos existentes, as propriedades RMO representam as propriedades do objeto existente, que só poderão ser modificadas para as propriedades passíveis de escrita ou configuração. As propriedades só podem ser definidas em objetos novos ou em objetos existentes.  
  
### <a name="setting-properties-for-new-replication-objects"></a>Definindo propriedades para objetos de replicação novos  
 Durante a criação de um novo objeto de replicação no servidor, será preciso especificar todas as propriedades exigidas antes de chamar o método `Create` do objeto. Para obter mais informações sobre como definir propriedades para um novo objeto de replicação, consulte [Configurar a publicação e a distribuição](../configure-publishing-and-distribution.md).  
  
### <a name="setting-properties-for-existing-replication-objects"></a>Definindo propriedades para objetos de replicação existentes  
 Para objetos de replicação existentes no servidor, dependendo do objeto, o RMO poderia oferecer suporte à capacidade de alterar algumas ou todas as suas propriedades. Somente as propriedades passíveis de escrita ou configuração podem ser alteradas. Antes de alterar as propriedades, chame o método `Load` ou o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades atuais do servidor. Chamar esses métodos indica que um objeto existente está sendo modificado.  
  
 Por padrão, ao alterar propriedades do objeto, o RMO confirma essas alterações no servidor com base no modo de execução do <xref:Microsoft.SqlServer.Management.Common.ServerConnection> usado. O método <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> pode ser usado para verificar a existência de um objeto no servidor antes da tentativa de recuperação ou de alteração de suas propriedades. Para obter mais informações sobre como alterar as propriedades de um objeto de replicação, consulte [Exibir e modificar as propriedades do Distribuidor e do Publicador](../view-and-modify-distributor-and-publisher-properties.md).  
  
> [!NOTE]  
>  Quando vários clientes RMO ou várias instâncias de um objeto da programação RMO estiverem acessando o mesmo objeto de replicação no servidor, o método `Refresh` do objeto RMO poderá ser chamado para atualizar as propriedades com base no estado atual do objeto no servidor.  
  
### <a name="caching-property-changes"></a>Armazenando alterações de propriedade em cache  
 Quando a propriedade <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes> é definida como <xref:Microsoft.SqlServer.Management.Common.SqlExecutionModes.CaptureSql>, todas as instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] geradas pelo RMO são capturadas para que possam ser executadas manualmente em um único lote usando um dos métodos de execução. O RMO permite que você armazene alterações de propriedade em cache e confirme-as em um único lote usando o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> do objeto. Para armazenar as alterações de propriedade em cache, a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> do objeto deve ser definida como `true`. Durante o armazenamento das alterações de propriedade em cache no RMO, o objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection> ainda controlará o momento em que as alterações serão enviadas ao servidor. Para obter mais informações sobre como armazenar em cache as alterações de propriedade de um objeto de replicação, consulte [Exibir e modificar as propriedades do Distribuidor e do Publicador](../view-and-modify-distributor-and-publisher-properties.md).  
  
> [!IMPORTANT]  
>  Embora a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> ofereça suporte à declaração explícita de transações durante a configuração de propriedades, tais transações poderão interferir em transações internas de replicação, poderão gerar resultados inesperados e não deverão ser usadas com RMO.  
  
## <a name="example"></a>Exemplo  
 Este exemplo demonstra o cache de alterações de propriedade. As alterações feitas nos atributos de uma publicação transacional são armazenadas em cache até serem explicitamente enviadas ao servidor.  
  
 [!code-csharp[HowTo#rmo_ChangeTranPub_cached](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_ChangeTranPub_cached)]  
  
## <a name="see-also"></a>Consulte também  
 [Replication System Stored Procedures Concepts](replication-system-stored-procedures-concepts.md)   
 [Conceitos de programação da replicação](replication-programming-concepts.md)  
  
  

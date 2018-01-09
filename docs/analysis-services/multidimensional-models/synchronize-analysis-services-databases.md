---
title: Sincronizar bancos de dados do Analysis Services | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Analysis Services deployments, Synchronize Database Wizard
- deploying [Analysis Services], Synchronize Database Wizard
- Synchronize Database Wizard
- synchronization [Analysis Services]
ms.assetid: 6aeff68d-8470-43fb-a3ed-a4b9685332c2
caps.latest.revision: "40"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 3bb86dbcb264f7073847cce62dc9c3e200208821
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="synchronize-analysis-services-databases"></a>Sincronizar bancos de dados do Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] inclui um recurso de sincronização de banco de dados que torna dois [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bancos de dados equivalentes copiando os dados e metadados de um banco de dados em um servidor de origem para um banco de dados em um servidor de destino. Use o recurso Sincronizar Banco de Dados para realizar as tarefas a seguir:  
  
-   Implantar um banco de dados de um servidor de preparo em um servidor de produção.  
  
-   Atualize um banco de dados em um servidor de produção com as alterações feitas aos dados e metadados em um banco de dados em um servidor de preparo.  
  
-   Gerar o script XMLA que pode ser executado posteriormente para sincronizar os bancos de dados.  
  
-   Em cargas de trabalho distribuídas em que os cubos e dimensões são processados em vários servidores, use a sincronização de banco de dados para mesclar as alterações em um único banco de dados.  
  
 A sincronização de banco de dados é iniciada no servidor de destino, efetuando pull de dados e metadados para uma cópia do banco de dados no servidor de origem. Se o banco de dados não existir, será criado. A sincronização é uma operação unidirecional única, concluída assim que o banco de dados é copiado. Ela não oferece uma paridade em tempo real entre os bancos de dados.  
  
 Você pode sincronizar novamente bancos de dados que já existam em servidores de origem e de destino para efetuar pull das alterações mais recentes de um servidor de preparo para um banco de dados de produção. Os arquivos nos dois servidores serão comparados em relação a alterações e os que forem diferentes serão atualizados. Um banco de dados existente em um servidor de destino permanece disponível enquanto a sincronização ocorre em segundo plano. Os usuários poderão continuar a consultar o banco de dados de destino enquanto a sincronização estiver em andamento. Após a conclusão da sincronização, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] alternará automaticamente os usuários para os dados e metadados recém-copiados e descartará os dados antigos do banco de dados de destino.  
  
 Para sincronizar bancos de dados, execute o Assistente para Sincronizar Banco de Dados para sincronizar imediatamente os bancos de dados, ou use-o para gerar um script de sincronização que possa ser executado posteriormente. Qualquer abordagem pode ser usada para aumentar a disponibilidade e a escalabilidade de seus bancos de dados e seu cubo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
> [!NOTE]  
>  Os whitepapers a seguir, escritos para versões anteriores do Analysis Services, ainda se aplicam às soluções multidimensionais escalonáveis criadas usando o SQL Server 2012. Para obter mais informações, consulte [Consulta em expansão com o Analysis Services](http://go.microsoft.com/fwlink/?LinkId=253136) e [Expansão de consulta para o Analysis Services com bancos de dados somente leitura](http://go.microsoft.com/fwlink/?LinkId=253137.)  
  
## <a name="prerequisites"></a>Prerequisites  
 No servidor de destino do qual a sincronização do banco de dados é iniciada, você deve ser membro da função de administrador de servidor do Analysis Services. No servidor de origem, sua conta de usuário do Windows deve ter permissões de Controle Total no banco de dados de origem. Se você estiver sincronizando o banco de dados interativamente, lembre-se de que a sincronização é executada no contexto de segurança de sua identidade de usuário do Windows. Se sua conta tiver acesso negado a objetos específicos, os objetos serão excluídos da operação. Para obter mais informações sobre as funções de administrador do servidor e as permissões de banco de dados, consulte [Conceder direitos de administração de servidor a uma instância do Analysis Services](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md) e [Conceder permissões de banco de dados &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md).  
  
 A porta TCP 2383 deve estar aberta em ambos os servidores para permitir conexões remotas entre instâncias padrão. Para obter mais informações sobre a criação de uma exceção no Firewall do Windows, consulte [Configure the Windows Firewall to Allow Analysis Services Access](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
 Servidores de origem e de destino devem ser a mesma versão e o service pack. Porque os metadados do modelo é sincronizado, para garantir a compatibilidade de compilação número para ambos os servidores deve ser o mesmo. A edição de cada instalação deve oferecer suporte à sincronização de banco de dados. No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], a sincronização do banco de dados tem suporte nas edições enterprise, developer e business intelligence. Para obter mais informações sobre os recursos em cada edição, consulte [edições e os recursos com suporte para SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 O modo de implantação de servidor deve ser idêntico em cada servidor. Se o banco de dados que você estiver sincronizando for multidimensional, os servidores de origem e de destino deverão ser configurados no modo de servidor multidimensional. Para obter mais informações sobre modos de implantação, consulte [Determine the Server Mode of an Analysis Services Instance](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md).  
  
 Desative o processamento de agregação lento se ele estiver em uso no servidor de origem. As agregações que estão sendo processadas em segundo plano podem interferir na sincronização de banco de dados. Para obter mais informações sobre como definir esta propriedade de servidor, consulte [OLAP Properties](../../analysis-services/server-properties/olap-properties.md).  
  
> [!NOTE]  
>  O tamanho do banco de dados é um fator para determinar se a sincronização é uma abordagem adequada. Não há requisitos de hardware, mas se a sincronização estiver muito lenta, considere a sincronização de vários servidores em paralelo, como descrito neste artigo técnico: [Práticas recomendadas de sincronização do Analysis Services](http://go.microsoft.com/fwlink/?LinkID=253136).  
  
## <a name="synchronize-database-wizard"></a>Assistente para Sincronizar Banco de Dados  
 Use o Assistente para Sincronizar Banco de Dados para executar a sincronização unidirecional de um banco de dados de origem para um de destino ou para gerar um script que especifique uma operação de sincronização de banco de dados. Você pode sincronizar partições locais e remotas durante o processo de sincronização e optar ou não por incluir funções.  
  
 O Assistente para Sincronizar Bancos de Dados fornece instruções para as seguintes etapas:  
  
-   Selecione a instância e o banco de dados de origem dos quais sincronizar.  
  
-   Selecionar os locais de armazenamento para partições locais na instância de destino.  
  
-   Selecionar locais de armazenamento para partições remotas em outras instâncias de destino.  
  
-   Selecionar o nível de segurança e informações de associação a serem copiadas da instância e do banco de dados de origem para a instância de destino.  
  
-   Selecione se deseja sincronizar imediatamente ou salvar o comando **Sincronizar** do XMLA (XML for Analysis) gerado pelo Assistente para Sincronizar Banco de Dados em um arquivo de script para sincronização posterior.  
  
 Por padrão, o assistente sincroniza todos os dados e metadados, em vez de associá-los nos grupos de segurança existentes. Também é possível copiar todas as configurações de segurança ou ignorá-las ao sincronizar os dados e metadados.  
  
#### <a name="run-the-wizard"></a>Executar o assistente  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que executará o banco de dados de destino. Por exemplo, se você estiver implantando um banco de dados em um servidor de produção, executará o assistente no servidor de produção.  
  
2.  No Pesquisador de Objetos, clique com o botão direito do mouse na pasta **Bancos de Dados** e clique em **Sincronizar**.  
  
3.  Especifique o servidor de origem e o banco de dados de origem. Na página Selecionar Banco de Dados para Sincronização, em **Servidor de Origem** e em **Banco de Dados de Origem**, digite o nome do servidor de origem e do banco de dados de origem. Por exemplo, se você estiver implantando de um ambiente de teste para um servidor de produção, a origem será o banco de dados do servidor de preparo.  
  
     **Servidor de Destino** exibe o nome da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] com a qual os dados e metadados do banco de dados selecionado em **Banco de dados de origem** são sincronizados.  
  
     A sincronização ocorrerá para bancos de dados de origem e destino que têm o mesmo nome. Se o servidor de destino já tiver um banco de dados que compartilha o mesmo nome que o banco de dados de origem, o banco de dados de destino será atualizado com os metadados e os dados de origem. Se o banco de dados não existir, ele será criado no servidor de destino.  
  
4.  Se preferir, altere a localização da partição local. Use a página **Especificar Locais para Partições Locais** para indicar onde as partições locais devem ser armazenadas no servidor de destino.  
  
    > [!NOTE]  
    >  Esta página será exibida apenas se pelo menos uma partição local existir no banco de dados especificado.  
  
     Se um conjunto de partições estiver instalado na unidade C do servidor de origem, o assistente permite copiar esse conjunto em um local diferente no servidor de destino. Se os locais padrão não forem alterados, o assistente implantará as partições do grupo de medidas de cada cubo do servidor de origem nos mesmos locais no servidor de destino. Do mesmo modo, se o servidor de origem usar partições remotas, as mesmas partições remotas serão usadas no servidor de destino.  
  
     A opção **Locais** exibe uma grade que lista a pasta de origem, a pasta de destino e o tamanho estimado das partições locais a serem armazenadas na instância de destino. A grade contém as seguintes colunas:  
  
     **Pasta de Origem**  
     Exibe o nome da pasta na instância de origem do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contém a partição local. Se a coluna contiver o valor "(Padrão)", o local padrão da instância de origem conterá a partição local.  
  
     **Pasta de Destino**  
     Exibe o nome da pasta na instância de destino do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na qual a partição local deve ser sincronizada. Se a coluna contiver o valor "(Padrão)", o local padrão da instância de destino conterá a partição local.  
  
     Clique no botão de reticências (**...**) para exibir a caixa de diálogo **Procurar Pasta Remota** e especifique uma pasta na instância de destino na qual as partições locais armazenadas no local selecionado devem ser sincronizadas.  
  
    > [!NOTE]  
    >  Essa coluna não pode ser alterada para partições locais armazenadas no local padrão da instância de origem.  
  
     **Tamanho**  
     Exibe o tamanho estimado da partição local.  
  
     A opção **Partições no local selecionado** exibe uma grade que descreve as partições locais armazenadas no local da instância de origem do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especificadas na coluna **Pasta de Origem** da linha selecionada em **Locais**.  
  
     **Cube**  
     Exibe o nome do cubo que contém a partição.  
  
     **Grupo de Medidas**  
     Exibe o nome do grupo de medidas no cubo que contém a partição.  
  
     **Nome da Partição**  
     Exibe o nome da partição.  
  
     **Tamanho(Mb)**  
     Exibe o tamanho, em MB (megabytes), da partição.  
  
5.  Opcionalmente, altere a localização de partições remotas. Use a página **Especificar Locais para Partições Remotas** para indicar se partições remotas gerenciadas pelo banco de dados especificado no servidor de origem devem ser sincronizadas e para especificar uma instância e um banco de dados de destino do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em que as partições remotas selecionadas devem ser armazenadas.  
  
    > [!NOTE]  
    >  Essa página só será exibida se pelo menos uma partição remota for gerenciada pelo banco de dados especificado na instância de origem do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
     A opção **Locais** exibe uma grade que lista detalhes sobre os locais nos quais partições remotas do banco de dados de origem são armazenadas, incluindo informações sobre a origem, o destino e o tamanho do armazenamento usado por cada local, disponíveis no banco de dados selecionado. A grade contém as seguintes colunas:  
  
     **Sincronizar**  
     Selecione para incluir um local que contém as partições remotas durante a sincronização.  
  
    > [!NOTE]  
    >  Se essa opção não estiver selecionada para um local, as partições remotas contidas naquele local não serão sincronizadas.  
  
     **Servidor de Origem**  
     Exibe o nome da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contém as partições remotas.  
  
     **Pasta de Origem**  
     Exibe o nome da pasta na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contém as partições remotas. Se a coluna contiver o valor "(Padrão)", o local padrão da instância exibida em **Servidor de Origem** conterá partições remotas.  
  
     **Servidor de Destino**  
     Exibe o nome da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na qual as partições remotas armazenadas no local especificado em **Servidor de Origem** e **Pasta de Origem** devem ser sincronizadas.  
  
     Clique no botão de reticências (**...**) para exibir a caixa de diálogo **Gerenciador de Conexões** e especifique uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na qual as partições remotas armazenadas no local selecionado devem ser sincronizadas.  
  
     **Pasta de Destino**  
     Exibe o nome da pasta na instância de destino do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] na qual a partição remota deve ser sincronizada. Se a coluna contiver o valor "(Padrão)", o local padrão da instância de destino deverá conter a partição remota.  
  
     Clique no botão de reticências (**...**) para exibir a caixa de diálogo **Procurar Pasta Remota** e especifique uma pasta na instância de destino na qual as partições remotas armazenadas no local selecionado devem ser sincronizadas.  
  
     **Tamanho**  
     Exibe o tamanho estimado de partições remotas armazenadas no local.  
  
     A opção **Partições no local selecionado** exibe uma grade que descreve as partições remotas armazenadas no local na instância de origem do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] especificada na coluna **Pasta de Origem** da linha selecionada em **Locais**. A grade contém as seguintes colunas:  
  
     **Cube**  
     Exibe o nome do cubo que contém a partição.  
  
     **Grupo de Medidas**  
     Exibe o nome do grupo de medidas no cubo que contém a partição.  
  
     **Nome da Partição**  
     Exibe o nome da partição.  
  
     **Tamanho(Mb)**  
     Exibe o tamanho, em MB (megabytes), da partição.  
  
6.  Especifique se as informações de permissão do usuário devem ser incluídas e se a compactação deve ser usada. Por padrão, o assistente compacta todos os dados e metadados antes de copiar os arquivos para o servidor de destino. Essa opção resulta em uma transmissão de arquivo mais rápida. Os arquivos são descompactados assim que chegam ao servidor de destino.  
  
     **Copiar tudo**  
     Selecione para incluir definições de segurança e informações de associação durante a sincronização.  
  
     **Ignorar associação**  
     Selecione para incluir definições de segurança, mas excluir informações de associação durante a sincronização.  
  
     **Ignorar tudo**  
     Selecione para ignorar a definição de segurança e as informações de associação que estejam atualmente no banco de dados de origem. Se um banco de dados de destino for criado durante a sincronização, nenhuma definição de segurança ou informação de associação será copiada. Se o banco de dados de destino já existir e tiver funções e associações, essas informações de segurança serão preservadas.  
  
7.  Escolha o método de sincronização. Você pode sincronizar imediatamente ou gerar um script que será salvo em um arquivo. Por padrão, o arquivo é salvo com uma extensão .xmla e colocado na pasta Documentos.  
  
8.  Clique em **Concluir** para sincronizar. Depois de verificar as opções na página **Concluindo o Assistente** , clique em **Concluir** novamente.  
  
## <a name="next-steps"></a>Next Steps  
 Se você não sincronizou funções ou associação, lembre-se de especificar agora as permissões de acesso de usuário no banco de dados de destino.  
  
## <a name="see-also"></a>Consulte Também  
 [Elemento Synchronize &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md)   
 [Implantar soluções de modelo usando XMLA](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)   
 [Implantar soluções de modelo usando o Assistente de implantação](../../analysis-services/multidimensional-models/deploy-model-solutions-using-the-deployment-wizard.md)  
  
  

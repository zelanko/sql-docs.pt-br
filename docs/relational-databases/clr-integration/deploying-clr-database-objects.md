---
title: Implantando objetos de banco de dados CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- deployment script [CLR integration]
- common language runtime [SQL Server], deploying
- deploying assemblies [CLR integration]
- deploying [CLR integration]
ms.assetid: 00752573-3367-41a7-af98-7b7a29e8e2f2
author: rothja
ms.author: jroth
ms.openlocfilehash: e82705236ec04c5618a4b43526078a6c218ceef9
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/25/2019
ms.locfileid: "72908678"
---
# <a name="deploying-clr-database-objects"></a>Implantando objetos de banco de dados CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Implantação é o processo pelo qual você distribui um aplicativo concluído ou módulo a ser instalado e executado em outro computador. Usando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio, é possível desenvolver objetos de banco de dados do CLR (Common Language Runtime) e implantá-los em um servidor de teste. Os objetos de banco de dados gerenciados também podem ser compilados com os arquivos de redistribuição do [!INCLUDE[msCoName](../../includes/msconame-md.md)].NET Framework, e não o Visual Studio. Quando compilados, os assemblies que contêm os objetos de banco de dados do CLR podem ser implantados em um servidor de teste que usa o Visual Studio ou as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. Observe que o Visual Studio .NET 2003 não pode ser usado na programação de integração ou no desenvolvimento do CLR. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece o .NET Framework pré-instalado, e o Visual Studio .NET 2003 não pode usar os assemblies do .NET Framework 2.0.  
  
 Quando testados e verificados no servidor de teste, os métodos do CLR podem ser distribuídos para servidores de produção usando um script de implantação. O script de implantação pode ser gerado manualmente ou usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (consulte o procedimento posteriormente neste tópico).  
  
 O recurso de integração CLR permanece desativado por padrão no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e deve ser habilitado para usar assemblies CLR. Para obter mais informações, consulte [Enabling CLR Integration](../../relational-databases/clr-integration/clr-integration-enabling.md).  
  
## <a name="deploying-the-assembly-to-the-test-server"></a>Implantando o assembly no servidor de teste  
 Usando o Visual Studio, é possível desenvolver funções, procedimentos, gatilhos, UDTs (tipos definidos pelo usuário) ou UDAs (agregações definidas pelo usuário) e implantá-los em um servidor de teste. Os objetos de banco de dados gerenciados também podem ser compilados com os compiladores de linha de comando como, por exemplo, csc.exe e vbc.exe, incluídos nos arquivos de redistribuição do .NET Framework. O ambiente de desenvolvimento integrado do Visual Studio não é obrigatório para desenvolver objetos de banco de dados gerenciados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Verifique se todos os erros e avisos do compilador são resolvidos. Dessa forma, os assemblies que contêm as rotinas do CLR podem ser registrados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usa o Visual Studio ou as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!NOTE]  
>  O protocolo de rede TCP/IP deve estar habilitado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio seja usado no desenvolvimento remoto, na depuração e no desenvolvimento. Para obter mais informações sobre como habilitar o protocolo TCP/IP no servidor, consulte [Configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md).  
  
#### <a name="to-deploy-the-assembly-using-visual-studio"></a>Para implantar o assembly que usa o Visual Studio  
  
1.  Crie o projeto selecionando **criar** \<nome do projeto > no menu **Compilar** .  
  
2.  Resolva todos os erros de compilação e avisos antes de implantar o assembly no servidor de teste.  
  
3.  Selecione **implantar** no menu **Compilar** . O assembly será registrado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e no banco de dados especificado quando o projeto do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi criado inicialmente no Visual Studio.  

#### <a name="to-deploy-the-assembly-using-transact-sql"></a>Para implantar o assembly que usa Transact-SQL  
  
1.  Compile o assembly no arquivo de origem que usa os compiladores de linha de comando incluídos no .NET Framework.  
  
2.  Em arquivos de origem do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#:  
  
3.  `csc /target:library C:\helloworld.cs`  
  
4.  Em arquivos de origem do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic:  
  
 `vbc /target:library C:\helloworld.vb`  
  
 Esses comandos iniciam o C# compilador Visual ou Visual Basic usando a opção **/target** para especificar a criação de uma DLL de biblioteca.  
  
1.  Resolva todos os erros de compilação e avisos antes de implantar o assembly no servidor de teste.  
  
2.  Abra o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] no servidor de teste. Crie uma consulta nova, conectada a um banco de dados de teste correspondente (como, por exemplo, AdventureWorks).  
  
3.  Crie o assembly no servidor, adicionando a seguinte [!INCLUDE[tsql](../../includes/tsql-md.md)] à consulta.  
  
 `CREATE ASSEMBLY HelloWorld from 'c:\helloworld.dll' WITH PERMISSION_SET = SAFE;`  
  
1.  Assim, o procedimento, a função, a agregação, o tipo definido pelo usuário ou o gatilho deve ser criado na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o assembly **HelloWorld** contiver um método chamado **HelloWorld** na classe **procedures** , a [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir poderá ser adicionada à consulta para criar um procedimento chamado **Hello** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 `CREATE PROCEDURE hello`  
  
 `AS`  
  
 `EXTERNAL NAME HelloWorld.Procedures.HelloWorld`  
  
 Para obter mais informações sobre como criar os diferentes tipos de objetos de banco de dados gerenciados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [funções CLR definidas](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-functions.md)pelo usuário, [agregações CLR definidas pelo](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)usuário, [tipos CLR definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md), [procedimentos armazenados CLR](https://msdn.microsoft.com/library/bbdd51b2-a9b4-4916-ba6f-7957ac6c3f33)e [CLR Gatilhos](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c).  
  
## <a name="deploying-the-assembly-to-production-servers"></a>Implantando o assembly em servidores de produção  
 Uma vez testados e verificados no servidor de teste, os objetos de banco de dados do CLR podem ser distribuídos para servidores de produção. Para obter mais informações sobre como depurar objetos de banco de dados gerenciado, consulte [DEBUGGING CLR Database Objects](../../relational-databases/clr-integration/debugging-clr-database-objects.md).  
  
 A implantação dos objetos de banco de dados gerenciados é semelhante à dos objetos de banco de dados regulares (tabelas, rotinas [!INCLUDE[tsql](../../includes/tsql-md.md)] etc.). Os assemblies que contêm os objetos de banco de dados do CLR podem ser implantados em outros servidores que usam um script de implantação. O script de implantação pode ser compilado usando a funcionalidade "Gerar Scripts" do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. O script de implantação também pode ser compilado manualmente, ou usando "Gerar Scripts", e alterados manualmente. Uma vez compilado, o script de implantação pode ser executado em outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para implantar os objetos de banco de dados gerenciados.  
  
#### <a name="to-generate-a-deployment-script-using-generate-scripts"></a>Para gerar um script de implantação usando scripts de geração  
  
1.  Abra o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e se conecte à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que o assembly gerenciado ou o objeto de banco de dados a ser implantado é registrado.  
  
2.  No Pesquisador de **objetos**, expanda as árvores **> de nome do servidor** e bancos de **dados** do\<. Clique com o botão direito do mouse no banco de dados em que o objeto de banco de dados gerenciado está registrado, selecione **tarefas**e, em seguida, selecione **gerar scripts**. O Assistente de Script é aberto.  
  
3.  Selecione o banco de dados na caixa de listagem e clique em **Avançar**.  
  
4.  No painel **escolher opções de script** , clique em **Avançar**ou altere as opções e clique em **Avançar**.  
  
5.  No painel **escolher tipos de objeto** , escolha o tipo de objeto de banco de dados a ser implantado. Clique em **Avançar**.  
  
6.  Para cada tipo de objeto selecionado no painel **escolher tipos de objeto** , um painel **escolher \<tipo >** é apresentado. Nesse painel, é possível escolher uma dentre todas as instâncias do tipo de objeto de banco de dados registrado no banco de dados especificado. Selecione um ou mais objetos e clique em **Avançar**.  
  
7.  O painel **Opções de saída** aparece quando todos os tipos de objeto de banco de dados desejados foram selecionados. Selecione **script para arquivo** e especifique um caminho de arquivo para o script. Selecione **Avançar**. Examine suas seleções e clique em **concluir**. O script de implantação é salvo no caminho do arquivo especificado.  
  
## <a name="post-deployment-scripts"></a>Scripts pós-implantação  
 É possível executar um script de pós-implantação.  
  
 Para adicionar um script de pós-implantação, adicione um arquivo chamado postdeployscript.sql no diretório do projeto do Visual Studio. Por exemplo, clique com o botão direito do mouse em seu projeto no **Gerenciador de soluções** e selecione **Adicionar item existente**. Adicione o arquivo na raiz do projeto, e não na pasta Test Scripts.  
  
 Quando você clicar na implantação, o Visual Studio executará esse script após a implantação do projeto.  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos de programação da Integração CLR &#40;Common Language Runtime&#41;](../../relational-databases/clr-integration/common-language-runtime-clr-integration-programming-concepts.md)  
  
  

---
title: Criando procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- registering assemblies
- database assemblies [Analysis Services]
- server assemblies [Analysis Services]
- stored procedures [Analysis Services], creating
- assemblies [Analysis Services]
ms.assetid: a12ff02f-6d0b-4488-9846-3609fc0d0554
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7beb77adf595b055a6c1e4a7543b428a06ce7640
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62703087"
---
# <a name="creating-stored-procedures"></a>Criando procedimentos armazenados
  Todos os procedimentos armazenados devem ser associados a uma classe CLR (Common Language Runtime) ou COM (Component Object Model) para poderem seu usados. A classe deve ser instalada no servidor – geralmente na forma de um [!INCLUDE[msCoName](../../includes/msconame-md.md)] ActiveX® biblioteca de vínculo dinâmico (DLL) e registrada como um assembly no servidor ou em um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados.  
  
 Procedimentos armazenados são registrados em um servidor ou em um banco de dados. Procedimentos armazenados do servidor podem ser chamados a partir de qualquer contexto de consulta. Procedimentos armazenados do banco de dados podem ser acessados somente se o contexto do banco de dados for o banco de dados no qual o procedimento armazenado foi definido. Se as funções de um assembly chamarem funções de um assembly diferente, registre ambos no mesmo contexto (servidor ou banco de dados). Para um servidor ou um banco [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de dados implantado em um servidor [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , você pode usar o para registrar um assembly. Para um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você pode usar o Designer do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para registrar um assembly no projeto.  
  
> [!IMPORTANT]  
>  Os assemblies COM podem representar um risco à segurança. Devido a esse risco e outras considerações, os assemblies COM foram preteridos no [!INCLUDE[ssASversion10](../../includes/ssasversion10-md.md)]. Talvez não haja suporte para assemblies COM em versões futuras.  
  
## <a name="registering-a-server-assembly"></a>Registrando um assembly de servidor  
 No Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], os assemblies de servidor são listados na pasta Assemblies sob uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Os assemblies de servidor podem conter assemblies .NET (CLR) e bibliotecas COM.  
  
### <a name="to-create-a-server-assembly"></a>Para criar um assembly de servidor  
  
1.  Expanda a instância [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] do no Pesquisador de objetos, clique com o botão direito do mouse na pasta **assemblies** e clique em **novo assembly**. Isso exibe a caixa de diálogo **registrar assembly do servidor** .  
  
2.  Para o **tipo** , especifique o tipo de assembly:  
  
    -   Como DLL de código gerenciado (CLR), especifique .NET Assembly.  
  
    -   Para uma DLL de código nativo (COM), especifique a DLL COM.  
  
3.  Para **nome do arquivo**, ESPECIFIQUE a DLL que contém os procedimentos armazenados.  
  
4.  Para **nome do assembly**, especifique um nome para o assembly.  
  
5.  Se essa for uma compilação de depuração da biblioteca que você pretende usar para depurar procedimentos armazenados, marque a caixa de seleção **incluir informações de depuração** . Para obter mais informações sobre como depurar procedimentos armazenados, consulte [Depurando procedimentos armazenados](debugging-stored-procedures.md).  
  
6.  Você pode clicar em **OK** para registrar o assembly imediatamente ou na barra de ferramentas da caixa de diálogo, você pode clicar em um comando no menu **script** para gerar o script da ação de registro para uma janela de consulta, um arquivo ou a área de transferência.  
  
 Depois de registrar um assembly de servidor, você pode configurá-lo clicando com o botão direito do mouse no assembly no Pesquisador de objetos e clicando em **Propriedades**.  
  
## <a name="registering-a-database-assembly-on-the-server"></a>Registrando um assembly de banco de dados no servidor  
 No Pesquisador de Objetos do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], os assemblies de banco de dados são listados na pasta Assemblies sob um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Os assemblies de banco de dados podem conter assemblies .NET (CLR) e bibliotecas COM.  
  
### <a name="to-create-a-database-assembly-on-a-server"></a>Para criar um assembly de banco de dados em um servidor  
  
1.  Expanda a instância [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] do banco de dados no Pesquisador de objetos, clique com o botão direito do mouse na pasta **assemblies** e clique em **novo assembly**. Isso exibe a caixa de diálogo **registrar assembly de banco de dados** .  
  
2.  Para o **tipo** , especifique o tipo de assembly:  
  
    -   Como DLL de código gerenciado (CLR), especifique .NET Assembly.  
  
    -   Como DLL de código nativo (COM), especifique COM DLL.  
  
3.  Para **nome do arquivo**, ESPECIFIQUE a DLL que contém os procedimentos armazenados.  
  
4.  Para **nome do assembly**, especifique um nome para o assembly.  
  
5.  Se essa for uma compilação de depuração da biblioteca que você pretende usar para depurar procedimentos armazenados, marque a caixa de seleção **incluir informações de depuração** . Para obter mais informações sobre como depurar procedimentos armazenados, consulte [Depurando procedimentos armazenados](debugging-stored-procedures.md).  
  
6.  Você pode clicar em **OK** para registrar o assembly imediatamente ou na barra de ferramentas da caixa de diálogo, você pode clicar em um comando no menu **script** para gerar o script da ação de registro para uma janela de consulta, um arquivo ou a área de transferência.  
  
 Depois de registrar um assembly de banco de dados, você pode configurá-lo clicando com o botão direito do mouse no assembly no Pesquisador de objetos e clicando em **Propriedades**.  
  
## <a name="registering-a-database-assembly-in-a-project"></a>Registrando um assembly de banco de dados em um projeto  
 No Gerenciador de Soluções do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], os assemblies de banco de dados são listados na pasta Assemblies sob um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Os assemblies de banco de dados podem conter assemblies .NET (CLR) e bibliotecas COM.  
  
### <a name="to-create-a-database-assembly-in-an-analysis-service-project"></a>Para criar um assembly de banco de dados em um projeto do Analysis Service  
  
1.  Expanda a instância [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] do banco de dados no Pesquisador de objetos, clique com o botão direito do mouse na pasta **assemblies** e clique em **nova referência de assembly**. Isso exibe a caixa de diálogo **Adicionar referência** . A guia **.net** da caixa de diálogo **Adicionar referência** lista os assemblies .net (CLR) existentes, enquanto a guia **projetos** lista os projetos.  
  
2.  Você pode clicar em um componente ou projeto existente e, **Add** em seguida, clicar em Adicionar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para adicioná-lo ao projeto. Para adicionar uma referência a uma DLL COM, clique na guia **procurar** para localizar o arquivo. A lista **projetos e componentes selecionados** mostra o nome, o tipo, a versão e o local de cada componente que você está adicionando ao projeto.  
  
3.  Quando terminar de selecionar os componentes a serem adicionados, clique em **OK** para adicioná- [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] los ao projeto.  
  
## <a name="script-format-for-an-assembly"></a>Formato de script para um assembly  
 Registrar um assembly .NET é bastante simples. Um assembly .NET é adicionado a um banco de dados em formato binário que usa o seguinte formato:  
  
```  
<Create>  
   <ObjectDefinition>  
      <Assembly>  
         <Files>  
            <File>  
               <Name>filename</Name>  
               <Type>filetype</Type>  
               <Data>  
                  <Block>binarydatablock</Block>  
                  <Block>binarydatablock</Block>  
                  ...  
               </Data>  
            </File>  
         </Files>  
         <PermissionSet>PermissionSet</PermissionSet>  
      </Assembly>  
   <ObjectDefinition>  
</Create>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciamento de assemblies de modelo multidimensional](../multidimensional-models/multidimensional-model-assemblies-management.md)   
 [Definindo procedimentos armazenados](defining-stored-procedures.md)  
  
  

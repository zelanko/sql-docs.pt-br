---
title: Compilando, implantando e depurando objetos personalizados | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom objects [Integration Services]
ms.assetid: b03685bc-5398-4c3f-901a-1219c1098fbe
caps.latest.revision: 50
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 99fdd71403b12cee8ba9f207890268cde2e1d450
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="building-deploying-and-debugging-custom-objects"></a>Compilando, implantando e depurando objetos personalizados
  Depois de escrever o código para um objeto personalizado para [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você deve compilar o assembly, implantá-lo e integrá-lo ao [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer para torná-lo disponível para uso em pacotes e teste e depurá-lo.  
  
##  <a name="top"></a>Etapas para compilar, implantar e depurar um objeto personalizado para o Integration Services  
 Você já gravou a funcionalidade personalizada para seu objeto. Agora você tem que testá-la e disponibilizá-la aos usuários. As etapas são bem similares para todos os tipos de objetos personalizados que você pode criar para o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Aqui estão as etapas para criar, implantar e testá-lo.  
  
1.  [Sinal de](#signing) o assembly a ser gerado com um nome forte.  
  
2.  [Criar](#building) o assembly.  
  
3.  [Implantar](#deploying) o assembly movendo ou copiando-o para apropriada [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pasta.  
  
4.  [Instalar](#installing) o assembly no cache de assembly global (GAC).  
  
     O objeto é automaticamente adicionado à Caixa de Ferramentas.  
  
5.  [Solucionar problemas de](#troubleshooting) a implantação, se necessário.  
  
6.  [Teste](#testing) e depurar seu código.  
  
 Agora você pode usar o Designer de SSIS no SQL Server Data Tools (SSDT) para criar, manter e executar pacotes que usam versões diferentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações sobre o impacto dessa melhoria em suas extensões personalizadas, consulte [obtendo suas extensões personalizadas do SSIS com suporte pelo suporte a várias versões de 2015 SSDT para SQL Server 2016](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/)  
  
##  <a name="signing"></a>Assinar o Assembly  
 Quando um assembly for compartilhado, ele deverá ser instalado no cache de assembly global. Depois de acrescentado ao cache de assembly global, ele poderá ser usado por aplicativos como [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Um requisito do cache de assembly global é que o assembly seja assinado com um nome forte, que garante que ele seja globalmente único. Um assembly com nome forte tem um nome totalmente qualificado que inclui nome, cultura, chave pública e número da versão do assembly. O tempo de execução usa essas informações para localizar o assembly e diferenciá-lo de outros assemblies com o mesmo nome.  
  
 Para assinar um assembly com um nome forte, você deve primeiro ter ou criar um par de chaves pública/privada. Esse par de chaves criptográficas pública e privada é usado na hora da compilação para criar um assembly com nome forte.  
  
 Para obter mais informações sobre nomes fortes e sobre as etapas que você deve seguir para assinar um assembly, consulte os tópicos a seguir na documentação do SDK [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]:  
  
-   Assembly de nome forte  
  
-   Criando um par de chaves  
  
-   Assinando um assembly com um nome forte  
  
 Você pode assinar seu assembly facilmente com um nome forte em [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] no momento da compilação. No **propriedades do projeto** caixa de diálogo, selecione o **assinatura** guia. Selecione a opção de **assinar o assembly** e, em seguida, forneça o caminho do arquivo de chave (. snk).  
  
##  <a name="building"></a>Compilando o Assembly  
 Depois de assinar o projeto, você deve compilar ou recompilar o projeto ou a solução usando os comandos disponíveis no **criar** menu [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Sua solução pode conter um projeto separado para uma interface do usuário personalizada, que também deve ser assinada com um nome forte e pode ser compilada ao mesmo tempo.  
  
 O método mais conveniente para efetuar as próximas duas etapas – implantação e instalação do assembly no cache de assembly global – é gerar o script dessas etapas como um evento pós-compilação em [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Eventos de compilação estão disponíveis no **compilar** página de propriedades do projeto para um [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] projeto e o **eventos de Build** página para um projeto c#. O caminho completo é obrigatório para utilitários de prompt de comando, como **gacutil.exe**. São necessárias aspas nos caminhos que contêm espaços e nas macros, como $ (TargetPath) que se expande para caminhos que contêm espaços.  
  
 Eis um exemplo de uma linha de comando de evento pós-compilação para um provedor de log personalizado:  
  
```  
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -u $(TargetName)  
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -i $(TargetFileName)  
copy $(TargetFileName) "C:\Program Files\Microsoft SQL Server\130\DTS\LogProviders "  
```  
  
##  <a name="deploying"></a>Implantando o Assembly  
 O [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer localiza os objetos personalizados disponíveis para uso em pacotes, enumerando os arquivos localizados em uma série de pastas que são criadas quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] está instalado. Quando o padrão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurações de instalação são usadas, esse conjunto de pastas está localizado em **C:\Program Files\Microsoft SQL Server\130\DTS**. No entanto se você criar um programa de instalação para seu objeto personalizado, você deve verificar o valor de **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS\Setup\DtsPath** chave do registro para verificar o local dessa pasta.  
  
> [!NOTE]  
>  Para obter informações sobre como implantar componentes personalizados para funcionar bem com o suporte de várias versões do SQL Server Data Tools, consulte [obtendo suas extensões personalizadas do SSIS com suporte pelo suporte a várias versões de 2015 SSDT para SQL Server 2016](https://blogs.msdn.microsoft.com/ssis/2016/04/19/getting-your-ssis-custom-extensions-to-be-supported-by-the-multi-version-support-of-ssdt-2015-for-sql-server-2016/).  
  
 Você pode colocar o assembly na pasta de dois modos:  
  
-   Mova ou copie o assembly para a pasta apropriada após compilá-lo. (Para sua conveniência, você pode incluir o comando de cópia em um Evento de Pós-Compilação).  
  
-   Compile o assembly diretamente na pasta apropriada.  
  
 As seguintes pastas de implantação em **C:\Program Files\Microsoft SQL Server\130\DTS** são usadas para os vários tipos de objetos personalizados:  
  
|Objeto personalizado|Pasta de implantação|  
|-------------------|-----------------------|  
|Tarefa|Tarefas|  
|Gerenciador de conexões|Conexões|  
|Provedor de log|LogProviders|  
|Componente de fluxo de dados|PipelineComponents|  
  
> [!NOTE]  
>  Os assemblies são copiados para essas pastas para dar suporte à enumeração de tarefas disponíveis, gerenciadores de conexões, e assim por diante. Portanto, não é necessário implantar assemblies que contenham somente a interface do usuário personalizada para objetos personalizados nessas pastas.  
  
##  <a name="installing"></a>Instalando o Assembly no Cache de Assembly Global  
 Para instalar o assembly da tarefa no cache de assembly global (GAC), use a ferramenta de linha de comando **gacutil.exe**, ou arraste os assemblies para o `%system%\assembly` directory. Para sua conveniência, você também pode incluir a chamada para **gacutil.exe** em um evento de pós-compilação.  
  
 O comando a seguir instala um componente denominado *MyTask.dll* no GAC usando **gacutil.exe**.  
  
 `gacutil /iF MyTask.dll`  
  
 É necessário fechar e reabrir o [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer depois que você instalar uma versão nova de seu objeto personalizado. Se você instalou versões anteriores do seu objeto personalizado no GAC, deve removê-las antes de instalar a versão nova. Para desinstalar um assembly, execute **gacutil.exe** e especifique o nome de assembly com o `/u` opção.  
  
 Para obter mais informações sobre o GAC, consulte a Ferramenta Cache de Assembly Global (Gactutil.exe) nas Ferramentas [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
##  <a name="troubleshooting"></a>Solucionando problemas de implantação  
 Se seu objeto personalizado aparece no **caixa de ferramentas** ou a lista de objetos disponíveis, mas não é possível adicioná-lo a um pacote, tente o seguinte:  
  
1.  Procure múltiplas versões do seu componente no GAC. Se houver múltiplas versões do componente no GAC, o designer talvez não consiga carregar seu componente. Exclua todas as instâncias do assembly do GAC e adicione o assembly novamente.  
  
2.  Verifique se há somente uma única instância do assembly na pasta de implantação.  
  
3.  Atualize a caixa de ferramentas.  
  
4.  Anexar [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] para **devenv.exe** e defina um ponto de interrupção para percorrer o código de inicialização para garantir que nenhuma exceção ocorra.  
  
##  <a name="testing"></a>Testar e depurar seu código  
 A abordagem mais simples para depurar os métodos de tempo de execução de um objeto personalizado é iniciar **dtexec.exe** de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] depois de compilar seu objeto personalizado e executar um pacote que usa o componente.  
  
 Se você deseja depurar os métodos do componente em tempo de design, como o **validar** método, abra um pacote que usa o componente em uma segunda instância de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]e anexar a sua **devenv.exe** processo.  
  
 Se você deseja depurar os métodos do componente tempo de execução quando um pacote é aberto e em execução [!INCLUDE[ssIS](../../includes/ssis-md.md)] designer, você deve forçar uma pausa na execução do pacote para que você também pode anexar ao **DtsDebugHost.exe** processo.  
  
#### <a name="to-debug-an-objects-run-time-methods-by-attaching-to-dtexecexe"></a>Para depurar os métodos de tempo de execução de um objeto anexando a dtexec.exe  
  
1.  Assine e compile seu projeto na configuração de Depuração, implante-o e instale-o no cache de assembly global como descrito neste tópico.  
  
2.  No **depurar** guia de **propriedades do projeto**, selecione **Iniciar programa externo** como o **iniciar ação**e localize **dtexec.exe**, que é instalado por padrão em C:\Program Files\Microsoft SQL Server\130\DTS\Binn.  
  
3.  No **opções de linha de comando** caixa de texto, em **iniciar opções**, digite os argumentos de linha de comando necessários para executar um pacote que usa seu componente. Frequentemente, o argumento de linha de comando consistirá no comutador /F [ILE] seguido pelo caminho e pelo nome do arquivo .dtsx. Para obter mais informações, consulte [dtexec Utility](../../integration-services/packages/dtexec-utility.md).  
  
4.  Defina pontos de interrupção no código fonte, quando apropriado, nos métodos de tempo de execução de seu componente.  
  
5.  Execute seu projeto.  
  
#### <a name="to-debug-a-custom-objects-design-time-methods-by-attaching-to-sql-server-data-tools"></a>Para depurar os métodos de tempo de design de um objeto personalizado anexando às Ferramentas de Dados do SQL Server  
  
1.  Assine e compile seu projeto na configuração de Depuração, implante-o e instale-o no cache de assembly global como descrito neste tópico.  
  
2.  Defina pontos de interrupção no código fonte, quando apropriado, nos métodos de tempo de design de seu objeto personalizado.  
  
3.  Abra uma segunda instância de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] e carregue um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contenha um pacote que use o objeto personalizado.  
  
4.  Da primeira instância do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], anexe à segunda instância de **devenv.exe** no qual o pacote é carregado selecionando **anexar ao processo** do **depurar** menu da primeira instância.  
  
5.  Execute o pacote da segunda instância de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
#### <a name="to-debug-a-custom-objects-run-time-methods-by-attaching-to-sql-server-data-tools"></a>Para depurar os métodos de tempo de execução de um objeto personalizado anexando às Ferramentas de Dados do SQL Server  
  
1.  Depois de concluir as etapas listadas no procedimento anterior, force uma pausa na execução do pacote para que você pode anexar a **DtsDebugHost.exe**. Você pode forçar essa pausa adicionando um ponto de interrupção a **OnPreExecute** evento, ou adicionando uma tarefa de Script ao seu projeto e inserindo um script que exibe uma caixa de mensagem modal.  
  
2.  Execute o pacote. Quando a pausa ocorrer, alterne para a instância do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] na qual o seu projeto de código aberto e selecione **anexar ao processo** do **depurar** menu. Certifique-se de anexar à instância do **DtsDebugHost.exe** listado como **gerenciada, x86** no **tipo** coluna, não à instância listada como **x86** somente.  
  
3.  Retornar ao pacote pausado e continuar após o ponto de interrupção ou clique **Okey** para ignorar a caixa de mensagem gerada pela tarefa Script e continuar a execução do pacote e a depuração.  
  
## <a name="see-also"></a>Consulte também  
 [Desenvolvendo objetos personalizados para o Integration Services](../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)   
 [Persistência de objetos personalizados](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)   
 [Solucionando problemas de ferramentas para desenvolvimento de pacotes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-development.md)  
  
  

---
title: Compilar, implantar e depurar objetos personalizados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom objects [Integration Services]
ms.assetid: b03685bc-5398-4c3f-901a-1219c1098fbe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 89d1e2fd7c4f0e414424ad678c7ea9f3936b02f0
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176376"
---
# <a name="building-deploying-and-debugging-custom-objects"></a>Compilando, implantando e depurando objetos personalizados
  Depois de escrever o código de um objeto personalizado do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você deve compilar o assembly, implantá-lo e integrá-lo ao [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer para disponibilizar seu uso em pacotes, além de testá-lo e depurá-lo.

##  <a name="top"></a> Etapas para compilar, implantar e depurar um objeto personalizado para Integration Services
 Você já gravou a funcionalidade personalizada para seu objeto. Agora você tem que testá-la e disponibilizá-la aos usuários. As etapas são bem similares para todos os tipos de objetos personalizados que você pode criar para o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].

 Eis as etapas que você segue ao compilar, implantar e depurar objetos personalizados:

1.  [Assine](#signing) o assembly para que ele seja gerado com um nome forte.

2.  [Compile](#building) o assembly.

3.  [Implante](#deploying) o assembly movendo-o ou copiando-o até a pasta do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] apropriada.

4.  [Instale](#installing) o assembly no GAC (cache de assembly global).

     O objeto é automaticamente adicionado à Caixa de Ferramentas.

5.  [Solucione problemas](#troubleshooting) de implantação, se necessário.

6.  [Teste](#testing) e depure seu código.

##  <a name="signing"></a>Assinando o assembly
 Quando um assembly for compartilhado, ele deverá ser instalado no cache de assembly global. Depois de acrescentado ao cache de assembly global, ele poderá ser usado por aplicativos como [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Um requisito do cache de assembly global é que o assembly seja assinado com um nome forte, que garante que ele seja globalmente único. Um assembly com nome forte tem um nome totalmente qualificado que inclui nome, cultura, chave pública e número da versão do assembly. O runtime usa essas informações para localizar o assembly e diferenciá-lo de outros assemblies com o mesmo nome.

 Para assinar um assembly com um nome forte, você deve primeiro ter ou criar um par de chaves pública/privada. Esse par de chaves criptográficas pública e privada é usado na hora da compilação para criar um assembly com nome forte.

 Para obter mais informações sobre nomes fortes e sobre as etapas que você deve seguir para assinar um assembly, consulte os tópicos a seguir na documentação do SDK [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]:

-   Assembly de nome forte

-   Criando um par de chaves

-   Assinando um assembly com um nome forte

 Você pode assinar seu assembly facilmente com um nome forte em [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] no momento da compilação. Na caixa de diálogo **Propriedades do projeto** , selecione a guia **assinatura** . Selecione a opção para **assinar o assembly** e forneça o caminho do arquivo de chave (. SNK).

##  <a name="building"></a>Compilando o assembly
 Depois de assinar o projeto, você deve compilar ou recompilar o projeto ou a solução usando os comandos disponíveis no menu **Compilar** do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Sua solução pode conter um projeto separado para uma interface do usuário personalizada, que também deve ser assinada com um nome forte e pode ser compilada ao mesmo tempo.

 O método mais conveniente para realizar as próximas duas etapas – implantação e instalação do assembly no cache de assembly global – é gerar o script dessas etapas como um evento pós-build em [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Os eventos de build estão disponíveis na página **Compilar** de Propriedades do Projeto para um projeto do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] e na página **Eventos de Build** para um projeto em C#. O caminho completo é obrigatório para utilitários de prompt de comando, como **gacutil.exe**. São necessárias aspas nos caminhos que contêm espaços e nas macros, como $ (TargetPath) que se expande para caminhos que contêm espaços.

 Eis um exemplo de uma linha de comando de evento pós-compilação para um provedor de log personalizado:

```
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -u $(TargetName)
"C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools\gacutil.exe" -i $(TargetFileName)
copy $(TargetFileName) "C:\Program Files\Microsoft SQL Server\120\DTS\LogProviders "
```

##  <a name="deploying"></a>Implantando o assembly
 O [!INCLUDE[ssIS](../../includes/ssis-md.md)] designer localiza os objetos personalizados disponíveis para uso em pacotes, enumerando os arquivos encontrados em uma série de pastas que são criadas quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] o é instalado. Quando as configurações [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de instalação padrão são usadas, esse conjunto de pastas está localizado em **C:\Arquivos de Programas\Microsoft SQL Server\120\DTS**. No entanto, se você criar um programa de instalação para seu objeto personalizado, verifique o valor da chave do registro **HKEY_LOCAL_MACHINE \SOFTWARE\MICROSOFT\MICROSOFT SQL Server\120\SSIS\Setup\DtsPath** para verificar o local dessa pasta.

 Você pode colocar o assembly na pasta de dois modos:

-   Mova ou copie o assembly para a pasta apropriada após compilá-lo. (Para sua conveniência, você pode incluir o comando de cópia em um Evento de Pós-Compilação).

-   Compile o assembly diretamente na pasta apropriada.

 As seguintes pastas de implantação em **C:\Program Files\Microsoft SQL Server\120\DTS** são usadas para os vários tipos de objetos personalizados:

|Objeto personalizado|Pasta de implantação|
|-------------------|-----------------------|
|Tarefa|Tarefas|
|Gerenciador de conexões|conexões|
|Provedor de log|LogProviders|
|Componente de fluxo de dados|PipelineComponents|

> [!NOTE]
>  Os assemblies são copiados para essas pastas para dar suporte à enumeração de tarefas disponíveis, gerenciadores de conexões, e assim por diante. Portanto, não é necessário implantar assemblies que contenham somente a interface do usuário personalizada para objetos personalizados nessas pastas.

##  <a name="installing"></a>Instalando o assembly no cache de assembly global
 Para instalar o assembly da tarefa no GAC (cache de assembly global), use a ferramenta de linha de comando **gacutil.exe** ou arraste os assemblies até o diretório `%system%\assembly`. Para sua conveniência, também é possível incluir a chamada para **gacutil.exe** em um evento posterior ao build.

 O comando a seguir instala um componente denominado *MyTask.dll* no GAC usando **gacutil.exe**.

 `gacutil /iF MyTask.dll`

 É necessário fechar e reabrir o [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer depois que você instalar uma versão nova de seu objeto personalizado. Se você instalou versões anteriores do seu objeto personalizado no GAC, deve removê-las antes de instalar a versão nova. Para desinstalar um assembly, execute **gacutil.exe** e especifique o nome do assembly com a opção `/u`.

 Para obter mais informações sobre o GAC, consulte a Ferramenta Cache de Assembly Global (Gactutil.exe) nas Ferramentas [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].

##  <a name="troubleshooting"></a>Solucionando problemas de implantação
 Se seu objeto personalizado aparecer na **Caixa de Ferramentas** ou na lista de objetos disponíveis mas você não conseguir adicioná-lo a um pacote, tente fazer o seguinte:

1.  Procure múltiplas versões do seu componente no GAC. Se houver múltiplas versões do componente no GAC, o designer talvez não consiga carregar seu componente. Exclua todas as instâncias do assembly do GAC e adicione o assembly novamente.

2.  Verifique se há somente uma única instância do assembly na pasta de implantação.

3.  Atualize a caixa de ferramentas.

4.  Anexe [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] a **devenv.exe** e defina um ponto de interrupção para percorrer seu código de inicialização e assegurar que nenhuma exceção ocorra.

##  <a name="testing"></a>Testando e Depurando seu código
 A abordagem mais simples para depurar os métodos de tempo de execução de um objeto personalizado é iniciar **dtexec.exe** de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] depois de compilar seu objeto personalizado e executar um pacote que use o componente.

 Se você quiser depurar os métodos de tempo de design do componente, como o `Validate` método, abra um pacote que usa o componente em uma segunda instância do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]e anexe-o ao processo **devenv. exe** .

 Se você também desejar depurar os métodos de tempo de execução do componente quando um pacote estiver aberto e em execução no designer [!INCLUDE[ssIS](../../includes/ssis-md.md)], deverá forçar uma pausa na execução do pacote para que também seja possível anexar ao processo **DtsDebugHost.exe**.

#### <a name="to-debug-an-objects-run-time-methods-by-attaching-to-dtexecexe"></a>Para depurar os métodos de tempo de execução de um objeto anexando a dtexec.exe

1.  Assine e compile seu projeto na configuração de Depuração, implante-o e instale-o no cache de assembly global como descrito neste tópico.

2.  Na guia **depurar** das **Propriedades do projeto**, selecione **Iniciar programa externo** como a **ação iniciar**e localize **dtexec. exe**, que é instalado por padrão em c:\Arquivos de Programas\Microsoft SQL Server\120\DTS\Binn.

3.  Na caixa de texto **Opções da linha de comando**, em **Iniciar Opções**, insira os argumentos de linha de comando necessários para executar um pacote que use o componente. Frequentemente, o argumento de linha de comando consistirá no comutador /F [ILE] seguido pelo caminho e pelo nome do arquivo .dtsx. Para saber mais, veja [dtexec Utility](../packages/dtexec-utility.md).

4.  Defina pontos de interrupção no código fonte, quando apropriado, nos métodos de tempo de execução de seu componente.

5.  Execute seu projeto.

#### <a name="to-debug-a-custom-objects-design-time-methods-by-attaching-to-sql-server-data-tools"></a>Para depurar os métodos de tempo de design de um objeto personalizado anexando às Ferramentas de Dados do SQL Server

1.  Assine e compile seu projeto na configuração de Depuração, implante-o e instale-o no cache de assembly global como descrito neste tópico.

2.  Defina pontos de interrupção no código fonte, quando apropriado, nos métodos de tempo de design de seu objeto personalizado.

3.  Abra uma segunda instância de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] e carregue um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contenha um pacote que use o objeto personalizado.

4.  Da primeira instância do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], anexe à segunda instância de **devenv.exe** na qual o pacote foi carregado selecionando **Anexar ao Processo** do menu **Depurar** da primeira instância.

5.  Execute o pacote da segunda instância de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].

#### <a name="to-debug-a-custom-objects-run-time-methods-by-attaching-to-sql-server-data-tools"></a>Para depurar os métodos de tempo de execução de um objeto personalizado anexando às Ferramentas de Dados do SQL Server

1.  Depois de concluir as etapas listadas no procedimento anterior, force uma pausa na execução do seu pacote para que você possa anexar ao **DtsDebugHost.exe**. Você pode forçar essa pausa adicionando um ponto de interrupção ao evento `OnPreExecute`, ou adicionando uma tarefa Script ao seu projeto e inserindo um script que exiba uma caixa de mensagem modal.

2.  Execute o pacote. Quando a pausa ocorrer, mude para a instância de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] em que seu projeto de código está aberto e selecione **Anexar ao Processo** do menu **Depurar**. Certifique-se de anexar à instância de **DtsDebugHost.exe** listada como **Gerenciada, x86** na coluna **Tipo**, mas não à instância listada apenas como **x86**.

3.  Retorne ao pacote em pausa e continue até o ponto de interrupção ou clique em **OK** para ignorar a caixa de mensagem gerada pela tarefa Script e continue a execução e a depuração do pacote.

![Ícone de Integration Services (pequeno)](../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.

## <a name="see-also"></a>Consulte Também
 [Desenvolvendo objetos personalizados para Integration Services](developing-custom-objects-for-integration-services.md) [persistência](persisting-custom-objects.md) de [ferramentas de solução de problemas de objetos personalizados para desenvolvimento de pacotes](../troubleshooting/troubleshooting-tools-for-package-development.md)



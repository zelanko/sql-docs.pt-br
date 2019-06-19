---
title: Implantação de pacote herdado (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.packageconfigurationorganizer.f1
- sql13.dts.configwizard.finishdtsconfiguration.f1
- sql13.dts.configwizard.selectobjects.f1
- sql13.dts.configwizard.selecconfigtype.f1
- sql13.dts.configwizard.welcome.f1
- sql13.dts.deploymentwizard.welcome.f1
- sql13.dts.deploymentwizard.confirminstallation.f1
- sql13.dts.deploymentwizard.deploydtspackages.f1
- sql13.dts.deploymentwizard.finish.f1
- sql13.dts.deploymentwizard.configurepackages.f1
- sql13.dts.deploymentwizard.selectinstfolder.f1
- sql13.dts.deploymentwizard.packagevalidation.f1
- sql13.dts.deploymentwizard.specifytargetsqlserver.f1
helpviewer_keywords:
- Integration Services packages, deploying
- deploying packages [Integration Services]
- SQL Server Integration Services packages, deploying
- deploying packages [Integration Services], about deploying packages
- packages [Integration Services], deploying
- SSIS packages, deploying
ms.assetid: 0f5fc7be-e37e-4ecd-ba99-697c8ae3436f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e5a9b49b743ed95766bfbd8d310bba40c6bfe396
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65719972"
---
# <a name="legacy-package-deployment-ssis"></a>Implantação de pacote herdado (SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui ferramentas e assistentes que simplificam a implantação de pacotes do computador de desenvolvimento para o servidor de produção ou para outros computadores.  
  
 Há quatro etapas no processo de implantação de pacotes:  
  
1.  A primeira etapa é opcional e envolve a criação de configurações de pacotes que atualizam as propriedades dos elementos dos pacotes em tempo de execução. As configurações são incluídas automaticamente quando se implantam os pacotes.  
  
2.  A segunda etapa é desenvolver o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para criar um utilitário de implantação de pacote. O utilitário de implantação para o projeto contém os pacotes que você quer implantar  
  
3.  A terceira etapa é copiar a pasta de implantação que foi criada quando você desenvolveu o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para o computador de destino.  
  
4.  A quarta etapa é executar no computador de destino o Assistente de Instalação de Pacotes para instalar os pacotes no sistema de arquivos ou em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

## <a name="package-configurations"></a>Configurações do Pacote
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece configurações de pacote que podem ser usadas para atualizar os valores das propriedades em tempo de execução.  
  
> **OBSERVAÇÃO:** As configurações estão disponíveis para o modelo de implantação de pacote. Os parâmetros são usados no lugar das configurações para o modelo de implantação de projeto. O modelo de implantação de projeto permite que você implante projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obter mais informações sobre os modelos de implantação, consulte [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).   
  
 Uma configuração é um par propriedade/valor que você adiciona a um pacote concluído. Normalmente, você cria uma definição de propriedades do pacote nos objetos do pacote durante o desenvolvimento do pacote e, depois, adiciona as configurações ao pacote. Quando o pacote é executado, obtém os novos valores da propriedade da configuração. Por exemplo, ao usar uma configuração, você pode alterar a cadeia de caracteres de conexão de um gerenciador de conexões ou atualizar o valor de uma variável.  
  
 As configurações de pacote fornecem os seguintes benefícios:  
  
-   As configurações facilitam a movimentação dos pacotes de um ambiente de desenvolvimento para um ambiente de produção. Por exemplo, uma configuração pode atualizar o caminho de um arquivo de origem, ou alterar o nome de um banco de dados ou de um servidor.  
  
-   As configurações são úteis quando você implanta pacotes em muitos servidores diferentes. Por exemplo, uma variável na configuração de cada pacote implantado pode conter um valor de espaço de disco diferente e, se o espaço em disco disponível não atingir esse valor, o pacote não será executado.  
  
-   As configurações tornam os pacotes mais flexíveis. Por exemplo, uma configuração pode atualizar o valor de uma variável usada em uma expressão de propriedade.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] oferece suporte a vários métodos diferentes de armazenamento de configurações de pacote, como arquivos XML, tabelas em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e variáveis de ambiente e pacote.  
  
 Cada configuração é um par propriedade/valor. O arquivo de configuração XML e os tipos de configuração [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem incluir várias configurações.  
  
 As configurações são incluídas quando você cria um utilitário de desenvolvimento de pacote para instalar pacotes. Quando você instala os pacotes, as configurações podem ser atualizadas como uma etapa na instalação de pacotes.  
  
### <a name="understanding-how-package-configurations-are-applied-at-run-time"></a>Compreendendo como as configurações de pacote são aplicadas em tempo de execução  
 Quando você usa o utilitário do prompt de comando **dtexec** para executar um pacote implantado, o utilitário aplica as configurações do pacote duas vezes. O utilitário aplica configurações antes e depois de aplicar as opções que você especificou na linha de comando.  
  
 Como o utilitário carrega e executa o pacote, os eventos ocorrem na seguinte ordem:  
  
1.  O utilitário **dtexec** carrega o pacote.  
  
2.  O utilitário aplica as configurações que foram especificadas no pacote em tempo de design e na ordem especificada no pacote. (A única exceção a essa regra são as configurações de Variáveis do Pacote Pai. O utilitário só aplica essas configurações uma vez e posteriormente no processo.)  
  
3.  Em seguida, o utilitário aplica qualquer opção que você especificou na linha de comando.  
  
4.  O utilitário recarrega as configurações que foram especificadas no pacote em tempo de design e na ordem especificada no pacote. (Novamente, a exceção a essa regra são as configurações de Variáveis do Pacote Pai). O utilitário usa qualquer opção de linha de comando que foi especificada para recarregar as configurações. Portanto, valores diferentes podem ser recarregados a partir de locais distintos.  
  
5.  O utilitário aplica as configurações Variáveis do Pacote Pai.  
  
6.  O utilitário executa o pacote.  
  
 O modo como o utilitário **dtexec** aplica as configurações afeta as seguintes opções da linha de comando:  
  
-   Você pode usar a opção **/Connection** ou **/Set** na execução para carregar as configurações do pacote por meio de um local diferente do especificado no design.  
  
-   Você pode usar a opção **/ConfigFile** para carregar as configurações adicionais não especificadas no design.  
  
 Porém, essas opções de linha de comando têm algumas restrições:  
  
-   Não é possível usar a opção **/Set** ou **/Connection** para substituir os valores únicos que também são definidos por uma configuração.  
  
-   Não é possível usar a opção **/ConfigFile** para carregar as configurações que substituem as configurações especificadas no design.  
  
 Para obter mais informações sobre essas opções e sobre como o comportamento delas difere entre o [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] e versões anteriores, consulte [Alterações de comportamento dos recursos do Integration Services no SQL Server 2016](https://msdn.microsoft.com/library/611d22fa-5ac7-485e-9a40-7131e852f794).  
  
### <a name="package-configuration-types"></a>Tipos de configuração de pacotes  
 A tabela a seguir descreve os tipos de configuração de pacotes.  
  
|Tipo|Descrição|  
|----------|-----------------|  
|Arquivo de configuração XML|Um arquivo XML contém as configurações. O arquivo XML pode incluir várias configurações.|  
|Variável de ambiente|Uma variável de ambiente contém a configuração.|  
|Entrada de Registro|Uma entrada de Registro contém a configuração.|  
|Variável de pacote pai|Uma variável no pacote contém a configuração. Normalmente, esse tipo de configuração é usado para atualizar as propriedades em pacotes filho.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] table|Uma tabela em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém a configuração. A tabela pode incluir várias configurações.|  
  
#### <a name="xml-configuration-files"></a>Arquivos de configuração XML  
 Se você selecionar o tipo de configuração **arquivo de configuração XML** , poderá criar um novo arquivo de configuração, reutilizar um arquivo existente e adicionar configurações novas ou reutilizar um arquivo existente, mas substituir o conteúdo do arquivo.  
  
 Um arquivo de configuração XML inclui duas seções:  
  
-   Um título que contém informações sobre o arquivo de configuração. Esse elemento inclui atributos tais como quando o arquivo foi criado e o nome da pessoa que gerou o arquivo.  
  
-   Elementos de configuração que contêm informações sobre cada configuração. Esse elemento inclui atributos como o caminho da propriedade e o valor configurado de uma propriedade.  
  
 O código XML a seguir mostra a sintaxe de um arquivo de configuração XML. Esse exemplo mostra uma configuração para a propriedade Value de uma variável de inteiro chamada `MyVar`.  
  
```xml
\<?xml version="1.0"?>  
<DTSConfiguration>  
   <DTSConfigurationHeading>  
      <DTSConfigurationFileInfo  
          GeneratedBy="DomainName\UserName"  
          GeneratedFromPackageName="Package"  
          GeneratedFromPackageID="{2AF06766-817A-4E28-9878-0DE37A150648}"  
          GeneratedDate="2/01/2005 5:58:09 PM"/>  
   </DTSConfigurationHeading>  
   <Configuration ConfiguredType="Property" Path="\Package.Variables[User::MyVar].Value" ValueType="Int32">  
      <ConfiguredValue>0</ConfiguredValue>  
   </Configuration>  
</DTSConfiguration>  
  
```  
  
#### <a name="registry-entry"></a>Entrada de Registro  
 Se você desejar usar uma entrada de Registro para armazenar a configuração, poderá usar uma chave existente ou criar uma nova chave em HKEY_CURRENT_USER. A chave do Registro que você usa deve ter um valor denominado **Value**. O valor pode ser um DWORD ou uma cadeia de caracteres.  
  
 Se você selecionar o tipo de configuração **Entrada de Registro** , digitará o nome da chave do Registro na caixa de entrada de Registro. O formato é \<registry key>. Se desejar usar uma chave do Registro que não está na raiz de HKEY_CURRENT_USER, use o formato \<Registry key\registry key\\...> para identificar a chave. Por exemplo, para usar a chave MyPackage localizada em SSISPackages, digite **SSISPackages\MyPackage**.  
  
#### <a name="sql-server"></a>SQL Server  
 Se você selecionar o tipo de configuração **SQL Server** , especifique a conexão para o banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que deseja armazenar as configurações. Você pode salvar as configurações em uma tabela existente ou criar uma tabela no banco de dados especificado.  
  
 A instrução SQL a seguir mostra a instrução padrão CREATE TABLE fornecida pelo Assistente de Configuração de Pacotes.  
  
```sql
CREATE TABLE [dbo].[SSIS Configurations]  
(  
ConfigurationFilter NVARCHAR(255) NOT NULL,  
ConfiguredValue NVARCHAR(255) NULL,  
PackagePath NVARCHAR(255) NOT NULL,  
ConfiguredValueType NVARCHAR(20) NOT NULL  
)  
  
```  
  
 O nome fornecido para a configuração é o valor armazenado na coluna **ConfigurationFilter** .  
  
### <a name="direct-and-indirect-configurations"></a>Configurações diretas e indiretas  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fornece configurações diretas e indiretas. Se você especificar as configurações diretamente, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] criará um vínculo direto entre o item de configuração e a propriedade de objeto do pacote. As configurações diretas são a melhor escolha quando o local da origem não é alterado. Por exemplo, se você tiver certeza de que todas as implantações no pacote usam o mesmo caminho de arquivo, poderá especificar um arquivo de configuração XML.  
  
 As configurações indiretas usam variáveis de ambiente. Em vez de especificar os parâmetros de configuração diretamente, a configuração aponta para uma variável de ambiente que, por sua vez, contém o valor da configuração. O uso de configurações indiretas é a escolha mais adequada quando o local da configuração pode ser alterado em cada implantação de um pacote.  

## <a name="create-package-configurations"></a>Criar configurações de pacote
  Crie as configurações do pacote por meio da caixa de diálogo **Organizador de Configurações de Pacote** e do Assistente de Configuração de Pacote. Para acessar essas ferramentas, clique em **Configurações do Pacote** no menu de **SSIS** em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
  
 **OBSERVAÇÕES:**
> Você também pode acessar o **Organizador de Configurações de Pacote** clicando no botão de reticências ao lado da propriedade **Configuração** . A propriedade Configuração aparece na janela de propriedades para o pacote.  
> 
> As configurações estão disponíveis para o modelo de implantação de pacote. Os parâmetros são usados no lugar das configurações para o modelo de implantação de projeto. O modelo de implantação de projeto permite que você implante projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obter mais informações sobre os modelos de implantação, consulte [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).    
> 
> Na caixa de diálogo **Organizador de Configurações do Pacote** , você pode habilitar pacotes para usar configurações, adicionar e excluir configurações e definir a ordem de preferência para carregar as configurações. 
> 
> Quando as configurações de pacote são carregadas na ordem preferencial, elas são carregadas da parte superior da lista mostrada na caixa de diálogo **Organizador de Configurações do Pacote** até a parte inferior da lista. Porém, no tempo de execução, talvez as configurações do pacote não sejam carregadas na ordem preferencial. Em particular, as configurações do pacote pai são carregadas depois das configurações de outros tipos.  
> 
> Se várias configurações definirem a mesma propriedade de objeto, o valor carregado por último será usado no tempo de execução.  
  
 Na caixa de diálogo **Organizador de Configurações do Pacote** , você executa o Assistente de Configuração de Pacotes, que o guia através de etapas para criar uma configuração. Para executar o Assistente de Configuração de Pacotes, adicione uma nova configuração na caixa de diálogo **Organizador de Configurações do Pacote** ou edite uma existente. Nas páginas do assistente, você escolhe o tipo de configuração, escolhe se quer acessar a configuração diretamente ou usar variáveis de ambiente, e seleciona as propriedades a serem salvas na configuração.  
  
 O exemplo a seguir mostra as propriedades de destino de uma variável e de um pacote, do modo como são mostradas na página Concluindo o Assistente, no Assistente de Configuração de Pacotes:  
  
 \Package.Variables[User::TodaysDate].Properties[RaiseChangedEvent]  
  
 \Package.Properties[MaximumErrorCount]  
  
 \Package.Properties[LoggingMode]  
  
 \Package.Properties[LocaleID]  
  
 \Package\My SQL Task.Variables[User::varTableName].Properties[Value]  
  
 Neste exemplo, a configuração atualiza estas propriedades:  
  
-   A propriedade RaiseChangedEvent da variável definida pelo usuário, `TodaysDate`.  
  
-   As propriedades MaximumErrorCount, LoggingMode e LocaleID do pacote.  
  
-   A propriedade Value da variável definida pelo usuário, `varTableName`, dentro do escopo da tarefa, My SQL Task.  
  
 O "\Package" representa a raiz e pontos (.) separam os objetos que definem o caminho até a propriedade que a configuração atualiza. Os nomes das variáveis e das propriedades estão entre parênteses. O termo Package sempre é usado na configuração, independente do nome do pacote; porém, todos os outros objetos no caminho usam os nomes definidos pelo usuário.  
  
 Depois que o assistente terminar, a nova configuração é adicionada à lista de configurações na caixa de diálogo **Organizador de Configurações do Pacote** .  
  
> **OBSERVAÇÃO:** A última página do Assistente de Configuração de Pacote, Concluindo o Assistente, lista as propriedades de destino da configuração. Se quiser atualizar as propriedades enquanto estiver executando pacotes usando o utilitário prompt de comando **dtexec**, você poderá gerar as cadeias de caracteres que representam os caminhos de propriedade executando o Assistente de Configuração de Pacotes e, então, copiá-las e colá-las na janela do prompt de comando para usar com a opção definida de **dtexec.**  
  
 A tabela a seguir descreve as colunas da lista de configurações na caixa de diálogo **Organizador de Configurações do Pacote** .  
  
|coluna|Descrição|  
|------------|-----------------|  
|**Nome da Configuração**|O nome da configuração.|  
|**Tipo de Configuração**|O tipo de configuração.|  
|**Cadeia de Caracteres de Configuração**|O local da configuração. O local pode ser um caminho, uma variável de ambiente, uma chave do Registro, um nome de variável do pacote pai ou uma tabela em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**Objeto de Destino**|O nome do objeto com uma propriedade que tem uma configuração. Se a configuração for um arquivo de configuração XML, a coluna ficará em branco, devido à configuração poder atualizar vários objetos.|  
|**Propriedade de Destino**|O nome da propriedade. Se a configuração gravar em um arquivo de configuração XML ou em uma tabela do SQL Server, a coluna ficará em branco, pois a configuração pode atualizar vários objetos.|  
  
### <a name="to-create-a-package-configuration"></a>Para criar uma configuração de pacote  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , clique na guia **Fluxo de Controle**, **Fluxo de Dados**, **Manipulador de Eventos**ou **Explorador de Pacotes** .  
  
4.  No menu **SSIS** , clique em **Configurações do Pacote**.  
  
5.  Na caixa de diálogo **Organizador de Configurações do Pacote** , selecione **Habilitar configurações do pacote**e clique em **Adicionar**.  
  
6.  Na página inicial da página Assistente de Configuração de Pacotes, clique em **Avançar**.  
  
7.  Na página Selecionar Tipo de Configuração, especifique o tipo de configuração e defina as propriedades pertinentes ao tipo de configuração. Para obter mais informações, consulte [Referência da interface do usuário do Assistente de Configuração de Pacotes](../../integration-services/packages/package-configuration-wizard-ui-reference.md).  
  
8.  Na página Selecionar Propriedades a Serem Exportadas, selecione as propriedades dos objetos do pacote a serem incluídas na configuração. Se o tipo de configuração oferecer suporte somente a uma propriedade, o título dessa página de assistente será Selecionar Propriedade de Destino. Para obter mais informações, consulte [Referência da interface do usuário do Assistente de Configuração de Pacotes](../../integration-services/packages/package-configuration-wizard-ui-reference.md).  
  
    > **OBSERVAÇÃO:** Somente os tipos de configuração **Arquivo de Configuração XML** e **SQL Server** dão suporte à inclusão de várias propriedades em uma configuração.  
  
9. Na página Concluindo o Assistente, digite o nome da configuração e clique em **Concluir**.  
  
10. Exiba a configuração na caixa de diálogo **Organizador de Configurações do Pacote** .  
  
11. Clique em **Fechar**.  

## <a name="package-configurations-organizer"></a>Organizador de Configurações do Pacote
  Use a caixa de diálogo **Organizador de Configurações do Pacote** para habilitar configurações de pacote, visualizar uma lista de configurações para o pacote atual e para definir a ordem de preferência para carregar as configurações.  
  
> **OBSERVAÇÃO:** As configurações estão disponíveis para o modelo de implantação de pacote. Os parâmetros são usados no lugar das configurações para o modelo de implantação de projeto. O modelo de implantação de projeto permite que você implante projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obter mais informações sobre os modelos de implantação, consulte [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).    
  
 Se várias configurações atualizarem a mesma propriedade, valores de configurações listadas na parte inferior da lista de configurações substituirão os valores das configurações na parte superior da lista. O último valor carregado na propriedade é o valor usado quando o pacote executar. Além disso, se o pacote usar uma combinação de configuração direta, como um arquivo de configuração XML, e uma configuração indireta, como uma variável de ambiente, a configuração indireta que aponta para o local da configuração direta deve estar na parte superior da lista.  
  
> **OBSERVAÇÃO:** Quando as configurações de pacote são carregadas na ordem preferencial, elas são carregadas da parte superior da lista mostrada na caixa de diálogo **Organizador de Configurações do Pacote** até a parte inferior da lista. Porém, no tempo de execução, talvez as configurações do pacote não sejam carregadas na ordem preferencial. Em particular, Configurações do Pacote Pai são carregadas depois das configurações de outros tipos.  
  
 Configurações de Pacote atualizam os valores das propriedades de objetos de pacote em tempo de execução. Quando um pacote é carregado, os valores das configurações substituem os valores que foram definidos quando o pacote foi desenvolvido. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] dá suporte a diferentes tipos de configuração. Por exemplo, é possível usar um arquivo XML que pode ter várias configurações, ou uma variável de ambiente que contenha uma única configuração. Para obter mais informações, consulte [Package Configurations](../../integration-services/packages/package-configurations.md).  
  
### <a name="options"></a>Opções  
 **Habilitar configurações de pacote**  
 Selecione para usar configurações com o pacote.  
  
 **Nome da Configuração**  
 Exibe o nome da configuração.  
  
 **Tipo de Configuração**  
 Exibe o tipo do local onde as configurações são armazenadas.  
  
 **Cadeia de Caracteres de Configuração**  
 Exibe o local no qual os valores de configuração são armazenados. O local pode ser um caminho de um arquivo, o nome de uma variável de ambiente, uma chave do Registro, o nome de uma variável do pacote pai ou o nome de uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Objeto de Destino**  
 Exibe o nome do objeto atualizado pela configuração. Se a configuração for um arquivo de configuração XML ou uma tabela do SQL Server, a coluna ficará em branco porque a configuração pode incluir vários objetos.  
  
 **Propriedade de Destino**  
 Exibe o nome da propriedade modificada pela configuração. Esta coluna estará em branco se o tipo de configuração oferecer suporte a várias configurações.  
  
 **Adicionar**  
 Adicione uma configuração usando o Assistente de Configuração do Pacote.  
  
 **Editar**  
 Edite uma configuração existente executando novamente o Assistente de Configuração do Pacote.  
  
 **Remover**  
 Selecione uma configuração e depois clique em **Remover**.  
  
 **Setas**  
 Selecione uma configuração e use as setas para cima e para baixo para movê-la para cima ou para baixo na lista. As configurações são carregadas na sequência exibida na lista.  

## <a name="package-configuration-wizard-ui-reference"></a>Referência da interface do usuário do Assistente de Configuração de Pacotes
  Use o **Assistente de Configuração de Pacotes** para criar configurações que atualizem as propriedades de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e seus respectivos objetos em tempo de execução. Esse assistente é executado quando você adiciona uma nova configuração ou modifica uma existente na caixa de diálogo **Organizador de Configurações do Pacote** . Para abrir a caixa de diálogo **Organizador de Configurações do Pacote** , selecione **Configurações de Pacote** no menu **SSIS** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para obter mais informações, consulte [Criar configurações de pacote](../../integration-services/packages/create-package-configurations.md).  
  
> **OBSERVAÇÃO:** As configurações estão disponíveis para o modelo de implantação de pacote. Os parâmetros são usados no lugar das configurações para o modelo de implantação de projeto. O modelo de implantação de projeto permite que você implante projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obter mais informações sobre os modelos de implantação, consulte [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).  
  
 As seções a seguir descrevem as páginas do Assistente.  
  
### <a name="welcome-to-the-package-configuration-wizard-page"></a>Bem-vindo à página Assistente de Configuração de Pacotes  
 Use o **Assistente de Configuração do SSIS** para criar configurações que atualizem as propriedades de um pacote e seus respectivos objetos no tempo de execução.  
  
#### <a name="options"></a>Opções  
 **Não mostrar esta página novamente**  
 Ignore a página inicial da próxima vez que abrir o assistente.  
  
 **Próximo**  
 Vá para a próxima página do assistente.  
  
### <a name="select-configuration-type-page"></a>Selecionar a página Tipo de configuração  
 Use a página **Selecionar Tipo de Configuração** para especificar o tipo de configuração que deseja criar.  
  
 Se precisar de mais informações para determinar qual tipo de configuração usar, consulte [Configurações de Pacote](../../integration-services/packages/package-configurations.md).  
  
#### <a name="static-options"></a>Opções estáticas  
 **Tipo de configuração**  
 Selecione o tipo de fonte na qual deseja armazenar a configuração usando as seguintes opções:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Arquivo de configuração XML**|Armazene a configuração como um arquivo XML. Se este valor for selecionado, as opções dinâmicas serão exibidas na seção **Tipo de Configuração**.|  
|**Variável de ambiente**|Armazene a configuração em uma das variáveis de ambiente. Se este valor for selecionado, as opções dinâmicas serão exibidas na seção **Tipo de Configuração**.|  
|**Entrada de Registro**|Armazene a configuração no Registro. Se este valor for selecionado, as opções dinâmicas serão exibidas na seção **Tipo de Configuração**.|  
|**Variável de pacote pai**|Armazene a configuração como uma variável no pacote que contém a tarefa.  Se este valor for selecionado, as opções dinâmicas serão exibidas na seção **Tipo de Configuração**.|  
|**SQL Server**|Armazene a configuração em uma tabela no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se este valor for selecionado, as opções dinâmicas serão exibidas na seção **Tipo de Configuração**.|  
  
 **Próximo**  
 Visualize a próxima página da sequência do assistente.  
  
#### <a name="dynamic-options"></a>Opções dinâmicas  
  
##### <a name="configuration-type-option--xml-configuration-file"></a>Opção Tipo de Configuração = Arquivo de Configuração XML  
 **Especificar as definições de configuração diretamente**  
 Use para especificar as configurações diretamente.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Nome do arquivo de configuração**|Digite o caminho do arquivo de configuração gerado pelo assistente.|  
|**Procurar**|Use a caixa de diálogo **Selecionar Local do Arquivo de Configuração** para especificar o caminho do arquivo de configuração gerado pelo assistente. Se o arquivo não existir, ele será criado pelo assistente.|  
  
 **O local de configuração é armazenado em uma variável de ambiente**  
 Use para especificar a variável de ambiente na qual você deseja armazenar a configuração.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Variável de ambiente**|Selecione uma variável de ambiente da lista.|  
  
##### <a name="configuration-type-option--environment-variable"></a>Opção Tipo de Configuração = Variável de Ambiente  
 **Variável de ambiente**  
 Selecione a variável de ambiente que contém as informações de configuração.  
  
##### <a name="configuration-type-option--registry-entry"></a>Opção Tipo de Configuração = Entrada de Registro  
 **Especificar as definições de configuração diretamente**  
 Use para especificar as configurações diretamente.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Entrada de Registro**|Digite a chave do Registro que contém as informações de configuração. O formato é \<registry key>.<br /><br /> A chave do Registro já deve existir em HKEY_CURRENT_USER e deve ter um valor chamado Value (valor). O valor pode ser um DWORD ou uma cadeia de caracteres.<br /><br /> Se desejar usar uma chave do Registro que não está na raiz de HKEY_CURRENT_USER, use o formato \<Registry key\registry key\\...> para identificar a chave.|  
  
 **O local de configuração é armazenado em uma variável de ambiente**  
 Use para especificar a variável de ambiente na qual deseja armazenar a configuração.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Variável de ambiente**|Selecione uma variável de ambiente da lista.|  
  
##### <a name="configuration-type-option--parent-package-variable"></a>Opção Tipo de Configuração = Variável de pacote pai  
 **Especificar as definições de configuração diretamente**  
 Use para especificar as configurações diretamente.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Variável pai**|Especifique a variável no pacote pai que contém as informações de configuração.|  
  
 **O local de configuração é armazenado em uma variável de ambiente**  
 Use para especificar a variável de ambiente que armazena a configuração.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Variável de ambiente**|Selecione uma variável de ambiente da lista.|  
  
##### <a name="configuration-type-options--sql-server"></a>Opções de Tipo de Configuração = SQL Server  
 **Especificar as definições de configuração diretamente**  
 Use para especificar as configurações diretamente.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Conexão**|Selecione uma conexão da lista ou clique em **Nova** para criar uma nova conexão.|  
|**Tabela de configuração**|Selecione uma tabela existente ou clique em **Nova** para gravar uma instrução SQL que cria uma nova tabela.|  
|**Filtro de configuração**|Selecione um nome de configuração existente ou digite um novo nome.<br /><br /> Podem ser armazenadas muitas configurações do SQL Server na mesma tabela e cada configuração pode incluir vários itens de configuração.<br /><br /> O valor definido pelo usuário é armazenado na tabela para identificar os itens de configuração que pertencem a uma determinada configuração.|  
  
 **O local de configuração é armazenado em uma variável de ambiente**  
 Use para especificar a variável de ambiente onde a configuração está armazenada.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Variável de ambiente**|Selecione uma variável de ambiente da lista.|  
  
### <a name="select-objects-to-export-page"></a>Selecionar a página Objetos a Exportar  
 Use a página **Selecionar Propriedade de Destino ou Selecionar Propriedades a Serem Exportadas** para especificar as propriedades do objeto que a configuração contém. O recurso para selecionar várias propriedades estará disponível somente se você selecionar o tipo de configuração XML.  
  
#### <a name="options"></a>Opções  
 **Objetos**  
 Expanda a hierarquia de pacotes e selecione as propriedades a serem exportadas.  
  
 **Atributos da propriedade**  
 Exiba os atributos de uma propriedade.  
  
 **Próximo**  
 Vá para a próxima página do assistente.  
  
### <a name="completing-the-wizard-page"></a>Concluindo a página do assistente  
 Use a página **Concluindo o Assistente** para fornecer um nome para a configuração e definições de exibição usado pelo assistente para criar a configuração. Ao concluir o assistente, o **Organizador de Configurações do Pacote** é exibido e ele lista todas as configurações do pacote.  
  
#### <a name="options"></a>Opções  
 **Nome da configuração**  
 Digite o nome da configuração.  
  
 **Visualização**  
 Exiba as definições usadas pelo assistente para criar a configuração.  
  
 **Concluir**  
 Crie a configuração e saia do **Assistente de Configuração de Pacotes**.  

## <a name="child"></a> Usar os valores de variáveis e parâmetros em um pacote filho
  Este procedimento descreve como criar uma configuração de pacote que usa o tipo de configuração variável pai. Este tipo de configuração habilita um pacote filho que é executado de um pacote pai para acessar uma variável no pai.  
  
> [!NOTE]  
>  Você também pode passar valores para um pacote filho configurando a tarefa Executar Pacote para mapear as variáveis de pacote pai ou parâmetros, ou parâmetros de projeto, para parâmetros de pacote filho. Para obter mais informações, consulte [Execute Package Task](../../integration-services/control-flow/execute-package-task.md).  
  
 Não é necessário criar a variável no pacote pai antes de criar a configuração de pacote no pacote filho. É possível adicionar a variável ao pacote pai a qualquer momento, mas será preciso usar o nome exato da variável pai na configuração do pacote. Entretanto, antes de criar uma configuração da variável pai, é preciso que exista uma variável no pacote filho que possa ser atualizada pela configuração. Para obter mais informações sobre como adicionar e configurar variáveis, consulte [Adicionar, excluir, alterar o escopo de uma variável definida pelo usuário em um pacote](https://msdn.microsoft.com/library/cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e).  
  
 O escopo da variável no pacote pai que é usado na configuração da variável pai pode ser definido como a tarefa Executar Pacote, tanto para o contêiner que tenha a tarefa quanto para o pacote. Se várias variáveis tiverem o mesmo nome, será usada a variável que tiver o escopo mais próximo da tarefa Executar Pacote. O escopo mais próximo da tarefa Executar Pacote é a própria tarefa.  
  
### <a name="to-add-a-variable-to-a-parent-package"></a>Adicionar uma variável a um pacote pai  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote no qual deseja adicionar uma variável para passar a um pacote filho.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , defina o escopo da variável, seguindo uma das ações:  
  
    -   Para definir o escopo para o pacote, clique na superfície de design da guia **Fluxo de Controle** .  
  
    -   Para definir o escopo para um contêiner pai da tarefa Executar Pacote, clique no contêiner.  
  
    -   Para definir o escopo da tarefa Executar Pacote, clique na tarefa.  
  
4.  Adicione e configure uma variável.  
  
    > [!NOTE]  
    >  Selecione um tipo de dados que seja compatível com os dados que serão armazenados pela variável.  
  
5.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
### <a name="to-add-a-variable-to-a-child-package"></a>Adicionar uma variável a um pacote filho  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote no qual deseja adicionar uma configuração de variável pai.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No Designer de [!INCLUDE[ssIS](../../includes/ssis-md.md)] , defina o escopo para o pacote e clique na superfície de design da guia **Fluxo de Controle** .  
  
4.  Adicione e configure uma variável.  
  
    > [!NOTE]  
    >  Selecione um tipo de dados que seja compatível com os dados que serão armazenados pela variável.  
  
5.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  

## <a name="create-a-deployment-utility"></a>Criar um utilitário de implantação
  A primeira etapa da implantação de pacotes é a criação de um utilitário de implantação para um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . O utilitário de implantação é uma pasta que contém os arquivos necessários para a implantação dos pacotes em um projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em um servidor diferente. O utilitário de implantação é criado no computador no qual o projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é armazenado.  
  
 Você cria um utilitário de implantação de pacotes para um projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] configurando primeiro o processo de compilação para criar um utilitário de implantação e, depois, compilando o projeto. Quando você compila o projeto, todos os pacotes e configurações de pacote do projeto são incluídos automaticamente. Para implantar arquivos adicionais como um arquivo Leiame com o projeto, coloque os arquivos na pasta **Diversos** do projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Quando o projeto é compilado, esses arquivos também são automaticamente incluídos.  
  
 Você pode configurar cada implantação de projeto de modo diferente. Antes de compilar o projeto e criar o utilitário de implantação do pacote, você pode definir as propriedades no utilitário de implantação para personalizar o modo como os pacotes do projeto serão implantados. Por exemplo, você pode especificar se as configurações do pacote podem ser atualizadas quando o projeto é implantado. Para acessar as propriedades de um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , clique com o botão direito do mouse no projeto e clique em **Propriedades**.  
  
 A tabela a seguir lista as propriedades do utilitário de implantação.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|AllowConfigurationChange|Um valor que especifica se as configurações podem ser atualizadas durante a implantação.|  
|CreateDeploymentUtility|Um valor que especifica se um utilitário de implantação do pacote é criado quando o projeto é compilado. Essa propriedade deve ser **True** para criar um utilitário de implantação.|  
|DeploymentOutputPath|O local, relativo ao projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , do utilitário de implantação.|  
  
 Quando você cria um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], um arquivo de manifesto, \<project name>.SSISDeploymentManifest.xml, é criado e adicionado, junto com cópias dos pacotes de projeto e dependências do pacote, à pasta bin\Deployment do projeto ou ao local especificado na propriedade DeploymentOutputPath. O arquivo de manifesto lista os pacotes, as configurações de pacote e os diversos arquivos do projeto.  
  
 O conteúdo da pasta de implantação é atualizado toda vez que você compila o projeto. Isso significa que qualquer arquivo salvo nessa pasta que não for copiado novamente na pasta pelo processo de compilação será excluído. Por exemplo, serão excluídos arquivos de configuração do pacote salvos nas pastas de implantação.  
  
### <a name="to-create-a-package-deployment-utility"></a>Para criar um utilitário de implantação de pacote  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra a solução que contém o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para o qual você quer criar um utilitário de implantação de pacote.  
  
2.  Clique com o botão direito do mouse no projeto e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Páginas de Propriedades do \<project name>** , clique em **Utilitário de Implantação**.  
  
4.  Para atualizar as configurações do pacote quando os pacotes são implantados, defina **AllowConfigurationChanges** como **True**.  
  
5.  Defina **CreateDeploymentUtility** como **True**.  
  
6.  Opcionalmente, atualize o local do utilitário de implantação modificando a propriedade do **DeploymentOutputPath** .  
  
7.  Clique em **OK**.  
  
8.  No Gerenciador de Soluções, clique com o botão direito do mouse no projeto e clique em **Criar**.  
  
9. Visualize o progresso da compilação e os erros de compilação na janela **Saída** .  

## <a name="deploy-packages-by-using-the-deployment-utility"></a>Implantar pacotes usando o utilitário de implantação
  Quando você cria um utilitário de implantação para instalar pacotes de um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em um computador diferente daquele em que o utilitário de implantação foi criado, é necessário primeiro copiar a pasta de implantação no computador de destino.  
  
 O caminho da pasta de implantação está especificado na propriedade DeploymentOutputPath do projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para o qual foi criado o utilitário de implantação. O caminho padrão é bin\Deployment, relativo ao projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obter mais informações, consulte [Criar um utilitário de implantação](../../integration-services/packages/create-a-deployment-utility.md).  
  
 É possível usar o Assistente de Instalação de Pacotes para instalar os pacotes. Para iniciar o assistente, clique duas vezes no arquivo do utilitário de implantação depois de ter copiado a pasta de implantação no servidor. Esse arquivo é chamado \<project name>.SSISDeploymentManifest e pode ser encontrado na pasta de implantação do computador de destino.  
  
> [!NOTE]  
>  Dependendo da versão do pacote que está sendo implantado, você poderá encontrar um erro se tiver diferentes versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas lado a lado. Esse erro pode ocorrer porque a extensão do nome de arquivo .SSISDeploymentManifest é a mesma para todas as versões do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Clicar duas vezes no arquivo chama o instalador (dtsinstall.exe) da versão instalada mais recentemente do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], que talvez não seja a mesma versão do arquivo de utilitário de implantação. Para resolver esse problema, execute a versão correta de dtsinstall.exe na linha de comando e forneça o caminho do arquivo de utilitário de implantação.  
  
 O Assistente de Instalação de Pacotes o guiará pelas etapas para instalar pacotes no sistema de arquivos ou no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você pode configurar a instalação das seguintes formas:  
  
-   Escolhendo o local e o tipo de local para instalar os pacotes.  
  
-   Escolhendo o local para instalar dependências dos pacotes.  
  
-   Validando os pacotes após a instalação no servidor de destino.  
  
 As dependências com base em arquivo para pacotes sempre são instaladas no sistema de arquivos. Se for instalado um pacote no sistema de arquivos, as dependências serão instaladas na mesma pasta especificada por você para o pacote. Se instalar um pacote em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você poderá especificar a pasta na qual armazenará as dependências com base no arquivo.  
  
 Se o pacote incluir configurações que deseja modificar para usar no computador destino, você poderá atualizar os valores e as propriedades usando o assistente.  
  
 Além de instalar os pacotes com o Assistente de Instalação de Pacotes, você pode copiar e mover pacotes com o utilitário de prompt de comando **dtutil** . Para obter mais informações, consulte [dtutil Utility](../../integration-services/dtutil-utility.md).  
  
### <a name="to-deploy-packages-to-an-instance-of-sql-server"></a>Para implantar pacotes em uma instância do SQL Server  
  
1.  Abra a pasta de implantação no computador de destino.  
  
2.  Clique duas vezes no arquivo de manifesto, \<project name>.SSISDeploymentManifest, para iniciar o Assistente de Instalação de Pacotes.  
  
3.  Na página **Implantar Pacotes SSIS** , selecione a opção **Implantação no SQL Server** .  
  
4.  Opcionalmente, selecione **Validar pacotes após instalação** para validar os pacotes depois de instalados no servidor de destino.  
  
5.  Na página **Especificar SQL Server de Destino** , especifique a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instalar os pacotes e selecionar um modo de autenticação. Se você selecionar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , precisará fornecer um nome de usuário e uma senha.  
  
6.  Na página **Selecionar Pasta de Instalação** , especifique a pasta no sistema de arquivos para as dependências do pacote que serão instaladas.  
  
7.  Se o pacote incluir configurações, você poderá editar as configurações atualizando os valores na lista **Valor** da página Configurar Pacotes.  
  
8.  Se você escolheu validar os pacotes após a instalação, exiba os resultados de validação dos pacotes implantados.  

## <a name="redeployment-of-packages"></a>Reimplantação de pacotes
  Após a implantação de um projeto, talvez seja necessário atualizar ou estender a funcionalidade de pacotes e reimplantar o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém os pacotes atualizados. Como parte do processo de reimplantação dos pacotes, você deve revisar as propriedades de configuração incluídas no utilitário de implantação. Por exemplo, você pode desejar não permitir mudanças de configuração depois que o pacote for reimplantado.  
  
### <a name="process-for-redeployment"></a>Processo de reimplantação  
 Após a conclusão da atualização dos pacotes, você deve recriar o projeto, copiar a pasta de implantação para o computador de destino e executar novamente o Assistente de Instalação de Pacotes.  
  
 Se você atualizar apenas alguns pacotes do projeto, talvez não queira reimplantar o projeto todo. Para implantar apenas alguns pacotes, você pode criar um novo projeto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , adicionar os pacotes atualizados ao novo projeto e compilar e implantar o projeto. As configurações de pacotes são copiadas automaticamente com o pacote quando você adiciona o pacote a um projeto diferente.  

## <a name="package-installation-wizard-ui-reference"></a>Referência da interface do usuário do Assistente de Instalação de Pacotes
  Use o **Assistente de Instalação de Pacotes** para implantar um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , inclusive os pacotes e arquivos diversos contidos nele, bem como todas as dependências do pacote.  
  
 Antes de implantar pacotes, você pode criar configurações e implantá-las com os pacotes. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa configurações para atualizar dinamicamente as propriedades de pacotes e objetos de pacote em tempo de execução. Por exemplo, a cadeia de conexão de uma conexão OLE DB pode ser definida dinamicamente em tempo de execução fornecendo-se uma configuração que mapeie um valor para uma propriedade que contenha a cadeia de conexão.  
  
 Você não pode executar o Assistente de Instalação de Pacotes enquanto não criar um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e um utilitário de implantação. Para obter mais informações, consulte [Implantar pacotes por meio do utilitário de implantação](../../integration-services/packages/deploy-packages-by-using-the-deployment-utility.md).  
  
 As seções a seguir descrevem as páginas do assistente.  
  
### <a name="welcome-to-the-package-installation-wizard-page"></a>Bem-vindo à página Assistente de Instalação de Pacotes  
 Use o **Assistente de Instalação de Pacotes** para implantar um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para o qual você criou um utilitário de implantação de pacotes.  
  
 **Não mostrar esta página inicial novamente**  
 Selecione para ignorar a página inicial ao executar o assistente novamente.  
  
 **Próximo**  
 Vá para a próxima página do assistente.  
  
 **Concluir**  
 Pule para a página Concluir o assistente de instalação de pacotes. Use esta opção caso você já tenha retornado às páginas anteriores do assistente para revisar suas opções e especificado todas as opções necessárias.  
  
### <a name="configure-packages-page"></a>Configurar a página Pacotes  
 Use a página **Configurar Pacotes** para editar as configurações do pacote.  
  
#### <a name="options"></a>Opções  
 **Arquivo de configuração**  
 Edite o conteúdo de um arquivo de configuração selecionando o arquivo na lista.  
  
 **Tópicos relacionados:** [Criar configurações de pacote](../../integration-services/packages/create-package-configurations.md)  
  
 **Caminho**  
 Exiba o caminho da propriedade a ser configurada.  
  
 **Tipo**  
 Exiba o tipo de dados da propriedade.  
  
 **Value**  
 Especifique o valor da configuração.  
  
 **Próximo**  
 Vá para a próxima página do assistente.  
  
 **Concluir**  
 Pule para a página Concluir o assistente de instalação de pacotes. Use esta opção caso você já tenha retornado às páginas anteriores do assistente para revisar suas opções e especificado todas as opções necessárias.  
  
### <a name="confirm-installation-page"></a>Página Confirmar Instalação  
 Use a página **Confirmar Instalação** para iniciar a instalação de pacotes, para exibir o status e para exibir as informações que serão usadas pelo assistente para instalar os arquivos a partir do projeto especificado.  
  
 **Próximo**  
 Instale os pacotes e suas dependências e vá para a próxima página do assistente quando instalação for concluída.  
  
 **Status**  
 Mostra o progresso da instalação do pacote.  
  
 **Concluir**  
 Vá para a página Concluir o assistente de instalação de pacotes. Use esta opção caso você já tenha retornado às páginas anteriores do assistente para revisar suas opções e especificado todas as opções necessárias.  
  
### <a name="deploy-ssis-packages-page"></a>Página Implantar Pacotes SSIS  
 Use a página **Implantar Pacotes do SSIS** para especificar onde os pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e suas dependências serão instalados.  
  
#### <a name="options"></a>Opções  
 **Implantação do sistema de arquivos**  
 Distribua os pacotes e suas dependências em uma pasta especificada no sistema de arquivos.  
  
 **Implantação no SQL Server**  
 Implante os pacotes e suas dependências em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use esta opção caso o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] compartilhe pacotes entre servidores. Todas as dependências do pacote são instaladas na pasta especificada no sistema de arquivos.  
  
 **Validar pacotes após a instalação**  
 Indique se é preciso validar os pacotes após a instalação.  
  
 **Próximo**  
 Vá para a próxima página do assistente.  
  
 **Concluir**  
 Pule para a página Concluir o assistente de instalação de pacotes. Use esta opção caso você já tenha retornado às páginas anteriores do assistente para revisar suas opções e especificado todas as opções necessárias.  
  
### <a name="packages-validation-page"></a>Página Validação de Pacotes  
 Use a página **Validação de Pacotes** para exibir o progresso e os resultados da validação do pacote.  
  
 **Próximo**  
 Vá para a próxima página do assistente.  
  
### <a name="select-installation-folder-page"></a>Página Selecionar Pasta de Instalação  
 Use a página **Selecionar Pasta de Instalação** para especificar a pasta do arquivo de sistemas na qual os pacotes e as dependências de pacotes serão instalados.  
  
#### <a name="options"></a>Opções  
 **Pasta**  
 Especifique o caminho e a pasta nos quais o pacote e suas dependências serão copiados.  
  
 **Procurar**  
 Procure a pasta de destino usando a caixa de diálogo **Procurar Pasta** .  
  
 **Próximo**  
 Vá para a próxima página do assistente.  
  
 **Concluir**  
 Pule para a página Concluir o assistente de instalação de pacotes. Use esta opção caso você já tenha retornado às páginas anteriores do assistente para revisar suas opções e especificado todas as opções necessárias.  
  
### <a name="specify-target-sql-server-page"></a>Página Especificar SQL Server de Destino  
 Use a página **Especificar SQL Server de Destino** para especificar as opções para implantar o pacote a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
#### <a name="options"></a>Opções  
 **Nome do servidor**  
 Especifique o nome do servidor para o qual deseja implantar os pacotes.  
  
 **Usar Autenticação do Windows**  
 Especifique se será usada a Autenticação do Windows para efetuar login no servidor. A Autenticação do Windows é recomendada para obter melhor segurança.  
  
 **Usar Autenticação do SQL Server**  
 Especifique se o pacote deve usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para fazer login no servidor. Se você usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , será preciso fornecer um nome de usuário e uma senha.  
  
 **User name**  
 Especifique um nome de usuário.  
  
 **Senha**  
 Especifique uma senha.  
  
 **Caminho do pacote**  
 Especifique o nome da pasta lógica ou digite "/" para a pasta padrão.  
  
 Para selecionar a pasta na caixa de diálogo **Pacote do SSIS** , clique em procurar (...). Entretanto, a caixa de diálogo não fornece uma maneira para selecionar a pasta padrão. Se desejar usar a pasta padrão, digite "/" na caixa de texto.  
  
> [!NOTE]  
>  Se você não inserir um caminho de pacote válido, a seguinte mensagem de erro será exibida: "Um ou mais argumentos são inválidos."  
  
 **Depender do armazenamento do servidor para criptografia**  
 Selecione esta opção para usar os recursos do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para ajudar a manter a segurança dos pacotes.  
  
 **Próximo**  
 Vá para a próxima página do assistente.  
  
 **Concluir**  
 Pule para a página Concluir o assistente de instalação de pacotes. Use esta opção caso você já tenha retornado às páginas anteriores do assistente para revisar suas opções e especificado todas as opções necessárias.  
  
### <a name="finish-the-package-installation-page"></a>Página Concluir o Assistente de Instalação de Pacotes  
 Use a página **Concluir o Assistente de Instalação de Pacotes** para exibir um resumo dos resultados da instalação do pacote. Esta página fornece detalhes como o nome do projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que foi implantado, os pacotes que foram instalados, os arquivos de configuração e o local da instalação.  
  
 **Concluir**  
 Para sair do assistente, clique em **Concluir**.  


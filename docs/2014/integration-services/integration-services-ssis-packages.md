---
title: Pacotes do SSIS (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Integration Services packages, about packages
- packages [Integration Services], about packages
- SSIS packages, about packages
- SSIS packages
- SQL Server Integration Services packages
- containers [Integration Services], packages
- packages [Integration Services]
- Integration Services packages, about packages
- Integration Services packages
ms.assetid: 9266bc64-7e1a-4e78-913b-a8deaa9843bf
caps.latest.revision: 68
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 85eeb75badeed90812c657b9dbdc64e261947e20
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117937"
---
# <a name="integration-services-ssis-packages"></a>Pacotes do SSIS (Integration Services)
  Um pacote é uma coleção organizada de conexões, elementos de fluxo de controle, elementos de fluxo de dados, manipuladores de eventos, variáveis, parâmetros e configurações que você agrupa usando as ferramentas de design gráfico fornecidas pelo [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ou cria programaticamente.  Você salva o pacote concluído no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], no armazenamento de pacotes do [!INCLUDE[ssIS](../includes/ssis-md.md)] ou no sistema de arquivos, ou pode implantar o projeto ssISnoversion para o servidor do [!INCLUDE[ssIS](../includes/ssis-md.md)] . O pacote é a unidade de trabalho que é recuperada, executada e salva.  
  
 Quando você cria um pacote pela primeira vez, ele é um objeto vazio que não desempenha nenhuma função. Para adicionar funcionalidade a um pacote, adicione um fluxo de controle e, opcionalmente, um ou mais fluxos de dados ao pacote.  
  
 O diagrama a seguir mostra um pacote simples que contém um fluxo de controle com uma tarefa de Fluxo de Dados, que, por sua vez, contém um fluxo de dados.  
  
 ![Um pacote com um fluxo de controle e um fluxo de dados](media/ssis-package.gif "Um pacote com um fluxo de controle e um fluxo de dados")  
  
 Depois de criar o pacote básico, você pode adicionar recursos avançados como registro e variáveis para estender a funcionalidade do pacote. Para obter mais informações, consulte a seção sobre Objetos que estendem a funcionalidade de pacotes.  
  
 O pacote concluído pode ser configurado com a definição de propriedades no nível do pacote que implementam a segurança, habilitam a reinicialização de pacotes a partir de pontos de verificação ou incorporam transações ao fluxo de trabalho do pacote. Para obter mais informações, consulte a seção sobre Propriedades que dão suporte a recursos estendidos.  
  
## <a name="package-content"></a>Conteúdo do pacote  
 Um fluxo de controle consiste em uma ou mais tarefas e contêineres executados quando o pacote é executado. Para controlar a ordem ou definir as condições para executar a próxima tarefa ou o contêiner no fluxo de controle do pacote, use restrições de precedência para conectar as tarefas e os contêineres em um pacote. Um subconjunto de tarefas e contêineres também pode ser agrupado e executado repetidamente como uma unidade dentro do fluxo de controle do pacote. Para obter mais informações, consulte [Control Flow](control-flow/control-flow.md).  
  
 Um fluxo de dados consiste nas fontes e destinos que extraem e carregam dados, nas transformações que modificam e estendem dados e nos caminhos que vinculam fontes, transformações e destinos. Antes de poder adicionar um fluxo de dados a um pacote, o fluxo de controle do pacote deve incluir uma tarefa de Fluxo de Dados. A tarefa de Fluxo de Dados é o executável dentro do pacote do [!INCLUDE[ssIS](../includes/ssis-md.md)] que cria, ordena e executa o fluxo de dados. Uma instância separada do mecanismo de fluxo de dados é aberta para cada tarefa de Fluxo de Dados em um pacote. Para obter mais informações, consulte [Data Flow Task](control-flow/data-flow-task.md) e [Data Flow](data-flow/data-flow.md).  
  
 Um pacote normalmente inclui pelo menos um gerenciador de conexões. Um gerenciador de conexões é um link entre um pacote e uma fonte de dados que define a cadeia de conexão para acesso a dados que as tarefas, transformações e manipuladores de eventos usados pelo pacote. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] inclui tipos de conexão para fontes de dados, como arquivos de texto e XML, bancos de dados relacionais e bancos de dados e projetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Conexões](connection-manager/integration-services-ssis-connections.md).  
  
## <a name="package-templates"></a>Modelos de pacote  
 Os pacotes costumam ser usados como modelos a partir dos quais se criam pacotes que compartilham funcionalidade básica. Crie o pacote básico e copie-o ou especifique que o pacote é um modelo. Por exemplo, um pacote que baixa e copia arquivos e extrai os dados pode incluir as tarefas de FTP e Sistema de Arquivos em um Loop Foreach que enumera arquivos em uma pasta. Ele também pode incluir gerenciadores de conexões de Arquivo Simples para acessar os dados e fontes de Arquivos Simples a fim de extrair os dados. O destino dos dados varia e é adicionado a cada novo pacote depois de ser copiado do pacote básico. Você também pode criar pacotes e usá-los como modelos para novos pacotes adicionados a um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Para obter mais informações, consulte [Create Packages in SQL Server Data Tools](create-packages-in-sql-server-data-tools.md).  
  
 Quando um pacote é criado pela primeira vez, seja programaticamente ou usando o Designer SSIS, um GUID é adicionado à sua `ID` propriedade e um nome para seu `Name` propriedade. Se você criar um novo pacote copiando um pacote existente ou usando um modelo de pacote, o nome e o GUID do pacote também serão copiados. Isso pode ser um problema se você usa log, porque o GUID e o nome do pacote são gravados em logs para identificar o pacote ao qual pertencem as informações registradas. Portanto, você deve atualizar o nome e o GUID dos novos pacotes para ajudar a diferenciá-los do pacote a partir do qual foram copiados e entre si nos dados de log.  
  
 Para alterar o GUID do pacote, você regenerar uma GUID de `ID` propriedade na janela Propriedades no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para alterar o nome do pacote, você pode atualizar o valor de `Name` propriedade na janela Propriedades. Você também pode usar o prompt de comando **dtutil** ou atualizar o GUID e o nome de forma programática. Para obter mais informações, consulte [Definir as propriedades do pacote](set-package-properties.md) e [Utilitário dtutil](dtutil-utility.md).  
  
## <a name="objects-that-extend-package-functionality"></a>Objetos que estendem a funcionalidade do pacote  
 Os pacotes podem incluir objetos adicionais que oferecem recursos avançados ou estendem a funcionalidade existente, como manipuladores de eventos, configurações, log e variáveis.  
  
### <a name="event-handlers"></a>Manipuladores de eventos  
 Um manipulador de eventos é um fluxo de trabalho que é executado como resposta aos eventos gerados por um pacote, tarefa ou contêiner. Por exemplo, você pode usar um manipulador de eventos para verificar o espaço em disco, caso ocorra um evento de pré-execução ou um erro, e enviar um email informando o espaço disponível ou os erros a um administrador. Um manipulador de eventos é criado como um pacote, com um fluxo de controle e fluxos de dados opcionais. Manipuladores de eventos podem ser adicionados a tarefas ou contêineres individuais no pacote. Para obter mais informações, consulte [Manipuladores de Eventos do Integration Services &#40;SSIS&#41;](integration-services-ssis-event-handlers.md).  
  
### <a name="configurations"></a>Configurações  
 Uma configuração é um conjunto de pares propriedade-valor que define as propriedade do pacote e suas tarefas, contêineres, variáveis, conexões e manipuladores de eventos quando o pacote é executado. Usar configurações possibilita atualizar as propriedades sem modificar o pacote. Quando o pacote é executado, as informações de configuração são carregadas, atualizando os valores das propriedades. Por exemplo, uma configuração pode atualizar a cadeia de conexão da conexão.  
  
 A configuração é salva e implantada com o pacote quando este é instalado em um computador diferente. Os valores da configuração podem ser atualizados quando o pacote é instalado para dar suporte ao pacote em um ambiente diferente. Para obter mais informações, consulte [Criar configurações de pacote](../../2014/integration-services/create-package-configurations.md).  
  
### <a name="logging-and-log-providers"></a>Log e provedores de log  
 Um log é uma coleção de informações sobre o pacote coletada quando este é executado. Por exemplo, um log pode fornecer a hora inicial e final da execução de um pacote. Um provedor de log define o tipo de destino e o formato que o pacote e seus contêineres e tarefas podem usar para registrar informações em tempo de execução. Os logs são associados a um pacote, mas as tarefas e os contêineres do pacote podem registrar informações em qualquer log de pacote. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] inclui vários provedores de log internos para registro em log. Por exemplo, o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] inclui provedores de log para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e arquivos de texto. Você também pode criar provedores de log personalizados e usá-los para registrar informações. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](performance/integration-services-ssis-logging.md).  
  
### <a name="variables"></a>Variáveis  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] dá suporte a variáveis de sistema e a variáveis definidas pelo usuário. As variáveis de sistema oferecem informações úteis sobre objetos de pacote em tempo de execução e as variáveis definidas pelo usuário suportam cenários personalizados em pacotes. Os dois tipos de variáveis podem ser usados em expressões, scripts e configurações.  
  
 As variáveis no nível do pacote incluem variáveis de sistema predefinidas disponíveis para um pacote e variáveis definidas pelo usuário com o escopo do pacote. Para obter mais informações, consulte [Integration Services &#40;SSIS&#41; Variables](integration-services-ssis-variables.md).  
  
### <a name="parameters"></a>Parâmetros  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] permitem atribuir valores às propriedades nos pacotes em tempo de execução do pacote. Você pode criar *parâmetros de projeto* em nível de projeto e *parâmetros de pacote* em nível de pacote. Os parâmetros do projeto são usados para fornecer uma entrada externa que o projeto recebe para um ou mais pacotes no projeto. Os parâmetros do pacote permitem modificar a execução do pacote sem a necessidade de editar e reimplantar o pacote. Para obter mais informações, consulte [Parâmetros do Integration Services &#40;SSIS&#41;](integration-services-ssis-package-and-project-parameters.md).  
  
## <a name="package-properties-that-support-extended-features"></a>Propriedades de pacote que dão suporte a recursos estendidos  
 O objeto do pacote pode ser configurado para dar suporte a recursos como reiniciar o pacote nos pontos de verificação, assinar o pacote com um certificado digital, definir o nível de proteção do pacote e assegurar a integridade de dados usando transações.  
  
### <a name="restarting-packages"></a>Reiniciando pacotes  
 O pacote inclui propriedades de pontos de verificação que você pode usar para reiniciar o pacote quando uma ou mais tarefas falham. Por exemplo, se um pacote tiver duas tarefas de Fluxo de Dados que atualizam duas tabelas diferentes e a segunda tarefa falhar, o pacote poderá ser executado novamente sem repetir a primeira tarefa de Fluxo de Dados. Reiniciar um pacote pode economizar tempo no caso de pacotes de longa execução. Reiniciar significa que você pode iniciar o pacote a partir da tarefa com falha em vez de ter que executar novamente o pacote inteiro. Para saber mais, confira [Reiniciar pacotes por meio de pontos de verificação](packages/restart-packages-by-using-checkpoints.md).  
  
### <a name="securing-packages"></a>Protegendo pacotes  
 Um pacote pode ser assinado com uma assinatura digital e criptografado usando uma senha ou uma chave de usuário. Uma assinatura digital autentica a fonte do pacote. No entanto, você também deve configurar o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para verificar a assinatura digital quando o pacote for carregado. Para obter mais informações, consulte [Identificar a origem de pacotes com assinaturas digitais](security/identify-the-source-of-packages-with-digital-signatures.md) e [Controle de acesso de dados confidenciais em pacotes](security/access-control-for-sensitive-data-in-packages.md).  
  
### <a name="supporting-transactions"></a>Dando suporte a transações  
 Definir um atributo de transação no pacote permite que tarefas, contêineres e conexões no pacote se unam à transação. Atributos de transação asseguram que o pacote e seus elementos tenham êxito ou falhem como uma unidade. Os pacotes também podem executar outros pacotes e envolver outros pacotes em transações, de modo que você pode executar vários pacotes como uma única unidade de trabalho. Para obter mais informações, consulte [Transações do Integration Services](integration-services-transactions.md).  
  
## <a name="custom-log-entries-available-on-the-package"></a>Entradas de log personalizadas disponíveis no pacote  
 A tabela a seguir relaciona as entradas de log personalizadas para pacotes. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](performance/integration-services-ssis-logging.md) e [Mensagens personalizadas para log](../../2014/integration-services/custom-messages-for-logging.md).  
  
|Entrada de log|Description|  
|---------------|-----------------|  
|`PackageStart`|Indica que o pacote começou a ser executado.<br /><br /> Observação: esta entrada de log é gravada no log automaticamente. Não é possível excluí-la.|  
|`PackageEnd`|Indica que o pacote foi concluído.<br /><br /> Observação: esta entrada de log é gravada no log automaticamente. Não é possível excluí-la.|  
|`Diagnostic`|Fornece informações sobre a configuração do sistema que afeta a execução de pacotes como os executáveis numéricos que podem ser executados simultaneamente.|  
  
## <a name="configuration-of-packages"></a>Configuração de pacotes  
 Você pode definir as propriedades na janela **Propriedades** do [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre como definir essas propriedades usando o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], consulte [Definir as propriedades do pacote](set-package-properties.md).  
  
 Para obter informações sobre como definir essas propriedades programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.Package>.  
  
## <a name="related-tasks"></a>Related Tasks  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] inclui duas ferramentas gráficas, o Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] e o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , além do modelo de objeto do [!INCLUDE[ssIS](../includes/ssis-md.md)] para criar pacotes. Consulte os tópicos a seguir para obter detalhes.  
  
-   [Executar o Assistente de Importação e Exportação do SQL Server](import-export-data/start-the-sql-server-import-and-export-wizard.md)  
  
-   [Criar pacotes nas Ferramentas de Dados do SQL Server](create-packages-in-sql-server-data-tools.md)  
  
-   Consulte a seção **Compilando pacotes programaticamente** no Guia do Desenvolvedor.  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Implementando o SQL Server Integration Services com Microsoft Dynamics Mobile](http://msdn.microsoft.com/library/cc563950)  
  
-   [Como: configurar o pacote do SQL Server Integration Services para Microsoft Dynamics AX](http://msdn.microsoft.com/library/bb986852)  
  
  
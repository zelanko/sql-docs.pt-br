---
title: Referência de interface do usuário do Assistente de configuração do pacote | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.configwizard.selectobjects.f1
- sql12.dts.configwizard.selecconfigtype.f1
- sql12.dts.configwizard.finishdtsconfiguration.f1
- sql12.dts.configwizard.welcome.f1
ms.assetid: adca6938-6d5a-40ec-950e-dceb79d044fe
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 72909e812418d26d9f9f2905b41e686c36f6b670
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66056943"
---
# <a name="package-configuration-wizard-ui-reference"></a>Referência da interface do usuário do Assistente de Configuração de Pacotes
  Use o **Assistente de Configuração de Pacotes** para criar configurações que atualizem as propriedades de um pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e seus respectivos objetos em tempo de execução. Esse assistente é executado quando você adiciona uma nova configuração ou modifica uma existente na caixa de diálogo **Organizador de Configurações do Pacote** . Para abrir a caixa de diálogo **Organizador de Configurações do Pacote**, selecione **Configurações de Pacote** no menu **SSIS** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para obter mais informações, consulte [Criar configurações de pacote](../../2014/integration-services/create-package-configurations.md).  
  
> [!NOTE]  
>  As configurações estão disponíveis para o modelo de implantação de pacote. Os parâmetros são usados no lugar das configurações para o modelo de implantação de projeto. O modelo de implantação de projeto permite que você implante projetos do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no servidor do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Para obter mais informações sobre os modelos de implantação, consulte [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
 As seções a seguir descrevem as páginas do Assistente.  
  
## <a name="welcome-to-the-package-configuration-wizard-page"></a>Bem-vindo à página Assistente de Configuração de Pacotes  
 Use o **Assistente de Configuração do SSIS** para criar configurações que atualizem as propriedades de um pacote e seus respectivos objetos no tempo de execução.  
  
### <a name="options"></a>Opções  
 **Não mostrar esta página novamente**  
 Ignore a página inicial da próxima vez que abrir o assistente.  
  
 **Próximo**  
 Vá para a próxima página do assistente.  
  
## <a name="select-configuration-type-page"></a>Selecionar a página Tipo de configuração  
 Use a página **Selecionar Tipo de Configuração** para especificar o tipo de configuração que deseja criar.  
  
 Se precisar de mais informações para determinar qual tipo de configuração usar, consulte [Configurações de Pacote](../../2014/integration-services/package-configurations.md).  
  
### <a name="static-options"></a>Opções estáticas  
 **Tipo de configuração**  
 Selecione o tipo de fonte na qual deseja armazenar a configuração usando as seguintes opções:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Arquivo de configuração XML**|Armazene a configuração como um arquivo XML. Se este valor for selecionado, as opções dinâmicas serão exibidas na seção **Tipo de Configuração**.|  
|**Variável de ambiente**|Armazene a configuração em uma das variáveis de ambiente. Se este valor for selecionado, as opções dinâmicas serão exibidas na seção **Tipo de Configuração**.|  
|**Entrada de Registro**|Armazene a configuração no Registro. Se este valor for selecionado, as opções dinâmicas serão exibidas na seção **Tipo de Configuração**.|  
|**Variável de pacote pai**|Armazene a configuração como uma variável no pacote que contém a tarefa.  Se este valor for selecionado, as opções dinâmicas serão exibidas na seção **Tipo de Configuração**.|  
|**SQL Server**|Armazene a configuração em uma tabela no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Se este valor for selecionado, as opções dinâmicas serão exibidas na seção **Tipo de Configuração**.|  
  
 **Próximo**  
 Visualize a próxima página da sequência do assistente.  
  
### <a name="dynamic-options"></a>Opções dinâmicas  
  
#### <a name="configuration-type-option--xml-configuration-file"></a>Opção Tipo de Configuração = Arquivo de Configuração XML  
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
  
#### <a name="configuration-type-option--environment-variable"></a>Opção Tipo de Configuração = Variável de Ambiente  
 **Variável de ambiente**  
 Selecione a variável de ambiente que contém as informações de configuração.  
  
#### <a name="configuration-type-option--registry-entry"></a>Opção Tipo de Configuração = Entrada de Registro  
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
  
#### <a name="configuration-type-option--parent-package-variable"></a>Opção Tipo de Configuração = Variável de pacote pai  
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
  
#### <a name="configuration-type-options--sql-server"></a>Opções de Tipo de Configuração = SQL Server  
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
  
## <a name="select-objects-to-export-page"></a>Selecionar a página Objetos a Exportar  
 Use a página **Selecionar Propriedade de Destino ou Selecionar Propriedades a Serem Exportadas** para especificar as propriedades do objeto que a configuração contém. O recurso para selecionar várias propriedades estará disponível somente se você selecionar o tipo de configuração XML.  
  
### <a name="options"></a>Opções  
 **Objetos**  
 Expanda a hierarquia de pacotes e selecione as propriedades a serem exportadas.  
  
 **Atributos da propriedade**  
 Exiba os atributos de uma propriedade.  
  
 **Próximo**  
 Vá para a próxima página do assistente.  
  
## <a name="completing-the-wizard-page"></a>Concluindo a página do assistente  
 Use a página **Concluindo o Assistente** para fornecer um nome para a configuração e definições de exibição usado pelo assistente para criar a configuração. Ao concluir o assistente, o **Organizador de Configurações do Pacote** é exibido e ele lista todas as configurações do pacote.  
  
### <a name="options"></a>Opções  
 **Nome da configuração**  
 Digite o nome da configuração.  
  
 **Visualização**  
 Exiba as definições usadas pelo assistente para criar a configuração.  
  
 **Concluir**  
 Crie a configuração e saia do **Assistente de Configuração de Pacotes**.  
  
## <a name="see-also"></a>Consulte também  
 [Criar configurações de pacote](../../2014/integration-services/create-package-configurations.md)  
  
  

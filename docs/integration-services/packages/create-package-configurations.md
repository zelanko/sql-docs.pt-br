---
title: "Criar configura&#231;&#245;es de pacote | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "pacotes do SQL Server Integration Services, configurações"
  - "caixa de diálogo Organizador de Configurações do Pacote"
  - "Pacotes do SSIS, configurações"
  - "pacotes do Integration Services, configurações"
  - "configurações [Integration Services]"
  - "pacotes [Integration Services], configurações"
  - "implantando pacotes [Integration Services], configurações"
ms.assetid: 91ac0347-f908-44f5-bd3d-115790223af4
caps.latest.revision: 72
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 72
---
# Criar configura&#231;&#245;es de pacote
  Crie as configurações do pacote por meio da caixa de diálogo **Organizador de Configurações de Pacote** e do Assistente de Configuração de Pacote. Para acessar essas ferramentas, clique em **Configurações do Pacote** no menu de **SSIS** em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
  
 **OBSERVAÇÕES:**
>Você também pode acessar o **Organizador de Configurações de Pacote** clicando no botão de reticências ao lado da propriedade **Configuração**. A propriedade Configuração aparece na janela de propriedades para o pacote.  
  
>As configurações estão disponíveis para o modelo de implantação de pacote. Os parâmetros são usados no lugar das configurações para o modelo de implantação de projeto. O modelo de implantação de projeto permite que você implante projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obter mais informações sobre os modelos de implantação, consulte [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).  
  
>Na caixa de diálogo **Organizador de Configurações do Pacote**, você pode habilitar pacotes para usar configurações, adicionar e excluir configurações e definir a ordem de preferência para carregar as configurações. 
 
>Quando as configurações de pacote são carregadas na ordem preferencial, elas são carregadas da parte superior da lista mostrada na caixa de diálogo **Organizador de Configurações do Pacote** até a parte inferior da lista. Porém, no tempo de execução, talvez as configurações do pacote não sejam carregadas na ordem preferencial. Em particular, as configurações do pacote pai são carregadas depois das configurações de outros tipos.  
  
>Se várias configurações definirem a mesma propriedade de objeto, o valor carregado por último será usado no tempo de execução.  
  
 Na caixa de diálogo **Organizador de Configurações do Pacote**, você executa o Assistente de Configuração de Pacotes, que o guia através de etapas para criar uma configuração. Para executar o Assistente de Configuração de Pacotes, adicione uma nova configuração na caixa de diálogo **Organizador de Configurações do Pacote** ou edite uma existente. Nas páginas do assistente, você escolhe o tipo de configuração, escolhe se quer acessar a configuração diretamente ou usar variáveis de ambiente, e seleciona as propriedades a serem salvas na configuração.  
  
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
  
 Depois que o assistente terminar, a nova configuração é adicionada à lista de configurações na caixa de diálogo **Organizador de Configurações do Pacote**.  
  
> **OBERVAÇÃO:** a última página do Assistente de Configuração de Pacote, Concluindo o Assistente, lista as propriedades de destino da configuração. Se quiser atualizar as propriedades enquanto estiver executando pacotes usando o utilitário prompt de comando **dtexec**, você poderá gerar as cadeias de caracteres que representam os caminhos de propriedade executando o Assistente de Configuração de Pacotes e, então, copiá-las e colá-las na janela do prompt de comando para usar com a opção definida de **dtexec.**  
  
 A tabela a seguir descreve as colunas da lista de configurações na caixa de diálogo **Organizador de Configurações do Pacote**.  
  
|Coluna|Description|  
|------------|-----------------|  
|**Nome da Configuração**|O nome da configuração.|  
|**Tipo de Configuração**|O tipo de configuração.|  
|**Cadeia de Caracteres de Configuração**|O local da configuração. O local pode ser um caminho, uma variável de ambiente, uma chave do Registro, um nome de variável do pacote pai ou uma tabela em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Objeto de Destino**|O nome do objeto com uma propriedade que tem uma configuração. Se a configuração for um arquivo de configuração XML, a coluna ficará em branco, devido à configuração poder atualizar vários objetos.|  
|**Propriedade de Destino**|O nome da propriedade. Se a configuração gravar em um arquivo de configuração XML ou em uma tabela do SQL Server, a coluna ficará em branco, pois a configuração pode atualizar vários objetos.|  
  
### Para criar uma configuração de pacote  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)], clique na guia **Fluxo de Controle**, **Fluxo de Dados**, **Manipulador de Eventos** ou **Explorador de Pacotes**.  
  
4.  No menu **SSIS** , clique em **Configurações do Pacote**.  
  
5.  Na caixa de diálogo **Organizador de Configurações do Pacote**, selecione **Habilitar configurações do pacote** e clique em **Adicionar**.  
  
6.  Na página inicial da página Assistente de Configuração de Pacotes, clique em **Avançar**.  
  
7.  Na página Selecionar Tipo de Configuração, especifique o tipo de configuração e defina as propriedades pertinentes ao tipo de configuração. Para obter mais informações, consulte [Referência da interface do usuário do Assistente de Configuração de Pacotes](../../integration-services/packages/package-configuration-wizard-ui-reference.md).  
  
8.  Na página Selecionar Propriedades a Serem Exportadas, selecione as propriedades dos objetos do pacote a serem incluídas na configuração. Se o tipo de configuração oferecer suporte somente a uma propriedade, o título dessa página de assistente será Selecionar Propriedade de Destino. Para obter mais informações, consulte [Referência da interface do usuário do Assistente de Configuração de Pacotes](../../integration-services/packages/package-configuration-wizard-ui-reference.md).  
  
    > **OBSERVAÇÃO:** somente os tipos de configuração **Arquivo de Configuração XML** e **SQL Server** dão suporte à inclusão de várias propriedades em uma configuração.  
  
9. Na página Concluindo o Assistente, digite o nome da configuração e clique em **Concluir**.  
  
10. Exiba a configuração na caixa de diálogo **Organizador de Configurações do Pacote**.  
  
11. Clique em **Fechar**.  
  
## Recursos externos  
  
-   Artigo técnico de [Noções básicas sobre configurações de pacotes do Integration Services](http://go.microsoft.com/fwlink/?LinkId=165643), em msdn.microsoft.com  
  
-   Entrada de blog, [Criando pacotes em código – Configurações de Pacote](http://go.microsoft.com/fwlink/?LinkId=217663), em www.sqlis.com.  
  
-   Entrada de blog, [Exemplo de API – Adicione programaticamente um arquivo de configuração a um pacote](http://go.microsoft.com/fwlink/?LinkId=217664), em blogs.msdn.com.  
  
## Consulte também  
 [Configurações de pacote](../../integration-services/packages/package-configurations.md)   
 [Implantação de pacote herdado &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md)   
 [Trabalhando com variáveis programaticamente](../../integration-services/building-packages-programmatically/working-with-variables-programmatically.md)  
  
  
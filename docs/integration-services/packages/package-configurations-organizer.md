---
title: "Organizador de Configura&#231;&#245;es do Pacote | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.packageconfigurationorganizer.f1"
helpviewer_keywords: 
  - "caixa de diálogo Organizador de Configurações do Pacote"
ms.assetid: f20ae6cb-9e6a-4d24-88ff-d7a903a4e8d3
caps.latest.revision: 39
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 39
---
# Organizador de Configura&#231;&#245;es do Pacote
  Use a caixa de diálogo **Organizador de Configurações do Pacote** para habilitar configurações de pacote, visualizar uma lista de configurações para o pacote atual e para definir a ordem de preferência para carregar as configurações.  
  
> **OBSERVAÇÃO:** as configurações estão disponíveis para o modelo de implantação de pacote. Os parâmetros são usados no lugar das configurações para o modelo de implantação de projeto. O modelo de implantação de projeto permite que você implante projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obter mais informações sobre os modelos de implantação, consulte [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).  
  
 Se várias configurações atualizarem a mesma propriedade, valores de configurações listadas na parte inferior da lista de configurações substituirão os valores das configurações na parte superior da lista. O último valor carregado na propriedade é o valor usado quando o pacote executar. Além disso, se o pacote usar uma combinação de configuração direta, como um arquivo de configuração XML, e uma configuração indireta, como uma variável de ambiente, a configuração indireta que aponta para o local da configuração direta deve estar na parte superior da lista.  
  
> **OBSERVAÇÃO:** quando as configurações de pacote são carregadas na ordem preferencial, elas são carregadas da parte superior da lista mostrada na caixa de diálogo **Organizador de Configurações do Pacote** até a parte inferior da lista. Porém, no tempo de execução, talvez as configurações do pacote não sejam carregadas na ordem preferencial. Em particular, Configurações do Pacote Pai são carregadas depois das configurações de outros tipos.  
  
 Configurações de Pacote atualizam os valores das propriedades de objetos de pacote em tempo de execução. Quando um pacote é carregado, os valores das configurações substituem os valores que foram definidos quando o pacote foi desenvolvido. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] dá suporte a diferentes tipos de configuração. Por exemplo, é possível usar um arquivo XML que pode ter várias configurações, ou uma variável de ambiente que contenha uma única configuração. Para obter mais informações, consulte [Package Configurations](../../integration-services/packages/package-configurations.md).  
  
## Opções  
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
  
## Consulte também  
 [Criar configurações de pacote](../../integration-services/packages/create-package-configurations.md)  
  
  
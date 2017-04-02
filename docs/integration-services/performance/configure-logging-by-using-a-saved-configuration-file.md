---
title: "Configurar o log por meio de um arquivo de configura&#231;&#227;o salvo | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "contêineres [Integration Services], logs"
  - "logs [Integration Services], contêineres"
ms.assetid: e5fdbbcb-94ca-4912-aa7c-0d89cebbd308
caps.latest.revision: 42
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 42
---
# Configurar o log por meio de um arquivo de configura&#231;&#227;o salvo
  Este procedimento descreve como configurar o registro em log de novos contêineres em um pacote carregando um arquivo de configuração de registro em log salvo anteriormente.  
  
 Por padrão, todos os contêineres em um pacote usam a mesma configuração de registro que o seu contêiner pai. Por exemplo, as tarefas em um Loop Foreach usam a mesma configuração de registro que o Loop Foreach.  
  
### Para configurar o registro de um contêiner  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No menu **SSIS** , clique em **Registrar em Log**.  
  
3.  Expanda a exibição de árvore do pacote e selecione o contêiner a ser configurado.  
  
4.  Na guia **Provedores e Logs**, selecione os logs a serem usados no contêiner.  
  
    > [!NOTE]  
    >  Você só pode criar logs no nível de pacote. Para obter mais informações, consulte [Habilitar o log de pacote no SQL Server Data Tools](../../integration-services/performance/enable-package-logging-in-sql-server-data-tools.md).  
  
5.  Clique na guia **Detalhes** e clique em **Carregar**.  
  
6.  Localize o arquivo de configuração de registro que você deseja usar e clique em **Abrir**.  
  
7.  Opcionalmente, selecione uma entrada de log diferente para o log marcando sua caixa de seleção na coluna **Eventos**. Clique em **Avançado** para selecionar o tipo de informações a serem registradas nesta entrada.  
  
    > [!NOTE]  
    >  O novo contêiner pode incluir entradas de log adicionais que não estão disponíveis para o contêiner usado originalmente para criar a configuração de registro. Essas entradas de log adicionais devem ser selecionadas manualmente se você quiser que elas sejam registradas.  
  
8.  Para salvar a versão atualizada da configuração de registro, clique em **Salvar**.  
  
9. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## Consulte também  
 [Registro em Log do Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
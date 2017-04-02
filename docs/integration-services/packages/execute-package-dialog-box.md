---
title: "Caixa de di&#225;logo Executar Pacote | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.ssms.ispackageexecute.f1"
  - "sql13.ssis.ssms.executepackage.f1"
ms.assetid: 4f7a806d-4867-4d1f-bc65-b00c1caee7b6
caps.latest.revision: 23
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 23
---
# Caixa de di&#225;logo Executar Pacote
  Use a caixa de diálogo **Executar Pacote** para executar um pacote armazenado no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pode conter parâmetros com valores armazenados em variáveis de ambiente. Antes de executar esse tipo de pacote, você deve especificar qual ambiente será usado para fornecer os valores de variável de ambiente. Um projeto pode conter vários ambientes, mas só um ambiente pode ser usado para associar valores de variável de ambiente no momento da execução. Se nenhuma variável de ambiente for usada no pacote, nenhum ambiente será necessário.  
  
 O que você deseja fazer?  
  
-   [Abrir a caixa de diálogo Executar Pacote](#open_dialog)  
  
-   [Definir as opções na página Geral](#general)  
  
-   [Definir as opções na guia Parâmetros](#parameters)  
  
-   [Definir as opções na guia de Gerenciadores de Conexões](#connection)  
  
-   [Definir as opções na guia Avançado](#advanced)  
  
-   [Criando scripts para as opções na caixa de diálogo Executar Pacote](#script)  
  
##  <a name="open_dialog"></a> Abrir a caixa de diálogo Executar Pacote  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se ao servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     Você está se conectando à instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que hospeda o banco de dados SSISDB.  
  
2.  Em Pesquisador de Objetos, expanda a árvore para exibir o nó **Catálogos do Integration Services** .  
  
3.  Expanda o nó **SSISDB** .  
  
4.  Expanda a pasta que contém o pacote que você deseja executar.  
  
5.  Clique com o botão direito do mouse no pacote e clique em **Executar**.  
  
##  <a name="general"></a> Definir as opções na página Geral  
 Selecione **Ambiente** para especificar o ambiente aplicado com o pacote executado.  
  
##  <a name="parameters"></a> Definir as opções na guia Parâmetros  
 Use a guia **Parâmetros** para modificar os valores de parâmetros usados quando o pacote for executado.  
  
##  <a name="connection"></a> Definir as opções na guia de Gerenciadores de Conexões  
 Use a guia Gerenciadores de Conexões para definir as propriedades dos gerenciadores de conexões do pacote.  
  
##  <a name="advanced"></a> Definir as opções na guia Avançado  
 Use a guia Avançado para gerenciar propriedades e outras configurações de pacote.  
  
 **Adicionar**, **Editar**, **Remover**  
 Clique para adicionar, editar ou remover uma propriedade.  
  
 **Nível de log**  
 Selecione o nível de log para a execução do pacote. Para obter mais informações, consulte [catalog.set_execution_parameter_value &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md).  
  
 **Despejar quando ocorrerem erros**  
 Especifique se um arquivo de despejo será criado quando ocorrerem erros durante a execução do pacote. Para obter mais informações, consulte [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).  
  
 **Tempo de execução de 32 bits**  
 Especifique se o pacote será executado em um sistema de 32 bits.  
  
##  <a name="script"></a> Criando scripts para as opções na caixa de diálogo Executar Pacote  
 Enquanto estiver na caixa de diálogo **Executar Pacote** , você também poderá usar o botão **Script** na barra de ferramentas para gravar o código [!INCLUDE[tsql](../../includes/tsql-md.md)] . O script gerado chama os procedimentos armazenados [catalog.start_execution &#40;Banco de dados SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) com as mesmas opções selecionadas na caixa de diálogo **Executar Pacote**. O script aparece em uma nova janela de script no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
  
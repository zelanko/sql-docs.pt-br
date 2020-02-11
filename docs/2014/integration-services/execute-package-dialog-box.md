---
title: Caixa de diálogo Executar Pacote | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.ssms.ispackageexecute.f1
- sql12.ssis.ssms.executepackage.f1
ms.assetid: 4f7a806d-4867-4d1f-bc65-b00c1caee7b6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b4b920b17e960059e1212be7dd15c176c0b25a47
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66059192"
---
# <a name="execute-package-dialog-box"></a>Execute Package Dialog Box
  Use a caixa de diálogo **Executar Pacote** para executar um pacote armazenado no servidor do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 Um pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] pode conter parâmetros com valores armazenados em variáveis de ambiente. Antes de executar esse tipo de pacote, você deve especificar qual ambiente será usado para fornecer os valores de variável de ambiente. Um projeto pode conter vários ambientes, mas só um ambiente pode ser usado para associar valores de variável de ambiente no momento da execução. Se nenhuma variável de ambiente for usada no pacote, nenhum ambiente será necessário.  
  
 O que você deseja fazer?  
  
-   [Abrir a caixa de diálogo Executar Pacote](#open_dialog)  
  
-   [Definir as opções na página Geral](#general)  
  
-   [Definir as opções na guia Parâmetros](#parameters)  
  
-   [Definir as opções na guia gerenciadores de conexões](#connection)  
  
-   [Definir as opções na guia Avançado](#advanced)  
  
-   [Criando scripts para as opções na caixa de diálogo Executar Pacote](#script)  
  
##  <a name="open_dialog"></a>Abrir a caixa de diálogo Executar Pacote  
  
1.  No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], conecte-se ao servidor do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
     Você está se conectando à instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] que hospeda o banco de dados SSISDB.  
  
2.  Em Pesquisador de Objetos, expanda a árvore para exibir o nó **Catálogos do Integration Services** .  
  
3.  Expanda o nó **SSISDB** .  
  
4.  Expanda a pasta que contém o pacote que você deseja executar.  
  
5.  Clique com o botão direito do mouse no pacote e clique em **Executar**.  
  
##  <a name="general"></a>Definir as opções na página Geral  
 Selecione **Ambiente** para especificar o ambiente aplicado com o pacote executado.  
  
##  <a name="parameters"></a>Definir as opções na guia parâmetros  
 Use a guia **Parâmetros** para modificar os valores de parâmetros usados quando o pacote for executado.  
  
##  <a name="connection"></a>Definir as opções na guia gerenciadores de conexões  
 Use a guia Gerenciadores de Conexões para definir as propriedades dos gerenciadores de conexões do pacote.  
  
##  <a name="advanced"></a>Definir as opções na guia Avançado  
 Use a guia Avançado para gerenciar propriedades e outras configurações de pacote.  
  
 **Adicionar**, **Editar**, **remover**  
 Clique para adicionar, editar ou remover uma propriedade.  
  
 **Nível de log**  
 Selecione o nível de log para a execução do pacote. Para obter mais informações, consulte [catalog.set_execution_parameter_value &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database).  
  
 **Despejar em erros**  
 Especifique se um arquivo de despejo será criado quando ocorrerem erros durante a execução do pacote. Para obter mais informações, consulte [Generating Dump Files for Package Execution](troubleshooting/generating-dump-files-for-package-execution.md).  
  
 **runtime de 32 bits**  
 Especifique se o pacote será executado em um sistema de 32 bits.  
  
##  <a name="script"></a>Criando scripts para as opções na caixa de diálogo Executar Pacote  
 Enquanto estiver na caixa de diálogo **Executar Pacote** , você também poderá usar o botão **Script** na barra de ferramentas para gravar o código [!INCLUDE[tsql](../includes/tsql-md.md)] . O script gerado chama os procedimentos armazenados [catalog.start_execution &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database) com as mesmas opções selecionadas na caixa de diálogo **Executar Pacote**. O script aparece em uma nova janela de script no [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
  

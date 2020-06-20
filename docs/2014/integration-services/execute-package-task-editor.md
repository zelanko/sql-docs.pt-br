---
title: Editor da tarefa Executar Pacote | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.executepackagetask.parameter.F1
- sql12.dts.designer.executepackagetask.package.f1
- sql12.dts.designer.executepackagetask.general.f1
ms.assetid: c2c96b4f-eb10-4d8b-be34-88edfd0785fb
author: janinezhang
ms.author: janinez
ms.openlocfilehash: b9e114802c6e69467ba9438ee4c525ef85e73024
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966826"
---
# <a name="execute-package-task-editor"></a>Editor da tarefa Executar Pacote
  Use o Editor da tarefa Executar Pacote para configurar a Tarefa Executar Pacote. A tarefa Executar Pacote estende os recursos empresariais do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ao permitir que pacotes executem outros pacotes como parte de um fluxo de trabalho.  
  
 **O que você deseja fazer?**  
  
-   [Abrir o editor da tarefa Executar Pacote](#open)  
  
-   [Definir as opções na página Geral](#general)  
  
-   [Definir as opções na página Pacote](#package)  
  
-   [Defina as opções na Página Associação de Parâmetros](#parameter)  
  
##  <a name="open-the-execute-package-task-editor"></a><a name="open"></a>Abrir o editor da tarefa Executar Pacote  
  
1.  Abra um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] que contém um tarefa Executar Pacote.  
  
2.  Clique com o botão direito do mouse na tarefa no Designer SSIS e clique em **Editar**.  
  
##  <a name="set-the-options-on-the-general-page"></a><a name="general"></a>Definir as opções na página Geral  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Executar Pacote. Esse nome é usado como rótulo no ícone de tarefa.  
  
> [!NOTE]  
>  Os nomes das tarefas devem ser exclusivos em um pacote.  
  
 **Descrição**  
 Digite uma descrição para a tarefa Executar Pacote.  
  
##  <a name="set-the-options-on-the-package-page"></a><a name="package"></a>Definir as opções na página pacote  
 **ReferenceType**  
 Selecione **Referência do Projeto** para pacotes filho que estão no projeto. Selecione **Referência Externa** para pacotes filho localizados fora do pacote  
  
> [!NOTE]  
>  A opção **ReferenceType** é somente leitura e será definida como **Referência Externa** se o projeto que contém o pacote não tiver sido convertido no modelo de implantação de projeto. Para obter mais informações sobre conversão, consulte [Implantar projetos no Servidor do Integration Services](../../2014/integration-services/deploy-projects-to-integration-services-server.md).  
  
 **Senha**  
 Se o pacote filho for protegido por senha, forneça a senha dele ou clique no botão de reticências (...) e crie uma senha para ele.  
  
 `ExecuteOutOfProcess`  
 Especifique se o pacote filho é executado no processo do pacote pai ou um processo separado. Por padrão, a Propriedade ExecuteOutOfProcess da tarefa executar pacote é definida como `False` e o pacote filho é executado no mesmo processo que o pacote pai. Se você definir esta propriedade como `true`, o pacote filho será executado em um processo separado. Isto pode reduzir a velocidade do lançamento do pacote filho. Além disso, se a propriedade foi definida como `true`, você não poderá depurar o pacote em uma instalação somente ferramentas; você deve instalar o produto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Para obter mais informações, consulte [Instalar o Integration Services](install-windows/install-integration-services.md).  
  
### <a name="referencetype-dynamic-options"></a>Opções dinâmicas ReferenceType  
  
#### <a name="referencetype--external-reference"></a>ReferenceType = referência externa  
 **Localidade**  
 Selecione o local de armazenamento do pacote filho. As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**SQL Server**|Defina o local como uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
|**Sistema de Arquivos**|Defina o local para o sistema de arquivos.|  
  
 **Conexão**  
 Selecione o tipo de local de armazenamento para o pacote filho.  
  
 **PackageNameReadOnly**  
 Exibe o nome do pacote.  
  
#### <a name="referencetype--project-reference"></a>ReferenceType = referência do projeto  
 **PackageNameFromProjectReference**  
 Selecione um pacote contido no projeto para ser o pacote filho.  
  
### <a name="location-dynamic-options"></a>Opções Dinâmicas de Local  
  
#### <a name="location--sql-server"></a>Local = SQL Server  
 **Conexão**  
 Selecione um OLE DB Gerenciador de conexões na lista ou clique \<**New connection...**> para criar um novo Gerenciador de conexões.  
  
 **Tópicos relacionados:** [Gerenciador de conexões OLE DB](connection-manager/ole-db-connection-manager.md), [Configurar Gerenciador de Conexões OLE DB](../../2014/integration-services/configure-ole-db-connection-manager.md)  
  
 **PackageName**  
 Digite o nome do pacote filho ou clique nas reticências (...) e localize o pacote.  
  
#### <a name="location--file-system"></a>Local = Sistema de arquivos  
 **Conexão**  
 Selecione um Gerenciador de conexões de arquivo na lista ou clique \<**New connection...**> para criar um novo Gerenciador de conexões.  
  
 **Tópicos relacionados:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 **PackageNameReadOnly**  
 Exibe o nome do pacote.  
  
##  <a name="set-the-options-on-the-parameter-bindings-page"></a><a name="parameter"></a>Definir as opções na página associações de parâmetro  
 Você pode passar valores do pacote pai ou do projeto para o pacote filho. O projeto deve usar o modelo de implantação de projeto e o pacote filho deve ser contido no mesmo projeto que contém o pacote pai.  
  
 Para obter mais informações sobre conversão de um projeto para o modelo de implantação de projetos, consulte [Implantar projetos no Servidor do Integration Services](../../2014/integration-services/deploy-projects-to-integration-services-server.md).  
  
 **Parâmetro de pacote filho**  
 Insira ou selecione um nome para o parâmetro de pacote filho.  
  
 **Parâmetro ou variável de associação**  
 Selecione o parâmetro ou variável que contêm o valor que você quer passar para o pacote filho.  
  
 **Adicionar**  
 Clique para mapear um parâmetro ou variável para um parâmetro de pacote filho.  
  
 **Removerr**  
 Clique para remover um mapeamento entre um parâmetro ou variável e um parâmetro de pacote filho.  
  
  

---
title: Salvar pacotes | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: non-specific
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.dts.designer.savecopyas.f1
helpviewer_keywords:
- Integration Services packages, saving
- packages [Integration Services], saving
- saving packages
- SSIS packages, saving
- SQL Server Integration Services packages, saving
ms.assetid: 17c1de2c-637f-45c2-a148-79294bae0af4
caps.latest.revision: 48
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 404b9d1933a8c8d4b3295b33cace3a182d4e07ed
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="save-packages"></a>Salvar pacotes
  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] , você cria pacotes usando o Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] e salva os pacotes no sistema de arquivos como arquivos XML (arquivos .dtsx). Você também pode salvar cópias do arquivo XML de pacote no banco de dados msdb no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou no repositório de pacotes. O repositório de pacotes representa as pastas no local do sistema de arquivos que o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] gerencia.  
  
 Se você salvar um pacote no sistema de arquivos, poderá depois usar o serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para importar o pacote para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou para o armazenamento de pacotes. Para obter mais informações, veja [Serviço Integration Services &#40;Serviço SSIS&#41;](../integration-services/service/integration-services-service-ssis-service.md).  
  
 Você também pode usar um utilitário de prompt de comando, **dtutil**, para copiar um pacote entre o sistema de arquivos e o msdb. Para obter mais informações, consulte [dtutil Utility](../integration-services/dtutil-utility.md).  
## <a name="save-a-package-to-the-file-system"></a>Salvar um pacote no sistema de arquivos  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote que você quer salvar em um arquivo.  
  
2.  No Gerenciador de Soluções, clique no pacote que você deseja salvar.  
  
3.  No menu **Arquivo** , clique em **Salvar Itens Selecionados**.  
  
    > [!NOTE]  
    >  É possível verificar na janela Propriedades o caminho e o nome de arquivo onde o pacote foi salvo.  

## <a name="save-a-copy-of-a-package"></a>Salvar uma cópia de um pacote
  Esta seção descreve como salvar uma cópia de um pacote no sistema de arquivos, no repositório de pacotes ou no banco de dados **msdb** no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Ao especificar um local para salvar a cópia do pacote, também é possível atualizar o nome do pacote.  
  
 O repositório do pacote pode incluir o banco de dados **msdb** e as pastas no sistema de arquivos, somente **msdb**, ou somente pastas no sistema de arquivos. No **msdb**, os pacotes são salvos na tabela **sysssispackages** . Esta tabela inclui uma coluna **folderid** que identifica a pasta lógica a qual o pacote pertence. As pastas lógicas fornecem uma maneira útil de agrupar pacotes salvos em **msdb** da mesma forma que as pastas no sistema de arquivos fornecem uma maneira de agrupar pacotes salvos no sistema de arquivos. As linhas na tabela **sysssispackagefolders** em **msdb** definem as pastas.  
  
 Se **msdb** não for definido como parte do armazenamento do pacote, você poderá continuar a associar pacotes com pastas lógicas existentes ao selecionar o SQL Server na opção **Caminho do Pacote** .  
  
> [!NOTE]  
>  O pacote deve ser aberto no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] antes que você possa salvar uma cópia do pacote.  
  
### <a name="to-save-a-copy-of-a-package"></a>Para salvar uma cópia de um pacote  
  
1.  No Gerenciador de Soluções, clique duas vezes no pacote do qual você quer salvar uma cópia.  
  
2.  No menu **Arquivo**, clique em **Salvar Cópia do \<arquivo de pacote> Como**.  
  
3.  Na caixa de diálogo **Salvar Cópia do Pacote** , selecione um local de pacote na lista **Local dos pacotes** . As seguintes opções estão disponíveis:  
    -   SQL Server
    -   Sistema de Arquivos 
    -   Armazenamento de Pacotes SSIS 
  
4.  Se o local for **SQL Server** ou **Armazenamento de Pacotes SSIS**, forneça um nome de servidor.  
  
5.  Se for salvar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], especifique o tipo de autenticação e, se estiver usando a Autenticação [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , forneça um nome de usuário e senha.  
  
6.  Para especificar o caminho do pacote, digite o caminho ou clique no botão Procurar **(…)** para especificar o local do pacote. O nome padrão do pacote é Pacote. Como opção, atualize o nome de pacote para um que atenda suas necessidades.  
  
     Se você selecionar **SQL Server** como a opção de **Caminho do Pacote** , o caminho do pacote consistirá de pastas lógicas no **msdb** e o nome do pacote. Por exemplo, se o pacote DownloadMonthlyData estiver associado à pasta Finance dentro da pasta MSDB (o nome padrão da pasta lógica raiz no **msdb**), o caminho do pacote chamado DownloadMonthlyData será MSDB/Finance/DownloadMonthlyData  
  
     Se você selecionar **Armazenamento de Pacotes SSIS** como a opção de **Caminho do Pacote** , o caminho do pacote consistirá da pasta que o serviço Integration Services gerencia. Por exemplo, se o pacote UpdateDeductions estiver localizado na pasta Recursos Humanos dentro da pasta do sistema de arquivo que o serviço gerencia, o caminho do pacote será /Sistema de Arquivos/Recursos Humanos/UpdateDeductions; da mesma forma, se o pacote PostResumes estiver associado à pasta Recursos Humanos dentro da pasta MSDB, o caminho do pacote será MSDB/Recursos Humanos/PostResumes.  
  
     Se você selecionar **Sistema de Arquivos** como a opção de **Caminho do Pacote** , o caminho do pacote será o local no sistema de arquivos e o nome do arquivo. Por exemplo, se o nome de pacote for UpdateDemographics, o caminho de pacote será C:\HumanResources\Quarterly\UpdateDemographics.dtsx.  
  
7.  Revise o nível de proteção do pacote.  
  
8.  Como opção, clique no botão Procurar **(…)** ao lado da caixa **Nível de proteção** para alterar o nível de proteção.  
  
    -   Na caixa de diálogo **Nível de Proteção do Pacote** , selecione um nível de proteção diferente.  
  
    -   Clique em **OK**.  
  
9. Clique em **OK**.  

## <a name="save-a-package-as-a-package-template"></a>Salvar um pacote como um modelo de pacote
 Esta seção descreve como designar e usar pacotes personalizados como modelos para criar novos pacotes do Integration Services no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Por padrão, o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] usa um modelo de pacote que cria um pacote vazio quando você adiciona um novo pacote a um projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Você não pode substituir este modelo padrão, mas pode adicionar novos modelos.  
  
 Você pode designar vários pacotes para serem usados como modelos. Antes de implementar os pacotes personalizados como modelos, é preciso criá-los.  
  
 Ao criar um pacote usando os pacotes personalizados como modelos, os novos pacotes apresentam o mesmo nome e GUID do modelo. Para obter a diferenciação dos pacotes, atualize o valor da propriedade **Name** e gere uma nova GUID para a propriedade **ID** . Para obter mais informações, consulte [Criar pacotes no SQL Server Data Tools](../integration-services/create-packages-in-sql-server-data-tools.md) e [Definir Propriedades de Pacote](../integration-services/set-package-properties.md).  
  
### <a name="to-designate-a-custom-package-as-a-package-template"></a>Para designar um pacote personalizado como um modelo de pacote  
  
1.  No sistema de arquivos, localize o pacote que deseja usar como modelo.  
  
2.  Copie o pacote para a pasta DataTransformationItems. Por padrão, esta pasta está em C:\Arquivos de Programas\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject.  
  
3.  Repita as etapas 1 e 2 para cada pacote que quiser usar como modelo.  
  
### <a name="to-use-a-custom-package-as-a-package-template"></a>Para usar um pacote personalizado como um modelo de pacote  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no qual você deseja criar um pacote.  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse no projeto, aponte para **Adicionar** e clique em **Novo Item**.  
  
3.  Na caixa de diálogo **Adicionar Novo Item – \<nome do projeto**, clique no pacote que deseja usar como modelo.  
  
     A lista de modelos inclui o modelo padrão do pacote chamado Novo Pacote SSIS. O ícone do pacote identifica os modelos que podem ser usados como modelos de pacote.  
  
4.  Clique em **Adicionar**.  

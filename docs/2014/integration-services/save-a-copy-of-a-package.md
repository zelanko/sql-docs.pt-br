---
title: Salvar uma cópia de um pacote | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, saving
- packages [Integration Services], saving
- saving packages
- SSIS packages, saving
- SQL Server Integration Services packages, saving
ms.assetid: 21482a20-e420-4452-b7eb-8f9fa1929f31
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e77ba9379ebf482d8ed2f587ea175706458bd275
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48193406"
---
# <a name="save-a-copy-of-a-package"></a>Salvar uma cópia de um pacote
  Este procedimento descreve como salvar uma cópia de um pacote no sistema de arquivos, no armazenamento do pacote ou no banco de dados **msdb** no [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Ao especificar um local para salvar a cópia do pacote, também é possível atualizar o nome do pacote.  
  
 O repositório do pacote pode incluir o banco de dados **msdb** e as pastas no sistema de arquivos, somente **msdb**, ou somente pastas no sistema de arquivos. No **msdb**, os pacotes são salvos na tabela **sysssispackages** . Esta tabela inclui uma coluna **folderid** que identifica a pasta lógica a qual o pacote pertence. As pastas lógicas fornecem uma maneira útil de agrupar pacotes salvos em **msdb** da mesma forma que as pastas no sistema de arquivos fornecem uma maneira de agrupar pacotes salvos no sistema de arquivos. As linhas na tabela **sysssispackagefolders** em **msdb** definem as pastas.  
  
 Se **msdb** não for definido como parte do armazenamento do pacote, você poderá continuar a associar pacotes com pastas lógicas existentes ao selecionar o SQL Server na opção **Caminho do Pacote** .  
  
> [!NOTE]  
>  O pacote deve ser aberto no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] antes que você possa salvar uma cópia do pacote.  
  
### <a name="to-save-a-copy-of-a-package"></a>Para salvar uma cópia de um pacote  
  
1.  No Gerenciador de Soluções, clique duas vezes no pacote do qual você quer salvar uma cópia.  
  
2.  No menu **Arquivo**, clique em **Salvar Cópia do \<arquivo de pacote> Como**.  
  
3.  Na caixa de diálogo **Salvar Cópia do Pacote** , selecione um local de pacote na lista **Local dos pacotes** .  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Serviços de integração &#40;SSIS&#41; pacotes](../../2014/integration-services/integration-services-ssis-packages.md)   
 [Configurar a integração com o serviço de serviços &#40;serviço SSIS&#41;](service/integration-services-service-ssis-service.md)  
  
  

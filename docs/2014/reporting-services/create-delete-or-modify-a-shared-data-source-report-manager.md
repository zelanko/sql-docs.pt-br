---
title: Criar, excluir ou modificar uma fonte de dados compartilhada (Gerenciador de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- removing shared data sources
- data sources [Reporting Services], shared
- deleting shared data sources
- modifying shared data sources
ms.assetid: cd7bace3-f8ec-4ee3-8a9f-2f217cdca9f2
caps.latest.revision: 47
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e48edf78d8b0a73c01871b47ac24fa1f0bf8babb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37202686"
---
# <a name="create-delete-or-modify-a-shared-data-source-report-manager"></a>Criar, excluir ou modificar uma fonte de dados compartilhada (Gerenciador de Relatórios)
  Uma fonte de dados compartilhada especifica propriedades de conexão para uma fonte de dados. Se você tiver uma fonte de dados usada por um número grande de relatórios, modelos ou assinaturas controladas por dados, considere a criação de uma fonte de dados compartilhada para eliminar a sobrecarga em manter as mesmas informações de conexão em vários lugares.  
  
 O ícone seguinte indica uma fonte de dados compartilhada na hierarquia da pasta do Gerenciador de Relatórios:  
  
 ![Ícone Fonte de dados compartilhada](media/hlp-16datasource.png "Ícone Fonte de dados compartilhada")  
ícone de fonte de dados compartilhada  
  
### <a name="to-create-a-shared-data-source"></a>Para criar uma fonte de dados compartilhada  
  
1.  Inicie o [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../../2014/reporting-services/report-manager-ssrs-native-mode.md).  
  
2.  No Gerenciador de Relatórios, navegue até a página **Conteúdo** .  
  
3.  Clique em **Nova Fonte de Dados**. A página **Nova Fonte de Dados** será aberta.  
  
4.  Digite um nome para o item. Um nome deve conter pelo menos um caractere e deve começar com uma letra. Ele também pode incluir certos símbolos, mas não espaços nem os caracteres ; ? : @ & = +, $ / * \< > | " /.  
  
5.  Como opção, digite uma descrição para oferecer aos usuários informações sobre a conexão. Essa descrição será exibida na página **Conteúdo** no Gerenciador de Relatórios.  
  
6.  Na lista **Tipo de fonte de dados** , especifique a extensão de processamento de dados usada para processar dados da fonte de dados.  
  
7.  Em **Cadeia de conexão**, especifique a cadeia de conexão usada pelo servidor de relatório para se conectar à fonte de dados. Recomendamos que você não especifique credenciais na cadeia de conexão.  
  
     O exemplo a seguir ilustra uma cadeia de caracteres de conexão para se conectar ao local [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] banco de dados:  
  
    ```  
    data source=<localservername>; initial catalog=AdventureWorks2012  
    ```  
  
8.  Em **Conectar usando**, especifique como são obtidas as credenciais na execução do relatório:  
  
    -   Se desejar solicitar ao usuário o nome de logon e a senha, clique em **Credenciais fornecidas pelo usuário que está executando o relatório**. Para usar as credenciais inseridas pelo usuário como credenciais do Windows, clique em **Usar as credenciais do Windows ao conectar-se à fonte de dados**. Se o nome de usuário e a senha forem credenciais de banco de dados, não selecione esta opção.  
  
    -   Caso pretenda usar a fonte de dados como uma fonte de dados compartilhada com credenciais salvas que são gerenciadas pelo proprietário da fonte de dados, ou para relatórios que dão suporte a assinaturas ou outras operações agendadas (como a geração automatizada de histórico de relatório), clique em **Credenciais armazenadas com segurança no servidor de relatório**. Se o servidor do banco de dados oferecer suporte a representação ou delegação, é possível selecionar **Representar o usuário autenticado depois que uma conexão é estabelecida com a fonte de dados**.  
  
    -   Se desejar que o servidor de relatório passe as credenciais do usuário que está acessando o relatório para o servidor que está hospedando a fonte de dados externa, clique em **Segurança Integrada do Windows**. Nesse caso, não é solicitado que o usuário digite um nome de usuário ou senha.  
  
    -   Se a fonte de dados não usar credenciais (se a fonte de dados for um arquivo XML acessado pelo sistema de arquivos, por exemplo), clique em **Não são necessárias credenciais**. Você deve especificar esse tipo de credencial somente se ele for válido para a fonte de dados. Se você selecionar essa opção para uma fonte de dados que requer autenticação, a conexão falhará. Se essa opção for selecionada, certifique-se de configurar a conta de execução autônoma que permite que o servidor de relatório se conecte a outros computadores para recuperar dados ou arquivos quando as credenciais do usuário não estiverem disponíveis.  
  
     Para obter mais informações sobre como configurar credenciais, consulte [especificar credenciais e informações de Conexão para fontes de dados de relatório](report-data/specify-credential-and-connection-information-for-report-data-sources.md). Para obter mais informações sobre a conta de execução autônoma, consulte [Configurar a conta de execução autônoma &#40; 	Gerenciador de Configurações do SSRS&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
9. Clique no botão **Testar Conexão** para validar a configuração da fonte de dados.  
  
    > [!NOTE]  
    >  O botão Testar Conexão não tem suporte para o tipo de fonte de dados XML.  
  
10. Clique em **OK**.  
  
### <a name="to-modify-a-shared-data-source"></a>Para modificar uma fonte de dados compartilhada  
  
1.  No Gerenciador de Relatórios, navegue até a página Conteúdo.  
  
2.  Navegue até o item de fonte de dados compartilhada, focalize o item, clique na lista suspensa e, no menu de contexto, clique em **Gerenciar**. A página **Propriedades** é exibida.  
  
3.  Modifique a fonte de dados e clique em **Aplicar**.  
  
### <a name="to-delete-a-shared-data-source"></a>Para excluir uma fonte de dados compartilhada  
  
-   No Gerenciador de Relatórios, navegue até a página **Conteúdo** e execute uma das seguintes opções:  
  
    -   Navegue até o item da fonte de dados compartilhada.  
  
         Clique no item para abri-lo. A página Propriedades Gerais será aberta.  
  
         Clique em **Excluir**e em **OK**.  
  
    -   Na página **Conteúdo** , navegue até a pasta que contém a fonte de dados que você quer excluir.  
  
         Focalize o item, clique na lista suspensa e, no menu de contexto, clique em **Excluir**.  
  
         [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Página de conteúdo &#40;Gerenciador de relatórios&#41;](../../2014/reporting-services/contents-page-report-manager.md)   
 [Criar, modificar e excluir fontes de dados compartilhadas &#40;SSRS&#41;](report-data/create-modify-and-delete-shared-data-sources-ssrs.md)   
 [Gerenciar fontes de dados de relatório](report-data/manage-report-data-sources.md)   
 [Configurar propriedades de fonte de dados para um relatório &#40;Gerenciador de relatórios&#41;](report-data/configure-data-source-properties-for-a-report-report-manager.md)  
  
  

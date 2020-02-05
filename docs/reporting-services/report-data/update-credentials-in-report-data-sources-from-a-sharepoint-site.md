---
title: Atualizar as credenciais em fontes de dados de relatório por meio de um site do SharePoint | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: e0c50b6e-89e7-4b4d-8fe5-c90682c5d1b1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0a9908e340dadeb1108e68ca10f466276c14df23
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "65575441"
---
# <a name="update-credentials-in-report-data-sources-from-a-sharepoint-site"></a>Atualizar credenciais em fontes de dados de relatório de um site do SharePoint
  Este tópico descreve como atualizar as fontes de dados incorporadas nos relatórios e nas fontes de dados compartilhadas salvas em uma biblioteca de documentos do SharePoint.  
  
 Muitos de seus relatórios poderiam incluir fontes de dados ou usar fontes de dados compartilhadas configuradas para usar a Autenticação do Windows. Em algumas circunstâncias, como a criação de alertas de dados em relatórios salvos em uma biblioteca de documentos do SharePoint, você precisa atualizar as credenciais de fonte de dados para credenciais armazenadas ou não requerer nenhuma credencial.  
  
 Para usar credenciais armazenadas em relatórios, você poderia optar por criar e usar um novo logon do SQL Server. Para obter mais informações, consulte [Crie um logon](../../relational-databases/security/authentication-access/create-a-login.md).  
  
### <a name="to-update-an-embedded-data-source-to-use-stored-credentials"></a>Para atualizar uma fonte de dados incorporada para usar credenciais armazenadas  
  
1.  Vá para a biblioteca de documentos do SharePoint onde salvou o relatório.  
  
2.  Clique no ícone para expandir o menu suspenso no relatório e clique em **Gerenciar Fontes de Dados**.  
  
     A página Gerenciar Fontes de Dados será aberta.  
  
3.  Na coluna **Nome** , clique na fonte de dados.  
  
4.  Em **Tipo de Conexão** , verifique se a opção **Fonte de dados personalizada** está selecionada.  
  
     Essa opção indica que a fonte de dados está incorporada no relatório.  
  
5.  Deixe as opções **Tipo de Fonte de Dados** e **Cadeia de conexão** como estão, a menos que você deseje que o relatório se conecte a outro tipo de fonte de dados, a outro servidor ou a um armazenamento de dados.  
  
6.  Em **Credenciais**, selecione **Credenciais armazenadas**. Essa opção só funcionará se a fonte de dados não aceitar credenciais ou se você estiver passando as credenciais de alguma outra forma.  
  
     A opção **Não são necessárias credenciais** também pode ser usada em algumas circunstâncias.  
  
     Em alguns tipos de fonte de dados, a conta de execução autônoma deve estar configurada no servidor de relatórios. Para obter mais informações, consulte o tópico do tipo de fonte de dados correspondente em [Adicionar dados de fontes de dados externas &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md) e [Configurar a conta de execução autônoma &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
7.  Digite um nome de usuário e uma senha.  
  
    -   Se a conta for uma conta de usuário de domínio do Windows, especifique-a neste formato: \<domain>\\<account\>. Em seguida, selecione **Usar as credenciais do Windows ao conectar-se à fonte de dados**.  
  
    -   Se o nome de usuário e a senha forem credenciais do banco de dados, não selecione **Usar as credenciais do Windows ao conectar-se à fonte de dados**. Se o servidor de banco de dados oferecer suporte à representação ou delegação, você poderá selecionar **Definir o contexto de execução para esta conta**.  
  
8.  Para verificar se a fonte de dados pode se conectar usando as credenciais atualizadas, clique em **Testar conexão**.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-update-a-shared-data-source-to-use-stored-credentials"></a>Para atualizar uma fonte de dados compartilhada para usar credenciais armazenadas  
  
1.  Vá para a biblioteca de documentos do SharePoint onde salvou a fonte de dados compartilhada.  
  
2.  Clique no ícone para expandir o menu suspenso na fonte de dados compartilhada e clique em **Editar Definição da Fonte de Dados**.  
  
     A página Fonte de Dados será aberta.  
  
3.  Deixe as opções **Tipo de Fonte de Dados** e **Cadeia de conexão** como estão, a menos que você deseje que a fonte de dados compartilhada se conecte a outro tipo de fonte de dados, a outro servidor ou a um armazenamento de dados.  
  
4.  Em **Credenciais**, selecione **Credenciais armazenadas**.  
  
     A opção **Não são necessárias credenciais** também pode ser usada em algumas circunstâncias. Essa opção só funcionará se a fonte de dados não aceitar credenciais ou se você estiver passando as credenciais de alguma outra forma.  
  
     Em alguns tipos de fonte de dados, a conta de execução autônoma deve estar configurada no servidor de relatórios. Para obter mais informações, consulte o tópico do tipo de fonte de dados correspondente em [Adicionar dados de fontes de dados externas &#40;SSRS&#41;](../../reporting-services/report-data/add-data-from-external-data-sources-ssrs.md) e [Configurar a conta de execução autônoma &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
5.  Digite um nome de usuário e uma senha.  
  
    -   Se a conta for uma conta de usuário de domínio do Windows, especifique-a neste formato: \<domain>\\<account\>. Em seguida, selecione **Usar as credenciais do Windows ao conectar-se à fonte de dados.**  
  
    -   Se o nome de usuário e a senha forem credenciais do banco de dados, não selecione **Usar as credenciais do Windows ao conectar-se à fonte de dados**. Se o servidor de banco de dados oferecer suporte à representação ou delegação, você poderá selecionar **Definir o contexto de execução para esta conta**.  
  
6.  Para verificar se a fonte de dados pode se conectar usando as credenciais atualizadas, clique em **Testar conexão**.  
  
7.  Verifique se a opção Habilitar esta fonte de dados está selecionada.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Carregar documentos em uma biblioteca do SharePoint &#40;Reporting Services no modo do SharePoint&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)  
  
  

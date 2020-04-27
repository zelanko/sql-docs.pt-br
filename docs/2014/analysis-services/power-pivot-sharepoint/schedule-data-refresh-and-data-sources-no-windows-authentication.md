---
title: Agendar a atualização de dados e fontes de dados que não dão suporte à autenticação do Windows (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d8d875bc-7823-46b7-a939-867cefd4de12
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b4851c8054434713e69d8bf63b046484a01f0398
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66071163"
---
# <a name="schedule-data-refresh-and-data-sources-that-do-not-support-windows-authentication-powerpivot-for-sharepoint"></a>Atualização de dados de agendamento e fontes de dados que não oferecem suporte à Autenticação do Windows (PowerPivot para SharePoint)
  Este tópico descreve um fluxo de trabalho de atualização de dados de agendamento do PowerPivot para SharePoint que pode usar fontes de dados que **NÃO** oferecem suporte à Autenticação do Windows. Por exemplo, fontes de dados Oracle ou IDM DB2. As ilustrações e as etapas neste tópico fazem referência a fontes de dados Oracle, mas o mesmo fluxo de trabalho aplica-se a outras fontes de dados.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2010 &#124; SharePoint 2013.|  
  
 **Visão geral:** Crie dois aplicativos de destino de repositório seguro. Configure o primeiro aplicativo de destino (PowerPivotDataRefresh) para usar as credenciais do Windows. Configure o segundo aplicativo de destino com as credenciais de uma fonte de dados que não ofereça suporte à autenticação do Windows; por exemplo, um banco de dados Oracle. O segundo aplicativo de destino também usa o primeiro aplicativo de destino para a conta autônoma de atualização de dados.  
  
 ![as_powerpivot_refresh_no_windows_auth](../media/as-powerpivot-refresh-no-windows-auth.gif "as_powerpivot_refresh_no_windows_auth")  
  
-   **(1) PowerPivotDatarefresh:** uma ID de aplicativo de destino de repositório seguro definida com a autenticação do Windows.  
  
-   **(2) OracleAuthentication:** uma ID de aplicativo de destino de repositório seguro definida com as credenciais do Oracle.  
  
-   **(3)** o aplicativo de serviço PowerPivot é configurado para usar o aplicativo de destino "PowerPivotDataRefresh" para a **conta de atualização de dados autônoma**.  
  
-   **(4)** A pasta de trabalho PowerPivot usa dados Oracle. As configurações de atualização da pasta de trabalho especificam a conexão da fonte de dados para usar o aplicativo de destino **(2)** para credenciais.  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
-   Existe um aplicativo de serviço PowerPivot.  
  
-   Existe um aplicativo de Serviço de Repositório Seguro.  
  
-   Existe uma pasta de trabalho do Excel com um modelo de dados PowerPivot.  
  
## <a name="to-create-a-target-application-id-that-uses-windows-authentication"></a>Para criar uma ID de aplicativo de destino que usa a Autenticação do Windows  
  
1.  Na administração central do SharePoint, clique em **gerenciar aplicativos de serviço**.  
  
2.  Clique no nome do aplicativo de Serviço de Repositório Seguro.  
  
3.  Na página **Gerenciar** , clique em **Nova**. ![as_powerpivot_refresh_sss_new_target_application](../media/as-powerpivot-refresh-sss-new-target-application.gif "as_powerpivot_refresh_sss_new_target_application")  
  
4.  Na página **Criar Novo Aplicativo de Destino de Repositório Seguro** , configure os seguintes valores:  
  
    -   **ID de Aplicativo de Destino:** PowerPivotDataRefresh.  
  
    -   **Nome para Exibição:** PowerPivotDataRefresh.  
  
    -   **Email de Contato:** ?  
  
    -   **Tipo de Aplicativo de Destino:** Grupo.  
  
    -   **URL da Página de Aplicativo de Destino:** Nenhuma.  
  
5.  Clique em **Avançar**.  
  
6.  Na página Credenciais, deixe os dois nomes de campo padrão e os tipos de campo de **Nome de Usuário do Windows** e **Senha do Windows**.  
  
7.  Clique em **Avançar**.  
  
8.  Na página **Configurações de Associação** , adicione pelo menos um **Administrador de Aplicativo de Destino** e adicione os membros que precisam acessar o aplicativo de destino.  
  
9. Clique em **OK**.  
  
10. Uma nova ID de aplicativo de destino será adicionada à lista. Selecione a ID do aplicativo de destino e clique em **definir credenciais**![as_powerpivot_refresh_sss_set_key](../media/as-powerpivot-refresh-sss-set-key.gif "as_powerpivot_refresh_sss_set_key").  
  
11. Digite o nome de usuário do Windows e a senha do Windows, e clique em **OK**.  
  
## <a name="to-create-a-target-application-id-that-uses-oracle-credentials"></a>Para criar uma ID de aplicativo de destino que usa as credenciais do Oracle  
  
1.  Na administração central do SharePoint, clique em **gerenciar aplicativos de serviço**.  
  
2.  Clique no nome do aplicativo de Serviço de Repositório Seguro.  
  
3.  Na página **gerenciar** , clique em **novo**![as_powerpivot_refresh_sss_new_target_application](../media/as-powerpivot-refresh-sss-new-target-application.gif "as_powerpivot_refresh_sss_new_target_application").  
  
4.  Na página **Criar Novo Aplicativo de Destino de Repositório Seguro** , configure os seguintes valores:  
  
    -   **ID do Aplicativo de Destino:** OracleAuthentication.  
  
    -   **Nome para Exibição:** OracleAuthentication.  
  
    -   **Email de Contato:** ?  
  
    -   **Tipo de Aplicativo de Destino:** Grupo.  
  
    -   **URL da Página de Aplicativo de Destino:** Nenhuma.  
  
5.  Clique em **Avançar**.  
  
6.  Na página **credenciais** , altere o nome do primeiro campo para `Oracle User ID` e altere o **tipo** de campo `User Name`para.  
  
     Altere o segundo nome de campo `Oracle Password` para e o **tipo** de `Password`campo para.  
  
7.  Clique em **Avançar**.  
  
8.  Na página **Configurações de Associação** , adicione pelo menos um **Administrador de Aplicativo de Destino** e adicione os membros que precisam acessar o aplicativo de destino.  
  
9. Clique em **OK**.  
  
10. Uma nova ID de aplicativo de destino será adicionada à lista. Selecione a ID do aplicativo de destino e clique em **definir credenciais**![as_powerpivot_refresh_sss_set_key](../media/as-powerpivot-refresh-sss-set-key.gif "as_powerpivot_refresh_sss_set_key").  
  
11. Digite a ID do Usuário Oracle e a Senha Oracle, e clique em **OK**.  
  
 Para obter mais informações, consulte a seção "para criar um aplicativo de destino para SQL Server autenticação" em [usar repositório seguro com autenticação SQL Server (SharePoint Server 2013)](https://technet.microsoft.com/library/gg298949.aspx) (https://technet.microsoft.com/library/gg298949.aspx).  
  
## <a name="to-configure-the-powerpivot-service-application"></a>Para configurar o aplicativo de serviço PowerPivot  
  
1.  Na Administração Central do SharePoint, clique em Gerenciar Aplicativos de Serviço.  
  
2.  Clique no nome do aplicativo de serviço PowerPivot, por exemplo, "aplicativo de serviço PowerPivot padrão".  
  
3.  Clique em **Definir configurações do aplicativo de serviço** na seção Ações.  
  
4.  Na seção **atualização de dados** , defina a **conta de atualização de dados autônoma**do PowerPivot`PowerPivotDataRefresh` para e clique em **OK**.  
  
     ![as_powerpivot_refresh_new_refresh_acount](../media/as-powerpivot-refresh-new-refresh-acount.gif "as_powerpivot_refresh_new_refresh_acount")  
  
## <a name="to-configure-the-workbook"></a>Para configurar a pasta de trabalho  
  
1.  Navegue até a pasta de trabalho na Galeria PowerPivot e clique em **gerenciar atualização de dados**![as_powerpivot_refresh_manage_reresh](../media/as-powerpivot-refresh-manage-reresh.gif "as_powerpivot_refresh_manage_reresh").  
  
2.  Se a página **Histórico de Atualização de Dados** for exibida, clique em **Configurar Agendamento**.  
  
3.  Clique em **Habilitar**.  
  
4.  Clique em **Também atualizar o mais rápido possível**.  
  
5.  Na seção **Credenciais** , clique em **Usar a conta de atualização de dados configurada pelo administrador**.  
  
6.  Limpe **Todas as fontes de dados**.  
  
7.  Selecione **Atualizar** para a fonte de dados que usa os dados Oracle. O nome da fonte de dados pode ser alterado no Microsoft Excel através do menu **Dados**, **Conexões**, **Propriedades** .  
  
8.  Abaixo da sua fonte de dados, selecione **Usar Agendamento Padrão**.  
  
9. Selecione **Conecte-se usando as credenciais salvas no SSS (Serviço de Repositório Seguro) para fazer logon na fonte de dados. Insira a ID usada para pesquisar as credenciais na caixa ID do SSS**.  
  
10. Na caixa **ID:** , digite `OracleAuthentication`.  
  
11. Clique em **OK**.  
  
     Se uma mensagem de erro semelhante a `The provided Secure Store target application is either incorrectly configured or does not exist`for exibida.  
  
     Há duas soluções comuns:  
  
    -   Verifique se a ID do aplicativo de destino está correta.  
  
    -   Verifique se você definiu as credenciais do aplicativo de destino.  
  
## <a name="to-verify-data-refresh-with-the-new-authentication"></a>Para verificar a atualização de dados com a nova autenticação  
 Ao clicar em **OK**, você verá a página **Histórico de Atualização** . Em alguns minutos, você verá um novo item no histórico de atualização porque, na etapa anterior, selecionou **Também atualizar o mais rápido possível**. O valor padrão do **Trabalho de Timer da Atualização de Dados PowerPivot** é um minuto. Se um novo item não aparecer no histórico de atualização, aguarde alguns minutos e atualize o navegador. Se, ainda assim, o novo item não aparecer, verifique o valor atual do trabalho de timer.  
  
## <a name="more-information"></a>Mais informações  
  
-   [Configurar o Serviço de Repositório Seguro no SharePoint 2013](https://technet.microsoft.com/library/ee806866.aspx).  
  
-   Consulte a seção "atualização de dados agendada" da [atualização de dados PowerPivot com o SharePoint 2013 e SQL Server 2012 SP1 (Analysis Services)](https://msdn.microsoft.com/library/jj879294.aspx#bkmk_windows_auth_interactive_data_refresh).  
  
  

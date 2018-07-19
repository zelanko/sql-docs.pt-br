---
title: Gerenciador de Conexões do Azure Data Lake Analytics | Microsoft Docs
ms.custom: ''
ms.date: 05/18/2018
ms.prod: sql
ms.prod_service: integration-services
ms.component: connection-manager
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
caps.latest.revision: 7
author: yanancai
ms.author: yanacai
manager: craigg
ms.openlocfilehash: 17b63aad55cf50262d7e1e56267859b1a34cc9d3
ms.sourcegitcommit: 44e9bf62f2c75449c17753ed66bf85c43928dbd5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/05/2018
ms.locfileid: "37854398"
---
# <a name="azure-data-lake-analytics-connection-manager"></a>Gerenciador de Conexão do Azure Data Lake Analytics

Um pacote do SSIS (SQL Server Integration Services) pode usar o Gerenciador de Conexões do Azure Data Lake Analytics para se conectar a uma conta do Azure Data Lake Analytics com um dos dois tipos de autenticação a seguir:
-   Identidade do Usuário do Azure AD
-   Identidade do Serviço do Azure AD 

O gerenciador de conexões do Azure Data Lake Analytics é um componente do [Feature Pack do SSIS (SQL Server Integration Services) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
 
## <a name="configure-the-azure-data-lake-analytics-connection-manager"></a>Configurar o Gerenciador de Conexão do Azure Data Lake Analytics

1.  Na caixa de diálogo **Adicionar gerenciador de conexões do SSIS**, selecione **AzureDataLakeAnalytics** e selecione **Adicionar**. A caixa de diálogo **Editor de conexões do Azure Data Lake Analytics** se abre.
  
2.  Na caixa de diálogo **Editor do Gerenciador de Conexão do Azure Data Lake Analytics**, no campo **Nome da Conta ADLA**, forneça o nome da conta do Azure Data Lake Analytics. Por exemplo: myadlaaccountname.
  
3.  No campo **Autenticação**, escolha o tipo de autenticação apropriado para acessar os dados no Azure Data Lake Analytics.

    1.  Se você selecionou a opção de autenticação **Identidade de Usuário do Azure AD**, faça o seguinte:
        1. Forneça valores para os campos **Nome de Usuário** e **Senha**. 
    
        2. Selecione **Testar Conexão** para testar a conexão. Se você ou o administrador do locatário não consentiu anteriormente em permitir que o SSIS acessasse a conta do Azure Data Lake Analytics, selecione **Aceitar** quando solicitado. Para obter mais informações sobre esta experiência de consentimento, consulte [integrando aplicativos com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications#updating-an-application).
    
        >   [!NOTE] 
        > Quando você seleciona a opção de autenticação por **Identidade do Usuário do Azure AD**, a autenticação multifator e a autenticação por conta da Microsoft não têm suporte.
    
    2. Se você selecionou a opção de autenticação **Identidade do Serviço do Azure AD**, faça o seguinte:
        1. Crie uma entidade de serviço e um aplicativo do AAD (Azure Active Directory) para acessar a conta do Azure Data Analytics. Para obter mais informações sobre essa opção de autenticação, consulte [Use o portal para criar a entidade de serviço e o aplicativo do Active Directory que pode acessar recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal).
    
        2. Atribua as permissões apropriadas para permitir que este aplicativo do AAD acesse sua conta do Azure Data Analytics. Saiba como conceder permissões para sua conta do Azure Data Lake Analytics [usando o Assistente para Adicionar Usuário](https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-manage-use-portal#add-a-new-user). 
    
        3. Forneça valores para os campos **ID do aplicativo**, **Chave de Autenticação** e **ID do locatário**.
    
        4. Selecione **Testar Conexão** para testar a conexão.  

4.  Selecione **OK** para fechar a caixa de diálogo **Editor do Gerenciador de Conexões do Azure Data Lake Analytics**.  

## <a name="view-the-properties-of-the-connection-manager"></a>Exibir as propriedades do gerenciador de conexões
Você pode ver as propriedades do gerenciador de conexões criado na janela **Propriedades** .  
  
  

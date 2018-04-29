---
title: Gerenciador de conexões do Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: integration-services
ms.service: ''
ms.component: connection-manager
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
caps.latest.revision: 7
author: Lingxi-Li
ms.author: lingxl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 19b837269fcfbf41723cee9cd15235f0e2136e15
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="azure-data-lake-store-connection-manager"></a>Gerenciador de conexões do Azure Data Lake Store
Um pacote do SSIS (SQL Server Integration Services) pode usar o Gerenciador de Conexões do Azure Data Lake Store para se conectar a um serviço do Azure Data Lake Store com um dos dois tipos de autenticação a seguir:
-   Identidade do Usuário do Azure AD
-   Identidade do Serviço do Azure AD 

O gerenciador de conexões do Azure Data Lake Store é um componente do [Feature Pack do SSIS (SQL Server Integration Services) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

>   [!NOTE]
> Para garantir que o Gerenciador de conexões do Azure Data Lake Store e os componentes que o utilizam, isto é, a Fonte do Azure Data Lake Store e o Destino do Azure Data Lake Store, possam se conectar aos serviços, verifique se você baixou a versão mais recente do Azure Feature Pack [aqui](https://www.microsoft.com/download/details.aspx?id=49492). 
 
## <a name="configure-the-azure-data-lake-store-connection-manager"></a>Configurar o Gerenciador de conexões do Azure Data Lake Store

1.  Na caixa de diálogo **Adicionar gerenciador de conexões do SSIS**, selecione **AzureDataLake** e selecione **Adicionar**. A caixa de diálogo **Editor de conexões do Azure Data Lake Store** se abre.
  
2.  Na caixa de diálogo **Editor de Gerenciador de conexões do Azure Data Lake Store**, no campo **Host ADLS**, forneça a URL do host do Azure Data Lake Store. Por exemplo: `https://test.azuredatalakestore.net` ou `test.azuredatalakestore.net`.
  
3.  No campo **Autenticação**, escolha o tipo de autenticação apropriado para acessar os dados no Azure Data Lake Store.

    1.  Se você selecionou a opção de autenticação **Identidade de Usuário do Azure AD**, faça o seguinte:
        1. Forneça valores para os campos **Nome de Usuário** e **Senha**. 
    
        2. Selecione **Testar Conexão** para testar a conexão. Se você ou o administrador do locatário não consentiu anteriormente em permitir que o SSIS acessasse os dados do Azure Data Lake Store, selecione **Aceitar** quando solicitado. Para obter mais informações sobre esta experiência de consentimento, consulte [integrando aplicativos com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications#updating-an-application).
    
        >   [!NOTE] 
        > Quando você seleciona a opção de autenticação por **Identidade do Usuário do Azure AD**, a autenticação multifator e a autenticação por conta da Microsoft não têm suporte.
    
    2. Se você selecionou a opção de autenticação **Identidade do Serviço do Azure AD**, faça o seguinte:
        1. Crie uma entidade de serviço e um aplicativo do AAD (Azure Active Directory) para acessar os dados do Azure Data Lake.
    
        2. Atribua as permissões apropriadas para permitir que este aplicativo do AAD acesse seus recursos do Azure Data Lake. Para obter mais informações sobre essa opção de autenticação, consulte [Use o portal para criar a entidade de serviço e o aplicativo do Active Directory que pode acessar recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal).
    
        3. Forneça valores para os campos **Id do cliente**, **Chave Secreta** e **Nome do Locatário**.
    
        4. Selecione **Testar Conexão** para testar a conexão.  
  
6.  Selecione **OK** para fechar a caixa de diálogo **Editor do Gerenciador de Conexões do Azure Data Lake Store**.  

## <a name="view-the-properties-of-the-connection-manager"></a>Exibir as propriedades do gerenciador de conexões
Você pode ver as propriedades do gerenciador de conexões criado na janela **Propriedades** .  
  
  

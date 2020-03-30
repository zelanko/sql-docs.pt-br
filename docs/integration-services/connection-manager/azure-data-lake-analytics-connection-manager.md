---
title: Gerenciador de conexões do Azure Data Lake Analytics | Microsoft Docs
description: Um pacote do SSIS (SQL Server Integration Services) pode usar o Gerenciador de Conexões do Azure Data Lake Analytics para se conectar a uma conta do Data Lake Analytics.
ms.custom: ''
ms.date: 05/18/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: maghan
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSCM.F1
- sql14.dts.designer.afpadlscm.f1
ms.assetid: f4c44553-0f08-4731-ac47-7534990b8c8d
author: yanancai
ms.author: yanacai
ms.openlocfilehash: c2ae186aa7d7fe9ee4ef7da26ed0f5e667b8e2d9
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67904817"
---
# <a name="azure-data-lake-analytics-connection-manager"></a>Gerenciador de conexão do Azure Data Lake Analytics

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Um pacote do SSIS (SQL Server Integration Services) pode usar o Gerenciador de Conexões do Azure Data Lake Analytics para se conectar a uma conta do Data Lake Analytics com um dos dois tipos de autenticação a seguir:
-   Identidade de Usuário do Azure Active Directory (Azure AD)
-   Identidade do Serviço do Azure AD 

O gerenciador de conexões do Data Lake Analytics é um componente do [Feature Pack do SSIS (SQL Server Integration Services) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
 
## <a name="configure-the-connection-manager"></a>Configurar o gerenciador de conexões

1. Na caixa de diálogo **Adicionar gerenciador de conexões do SSIS**, selecione **AzureDataLakeAnalytics** > **Adicionar**. A caixa de diálogo **Editor de conexões do Azure Data Lake Analytics** se abre.
  
2. Na caixa de diálogo **Editor do Gerenciador de Conexões do Data Lake Analytics**, no campo **Nome da Conta ADLA**, forneça o nome da conta do Azure Data Lake Analytics. Por exemplo: myadlaaccountname.
  
3. No campo **Autenticação**, escolha o tipo de autenticação apropriado para acessar os dados no Data Lake Analytics.

   a. Se você selecionou a opção de autenticação **Identidade de Usuário do Azure AD**:
   
      i. Forneça valores para os campos **Nome de Usuário** e **Senha**.    
      ii. Selecione **Testar Conexão** para testar a conexão. Se você ou o administrador do locatário não consentiu anteriormente em permitir que o SSIS acessasse a conta do Data Lake Analytics, selecione **Aceitar** quando solicitado. Para obter mais informações sobre esta experiência de consentimento, consulte [integrando aplicativos com o Azure Active Directory](https://docs.microsoft.com/azure/active-directory/manage-apps/plan-an-application-integration#integrating-applications-with-azure-ad).
    
   > [!NOTE] 
   > Quando você seleciona a opção de autenticação por **Identidade do Usuário do Azure AD**, a autenticação multifator e a autenticação por conta da Microsoft não têm suporte.
    
   b. Se você selecionou a opção de autenticação **Identidade do Serviço do Azure AD**:
   
      i. Crie uma entidade de serviço e um aplicativo do Azure AD para acessar a conta do Data Lake Analytics. Para obter mais informações sobre essa opção de autenticação, consulte [Use o portal para criar a entidade de serviço e o aplicativo do Active Directory que pode acessar recursos](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal).    
      ii. Atribua as permissões apropriadas para permitir que este aplicativo do Azure AD acesse sua conta do Data Lake Analytics. Saiba como conceder permissões para sua conta do Data Lake Analytics usando o [Assistente para Adicionar Usuário](https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-manage-use-portal#add-a-new-user).    
      III. Forneça valores para os campos **ID do aplicativo**, **Chave de Autenticação** e **ID do locatário**.    
      iv. Selecione **Testar Conexão** para testar a conexão.  

4. Selecione **OK** para fechar a caixa de diálogo **Editor do Gerenciador de Conexões do Azure Data Lake Analytics**.  

## <a name="view-the-properties-of-the-connection-manager"></a>Exibir as propriedades do gerenciador de conexões
Você pode ver as propriedades do gerenciador de conexões criado na janela **Propriedades** .  
  
  

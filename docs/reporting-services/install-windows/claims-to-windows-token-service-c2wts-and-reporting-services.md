---
description: C2WTS (Declarações para Serviço de Token do Windows) e Reporting Services
title: c2WTS (Declarações para Serviço de Token do Windows) e Reporting Services | Microsoft Docs
author: maggiesMSFT
ms.author: maggies
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.topic: conceptual
ms.date: 09/15/2017
ms.openlocfilehash: 78d7265398cab553a9378fecc54b25a32d36e84d
ms.sourcegitcommit: 3bd188e652102f3703812af53ba877cce94b44a9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97489826"
---
# <a name="claims-to-windows-token-service-c2wts-and-reporting-services"></a>Claims to Windows Token Service (C2WTS) e Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)]

O C2WTS (Declarações para Serviço de Token do Windows) do SharePoint é obrigatório se você deseja exibir relatórios no modo nativo na [web part do Visualizador de Relatórios do SQL Server Reporting Services](../report-server-sharepoint/deploy-report-viewer-web-part.md).

O C2WTS também é obrigatório com o modo do SharePoint do SQL Server Reporting Services se você deseja usar a autenticação do Windows para fontes de dados que estão fora do farm do SharePoint. O C2WTS é necessário até mesmo quando as fontes de dados estão no mesmo computador que o serviço compartilhado. Entretanto, neste cenário, a delegação restrita não é necessária.

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.

## <a name="report-viewer-native-mode-web-part-configuration"></a>Configuração de Web part do Visualizador de Relatórios (Modo Nativo)

A web part do Visualizador de Relatórios pode ser usada para inserir relatórios no modo nativo do SQL Server Reporting Services no site do SharePoint. Essa web part está disponível para o SharePoint 2013 e SharePoint 2016. O SharePoint 2013 e SharePoint 2016 fazem uso da autenticação de declarações. Como resultado, o C2WTS precisa ser configurado corretamente e o Reporting Services precisa ser configurado para autenticação Kerberos para que os relatórios sejam renderizados corretamente.

1. Configure sua instância do Reporting Services (Modo Nativo) para autenticação Kerberos determinando a conta de serviço do SSRS, definindo um SPN e atualizando o arquivo rsreportserver.config para usar o tipo de autenticação RSWindowsNegotiate. [Registrar um SPN (Nome da Entidade de Serviço) para um servidor de relatório](../report-server/register-a-service-principal-name-spn-for-a-report-server.md)

2. Siga as etapas em [Etapas necessárias para configurar o c2WTS](#steps-needed-to-configure-c2wts)
 

## <a name="sharepoint-mode-integration"></a>Integração de modo do SharePoint

**Esta seção se aplica apenas ao SQL Server 2016 Reporting Services e anterior.**

O C2WTS (Declarações para Serviço de Token do Windows) do SharePoint é obrigatório com o modo do SharePoint do SQL Server Reporting Services se você deseja usar a Autenticação do Windows para fontes de dados que estão fora do farm do SharePoint. Isso ocorre mesmo quando o usuário acessa as fontes de dados com a Autenticação do Windows porque a comunicação entre o WFE (front-end da Web) e o serviço compartilhado do Reporting Services sempre será uma Autenticação de Declarações.

## <a name="steps-needed-to-configure-c2wts"></a>Etapas necessárias para configurar o c2WTS

Os tokens criados por C2WTS só funcionarão com a delegação restrita (restrições a serviços específicos) e a opção de configuração "usando qualquer protocolo de autenticação" (Transição de protocolo).

Se seu ambiente usar a delegação restrita de Kerberos, o serviço do SharePoint Server e as fontes de dados externas precisarão residir no mesmo domínio do Windows. Qualquer serviço que dependa do c2WTS (Declarações para Serviço de Token do Windows) deve usar a delegação **restrita** Kerberos para permitir que o c2WTS use a transição do protocolo Kerberos para traduzir declarações em credenciais do Windows. Estes requisitos são verdadeiros para todos os Serviços Compartilhados do SharePoint. Para obter mais informações, consulte [Plano para autenticação Kerberos no SharePoint 2013](/SharePoint/security-for-sharepoint-server/kerberos-authentication-planning).  

1. Configure a conta de domínio de serviço do C2WTS. 

    **Como melhor prática, o C2WTS deve ser executado com sua própria identidade de domínio.**

    * Crie uma conta do Active Directory e registre a conta como uma conta gerenciada no SharePoint Server.
   
    * Configure o serviço do C2WTS para usar a conta gerenciada em Administração Central do SharePoint > Segurança > Configurar Contas de Serviço > Serviço Windows – Declarações do Serviço de Token do Windows

    Adicione a conta de serviço do C2WTS ao grupo de Administradores local em cada servidor em que o C2WTS será usado. Para a **web part do Visualizador de Relatórios**, eles serão os servidores WFE (Front-end da Web). Para o **modo integrado do SharePoint**, eles serão os servidores de aplicativos em que o serviço Reporting Services está em execução.
    * Conceda à conta do C2WTS as seguintes permissões na política de segurança local em Políticas Locais > Atribuição de direitos de usuário:
        * Atuar como parte do sistema operacional
        * Representar um cliente após a autenticação
        * Fazer logon como um serviço

    
2. Configure a delegação para a conta de serviço do C2WTS.

    A conta precisa da Delegação Restrita com Transição de Protocolo e de permissões para delegar aos serviços com os quais ela precisa se comunicar (ou seja, Mecanismo de Banco de Dados do SQL Server, SQL Server Analysis Services). Para configurar a delegação, você pode usar o snap-in Usuários e Computador do Active Directory e precisará ser um administrador de domínio.

    > [!IMPORTANT]
    > Todas as configurações que você definir para a conta de serviço do C2WTS na guia Delegação precisarão corresponder à conta de serviço principal usada. Para a **web part do Visualizador de Relatórios**, essa será a conta de serviço do aplicativo Web do SharePoint. Para o **modo integrado do SharePoint**, essa será a conta de serviço do Reporting Services.
    >
    > Por exemplo, se você permitir que a conta de serviço do C2WTS delegue para um Serviço SQL, precisará fazer o mesmo na conta de serviço do Reporting Services para o modo integrado do SharePoint.

    * Clique com o botão direito do mouse em cada conta de serviço e abra a caixa de diálogo de propriedades. Na caixa de diálogo, clique na guia **Delegação** .

        A guia Delegação só ficará visível se o objeto tiver um SPN (Nome da Entidade de Serviço) atribuído a ele. O C2WTS não exige um SPN na Conta do C2WTS; porém, sem um SPN, a guia **Delegação** não ficará visível. Um modo alternativo de configurar a delegação restrita é usar um utilitário como **ADSIEdit**.

    * Principais opções de configuração na guia delegação:

        * Selecione **Confiar neste usuário apenas para delegação a serviços especificados**
        * Selecione **Usar qualquer protocolo de autenticação**

    * Selecione **Adicionar** para adicionar um serviço para delegação.

    * Selecione **Usuários ou Computadores...&#42;** e insira a conta que hospeda o serviço. Por exemplo, se um SQL Server for executado em uma conta chamada *sqlservice*, insira `sqlservice`. 
      Para a **Web part do Visualizador de Relatórios**, essa será a conta de serviço da Instância do Reporting Services (Modo Nativo).

    * Selecione a lista de serviços. Isso mostrará os SPNs que estão disponíveis nessa conta. Se você não vir o serviço listado nessa conta, ele pode estar ausente ou colocado em uma conta diferente. Você pode usar o utilitário SetSPN para ajustar os SPNs. Para a **Web part do Visualizador de Relatórios**, você verá o SPN HTTP configurado em [Configuração de Web part do Visualizador de Relatórios](#report-viewer-native-mode-web-part-configuration).

    * Selecione OK para sair das caixas de diálogo.

3. Configure o *AllowedCallers* do C2WTS.

    O C2WTS exige que as identidades dos "chamadores" sejam explicitamente listadas no arquivo de configuração, **C2WTShost.exe.config**. O C2WTS não aceita solicitações de todos os usuários autenticados no sistema, a menos que esteja configurado para fazer assim. Neste caso, o “chamador” é o grupo WSS_WPG do Windows. O arquivo C2WTShost.exe.confi é salvo no seguinte local:

    Alterar a conta de serviço na Administração Central do SharePoint para o serviço C2WTS adicionará essa conta ao grupo WSS_WPG.

    **\Arquivos de Programas\Windows Identity Foundation\v3.5\c2WTShost.exe.config**

    Este é um exemplo do arquivo de configuração:

    ```
    <configuration>
      <windowsTokenService>
        <!--  
            By default no callers are allowed to use the Windows Identity Foundation Claims To NT Token Service.  
            Add the identities you wish to allow below.  
          -->
        <allowedCallers>
          <clear/>
          <add value="WSS_WPG" />
        </allowedCallers>
      </windowsTokenService>
    </configuration>
    ```

4. Inicie (pare e inicie se já estiver iniciado) as Declarações para Serviço de Token do Windows pela Administração Central do SharePoint na página **Gerenciar Serviços no Servidor**. O serviço deverá ser iniciado no servidor que estará executando a ação. Por exemplo, se você tiver um servidor que é um WFE e outro servidor que é um Servidor de Aplicativos que tem o serviço compartilhado SQL Server Reporting Services em execução, precisará apenar iniciar o C2WTS no Servidor de Aplicativos. O C2WTS só será obrigatório em um servidor WFE se você estiver executando a web part do Visualizador de Relatórios.

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)

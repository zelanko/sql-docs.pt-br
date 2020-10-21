---
title: Implantação no modo do Active Directory – Pré-requisitos
titleSuffix: SQL Server Big Data Cluster
description: Configurar o Active Directory para Clusters de Big Data do SQL Server
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 09/30/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 6c25038680d71257e609d99460841d63b8e87d33
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91898651"
---
# <a name="deploy-big-data-clusters-2019-in-active-directory-mode-prerequisites"></a>Implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no modo do Active Directory: Pré-requisitos

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

Este documento explica como preparar a implantação de um BDC (cluster de Big Data) do SQL Server no modo de autenticação do Active Directory. O cluster usa um domínio existente do AD para autenticação.

>[!Note]
>Antes do lançamento do SQL Server 2019 CU5, havia uma restrição nos Clusters de Big Data que especificava que apenas um cluster podia ser implantado em um domínio do Active Directory. Essa restrição foi removida na versão CU5. Confira [Conceito: implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no modo do Active Directory](active-directory-deployment-background.md) para obter detalhes sobre as novas funcionalidades. Os exemplos deste artigo foram ajustados para acomodar os dois casos de uso de implantação.

## <a name="background"></a>Segundo plano

Para habilitar a autenticação do AD (Active Directory), o BDC cria automaticamente os usuários, os grupos, as contas de computadores e os SPNs (nomes da entidade de serviço) de que os diversos serviços do cluster. Para fornecer alguma independência a essas contas e permitir a definição de escopos para as permissões, sugerimos a criação de uma UO (unidade organizacional) antes da implantação do cluster. Todos os objetos do AD relacionados ao BDC serão criados durante a implantação. 

## <a name="pre-requisites"></a>Pré-requisitos

### <a name="organizational-unit-ou"></a>OU (Unidade Organizacional)
Uma UO (unidade organizacional) é uma subdivisão dentro de um Active Directory na qual se coloca usuários, grupos e até mesmo outras unidades organizacionais. É possível usar as unidades organizacionais da visão global para espelhar a estrutura funcional ou comercial de uma organização. Este artigo criará uma UO chamada `bdc` como um exemplo. 

>[!NOTE]
>A UO (unidade organizacional) representa limites administrativos e permite que os clientes controlem o escopo de autoridade dos administradores de dados. 

Você pode seguir [Princípios de Design de UO](/windows-server/identity/ad-ds/plan/reviewing-ou-design-concepts) para decidir a melhor estrutura ao trabalhar com UOs em sua organização.

### <a name="ad-account-for-bdc-domain-service-account"></a>Conta no AD para a conta de serviço de domínio do BDC

Para poder criar automaticamente todos os objetos necessários no Active Directory, o BDC precisa de uma conta do AD que tenha permissões específicas para criar usuários, grupos e contas de computador dentro da UO (unidade organizacional) fornecida. Este artigo explicará como configurar a permissão dessa conta do AD. Usamos uma chamada de Conta do AD `bdcDSA` como um exemplo neste artigo.

### <a name="auto-generated-active-directory-objects"></a>Objetos do Active Directory gerados automaticamente
A implantação do BDC gera automaticamente nomes de contas e grupos. Cada uma das contas representa um serviço no BDC e será gerenciada pelo BDC durante o tempo de vida em que o cluster BDC estiver em uso. Essas contas são proprietárias dos SPNs (Nomes da Entidade de Serviço) necessários para cada serviço.  Para obter uma lista completa de contas, grupos e serviços gerados automaticamente pelo AD que eles gerenciaram, confira [Objetos do Active Directory gerados automaticamente](active-directory-objects.md).

>[!IMPORTANT]
>Dependendo da política de expiração de senha definida no Controlador de Domínio, as senhas dessas contas podem expirar. A política de expiração padrão é de 42 dias. Não há mecanismo para girar credenciais para todas as contas no BDC, portanto, o cluster se tornará inoperante assim que o período de expiração for atingido. Para solucionar esse problema, atualize a política de expiração das contas de serviço BDC para “A senha nunca expira” no controlador de domínio. Essa ação pode ser realizada antes ou depois do horário de expiração. No último caso, o Active Directory reativará as senhas expiradas.
>
>A imagem a seguir mostra onde definir essa propriedade em Usuários e Computadores do Active Directory.
>
>:::image type="content" source="media/deploy-active-directory/image25.png" alt-text="Definir política de expiração de senha":::

As etapas a seguir pressupõem que você já tenha um controlador de domínio do Active Directory Domain Services. Se você não tem um controlador de domínio, o [guia](https://social.technet.microsoft.com/wiki/contents/articles/37528.create-and-configure-active-directory-domain-controller-in-azure-windows-server.aspx) a seguir inclui etapas que podem ser úteis.

## <a name="create-ad-objects"></a>Criar objetos do AD

Faça o seguinte antes de implantar um BDC com a integração do AD:

1. Crie uma UO (unidade organizacional) na qual todos os objetos do AD relacionados do BDC serão armazenados. Como alternativa, você pode escolher uma UO existente durante a implantação.
1. Crie uma conta do AD para o BDC (ou use uma conta existente) e forneça para essa conta do AD do BDC as permissões corretas dentro da UO (unidade organizacional).

### <a name="create-a-user-in-ad-for-bdc-domain-service-account"></a>Crie um usuário no AD para a conta de serviço de domínio do BDC

O cluster de Big Data requer uma conta com permissões específicas. Antes de prosseguir, verifique se você tem uma conta existente do AD ou crie uma nova conta que o cluster de Big Data possa usar para configurar os objetos necessários.

Para criar um novo usuário no AD, você pode clicar com o botão direito do mouse no domínio ou na UO e selecionar **Novo** > **Usuário**:

![Caixa de diálogo de usuários do Active Directory](./media/deploy-active-directory/image12.png)

Esse usuário será chamado de *conta de serviço de domínio do BDC* neste artigo.

### <a name="create-an-ou"></a>Criar uma UO

No controlador de domínio, abra **Usuários e Computadores do Active Directory**. No painel esquerdo, clique com o botão direito do mouse no diretório no qual deseja criar a UO e selecione **Nova** \> **Unidade Organizacional** e siga os avisos do assistente para criar a UO. Como alternativa, você pode criar uma UO com o PowerShell:

```powershell
New-ADOrganizationalUnit -Name "<name>" -Path "<Distinguished name of the directory you wish to create the OU in>"
```

Os exemplos deste artigo usam `bdc` como o nome da UO.

![Unidade organizacional do Active Directory](./media/deploy-active-directory/image13.png)

![Novo objeto – unidade organizacional](./media/deploy-active-directory/image14.png)

### <a name="set-permissions-for-an-ad-account"></a>Definir permissões para uma conta do AD

Quer você tenha criado um novo usuário ou esteja usando um usuário existente do AD, há certas permissões que o usuário precisa ter. Essa conta é a conta de usuário que o controlador do BDC usará ao ingressar o cluster no AD.

A DSA (conta de serviço de domínio) do BDC precisa ser capaz de criar usuários, grupos e contas de máquina na UO. Nas etapas a seguir, demos à conta de serviço de domínio do BDC o nome `bdcDSA`. Você pode escolher qualquer nome para a conta.

1. No controlador de domínio, abra **Usuários e Computadores do Active Directory**

1. No painel esquerdo, navegue para seu domínio e, em seguida, para a UO que `bdc` usará

1. Clique com o botão direito do mouse na UO e selecione **Propriedades**.

1. Vá para a guia Segurança (verifique se você selecionou **Recursos Avançados** clicando com o botão direito do mouse na UO e selecionando **Exibir**)

    ![Propriedades de objeto do BDC](./media/deploy-active-directory/image15.png)

1. Clique em **Adicionar...** e adicione o usuário do **bdcDSA**

    ![Adicionar propriedades de objeto do BDC](./media/deploy-active-directory/image16.png)

    ![Selecionar objeto](./media/deploy-active-directory/image17.png)

1. Selecione o usuário do **bdcDSA**, desmarque todas as permissões e clique em **Avançado**

1. Clique em **Adicionar**

    ![Clicar em Adicionar](./media/deploy-active-directory/image18.png)

    - Clique em **Selecionar uma Entidade de Segurança**, insira **bdcDSA** e clique em OK

    - Defina o **Tipo** como **Permitir**

    - Defina **Aplica-se a** como **Este objeto e todos os descendentes**

        ![Definir a opção Permitir para propriedades](./media/deploy-active-directory/image19.png)

    - Role até a parte inferior e clique em **Limpar tudo**

    - Role de volta para a parte superior e selecione:
       - **Ler todas as propriedades**
       - **Gravar todas as propriedades**
       - **Criar Objetos de computador**
       - **Excluir Objetos de computador**
       - **Criar Objetos de grupo**
       - **Excluir Objetos de grupo**
       - **Criar Objetos de usuário**
       - **Excluir objetos de usuário**

    - Clique em **OK**

- Clique em **Adicionar**

    - Clique em **Selecionar uma Entidade de Segurança**, insira **bdcDSA** e clique em OK

    - Defina o **Tipo** como **Permitir**

    - Defina **Aplica-se a** como **Objetos de computador descendentes**

    - Role até a parte inferior e clique em **Limpar tudo**

    - Role de volta para a parte superior e selecione **Redefinir senha**

    - Clique em **OK**

- Clique em **Adicionar**

    - Clique em **Selecionar uma Entidade de Segurança**, insira **bdcDSA** e clique em OK

    - Defina o **Tipo** como **Permitir**

    - Defina **Aplica-se a** como **Objetos de usuário descendentes**

    - Role até a parte inferior e clique em **Limpar tudo**

    - Role de volta para a parte superior e selecione **Redefinir senha**

    - Clique em **OK**

- Clique em **OK** mais duas vezes para fechar as caixas de diálogo abertas

## <a name="next-steps"></a>Próximas etapas

[Implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no modo do Active Directory](active-directory-deploy.md)

[Solucionar problemas de integração do Active Directory ao cluster de Big Data do SQL Server](troubleshoot-active-directory.md)

[Conceito: implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no modo do Active Directory](active-directory-deployment-background.md)

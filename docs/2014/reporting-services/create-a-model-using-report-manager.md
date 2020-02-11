---
title: Criar um modelo usando Report Manager | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report models [Reporting Services], creating
- Report Manager [Reporting Services], model creation
ms.assetid: 8e5d2bd3-48ec-45f3-afee-6d86797c8f28
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 7b67e2a7048520d8a411789e501dbbe545d3cc02
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109668"
---
# <a name="create-a-model-using-report-manager"></a>Criar um modelo com o Gerenciador de Relatórios
  Você pode gerar modelos de um cubo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , um banco de dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou um banco de dados Oracle usando o Gerenciador de Relatórios. Os modelos de relatório são gerados a partir de fontes de dados compartilhadas que são publicadas no servidor de relatório. Se você ainda não tiver uma fonte de dados compartilhada, é preciso criar uma.  
  
 O modelo de relatório que você gera se baseia totalmente no esquema de fonte de dados compartilhados. Não é possível escolher quais partes da fonte de dados são incluídas no modelo, nem é possível editar as regras ou metadados de um modelo gerado. Entretanto, você pode definir propriedades no modelo após ele ser gerado e definir atribuições de funções que restringem o acesso à parte ou a todo o modelo.  
  
> [!NOTE]  
>  Um modelo baseado em Oracle gerado usando Report Manager ou [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[offSPServ](../includes/offspserv-md.md)] 2007 [!INCLUDE[SPS2010](../includes/sps2010-md.md)] incluirá objetos de banco de dados que fazem parte do esquema para a conta de usuário usada para conectar-se à fonte do Oracle Data. O nome de conta de usuário é especificado nas credenciais de propriedades de fonte de dados.  
  
### <a name="to-create-a-new-data-source-for-a-report-model-using-report-manager"></a>Para criar uma nova fonte de dados para um modelo de relatório que usa o Gerenciador de Relatórios  
  
1.  No navegador da Web, digite a URL do servidor de relatório na barra de endereços.  
  
2.  Clique em **Nova Fonte de Dados**.  
  
3.  Na caixa **Nome** , digite um nome para a fonte de dados.  
  
4.  Opcionalmente, digite uma breve descrição do modo na caixa de texto **Descrição** .  
  
5.  Verifique se a caixa de seleção **Habilitar esta fonte de dados** está selecionada.  
  
6.  Na lista **Tipo de conexão** , selecione o tipo de fonte de dados para o qual você deseja se conectar. O tipo de conexão deve ser um dos seguintes: **Oracle**, **Microsoft SQL Server** ou **Microsoft SQL Server Analysis Services**.  
  
7.  Na caixa **Cadeia de conexão** , digite a cadeia de conexão que aponta para o banco de dados.  
  
8.  Selecione o método de conexão que os usuários do Construtor de Relatórios necessitarão usar para se conectar ao banco de dados.  
  
    -   Autenticação do Windows: Selecione esta opção quando desejar que o sistema operacional autentique os usuários [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Esta opção permite [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usar os recursos de segurança do Windows como a criptografia de senha para autenticar os usuários. É altamente recomendado que você selecione essa opção.  
  
    -   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]Autenticação: Selecione esta opção quando desejar que os usuários usem uma [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] conta de logon que você criou. Os usuários devem fornecer um nome de logon e senha válidos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
        > [!CAUTION]  
        >  Sempre que for possível, use a Autenticação do Windows.  
  
9. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-create-a-report-model-using-report-manager"></a>Para criar um modelo de relatório usando o Gerenciador de Relatórios  
  
1.  No Gerenciador de Relatórios, selecione a fonte de dados que você deseja usar em seu modelo.  
  
     A página Propriedades é exibida.  
  
2.  Verifique se você deseja usar as opções especificadas para a fonte de dados.  
  
3.  Clique em **Gerar Modelo**.  
  
     A página Geral é exibida para a fonte de dados.  
  
4.  Na caixa **Nome** , digite um nome para o modelo de relatório.  
  
5.  Na caixa **Descrição** , digite uma breve descrição do modelo.  
  
6.  Para especificar um novo local para salvar o modelo de relatório, clique em **Alterar Local**.  
  
     Por padrão, o modelo de relatório é salvo na página inicial do Gerenciador de Relatórios.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     O modelo de relatório é criado e salvo no local por você especificado. Você pode atribuir permissões a este modelo usando o Gerenciador de Relatórios.  
  
## <a name="see-also"></a>Consulte Também  
 [Concedendo permissões em um servidor de relatório no modo nativo](security/granting-permissions-on-a-native-mode-report-server.md)   
 [Conexões de dados, fontes de dados e cadeias de conexão no Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Nova página de fonte de dados &#40;Report Manager&#41;](../../2014/reporting-services/new-data-source-page-report-manager.md)  
  
  

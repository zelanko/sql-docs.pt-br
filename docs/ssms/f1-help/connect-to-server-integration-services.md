---
title: Conectar ao servidor (Integration Services) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.connection.login.dtsserver.f1
ms.assetid: 5be897bd-f36c-4c6a-a91a-13d0d016f8b6
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 4d7f292d113fb3d9bc8197f7be3134524e8116af
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="connect-to-server-integration-services"></a>Conectar ao servidor (Integration Services)
Use essa caixa de diálogo para exibir ou especificar opções ao se conectar com o [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion_md.md)].  
  
## <a name="options"></a>Opções  
**Tipo de servidor**  
Ao registrar um servidor a partir do Pesquisador de Objetos, selecione o tipo de servidor ao qual se conectar: [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services ou Integration Services. O restante da caixa de diálogo mostra somente as opções que válidas ao tipo de servidor selecionado. Quando é registrado um servidor dos Servidores Registrados, a caixa Tipo de servidor é somente leitura e corresponde ao tipo de servidor exibido no componente Servidores Registrados. Para registrar outro tipo de servidor, selecione [!INCLUDE[ssDE](../../includes/ssde_md.md)], Analysis Services, Reporting Services ou Integration Services na barra de ferramentas Servidores Registrados antes de iniciar o registro de um novo servidor.  
  
**Nome do servidor**  
Selecione o servidor ao qual conectar-se. Por padrão, é exibida a instância de servidor usada na última conexão.  
  
> [!NOTE]  
> Não use *<servername>*\\*<instancename>*, porque o [!INCLUDE[ssIS](../../includes/ssis_md.md)] não dá suporte a diversas instâncias em um computador.  
  
**Autenticação**  
Somente a Autenticação do [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows está disponível para o [!INCLUDE[ssIS](../../includes/ssis_md.md)]. O modo de Autenticação do Windows permite que um usuário se conecte por uma conta de usuário Windows.  
  
**Nome de usuário**  
Essa opção não está disponível porque só a Autenticação do Windows está disponível para o [!INCLUDE[ssIS](../../includes/ssis_md.md)].  
  
**Senha**  
Essa opção não está disponível porque só a Autenticação do Windows está disponível para o [!INCLUDE[ssIS](../../includes/ssis_md.md)].  
  
**Conectar**  
Clique para conectar-se com o servidor selecionado acima.  
  
**Opções**  
Clique para exibir opções de conexão de servidor adicionais, como registrar um servidor e lembrar a senha.  
  


---
title: Conectar ao Mecanismo de Banco de Dados do Servidor (página Logon) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connecttosqlserver.login.f1
ms.assetid: e08cfbc3-bed5-4401-a13b-1c66d902fe32
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b7f8c761a052bc3c82789087bb955c760e9a1b49
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37181233"
---
# <a name="connect-to-server-login-page-database-engine"></a>Conectar ao Servidor (página Logon) Mecanismo de Banco de Dados
  Use essa guia para exibir ou especificar opções ao se conectar ao [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
> [!NOTE]  
>  Para se conectar usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverá ser configurado no modo de Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows. Para obter mais informações sobre como determinar o modo de autenticação e para alterar o modo de autenticação, consulte [alterar o modo de autenticação de servidor](../../database-engine/configure-windows/change-server-authentication-mode.md).  
  
## <a name="options"></a>Opções  
 **Tipo de servidor**  
 Ao registrar um servidor a partir do Pesquisador de Objetos, selecione o tipo de servidor ao qual se conectar: [!INCLUDE[ssDE](../../includes/ssde-md.md)], Analysis Services, Reporting Services ou Integration Services. O restante da caixa de diálogo mostra somente as opções que se aplicam ao tipo de servidor selecionado. Ao registrar um servidor de Servidores Registrados, a caixa **Tipo de servidor** é somente leitura e corresponde ao tipo de servidor exibido no componente Servidores Registrados. Para registrar outro tipo de servidor, selecione [!INCLUDE[ssDE](../../includes/ssde-md.md)], Analysis Services, Reporting Services ou Integration Services na barra de ferramentas Servidores Registrados antes de iniciar o registro de um novo servidor.  
  
 Ao conectar-se a uma instância do Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], você deve usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e especificar um banco de dados na caixa de diálogo **Conectar ao Servidor** , na guia **Propriedades da Conexão** . Verifique se você marcou a caixa de seleção **Criptografar conexão** .  
  
 Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conecta-se ao **mestre**. Se você especificar um banco de dados de usuário, consultará somente esse banco de dados e seus objetos no Pesquisador de Objetos. Se você se conectar ao **mestre**, poderá ver todos os bancos de dados. Para obter mais informações, consulte [Visão geral do banco de dados SQL do Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=163948).  
  
 **Nome do servidor**  
 Selecione a instância do servidor com a qual se conectar. Por padrão, é exibida a instância de servidor usada na última conexão.  
  
 **Autenticação**  
 Dois modos de autenticação estão disponíveis quando se estabelece conexão com uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
 Ao conectar-se a uma instância do Mecanismo de Banco de Dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio do [!INCLUDE[ssSDS](../../includes/sssds-md.md)], você deve usar a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e especificar um banco de dados na caixa de diálogo **Conectar ao Servidor** , na guia **Propriedades da Conexão** . Verifique se você marcou a caixa de seleção **Criptografar conexão** .  
  
 Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conecta-se ao **mestre**. Se você especificar um banco de dados de usuário, consultará somente esse banco de dados e seus objetos no Pesquisador de Objetos. Se você se conectar ao **mestre**, poderá ver todos os bancos de dados. Para obter mais informações, consulte [Visão geral do banco de dados SQL do Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=163948).  
  
 **Modo de Autenticação do Windows (Autenticação do Windows)**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] O modo de Autenticação do Windows permite que um usuário se conecte por uma conta de usuário Windows.  
  
 **Autenticação do SQL Server**  
 Quando um usuário se conecta com um nome de logon e uma senha especificados em uma conexão não confiável, o próprio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] efetua a autenticação verificando se foi definida uma conta de logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e se a senha especificada corresponde a uma senha já registrada. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tiver uma conta de logon definida, ocorrerá falha na autenticação e o usuário receberá uma mensagem de erro.  
  
> [!IMPORTANT]  
>  Quando possível, use a Autenticação do Windows.  
  
 **Nome de usuário**  
 Digite o nome do usuário com o qual se conectar. Essa opção estará disponível somente se você decidiu conectar-se usando a Autenticação do Windows.  
  
 **Logon**  
 Insira o logon com o qual se conectar. Essa opção estará disponível somente se você decidiu conectar-se usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Senha**  
 Digite a senha do logon. Essa opção poderá ser editada somente se você decidiu conectar-se usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Lembrar senha**  
 Clique para que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] armazene a senha que você digitou. Essa opção só será exibida se você tiver optado por conectar-se usando a autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Conectar**  
 Clique para conectar-se com o servidor selecionado acima.  
  
 **Opções**  
 Clique para alterar a caixa de diálogo e ocultar as opções de conexão de servidor adicionais, como lembrar a senha.  
  
  

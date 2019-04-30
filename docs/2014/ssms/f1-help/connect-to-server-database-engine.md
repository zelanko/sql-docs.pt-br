---
title: Conectar ao Servidor (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.connectoserverunknownservertype.f1
- sql12.swb.connection.login.sqlserver.f1
- sql12.swb.connection.login.sqlce.f1
- sql12.swb.manageSS2k.f1
- sql12.swb.connecttoce.f1
- sql12.swb.connecttoce.connectionproperties.f1
ms.assetid: ee9017b4-8a19-4360-9003-9e6484082d41
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 018ca302bf4d5fe8271369008ffbfec7d228cfbf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63245737"
---
# <a name="connect-to-server-database-engine"></a>Conectar ao Servidor (Mecanismo de Banco de Dados)
  Use essa caixa de diálogo para exibir ou especificar opções ao se conectar com o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. Na maioria das vezes, é possível conectar-se informando o nome do computador do servidor de banco de dados na caixa **Nome do servidor** e clicando em **Conectar**. Se você estiver se conectando ao [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], use o nome do computador seguido por **\sqlexpress**.  
  
 Muitos fatores podem afetar sua possibilidade de conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="options"></a>Opções  
 **Tipo de servidor**  
 Ao registrar um servidor a partir do Pesquisador de Objetos, selecione o tipo de servidor ao qual se conectar: [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]ou [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. O restante da caixa de diálogo mostra somente as opções que válidas ao tipo de servidor selecionado. Ao registrar um servidor de Servidores Registrados, a caixa **Tipo de servidor** é somente leitura e corresponde ao tipo de servidor exibido no componente Servidores Registrados. Para registrar um tipo diferente de servidor, selecione [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssEW](../../includes/ssew-md.md)]ou [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] na barra de ferramentas Servidores Registrados antes de começar a registrar um novo servidor.  
  
 **Nome do servidor**  
 Selecione a instância do servidor com a qual se conectar. Por padrão, é exibida a instância de servidor usada na última conexão.  
  
> [!NOTE]  
>  Para se conectar a uma instância de usuário ativa do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , conecte-se usando o protocolo de pipes nomeados especificando o nome do pipe, por exemplo, np:\\\\.\pipe\3C3DF6B1-2262-47\tsql\query. Para obter mais informações, consulte a documentação do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] .  
  
 **Autenticação**  
 Existem dois modos de autenticação disponíveis quando se estabelece conexão com uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
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
  
 **Connect**  
 Clique para conectar-se com o servidor selecionado acima.  
  
 **Opções**  
 Clique para exibir opções de conexão de servidor adicionais, como registrar um servidor e lembrar a senha.  
  
  

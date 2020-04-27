---
title: Criar ou excluir um alias de servidor para uso por um cliente (SQL Server Configuration Manager) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- server alias
helpviewer_keywords:
- aliases [SQL Server], deleting
- aliases [SQL Server], creating
ms.assetid: b687e376-ee33-470d-b65a-87246bfefe6f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 20c8ef211fe32d1459704c963c525a6cc9235d4a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62810656"
---
# <a name="create-or-delete-a-server-alias-for-use-by-a-client-sql-server-configuration-manager"></a>Criar ou excluir um alias de servidor para ser usado por um cliente (SQL Server Configuration Manager)
  Este tópico descreve como criar ou excluir um alias de servidor no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o SQL Server Configuration Manager. O alias é um nome alternativo que pode ser usado para fazer uma conexão. Ele encapsula os elementos necessários de uma cadeia de conexão, expondo-os com um nome escolhido pelo usuário. Aliases podem ser usados com qualquer aplicativo cliente. Criando aliases de servidor, seu computador cliente pode se conectar a vários servidores usando protocolos de rede diferentes, sem a necessidade de especificar o protocolo e os detalhes da conexão para cada um deles. Além disso, você também poderá ter diferentes protocolos de rede habilitados o tempo todo, mesmo se precisar usá-los apenas ocasionalmente. Se você configurou o servidor para escutar em um pipe nomeado ou número de porta que não seja padrão e desabilitou o serviço SQL Server Browser, crie um alias que especifique o novo pipe nomeado ou o número de porta.  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### <a name="to-create-an-alias"></a>Criar um alias  
  
1.  No SQL Server Configuration Manager, expanda **Configuração do SQL Server Native Client**, clique com o botão direito do mouse em **Aliases**e clique em **Novo Alias**.  
  
2.  Na caixa **Nome do Alias** , digite o nome do alias. Os aplicativos cliente usam este nome quando se conectam.  
  
3.  Na caixa **Servidor** , digite o nome ou o endereço IP de um servidor. Para uma instância nomeada, acrescente o nome da instância.  
  
4.  Na caixa **Protocolo** , selecione o protocolo usado para este alias. A seleção de um protocolo altera o título da caixa de propriedades opcional para Número da Porta, Nome do Pipe ou Cadeia de Conexão.  
  
 As cadeias de conexão descritas na Ajuda do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager podem ser úteis para programadores que criam suas próprias cadeias de conexão. Para acessar estas informações, na caixa de diálogo **Novo Alias** , pressione F1 ou clique em **Ajuda**.  
  
> [!NOTE]  
>  Se um alias configurado estiver se conectando ao servidor ou à instância incorreta, desabilite e habilite novamente o protocolo de rede associado. Fazendo isso, você limpa todas as informações de conexão em cache e permite que o cliente se conecte corretamente.  
  
#### <a name="to-delete-an-alias"></a>Para excluir um alias  
  
1.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, expanda **Configuração do SQL Server Native Client**e clique em **Aliases**.  
  
2.  No painel de detalhes, clique com o botão direito do mouse no alias que você deseja excluir e clique em **Excluir**.  
  
  

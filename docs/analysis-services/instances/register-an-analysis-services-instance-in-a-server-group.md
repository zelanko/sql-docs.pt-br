---
title: Registrar uma instância do Analysis Services em um grupo de servidores | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 45edecf23d0db4580aad134780ee31ea938e887c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62709004"
---
# <a name="register-an-analysis-services-instance-in-a-server-group"></a>Registrar uma instância do Analysis Services em um grupo de servidores
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Se houver um grande número de instâncias de servidor do Analysis Services, você poderá criar grupos de servidores no Management Studio para facilitar a administração de servidor. O propósito de um grupo de servidores é fornecer proximidade entre um grupo de servidores relacionados dentro do workspace administrativo. Por exemplo, vamos supor que você receba a tarefa de gerenciar dez instâncias separadas do Analysis Services. Agrupá-los por modo de servidor, critérios de tempo de atividade ou por departamento ou região permitiria a você exibir e se conectar a instâncias que compartilham as mesmas características com mais facilidade. Também é possível adicionar informações descritivas que ajudam você a se lembrar de como o servidor é usado.  
  
 ![Painel do servidor registrado com servidores de membro](../../analysis-services/instances/media/ssas-ssms-registerserver.gif "painel servidor registrado com servidores de membro")  
  
 É possível criar grupos de servidores em uma estrutura hierárquica. O Grupo de Servidores Local é o nó raiz. Ele sempre contém instâncias do Analysis Services executadas no computador local. Você pode adicionar servidores remotos a qualquer grupo, inclusive o grupo local.  
  
 Depois que criar um grupo de servidores, você deverá usar o painel Servidores Registrados para exibir e se conectar aos servidores membro. O painel filtra instâncias do SQL Server por tipo de servidor (Mecanismo de Banco de Dados, Analysis Services, Reporting Services e Integration Services). Clique em um tipo de servidor para exibir os grupos de servidores criados para ele. Para se conectar a um servidor específico no grupo, clique duas vezes em um servidor no grupo.  
  
 As informações de conexão definidas para o servidor, inclusive o nome do servidor, são mantidas com o registro de servidor. Não é possível modificar as informações de conexão, nem usar o nome registrado ao se conectar ao servidor usando outras ferramentas.  
  
## <a name="create-a-server-group-and-add-registered-servers"></a>Criar um grupo de servidores e adicionar servidores registrados  
  
1.  No Management Studio, clique em Servidores Registrados no menu Exibir para abrir o painel Servidores Registrados no workspace. Por padrão, um Grupo de Servidores local já está criado. Todas as instâncias do Analysis Services em execução no servidor local são membros.  
  
2.  Clique com o botão direito do mouse no Grupo de Servidores Local, selecione Novo Grupo de Servidores e dê um nome ao grupo.  
  
3.  Clique com o botão direito do mouse no grupo de servidores e selecione Novo Registro de Servidor. Insira o nome de rede de um servidor local ou remoto, incluindo o nome de instância se o servidor foi instalado como uma instância nomeada. Opcionalmente, você pode fornecer um nome de servidor registrado que aparece em Servidores Registrados. Esse nome é usado apenas em Servidores Registrados. Você não pode usá-lo para renomear um servidor, nem em uma cadeia de conexão. Um nome de servidor registrado pode ser mais descritivo do que o nome de servidor real ou pode incluir outras características de identificação que o ajudem a distinguir esse servidor dos demais.  
  
  

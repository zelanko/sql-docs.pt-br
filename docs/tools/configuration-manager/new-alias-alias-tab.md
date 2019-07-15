---
title: Novo Alias (guia Alias) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 785eb6fb-f67e-449d-b1c8-c38dfbb95ef6
author: markingmyname
ms.author: maghan
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: 6d7dddd07463e16d0fe85d4feba4a9a347435854
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67732634"
---
# <a name="new-alias-alias-tab"></a>Novo Alias (guia Alias)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  O alias é um nome alternativo que pode ser usado para fazer uma conexão. Ele encapsula os elementos necessários de uma cadeia de conexão, expondo-os com um nome escolhido pelo usuário. Use a página **Alias** na caixa de diálogo **Alias - Novo** para especificar os elementos da cadeia de conexão de um alias. Para alterar a cadeia de conexão de um alias existente, consulte [Propriedades &#60;Alias&#62; &#40;Guia Alias&#41;](../../tools/configuration-manager/alias-properties-alias-tab.md).  
  
 Os valores da grade **Propriedades** não precisam ser completados. As combinações válidas variam, dependendo do protocolo selecionado. Consulte os tópicos listados abaixo para obter exemplos de combinações válidas.  
  
 **Nome do Alias**  
 O nome (alias) que você deseja usar para se referir a essa conexão.  
  
 **Nome do Pipe** / **Número da Porta**  
 Elementos adicionais da cadeia de conexão. O nome desta caixa varia de acordo com o protocolo selecionado.  
  
 **Protocolo**  
 O protocolo usado para a conexão.  
  
 **Servidor**  
 O nome da instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo conectada.  
  
## <a name="when-to-use-an-alias"></a>Quando usar um alias  
 Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecta a uma instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o protocolo **Memória Compartilhada** , e se conecta a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em outro computador usando **TCP/IP** ou **Pipes Nomeados**. Crie um alias quando estiver usando TCP/IP ou pipes nomeados e quiser fornecer uma cadeia de conexão personalizada, ou quando desejar usar um nome diferente do nome do servidor para a conexão.  
  
### <a name="examples"></a>Exemplos  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não está escutando na porta TCP/IP padrão 1433, então você deseja fornecer uma cadeia de conexão com um número da porta diferente.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não está escutando no pipe nomeado padrão, então você deseja fornecer uma cadeia de conexão com um nome de pipe diferente.  
  
-   Um aplicativo espera se conectar a um banco de dados no servidor `ACCT`, mas esse banco de dados foi consolidado como uma instância chamada `ACCT` em um servidor chamado `CENTRAL`. O aplicativo não pode ser alterado facilmente. Crie um alias chamado `ACCT`, com uma cadeia de conexão que aponte para `CENTRAL\ACCT`.  
  
## <a name="creating-a-valid-connection-string"></a>Criando uma cadeia de conexão válida  
 Consulte os seguintes tópicos para obter uma descrição e exemplos de combinações válidas de propriedades de alias:  
  
-   [Criando uma cadeia de conexão válida usando o protocolo de memória compartilhada](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)  
  
-   [Criando uma cadeia de conexão válida usando TCP/IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)  
  
-   [Criando uma cadeia de conexão válida usando pipes nomeados](https://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)  
  
  

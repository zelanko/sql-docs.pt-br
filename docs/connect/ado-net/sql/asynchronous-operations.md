---
title: Operações assíncronas
description: Descreve como executar operações de banco de dados assíncronas usando uma API que é modelada após o modelo assíncrono usado pelo .NET Framework.
ms.date: 09/30/2019
ms.assetid: e7d32c3c-bf78-4bfc-a357-c9e82e4a4b3c
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: 3923db97ce144662f7fe5410c13278862d1ab6a1
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725674"
---
# <a name="asynchronous-operations"></a>Operações assíncronas

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Algumas operações de banco de dados, como execuções de comando, podem demorar significativamente para serem concluídas. Nesses casos, os aplicativos de thread único devem bloquear outras operações e aguardar a conclusão do comando antes de poderem continuar suas próprias operações. Por outro lado, poder atribuir a operação demorada a um thread em segundo plano permite que o thread de primeiro plano permaneça ativo durante toda a operação. Em um aplicativo do Windows, por exemplo, delegar a operação demorada para um thread em segundo plano permite que o thread de interface do usuário permaneça responsivo enquanto a operação está em execução.  
  
O .NET fornece vários projetos de design assíncrono padrão que os desenvolvedores podem usar para aproveitar os threads em segundo plano e liberar a interface do usuário ou os threads de alta prioridade para concluir outras operações em sua classe <xref:Microsoft.Data.SqlClient.SqlCommand>. Especificamente, os métodos <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A>, <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A> e <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A>, emparelhados com os métodos <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteNonQuery%2A>, <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteReader%2A> e <xref:Microsoft.Data.SqlClient.SqlCommand.EndExecuteXmlReader%2A>, fornecem o suporte assíncrono.  
  
> [!NOTE]
>  A programação assíncrona é um recurso fundamental do .NET. Para obter mais informações sobre as diferentes técnicas assíncronas disponíveis para os desenvolvedores, confira [Chamar métodos síncronos de forma assíncrona](/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously).  
  
Embora o uso de técnicas assíncronas com recursos do ADO.NET não inclua nenhuma consideração especial, é importante estar ciente dos benefícios e das armadilhas da criação de aplicativos multithread. Os exemplos a seguir nesta seção apontam vários problemas importantes que os desenvolvedores precisarão levar em consideração ao criar aplicativos que incorporam a funcionalidade multithread.  
  
## <a name="in-this-section"></a>Nesta seção  
[Aplicativos do Windows usando retornos de chamada](windows-applications-callbacks.md)  
Fornece um exemplo que demonstra como executar um comando assíncrono com segurança, manipulando corretamente a interação com um formulário e seu conteúdo de um thread separado.  
  
[Aplicativos ASP.NET usando identificadores de espera](aspnet-apps-use-wait-handles.md)  
Fornece um exemplo que demonstra como executar vários comandos simultâneos de uma página do ASP.NET, usando os identificadores de espera para gerenciar a operação na conclusão de todos os comandos.  
  
[Sondagem em aplicativos de console](poll-console-applications.md)  
Fornece um exemplo que demonstra o uso de sondagem para aguardar a conclusão de uma execução de comando assíncrona de um aplicativo de console. Essa técnica também é válida em uma biblioteca de classes ou outro aplicativo sem uma interface do usuário.  
  
## <a name="next-steps"></a>Próximas etapas
- [SQL Server e ADO.NET](index.md)
- [Chamar métodos síncronos de forma assíncrona](/dotnet/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously)
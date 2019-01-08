---
title: Criando programas SMO | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual Basic [SMO]
- Visual C# [SMO]
- programming [SMO]
- SQL Server Management Objects, programming
- SMO [SQL Server], programming
ms.assetid: 7d2f0bcf-f1ae-45b8-bc3f-7aea4fae7e45
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ccf26cf30c53e3a336e842cbbffc1ff517075fef
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52807838"
---
# <a name="creating-smo-programs"></a>Criando programas SMO
  A programação geral de objetos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO) inclui as áreas comuns compartilhadas por todos os objetos, como a execução de métodos, a configuração de propriedades e a manipulação de coleções.  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Conectando-se a uma instância do SQL Server](connecting-to-an-instance-of-sql-server.md)|O programa SMO mais básico que estabelece uma conexão com uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Demonstra a Autenticação do Windows e a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Também inclui exemplos que mostram a conexão com um local e uma instância remota do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Desconectando de uma instância do SQL Server](disconnecting-from-an-instance-of-sql-server.md)|Um programa que demonstra como se desconectar da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Chamando métodos](calling-methods.md)|Esta seção descreve a abordagem geral de chamada de métodos. Mostra o uso de parâmetros e como tratar tabelas de dados retornadas em um objeto <xref:System.Data.DataTable>. Também inclui um exemplo de como chamar um construtor de objeto e como chamar o método `Clone`.|  
|[Definindo propriedades](setting-properties-smo.md)|Esta seção descreve como definir diferentes tipos de propriedades. Mostra como definir e obter propriedades de objetos. Também inclui exemplos que definem propriedades de objetos quando o objeto é criado e como iterar por todas as propriedades de um objeto.|  
|[Usando coleções](using-collections.md)|Vários programas que discutem as técnicas usadas com coleções de objetos. Mostra como referenciar um objeto usando coleções. Também inclui um exemplo de como iterar pelos membros de uma coleção.|  
|[Manipulando eventos SMO](handling-smo-events.md)|Esta seção descreve como configurar e tratar eventos no SMO. Inclui um exemplo de como configurar um manipulador de eventos e como configurar uma assinatura de evento.|  
|[Manipulando exceções SMO](handling-smo-exceptions.md)|Esta seção descreve como interceptar exceções no SMO. Inclui exemplos de como capturar uma exceção e como exibir uma exceção interna.|  
|[Trabalhando com tipos de dados](working-with-data-types.md)|Esta seção descreve como trabalhar com diferentes tipos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Descreve como construir um tipo de dados com a especificação do construtor de objeto. Também inclui um exemplo de como criar um tipo de dados usando o construtor padrão.|  
|[Usando transações](using-transactions.md)|Esta seção descreve como implementar o processamento de transações em um programa SMO. Inclui um exemplo de como usar transações em um programa SMO.|  
|[Usando modo de captura](using-capture-mode.md)|Esta seção descreve como registrar a saída do programa SMO. O exemplo registra o programa SMO como instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] enviadas à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para execução posterior.|  
  
  

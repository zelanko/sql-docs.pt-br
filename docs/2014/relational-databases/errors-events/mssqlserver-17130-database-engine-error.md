---
title: MSSQLSERVER_17130 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 17130 (Database Engine error)
ms.assetid: 7ce6afca-221d-402f-89df-da7e74a339a8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4f8d62a98d39a65db78f79fdfaf3ecdb2921408e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62915368"
---
# <a name="mssqlserver_17130"></a>MSSQLSERVER_17130
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|17130|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|INIT_NOLOCKSPACE|  
|Texto da mensagem|Não há memória suficiente para o número de bloqueios configurado. Tente começar com uma tabela de hash de bloqueio menor, que pode causar impacto no desempenho. Contate o administrador de banco de dados para configurar mais memória para a instância do Mecanismo de Banco de Dados.|  
  
## <a name="explanation"></a>Explicação  
 Não há memória suficiente para o tamanho da tabela de hash do gerenciador de bloqueios desejado.  Ocorrerá uma tentativa para alocar uma tabela de hash menor.  
  
## <a name="user-action"></a>Ação do usuário  
 Verifique os parâmetros de configuração da memória do servidor (min/max server memory) e verifique se há pressões de memória. Forneça mais memória ao SQL Server.  
  
  

---
title: MSSQLSERVER_17130 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 17130 (Database Engine error)
ms.assetid: 7ce6afca-221d-402f-89df-da7e74a339a8
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: bbf8c071d0f64b4fe09322179c7d71c538d9d6e7
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver17130"></a>MSSQLSERVER_17130
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|17130|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|INIT_NOLOCKSPACE|  
|Texto da mensagem|Não há memória suficiente para o número de bloqueios configurado. Tente começar com uma tabela de hash de bloqueio menor, que pode causar impacto no desempenho. Contate o administrador de banco de dados para configurar mais memória para a instância do Mecanismo de Banco de Dados.|  
  
## <a name="explanation"></a>Explicação  
Não há memória suficiente para o tamanho da tabela de hash do gerenciador de bloqueios desejado.  Ocorrerá uma tentativa para alocar uma tabela de hash menor.  
  
## <a name="user-action"></a>Ação do usuário  
Verifique os parâmetros de configuração da memória do servidor (min/max server memory) e verifique se há pressões de memória. Forneça mais memória ao SQL Server.  
  


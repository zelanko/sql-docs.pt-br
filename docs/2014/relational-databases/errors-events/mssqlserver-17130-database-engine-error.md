---
title: MSSQLSERVER_17130 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 17130 (Database Engine error)
ms.assetid: 7ce6afca-221d-402f-89df-da7e74a339a8
caps.latest.revision: 16
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e4f8a2414ef1d1aba309bdbaffdbcce1d6494a87
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36007937"
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
  
  
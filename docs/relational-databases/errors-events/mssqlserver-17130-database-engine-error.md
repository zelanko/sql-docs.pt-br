---
description: MSSQLSERVER_17130
title: MSSQLSERVER_17130 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17130 (Database Engine error)
ms.assetid: 7ce6afca-221d-402f-89df-da7e74a339a8
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c60cada5e0f1172c927fdb4ef5ebd8c89e719a33
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499519"
---
# <a name="mssqlserver_17130"></a>MSSQLSERVER_17130
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
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
  

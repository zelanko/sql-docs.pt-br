---
title: Parâmetros de conexão | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server], connections
- authentication [Upgrade Advisor]
- SQL Server Upgrade Advisor, connections
- connections [Upgrade Advisor]
- server instances [Upgrade Advisor]
- default server instances
- analyzing system [Upgrade Advisor], connections
ms.assetid: f754d038-637a-4d8e-85b0-b242e6499d26
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ca5d6ed8f1e8a92d22bd32e39c8afe946a0fcfee
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66095974"
---
# <a name="connection-parameters"></a>Parâmetros de conexão
  Para analisar certos tipos de servidor, como o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], você deve selecionar uma instância específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é selecionada automaticamente. Você pode alterar essa seleção, mas pode selecionar somente uma instância de cada vez para análise pelo Supervisor de Atualização. Se você incluiu um tipo de servidor que requer autenticação, deve indicar o modo de autenticação e as credenciais.  
  
## <a name="options"></a>Opções  
 **Nome do servidor**  
 Pré-populado com o nome do computador digitado no painel Componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Nome da instância**  
 Selecione uma das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponíveis no computador. Se você não vir uma lista de instâncias, use MSSQLSERVER para verificar a instância padrão. Isso é especialmente relevante para computadores remotos. Você também pode usar a palavra ‘default’ para verificar a instância padrão.  
  
 **Autenticação**  
 Selecione um método na lista de modos de autenticação disponíveis neste computador. Por padrão, o modo de autenticação é a Autenticação do Windows.  
  
 **Nome de usuário**  
 Se estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], digite o nome de usuário na caixa. Recomendamos que o nome de usuário tenha credenciais administrativas neste computador.  
  
> [!NOTE]  
>  Se você selecionar Autenticação do Windows, o nome de usuário do usuário conectado no momento será preenchido na caixa de texto **nome de usuário** .  
  
 **Senha**  
 Digite a senha para o usuário especificado.  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhando com o supervisor de atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Referência da interface de usuário do Supervisor de Atualização](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  

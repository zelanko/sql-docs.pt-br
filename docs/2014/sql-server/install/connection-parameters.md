---
title: Parâmetros de Conexão | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
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
ms.openlocfilehash: b5259f12613a67d94f704d9c6d170e09f2ee5f17
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48125386"
---
# <a name="connection-parameters"></a>Parâmetros de conexão
  Para analisar certos tipos de servidor, como o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], você deve selecionar uma instância específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é selecionada automaticamente. Você pode alterar essa seleção, mas pode selecionar somente uma instância de cada vez para análise pelo Supervisor de Atualização. Se você incluiu um tipo de servidor que requer autenticação, deve indicar o modo de autenticação e as credenciais.  
  
## <a name="options"></a>Opções  
 **Nome do servidor**  
 Pré-populado com o nome do computador digitado no painel Componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **nome da instância**  
 Selecione uma das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] disponíveis no computador. Se você não vir uma lista de instâncias, use o MSSQLSERVER para verificar a instância padrão. Isso é especialmente relevante para computadores remotos. Você também pode usar a palavra ‘default’ para verificar a instância padrão.  
  
 **Autenticação**  
 Selecione um método na lista de modos de autenticação disponíveis neste computador. Por padrão, o modo de autenticação é a Autenticação do Windows.  
  
 **Nome de usuário**  
 Se estiver usando a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], digite o nome de usuário na caixa. Recomendamos que o nome de usuário tenha credenciais administrativas neste computador.  
  
> [!NOTE]  
>  Se você selecionar a autenticação do Windows, o nome de usuário do usuário conectado no momento é preenchido na **nome de usuário** caixa de texto.  
  
 **Senha**  
 Digite a senha para o usuário especificado.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com o Supervisor de atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Referência de Interface de usuário do Supervisor de atualização](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  

---
title: Parâmetros de Conexão | Microsoft Docs
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
- Upgrade Advisor [SQL Server], connections
- authentication [Upgrade Advisor]
- SQL Server Upgrade Advisor, connections
- connections [Upgrade Advisor]
- server instances [Upgrade Advisor]
- default server instances
- analyzing system [Upgrade Advisor], connections
ms.assetid: f754d038-637a-4d8e-85b0-b242e6499d26
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: dc99f9fc26f0e46f0f5ea0d717614bf5935f4814
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36121208"
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
>  Se você selecionar a autenticação do Windows, o nome de usuário do usuário conectado no momento é populado no **nome de usuário** caixa de texto.  
  
 **Senha**  
 Digite a senha para o usuário especificado.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com o Supervisor de atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Referência de Interface de usuário do Supervisor de atualização](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
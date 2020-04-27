---
title: MSSQLSERVER_33028 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 33028 (Database Engine error)
ms.assetid: c5cec0e4-0bcd-4907-826f-e7d835cfcb37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 89f02cfd7ab2116528adb82d6e98023c912c6437
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62868659"
---
# <a name="mssqlserver_33028"></a>MSSQLSERVER_33028
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|33028|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SEC_CRYPTOPROV_CANTOPENSESSION|  
|Texto da mensagem|Não é possível abrir a sessão para %S_MSG '%.*ls'. Código de erro do provedor: %d.|  
  
## <a name="explanation"></a>Explicação  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pôde abrir o provedor criptográfico listado na mensagem de erro. O provedor criptográfico forneceu o código de erro listado. Você talvez precise contatar seu provedor criptográfico para obter mais informações sobre o erro.  
  
|Código do erro|DESCRIÇÃO|  
|----------------|-----------------|  
|0|Sucesso. Nenhum erro.|  
|1|Falha. Ocorreu um erro não especificado ou inesperado. Não há informações adicionais disponíveis.|  
|2|Buffer insuficiente. Não foi possível alocar espaço para o provedor criptográfico.|  
|3|Sem suporte. Não há suporte para o provedor criptográfico nesta versão. Selecione outro provedor criptográfico.|  
|4|Não encontrado. O provedor criptográfico especificado não está presente ou você não tem autorização para acessar os arquivos.|  
|5|Falha de autorização. Talvez uma senha ou um nome de usuário incorreto tenha sido fornecido durante a criação da credencial. Pode ocorrer quando a credencial não existe.|  
|6|Argumento inválido. Um argumento inválido foi passado ao provedor criptográfico.|  
  
## <a name="user-action"></a>Ação do usuário  
 Resolva o erro ou contate o provedor criptográfico para obter mais informações.  
  
  

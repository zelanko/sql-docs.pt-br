---
title: MSSQLSERVER_33028 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 33028 (Database Engine error)
ms.assetid: c5cec0e4-0bcd-4907-826f-e7d835cfcb37
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ae11fbccaa4f577815e503d9a0dffaa34c7c04ed
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723609"
---
# <a name="mssqlserver_33028"></a>MSSQLSERVER_33028
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|33028|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SEC_CRYPTOPROV_CANTOPENSESSION|  
|Texto da mensagem|Não é possível abrir a sessão para %S_MSG '%.*ls'. Código de erro do provedor: %d.|  
  
## <a name="explanation"></a>Explicação  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pôde abrir o provedor criptográfico listado na mensagem de erro. O provedor criptográfico forneceu o código de erro listado. Você talvez precise contatar seu provedor criptográfico para obter mais informações sobre o erro.  
  
|Código do erro|Descrição|  
|--------------|---------------|  
|0|Sucesso. Nenhum erro.|  
|1|Falha. Ocorreu um erro não especificado ou inesperado. Não há informações adicionais disponíveis.|  
|2|Buffer insuficiente. Não foi possível alocar espaço para o provedor criptográfico.|  
|3|Sem suporte. Não há suporte para o provedor criptográfico nesta versão. Selecione outro provedor criptográfico.|  
|4|Não encontrado. O provedor criptográfico especificado não está presente ou você não tem autorização para acessar os arquivos.|  
|5|Falha de autorização. Talvez uma senha ou um nome de usuário incorreto tenha sido fornecido durante a criação da credencial. Pode ocorrer quando a credencial não existe.|  
|6|Argumento inválido. Um argumento inválido foi passado ao provedor criptográfico.|  
  
## <a name="user-action"></a>Ação do usuário  
Resolva o erro ou contate o provedor criptográfico para obter mais informações.  
  

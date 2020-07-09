---
title: MSSQLSERVER_17053 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17053 (Database Engine error)
ms.assetid: e0a01f3d-d0aa-4c38-8bcc-82e59de50512
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5d9eb240ffe26a91b59413468f54cf5b2376779e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85780922"
---
# <a name="mssqlserver_17053"></a>MSSQLSERVER_17053
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|17053|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|OS_ERROR|  
|Texto da mensagem|%ls: Erro %ls do sistema operacional encontrado.|  
  
## <a name="explanation"></a>Explicação  
Ocorreu um erro genérico do sistema operacional.  Não desmarque a informação resultante.  
  
## <a name="user-action"></a>Ação do usuário  
Normalmente, isso ocorre com algum outro erro e pode ser usado para ajudar a diagnosticar essa falha. Os exemplos podem incluir falhas em leituras ou gravações de dados ou em arquivos de log, operações de leitura/gravação no Registro ou outras falhas inesperadas da Win32API.  
  

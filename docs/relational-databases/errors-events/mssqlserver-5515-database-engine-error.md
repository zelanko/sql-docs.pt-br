---
title: MSSQLSERVER_5515 | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5515 (Database Engine error)
ms.assetid: ccd793bc-ba5d-4782-8d72-731fd01fc177
author: MashaMSFT
ms.author: mathoma
robots: noindex,nofollow
ms.openlocfilehash: a9456aed02e9e1a2566bf0281dacd07f435af44b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85728373"
---
# <a name="mssqlserver_5515"></a>MSSQLSERVER_5515
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|MSSQLSERVER|  
|ID do evento|5515|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|FS_OPEN_CONTAINER_FAILED|  
|Texto da mensagem|Diretório do contêiner ''%.*ls'' do arquivo de FILESTREAM não pode ser aberto. O sistema operacional retornou o código de status do Windows 0x%x.|  
  
## <a name="explanation"></a>Explicação  
O diretório do contêiner especificado para o arquivo de FILESTREAM não pode ser aberto.  
  
## <a name="user-action"></a>Ação do usuário  
Para saber a causa do erro, consulte o código de status específico do Windows.  
  

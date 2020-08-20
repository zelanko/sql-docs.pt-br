---
description: MSSQLSERVER_5515
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
ms.openlocfilehash: aecbc4ad6ee5c3f8a0ebcf596dca0a06392acedf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470886"
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
  

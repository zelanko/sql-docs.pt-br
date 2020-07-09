---
title: MSSQLSERVER_3417 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3417 (Database Engine error)
ms.assetid: 005829c8-cf57-4828-818a-bbe8ee2e00f0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9d246ea9033bac031da85fe4dddd968ebb9af07d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85723511"
---
# <a name="mssqlserver_3417"></a>MSSQLSERVER_3417
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|3417|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|REC_BADMASTER|  
|Texto da mensagem|Não é possível recuperar o banco de dados mestre. O SQL Server não pode ser executado. Restaure o banco de dados mestre usando um backup completo, repare-o ou recrie-o. Para obter mais informações sobre como recriar o banco de dados mestre, consulte os Manuais Online do SQL Server.|  
  
## <a name="explanation"></a>Explicação  
O SQL Server não pode iniciar o banco de dados **mestre**. Se o banco de dados **master** ou **tempdb** não puderem ficar online, o SQL Server não poderá ser executado. Esse erro normalmente é precedido por outros erros. Revise os logs de erros para encontrar a causa original.  
  
## <a name="user-action"></a>Ação do usuário  
Restaure o backup do banco de dados ou repare o banco de dados.  
  

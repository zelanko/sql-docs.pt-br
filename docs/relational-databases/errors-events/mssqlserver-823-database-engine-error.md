---
title: MSSQLSERVER – erro do mecanismo de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 823 (Database Engine error)
ms.assetid: 0d9fce3c-3772-46ce-a7a3-4f4988dc6cae
caps.latest.revision: 24
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 879077ad0440edb4b0f6d65c3087d309a8e225e7
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver---database-engine-error"></a>MSSQLSERVER – erro do mecanismo de banco de dados
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|823|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|B_HARDERR|  
|Texto da mensagem|O sistema operacional retornou o erro %ls para o SQL Server durante um %S_MSG no deslocamento %#016I64x do arquivo '%ls'. Additional messages in the SQL Server error log and system event log may provide more detail. Essa é uma condição de erro grave em nível de sistema que ameaça a integridade do banco de dados e deve ser corrigida imediatamente. Faça uma verificação completa da consistência do banco de dados (DBCC CHECKDB). Esse erro pode ter sido causado por vários fatores. Para obter mais informações, consulte os Manuais Online do SQL Server.|  
  
## <a name="explanation"></a>Explicação  
Falha de solicitação de leitura ou gravação do Windows. O código de erro retornado pelo Windows e o texto correspondente estão inseridos na mensagem. No caso de leitura, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] já terá tentado novamente a solicitação de leitura quatro vezes. Normalmente, esse erro se deve a um erro de hardware, mas pode ser causado pelo driver de dispositivo. Para obter mais informações sobre o erro 823, consulte [http://support.microsoft.com/kb/828339](http://support.microsoft.com/kb/828339). Para obter mais informações sobre erros de E/S, consulte [Microsoft SQL Server I/O Basics, Chapter 2](http://go.microsoft.com/fwlink/?LinkId=69370) (Noções básicas de E/S do Microsoft SQL Server, Capítulo 2).  
  
## <a name="user-action"></a>Ação do usuário  
Verifique se há mais informações no log de eventos do sistema. Entre em contato com o fabricante de hardware ou o Atendimento ao Cliente e o Suporte da Microsoft para determinar a causa e ação corretiva. Depois que o erro de hardware for corrigido, restaure todos os bancos de dados e execute o DBCC CHECKDB.  
  

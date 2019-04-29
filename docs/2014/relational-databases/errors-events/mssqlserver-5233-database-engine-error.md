---
title: MSSQLSERVER_5233 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5233 (Database Engine error)
ms.assetid: 7a855afa-2d3b-49b7-adef-197b99fc98b1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a54c45746ec786461135fb3f2a50f4753dbe2df5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62867900"
---
# <a name="mssqlserver5233"></a>MSSQLSERVER_5233
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|5233|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC4_INCORRECT_VALUE_IN_PAGE_HEADER_NO_METADATA|  
|Texto da mensagem|Erro de tabela: ID de unidade de alocação A_ID, página P_ID. Falha no teste (TEST). Os valores são VAL1 e VAL2.|  
  
## <a name="explanation"></a>Explicação  
A página *P_ID* não foi aprovada na auditoria devido a um dano no cabeçalho. A cadeia de caracteres em TEST informa o teste real não aprovado.  
  
### <a name="look-for-hardware-failure"></a>Procurar falhas de hardware  
Execute o diagnóstico de hardware e corrija quaisquer problemas. Examine também os logs do aplicativo e do sistema [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para verificar se o erro ocorreu devido a uma falha de hardware. Corrija quaisquer problemas relacionados a hardware existentes nos logs.  
  
Se você tiver problemas contínuos de danos aos dados, tente alternar diferentes componentes de hardware para isolar o problema. Verifique se o sistema não está com a gravação em cache habilitada no controlador de disco. Se você suspeitar que a gravação de caching seja o problema, contate o fornecedor do hardware.  
  
Finalmente, pode ser útil mudar para um sistema de hardware novo. Essa mudança pode incluir a reformatação de unidades de disco e a reinstalação do sistema operacional.  
  
### <a name="restore-from-backup"></a>Restaurar a partir de backup  
Se o problema não estiver relacionado ao hardware e se houver um backup limpo conhecido, restaure o banco de dados do backup.  
  
### <a name="run-dbcc-checkdb"></a>Executar DBCC CHECKDB  
Não aplicável. Esse erro não pode ser reparado. Se você não conseguir restaurar o banco de dados a partir de um backup, entre em contato com o Suporte e Atendimento ao Cliente Microsoft (CSS).  
  

---
title: MSSQLSERVER_7931 | Microsoft Docs
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
- 7931 (Database Engine error)
ms.assetid: 18e7a3dc-7d8a-41b9-8724-d2a8587b6903
caps.latest.revision: 15
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 8f255855f68304f50a6704a4dce84bdc1adbe16d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36008891"
---
# <a name="mssqlserver7931"></a>MSSQLSERVER_7931
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|SQL Server|  
|ID do evento|7931|  
|Origem do evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC2_FS_DOUBLE_ROWSET_ACTUAL_FACT|  
|Texto da mensagem|Erro de banco de dados: a ID de diretório de FILESTREAM F_ID de uma partição foi vista duas vezes.|  
  
## <a name="explanation"></a>Explicação  
 A mesma ID de partição de um diretório de Filestream foi encontrada nos metadados.  
  
## <a name="user-action"></a>Ação do usuário  
  
### <a name="look-for-hardware-failure"></a>Procurar falhas de hardware  
 Execute o diagnóstico de hardware e corrija quaisquer problemas. Examine também os logs do aplicativo e do sistema [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para verificar se o erro ocorreu devido a uma falha de hardware. Corrija quaisquer problemas relacionados a hardware existentes nos logs.  
  
 Se você tiver problemas contínuos de danos aos dados, tente alternar diferentes componentes de hardware para isolar o problema. Verifique se o sistema não está com a gravação em cache habilitada no controlador de disco. Se você suspeitar que a gravação de caching seja o problema, contate o fornecedor do hardware.  
  
 Finalmente, pode ser útil mudar para um sistema de hardware novo. Essa mudança pode incluir a reformatação de unidades de disco e a reinstalação do sistema operacional.  
  
### <a name="restore-from-backup"></a>Restaurar a partir de backup  
 Se o problema não estiver relacionado ao hardware e se houver um backup limpo conhecido, restaure o banco de dados do backup.  
  
### <a name="run-dbcc-checkdb"></a>Executar DBCC CHECKDB  
 Não aplicável. Não é possível corrigir esse erro automaticamente. Se você não conseguir restaurar o banco de dados com base em um backup, contate o CSS (Suporte e Atendimento ao Cliente) [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
  
---
title: MSSQLSERVER_7984 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7984 (Database Engine error)
ms.assetid: e3192f56-e4e2-41da-b132-65f1e7540b1a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1e7ee58e9db83f3382d3dcfb07707390fff6881e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767884"
---
# <a name="mssqlserver_7984"></a>MSSQLSERVER_7984
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|7984|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC2_PRE_CHECKS_BAD_PAGE_TYPE|  
|Texto da mensagem|Verificações prévias de tabela do sistema: ID do objeto O_ID. A página P_ID tem um tipo PAGETYPE inesperado. Instrução de verificação encerrada devido a um erro irreparável.|  
  
## <a name="explanation"></a>Explicação  
Uma página com um tipo diferente de DATA_PAGE foi encontrada no nível de dados do objeto especificado. Esse erro ocorre durante a primeira fase das verificações do comando DBCC CHECKDB. Nessa fase, DBCC CHECKDB executa verificações primitivas nas páginas de dados de tabelas base do sistema que são críticas.  
  
> [!NOTE]  
> Se forem encontrados erros nas tabelas do sistema, não será possível corrigi-los; por isso, o comando DBCC CHECKDB é encerrado imediatamente.  
  
## <a name="user-action"></a>Ação do usuário  
  
### <a name="look-for-hardware-failure"></a>Procurar falhas de hardware  
Execute o diagnóstico de hardware e corrija quaisquer problemas. Examine também os logs do aplicativo e do sistema [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para verificar se o erro ocorreu devido a uma falha de hardware. Corrija quaisquer problemas relacionados a hardware existentes nos logs.  
  
Se você tiver problemas contínuos de danos aos dados, tente alternar diferentes componentes de hardware para isolar o problema. Verifique se o sistema não está com a gravação em cache habilitada no controlador de disco. Se você suspeitar que a gravação de caching seja o problema, contate o fornecedor do hardware.  
  
Finalmente, pode ser útil mudar para um sistema de hardware novo. Essa mudança pode incluir a reformatação de unidades de disco e a reinstalação do sistema operacional.  
  
### <a name="restore-from-backup"></a>Restaurar a partir de backup  
Se o problema não estiver relacionado ao hardware e se houver um backup limpo conhecido, restaure o banco de dados do backup.  
  
### <a name="run-dbcc-checkdb"></a>Executar DBCC CHECKDB  
Não aplicável. Não é possível corrigir esse erro automaticamente. Se você não conseguir restaurar o banco de dados a partir de um backup, entre em contato com o Suporte e Atendimento ao Cliente [!INCLUDE[msCoName](../../includes/msconame-md.md)] (CSS).  
  

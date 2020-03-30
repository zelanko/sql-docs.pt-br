---
title: MSSQLSERVER_7987 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 7987 (Database Engine error)
ms.assetid: 314aebf1-6cdf-488d-a274-ce967fadb57b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d626c0dcf44bc0907516d78aefd54b3ec0bb608a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68007071"
---
# <a name="mssqlserver_7987"></a>MSSQLSERVER_7987
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|7987|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC2_PRE_CHECKS_CHAIN_LINKAGE_MISMATCH|  
|Texto da mensagem|Verificações prévias de tabela do sistema: a ID de objeto O_ID tem incompatibilidade de vínculos de cadeia. P_ID1 ->next = P_ID2, mas P_ID2 ->prev = P_ID3. Instrução de verificação encerrada devido a um erro irreparável.|  
  
## <a name="explanation"></a>Explicação  
A primeira fase de um DBCC CHECKDB envolve a execução de verificações primitivas nas páginas de dados das tabelas de sistema críticas. Se forem encontrados erros, não será possível corrigi-los; por isso, DBCC CHECKDB é encerrado imediatamente.  
  
O ponteiro de próxima página da página *P_ID1* aponta para a página *P_ID2*, no entanto, o ponteiro de página anterior da página *P_ID2* aponta para a página *P_ID3*, mas não retorna para a página *P_ID1* como deveria.  
  
## <a name="user-action"></a>Ação do usuário  
  
### <a name="look-for-hardware-failure"></a>Procurar falhas de hardware  
Execute o diagnóstico de hardware e corrija quaisquer problemas. Examine também os logs do aplicativo e do sistema [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para verificar se o erro ocorreu devido a uma falha de hardware. Corrija quaisquer problemas relacionados a hardware existentes nos logs.  
  
Se você tiver problemas contínuos de danos aos dados, tente alternar diferentes componentes de hardware para isolar o problema. Verifique se o sistema não está com a gravação em cache habilitada no controlador de disco. Se você suspeitar que a gravação de caching seja o problema, contate o fornecedor do hardware.  
  
Finalmente, pode ser útil mudar para um sistema de hardware novo. Essa mudança pode incluir a reformatação de unidades de disco e a reinstalação do sistema operacional.  
  
### <a name="restore-from-backup"></a>Restaurar a partir de backup  
Se o problema não estiver relacionado ao hardware e se houver um backup limpo conhecido, restaure o banco de dados do backup.  
  
### <a name="run-dbcc-checkdb"></a>Executar DBCC CHECKDB  
Não aplicável. Não é possível corrigir esse erro automaticamente. Se você não conseguir restaurar o banco de dados a partir de um backup, entre em contato com o Suporte e Atendimento ao Cliente [!INCLUDE[msCoName](../../includes/msconame-md.md)] (CSS).  
  

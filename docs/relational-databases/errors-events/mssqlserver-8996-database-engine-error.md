---
description: MSSQLSERVER_8996
title: MSSQLSERVER_8996 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 8996 (Database Engine error)
ms.assetid: 4e655cdc-945a-4a18-95dd-75f050563d26
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d8b46fb55c77ac13624af28cc349a23191519752
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470767"
---
# <a name="mssqlserver_8996"></a>MSSQLSERVER_8996
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|8996|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC3_IAM_PAGE_RANGE_IN_WRONG_FILEGROUP|  
|Texto da mensagem|Página IAM P_ID da ID do objeto O_ID, ID do índice I_ID, ID da partição PN_ID, ID da unidade de alocação A_ID (tipo TYPE), páginas de controles do grupo de arquivos FG_ID1 que deveriam estar no grupo de arquivos FG_ID2.|  
  
## <a name="explanation"></a>Explicação  
A página IAM (mapa de alocação de índice) *P_ID* no grupo de arquivos *FG_ID1* inclui extensões do grupo de arquivos *FG_ID2* incorretamente. Todas as extensões de uma página IAM deveriam estar no mesmo grupo de arquivos que a página IAM propriamente dita.  
  
## <a name="user-action"></a>Ação do usuário  
  
### <a name="look-for-hardware-failure"></a>Procurar falhas de hardware  
Execute o diagnóstico de hardware e corrija quaisquer problemas. Examine também os logs do aplicativo e do sistema [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para verificar se o erro ocorreu devido a uma falha de hardware. Corrija quaisquer problemas relacionados a hardware existentes nos logs.  
  
Se você tiver problemas contínuos de danos aos dados, tente alternar diferentes componentes de hardware para isolar o problema. Verifique se o sistema não está com a gravação em cache habilitada no controlador de disco. Se você suspeitar que a gravação de caching seja o problema, contate o fornecedor do hardware.  
  
Finalmente, pode ser útil mudar para um sistema de hardware novo. Essa mudança pode incluir a reformatação de unidades de disco e a reinstalação do sistema operacional.  
  
### <a name="restore-from-backup"></a>Restaurar a partir de backup  
Se o problema não estiver relacionado ao hardware e se houver um backup limpo conhecido, restaure o banco de dados do backup.  
  
### <a name="run-dbcc-checkdb"></a>Executar DBCC CHECKDB  
Não aplicável. Esse erro não pode ser reparado. Se você não conseguir restaurar o banco de dados com base em um backup, contate o CSS (Suporte e Atendimento ao Cliente) [!INCLUDE[msCoName](../../includes/msconame-md.md)].  
  
